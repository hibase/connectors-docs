## Advertiser Lookup API

The *Advertiser Lookup API* from **Commission Junction** allows to search advertisers on the platform and filter them by a variety of dimensions.

> Please check the official documentation for the *Commission Junction Advertiser Lookup API* for details on filter parameters. This can be accessed in the [Commission Junction Support Center](https://cjcommunity.force.com/s/article/Advertiser-Lookup-API-4777195) after login.

Please note that **at least one** of the following parameters has to be provided in order for the API to return anything: advertiser-ids, keywords or advertiser-name.

### Response normalization

hibase does not perform any particular transformation onto data returned by this endpoint. Here is an example of what a product record might look like:

```json
  {
    "ad_id": 12345678,
    "advertiser_id": 12345678,
    "advertiser_name": "My Shop",
    "advertiser_category": "Fashion",
    "buy_url": "https://...",
    "catalog_id": "cat:1234",
    "currency": "EUR",
    "description": "Lorem ipsum...",
    "image_url": "https://...",
    "in_stock": "true",
    "isbn": "12345678",
    "manufacturer_name": "My Brand",
    "manufacturer_sku": "12345678",
    "name": "My Product",
    "price": 42.0,
    "retail_price": 42.0,
    "sale_price": 42.0,
    "sku": "12345678",
    "upc": "12345678"
  }
```

### Pagination

The *Advertiser Lookup API* is automatically paginated by **hibase** until the full records set has been returned.