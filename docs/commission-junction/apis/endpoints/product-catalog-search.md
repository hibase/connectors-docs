## Product Catalog Search API

The *Product Catalog Search API* from **Commission Junction** allows to search the products catalog and filter it by a variety of dimensions.

> Please check the official documentation for the *Commission Junction Product Catalog Search API* for details on filter parameters. This can be accessed in the [Commission Junction Support Center](https://cjcommunity.force.com/s/article/Product-Catalog-Search-API-4777185) after login.

Parameters that are not explicitly provided by the **hibase** query interface can be added in JSON format through the `other_params` parameter, for example:

```json
  {
    "manufacturer-name": "My Brand",
    "sort-by": "name"
  }
```

There are a few important gotchas regarding this API:

- **At least one** of the optional parameters is required in order for the API to return anything
- A **maximum of 10.000 results** will be returned for any given query, even when more results match the provided parameters

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

The *Product Catalog Search API* is automatically paginated by **hibase** until the full records set has been returned or the maximum 10.000 records limit has been reached.

In case more than 10.000 records match the API, you should consider breaking down your query into a more granular set of parameters.