# HubSpot CRM API (v3)

### Getting started

In order to start using the **hibase** connector to the [HubSpot CRM API (v3)](https://developers.hubspot.com/docs/api/crm/understanding-the-crm), you need to create a dedicated app within your *developer account* and authorize it through an OAuth2 authentication flow.

The instructions below make use of [Postman's OAuth2 collection](https://documenter.getpostman.com/view/1559645/Szzhcxzz), but the same result can be achieved through `cURL` or similar alternatives.

1. Register on Postman if you don't already have an account

2. Import [Postman's OAuth2 collection](https://elements.getpostman.com/view/import?collection=1559645-e1dfc9cb-3de7-4a73-82cd-602334bae284-Szzhcxzz&versionTag=latest&environment=1559645-310ffadd-efd2-457b-8b69-6d1c0beb2f97-Szzhcxzz) into your workspace

3. Create a [HubSpot developer account](https://app.hubspot.com/signup-hubspot/developers) if you don't already have one

4. Click on *Manage Apps* and then on *Create app* in the top right corner

5. Choose a name for the app (for example *hibase-connector*)

6. Within the *Auth* tab of the app creation dialog, select the scopes you want hibase to have access to (for example *contacts*, *companies* and *deals*)

7. Input the following URL into the *Redirect URL* field: `https://oauth.pstmn.io/v1/browser-callback`

8. Save the app in HubSpot

9. Copy the *Client ID*, *Client secret* and *scopes* (space-separated) from HubSpot into the Postman OAuth2 settings

10. Input the following URL into the *Auth URL* field in Postman: `https://app.hubspot.com/oauth/authorize`

11. Input the following URL into the *Access Token URL* field in Postman: `https://api.hubapi.com/oauth/v1/token`

12. In Postman, select *Send client credentials in body* within the *Client Authentication* field

13. Click on *Get new access token* and follow the authentication flow

14. If the authentication is successful, you will be provided with a *Refresh token* within the Postman interface

15. Copy the *Refresh token* you just received, together with the *Client ID* and *Client secret* of the HubSpot app into the HubSpot connector for *hibase*