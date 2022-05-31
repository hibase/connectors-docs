# Zabbix API (v1)

### Getting started

In order to start using the **hibase** connector to the [Zabbix API (v1)](https://www.zabbix.com/documentation/current/en/manual/api), you need to fetch an *API token* for your account and provide the *Base URL* for your installation.

1. Issue a POST request to your Zabbix API as follows (fill *Base URL*, *username* and *password* with valid values):

```
POST [Base URL]/api_jsonrpc.php
  {
    "jsonrpc": "2.0",
    "method": "user.login",
    "params": {
      "user": [username],
      "password": [password]
    },
    "id": 1,
    "auth": null
  }

```

2. Copy the *result* string of the request above (this is your API token)

3. In **hibase**, provide the *API Token* you just copied when adding the *Zabbix API* connector
