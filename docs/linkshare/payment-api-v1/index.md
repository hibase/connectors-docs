# Linkshare Payment API (v1)

### Getting started

In order to start using the hibase connector to the [Linkshare Payment API (v1)](https://pubhelp.rakutenmarketing.com/hc/en-us/articles/201046046), you first need to setup *Subscriptions* to the APIs you want to use within the [Linkshare API Developer Portal](https://developers.rakutenmarketing.com/subscribe/site/pages/subscriptions.jag).

1. Log into your [Linkshare API Developer Portal](https://developers.rakutenmarketing.com/subscribe/site/pages/subscriptions.jag) and navigate to *APIs*

2. In the search bar, look up the API you want to subscribe to, in this case *Advanced Reports*

3. If you did not do so already, create an Application from the *Applications* drop down menu on the right. You can omit the *Callback URL* and you can select *Unlimited* as *Throttling Tier*, or anything else according to your security policy

4. Back in the Subscriptions page, with the API selected, choose your desired *Application* and *Tiers* from the dropdown menus on the right and hit *Subscribe*

5. As the new Subscription is created, a *Keys* section should display a few tokens

6. Copy the *Token Request Authorization* hash (excluding the `Basic` word). This is the `Token Request Authorization` you will need to input in **hibase** when subscribing to the connector

7. For some calls, you will need an additional `Security Token` which can be found in your [Publisher Portal](https://cli.linksynergy.com/cli/publisher/links/webServices.php) under *Links > Web Services*

8. In **hibase**, when adding the *Linkshare* connector, you will need to provide the token you just copied, together with your username, password and *Merchant ID* or *Site ID* as **Scope**. The latter can be obtained by logging into your [Rakuten Marketing Account](https://rakutenmarketing.com/)

9. Save the connector and you are good to make requests to the API you just subscribed to
