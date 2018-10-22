# Linkshare Reporting API (v1)

### Getting started

In order to start using the hibase connector to the Linkshare Reporting API (v1), you need to retrieve a *Token* from the [Linkshare Reporting Interface](https://rakutenmarketing.com/affiliate):

1. Log into your [Linkshare Reporting Interface](https://rakutenmarketing.com/affiliate) and navigate to *Reports*

2. Within the *Reporting* Tab, click on *Choose a Report* and pick any report from the list

3. Click on the down arrow next to *View Report* and select *Get API*

4. Copy the token that you'll find as the last parameter in the displayed URL, excluding the "`token=`" key:

> https://ran-reporting.rakutenmarketing.com/en/reports/...token=[XXXXX]

5. In **hibase**, when adding the *Linkshare Reporting API* connector, you will need to provide the token you just copied

6. Save the connector and you are good to make requests to the *Linkshare Reporting API*
