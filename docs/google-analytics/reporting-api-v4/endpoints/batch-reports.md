## Batch Reports

The *Batch Reports* endpoint requires you to specify a JSON Query, which should be an instance of the Google Analytics API's **[ReportRequest](https://developers.google.com/analytics/devguides/reporting/core/v4/rest/v4/reports/batchGet#ReportRequest)** class.

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