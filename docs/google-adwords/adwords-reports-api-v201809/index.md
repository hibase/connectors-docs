# Google AdWords API (v201809)

### Getting started

In order to start using the hibase connector to the Google AdWords API (v201809), you need to get a [*Developer Token*](https://developers.google.com/adwords/api/docs/guides/signup) and a [*OAuth2 Refresh Token*](https://developers.google.com/adwords/api/docs/guides/authentication#oauth2_service_accounts) from Google.

1. Navigate to your [*Google Ads Manager Account API Centre*](https://ads.google.com/aw/apicenter) and first of all copy the *Account ID* you see right of the AdWords logo at the top of the page (e.g. 123-456-7890)

2. Fill out the form and apply for a *Developer Token* if you do not have one already. Apply for Basic API Access as described [here](https://developers.google.com/adwords/api/docs/guides/signup). You will have to wait until your application is approved in order to start using the connector, but you can move on to the next steps already to ensure everything is set up

3. Navigate to the [Google API Console Credentials page](https://console.developers.google.com/apis/credentials) and select your Project (or create a new one if needed)

4. Click on *Create Credentials*, then *OAuth client ID*

5. Set up an *OAuth consent screen* if asked to do so. You only have to provide an Application name for the purpose of this guide

6. Back in the *OAuth client ID* setup form, select *Web application* as as *Application type* and provide a name for the application (e.g. *hibase*)

7. Under Authorized redirect URIs, type `https://developers.google.com/oauthplayground`

8. Click *Create* and note down the *client ID* and *secret* that are provided in the confirmation screen

9. Navigate to the [*Google OAuth2 Playground*](https://developers.google.com/oauthplayground/#step1&scopes=https%3A//www.googleapis.com/auth/adwords&url=https%3A//&content_type=application/json&http_method=GET&useDefaultOauthCred=checked&oauthEndpointSelect=Google&oauthAuthEndpointValue=https%3A//accounts.google.com/o/oauth2/auth&oauthTokenEndpointValue=https%3A//oauth2.googleapis.com/token&includeCredentials=unchecked&accessTokenType=bearer&autoRefreshToken=unchecked&accessType=offline&forceAprovalPrompt=checked&response_type=code) and click on the gear icon in the top-right corner

10. Paste your *client ID* and *secret* at the bottom of the form

11. On the left-hand side of the screen, under *Select & authorize APIs*, paste `https://www.googleapis.com/auth/adwords` and click *Authorize APIs*. Note that if you get a `400` error stating the redirect URI is not authorized, you might simply have to retry in a few minutes after the changes you just saved above have propagated

12. Authenticate with your Google Account in the *OAuth2 consent screen* and grant permissions to manage AdWords campaigns

13. Back in the *OAuth2 Playground*, hit *Exchange authorization code for tokens* and copy the *Refresh token* that is provided

14. In your [*credentials page*](https://console.developers.google.com/apis/credentials), you can now remove `https://developers.google.com/oauthplayground` from the Authorized redirect URIs of your OAuth Client ID

15. In *hibase*, provide the *Account ID*, *Developer Token*, *Client ID*, *Client Secret* and *Refresh Token* when adding the *Google Adwords API* connector