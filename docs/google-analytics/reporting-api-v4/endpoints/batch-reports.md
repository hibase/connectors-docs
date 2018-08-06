## Batch Reports

The *Batch Reports* endpoint requires you to specify a JSON Query, which must be an instance of the Google Analytics API's **[ReportRequest](https://developers.google.com/analytics/devguides/reporting/core/v4/rest/v4/reports/batchGet#ReportRequest)** class.

Please refer to the [official documentation](https://developers.google.com/analytics/devguides/reporting/core/v4/rest/v4/reports/batchGet) for details on how to compose a ReportRequest query.

A valid query might look something like this:

```json
  {
    "viewId":"XXXXXXXXX",
    "dateRanges":[
      {"startDate":"2018-07-30","endDate":"2018-07-31"}
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
      {"startDate":"{{ $today - 7 }}","endDate":"{{ $today - 7 }}"}
    ],
    // ...
  }
```

### Response normalization

hibase takes care of normalizing the data coming back from the GA API, in order to represent it in a two-dimensional, tabular format.

The response from the API for the query above will look something like this:

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
                    "123",
                    "1234",
                    "12345"
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
                    "123",
                    "1234",
                    "12345"
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

hibase will parse it and serve it as follows:

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
        "2",
        "4",
        "49"
      ],
      [
        "20180730",
        "Berlin",
        "Chrome",
        "2",
        "10",
        "108"
      ]
    ]
  }
```

As you can see, a few things are happening here:

- Colons within header names are being changed to underscores, in order to be valid as column names for a possible SQL insert
- Header data types are being inferred from the response
- Data from different paths within the JSON is being aggregated into one-dimensional rows

