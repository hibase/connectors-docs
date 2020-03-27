# Zoho CRM Rest API (v2)

### Getting started

Follow the steps below in order to start using the hibase connector to the Zoho CRM API (v2):

1. Navigate to the [Zoho Developer Console](https://api-console.zoho.eu/) and create a _Self Client_ if one is not already available

2. Note down the *Client ID* and *Client Secret* that are provided by the console

3. Determine which *domain* of the Zoho API you are using and note it down. The available options are as follows:
  - For US: https://accounts.zoho.eu
  - For AU: https://accounts.zoho.eu.au
  - For EU: https://accounts.zoho.eu
  - For IN: https://accounts.zoho.in
  - For CN: https://accounts.zoho.com.cn

4. Navigate to the *Generate Code* tab and paste the following line in *Scope* for complete read access (you can adapt scopes according to what you would like hibase to have access to): 

```
ZohoBooks.fullaccess.read,ZohoCRM.modules.custom.read,ZohoCRM.modules.contacts.read,ZohoCRM.modules.read,ZohoCRM.settings.read,ZohoCRM.users.read,ZohoCRM.org.read
```

5. Give a description to the Scope (e.g. "hibase full access") and hit *Generate*

6. Copy the code that is generated

7. Use an HTTP client to make a POST request to the Zoho API and fetch a refresh token, which you will need to provide as credentials to the *Zoho connector* in *hibase*. For example, you can use `curl` from your terminal as follows:

```
curl -v -X POST \
  --data-urlencode "code=[Code generated in step 5]" \
  --data-urlencode "client_id=[Client ID]" \
  --data-urlencode "redirect_uri=hibase.co" \
  --data-urlencode "client_secret=[Client Secret]" \
  --data-urlencode "grant_type=authorization_code" \
  --data-urlencode "access_type=offline" \
  [Zoho API Domain as in step 3]/oauth/v2/token
```

8. Copy the *Refresh token* that is provided by the HTTP response

9. Provide the *API URL* (as in step 3), *Client ID*, *Client Secret* and *Refresh token* to the hibase Zoho CRM connector