# Google Analytics Reporting API (v4)

### Getting started

In order to start using the hibase connector to the Google Analytics API (v4), you first need to set up a [*Service Account*](https://developers.google.com/analytics/devguides/reporting/core/v2/authorization#service_accounts) within your Google Analytics account.

1. Navigate to your [Google APIs Dashboard](https://console.developers.google.com/apis/dashboard) and check whether a *Project* already exsists for your app

2. If a project was not already set up, you can do so through this [Setup tool](https://console.developers.google.com/start/api?id=analytics&credential=client_key)

3. Navigate to the [Google APIs Library](https://console.developers.google.com/apis/library) and activate the [**Google Analytics Reporting** API](https://console.developers.google.com/apis/library/analyticsreporting.googleapis.com) for the project if it was not already activated

4. Navigate to the [Credentials](https://console.developers.google.com/apis/credentials) tab and select *Create credentials -> Service account key*

5. Save your credentials as JSON. **Warning**: Store this file securely as this is the only time you will be able to download it

6. Within hibase, add a new **Google Analytics API (v4)** Connector and fill your *client email* and *private key*, which you can find in the downloaded JSON file.

  **Important:** make sure you correctly add **line breaks** to your private key, by substituting any occurrence of `\n` in the JSON file with an actual line break. From:

  ```json
  	-----BEGIN PRIVATE KEY-----\nXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\nXXXXXXXXXXXXX...
  ```

  ... to:

  ```json
  	-----BEGIN PRIVATE KEY-----
  	XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
  	XXXXXXXXXXXXX...
  ```

7. Save the connector and you are good to go

In case you experience issues querying the API, check again the steps above and especially that you copied your *private key* correctly (step 6). You can edit the Connector you just added at any time and overwrite the credentials you originally provided.