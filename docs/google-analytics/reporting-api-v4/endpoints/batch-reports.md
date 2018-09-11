## Batch Reports

The *Batch Reports* endpoint requires you to specify a JSON Query, which must be an instance of the Google Analytics API's **[ReportRequest](https://developers.google.com/analytics/devguides/reporting/core/v4/rest/v4/reports/batchGet#ReportRequest)** class.

Please refer to the [official documentation](https://developers.google.com/analytics/devguides/reporting/core/v4/rest/v4/reports/batchGet) for details on how to compose a ReportRequest query.

A valid query might look something like this:

```json
  {
    "viewId":"XXXXXXXXX",
    "dateRanges":[
      {
        "startDate":"2018-07-30",
        "endDate":"2018-07-31"
      }
    ],
    "metrics":[
      {"expression":"ga:users"},
      {"expression":"ga:sessions"},
      {"expression":"ga:hits"}
    ],
    "dimensions":[
      {"name":"ga:date"},
      {"name":"ga:city"},
      {"name":"ga:browser"}
    ]
  }
```

You can interpolate variables into your Query through the hibase syntax, for example:

```json
  {
    // ...
    "dateRanges":[
      {
        "startDate":"{{ $today - 7 }}",
        "endDate":"{{ $today }}"
      }
    ],
    // ...
  }
```

### Response normalization

hibase takes care of normalizing the data coming back from the Google Analytics Reporting API, in order to represent it in a two-dimensional, tabular format.

Provided this response originating from the API call...

```json
  {
    "reports": [
      {
        "columnHeader": {
          "dimensions": [
            "ga:date",
            "ga:city",
            "ga:browser"
          ],
          "metricHeader": {
            "metricHeaderEntries": [
              {
                "name": "ga:users",
                "type": "INTEGER"
              },
              {
                "name": "ga:sessions",
                "type": "INTEGER"
              },
              {
                "name": "ga:hits",
                "type": "INTEGER"
              }
            ]
          }
        },
        "data": {
          "rows": [
            {
              "dimensions": [
                "20180727",
                "Berlin",
                "Chrome"
              ],
              "metrics": [
                {
                  "values": [
                    "42",
                    "56",
                    "322"
                  ]
                }
              ]
            },
            {
              "dimensions": [
                "20180728",
                "Berlin",
                "Chrome"
              ],
              "metrics": [
                {
                  "values": [
                    "44",
                    "62",
                    "398"
                  ]
                }
              ]
            },
            // ...
          ]
        }
      }
    ]
  }
```

... hibase will parse it and serve it as follows:

```json
  {
    "headers": [
      {
        "name": "ga_date",
        "type": "string"
      },
      {
        "name": "ga_city",
        "type": "string"
      },
      {
        "name": "ga_browser",
        "type": "string"
      },
      {
        "name": "ga_users",
        "type": "integer"
      },
      {
        "name": "ga_sessions",
        "type": "integer"
      },
      {
        "name": "ga_hits",
        "type": "integer"
      }
    ],
    "data": [
      [
        "20180727",
        "Berlin",
        "Chrome",
        "42",
        "56",
        "322"
      ],
      [
        "20180728",
        "Berlin",
        "Chrome",
        "44",
        "62",
        "398"
      ],
      // ...
    ]
  }
```

As you can see, a few things are happening here:

- Colons within header names are being changed to underscores, in order to be valid as column names for a possible SQL insert: e.g. `ga:users` becomes `ga_users`
- Header *data types* are being inferred from the response
- Data from different paths within the JSON is being aggregated into one-dimensional rows: 
```json
  [
    "20180727",
    "Berlin",
    "Chrome",
    "42",
    "56",
    "322"
  ]
```


### Pagination

The Google Analytics Reporting API is paginated through the `pageToken` and `pageSize` parameters, as outlined in the [official docs](https://developers.google.com/analytics/devguides/reporting/core/v4/rest/v4/reports/batchGet). 

hibase takes care of automatically iterating requests if a `nextPageToken` is received from the API. If given no other instruction, it will do so until an empty data set is returned or the `nextPageToken` parameter is not returned anymore. 

> **NB**: Limits apply to how many subsequent calls can be made through automatic pagination. Please get in touch in case you are reaching your limits and you would like them to be increased. 

You can still take back control of the API call and retrieve a specific set of records by manually providing a `pageToken` parameter in your `query`. In this case, hibase will not iterate any further regardless of what `nextPageToken` is returned by the API.
