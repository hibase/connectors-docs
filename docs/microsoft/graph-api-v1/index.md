# Microsoft Graph API v1.0

### Getting started

Follow these steps in order to start using the hibase connector to the Microsoft Graph API:

1. Register a new app in your [Azure account](https://go.microsoft.com/fwlink/?linkid=2083908) with the following settings:

  - **Name**: *hibase*
  - **Supported account types**: *Accounts in this organizational directory only (Single tenant)*
  - **Redirect URI**: `https://localhost`

2. Take note of the *Client ID* and *Tenant ID* that are displayed at the top of your new App's page

3. Navigate to the *Certificates & secrets* page of your App and click on *New client secret* to issue a new secret. Take note of it as it will be required later in the process

4. Navigate to the *API permissions* page of your new App and add the following **Delegated permissions**, all of which are available under *Microsoft Graph*:

  - Files.Read.All
  - Sites.Read.All
  - User.Read

5. In your browser, navigate to the following URL after replacing *Client ID* and *Tenant ID* with the values you noted above:

```
https://login.microsoftonline.com/[Tenant ID]/oauth2/v2.0/authorize?client_id=[Client ID]&response_type=code&redirect_uri=https%3A%2F%2Flocalhost&scope=offline_access%20user.read%20files.read%20sites.read.all
```

6. You will be redirected to your `localhost`, most likely resulting in a "This site can't be reached" page in your browser. Copy the URL from the URL bar and take note of the value of the `code` param therein included. This is the *Authorization Code* you will need in the following step

7. Issue a POST request as follows, replacing all the values in brackets with the ones you noted above (the example is using curl):

```
curl -v -X POST \
  --data-urlencode "grant_type=authorization_code" \
  --data-urlencode "client_id=[Client ID]" \
  --data-urlencode "code=[Authorization Code]" \
  --data-urlencode "scope=offline_access user.read files.read sites.read.all" \
  --data-urlencode "redirect_uri=https://localhost" \
  --data-urlencode "client_secret=[Client Secret]" \
  https://login.microsoftonline.com/[Tenant ID]/oauth2/v2.0/token
```

8. Take note of the *Refresh token* provided in the response

9. Provide your *Tenant ID*, *Client ID*, *Client Secret* and *Refresh Token* to the hibase connector for Microsoft Graph when adding it to your account. Additionally, write `offline_access user.read files.readWrite sites.read.all` as *Scope* and `https://localhost` as *Redirect Uri*

You are now ready to start using the *Microsoft Graph* connector for *hibase*