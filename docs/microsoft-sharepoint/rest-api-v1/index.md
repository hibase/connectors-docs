# Microsoft Sharepoint REST API

### Getting started

In order to start using the hibase connector to the Microsoft Sharepoint REST API, you need to get an *Access Token* to your Sharepoint installation.

1. Register a new app by navigating to *https://[Host].sharepoint.com/_layouts/15/appregnew.aspx*, or *https://[Host].sharepoint.com/sites/[Site]/_layouts/15/appregnew.aspx*, where *Host* is the subdomain assigned to your sharepoint installation. This requires the right set of permissions and you might need administrator support in order to get access

2. Click *Generate* next to *Client ID* and *Client Secret*

3. Type *hibase* in *Title*, *localhost* in *App Domain* and *https://localhost* in *Redirect URI*. Next, click on *Create*

4. Take note of the generated *Client ID* and *Client Secret*

5. Navigate to *https://[Host].sharepoint.com/_layouts/15/appinv.aspx*, or *https://[Host].sharepoint.com/sites/[Site]/_layouts/15/appinv.aspx*

6. Copy-paste your *Client ID* in the *App ID* field and hit *Lookup* in order to find your app

7. In the *Permission Request XML*, paste the following in order to grant the app *Read* access to Sharepoint:

```
<AppPermissionRequests AllowAppOnlyPolicy="true">
  <AppPermissionRequest Scope="http://sharepoint/content/sitecollection/web" Right="Read"/>
</AppPermissionRequests>
```

8. Click *Create* and hit *Trust it* in the next screen

9. Issue a GET request to *https://[Host].sharepoint.com/_layouts/15/_vti_bin/client.svc*, or *https://[Host].sharepoint.com/sites/[Site]/_layouts/15/_vti_bin/client.svc* with *Authorization: Bearer* as a header, for example in curl:

```
curl -v \
  -H "Authorization: Bearer" \
  https://[Host].sharepoint.com/_layouts/15/_vti_bin/client.svc
```

10. Copy the *realm* value from the *www-authenticate* header provided in the response. This is your *Realm ID*, which you will need in the following step

11. Provide your *Client ID*, *Client Secret*, *Realm ID* and *Host* to the hibase connector for Sharepoint when adding it to your account
