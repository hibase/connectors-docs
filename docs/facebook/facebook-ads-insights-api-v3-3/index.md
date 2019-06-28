# Facebook Ads Insights API (v3.2)

### Getting started

In order to start using the hibase connector to the Facebook Ads API, go through the following steps:

1. From your [Facebook Developer console](https://developers.facebook.com), create a new app and call it `[company name]-hibase`

2. Navigate to the _Apps_ section of your [Business Settings page](https://business.facebook.com/settings/apps) and add the newly created App by clicking _+ Add_ and copy-pasting the _App ID_ of the App

3. Navigate to the _System Users_ section of your [Business Settings page](https://business.facebook.com/settings/system-users) and add a new _Regular System User_, which you can call simply `hibase`

4. Go back to the App page in your [Business Settings page](https://business.facebook.com/settings/apps), select the App and select the _People_ tab on the right hand side of the screen

5. Click on _Add People_ and add the newly created System User as a developer to the App

6. Back in the System Users section of your [Business Settings page](https://business.facebook.com/settings/system-users), select the System User you created and navigate to the _Assets_ tab

7. Click on _Add Assets_ and then on _Ad Accounts_ within the dialog that pops up

8. Tick all the Ad Accounts that should be accessible through hibase and select _View Performance_ as permissions

9. Click on _Save Changes_

10. Back in the System Users section of your [Business Settings page](https://business.facebook.com/settings/system-users), click on _Generate New Token_

11. In the dialog that pops up, select your App and tick `reads_insights` and `ads_read` from the list of permissions

12. Hit _Generate Token_

13. Copy the Access Token and store it safely (e.g. in a Password Manager)

14. Copy-paste the token in _hibase_ when adding the Facebook 