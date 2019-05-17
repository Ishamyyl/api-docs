# Product Activity

Using the Product Activity endpoint will enable product-triggered automations in your Drip account. An example: price drop notifications. Send an email when a product in a customer’s cart drops in price, encouraging the customer to return and place an order.

## Create or update a product

To update an existing product, include the <code>provider</code> and <code>product_id</code> for that order in the payload.

> To record an order event:

```shell
curl -X POST "https://api.getdrip.com/v3/YOUR_ACCOUNT_ID/shopper_activity/product" \
  -H "Content-Type: application/json" \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -u YOUR_API_KEY: \
  -d @- << EOF
  {
    "provider": "my_custom_platform",
    "action": "created",
    "occurred_at": "2019-01-28T12:15:23Z",
    "product_id": "B01J4SWO1G",
    "product_variant_id": "B01J4SWO1G-CW-BOTT",
    "sku": "XHB-1234",
    "name": "The Coolest Water Bottle",
    "brand": "Drip",
    "categories": [
      "Accessories"
    ],
    "price": 11.16,
    "inventory": 42,
    "product_url": "https://mysuperstore.com/dp/B01J4SWO1G",
    "image_url": "https://www.getdrip.com/images/example_products/water_bottle.png"
  }
  EOF
```

> Responds with a <code>202 Accepted</code> if successful. That means the server accepted the request and queued it for processing. The response includes a unique request_id that can be used to check the status of the request later on:

```json
{
  "request_id": "990c99a7-5cba-42e8-8f36-aec3419186ef"
}
```

### HTTP Endpoint

`POST /v3/:account_id/shopper_activity/product`

### Arguments

<table>
  <thead>
    <tr>
      <th>Property</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>provider</code></td>
      <td>Required. The identifier for the provider from which the product data was received in lower snake cased form. For example, <code>shopify</code> or <code>my_custom_platform</code> or <code>my_store</code>.</td>
    </tr>
    <tr>
      <td><code>action</code></td>
      <td>Required. The event's action. For Product Activity, this can be either <code>created</code>, <code>updated</code> or <code>deleted</code>.
    </tr>
    <tr>
      <td><code>occurred_at</code></td>
      <td>Optional. The String time at which the product activity occurred in <a href="http://en.wikipedia.org/wiki/ISO_8601">ISO 8601</a> format. Defaults to the current time.</td>
    </tr>
    <tr>
      <td><code>product_id</code></td>
      <td>Required. A unique, internal id for the product (generally the primary key generated by the ecommerce platform).</td>
    </tr>
    <tr>
      <td><code>product_variant_id</code></td>
      <td>Optional. If applicable, a unique identifier for the specific product variant from the provider. For example, a t-shirt may have one product_id, but several product_variant_ids for sizes and colors.</td>
    </tr>
    <tr>
      <td><code>sku</code></td>
      <td>Optional. The product SKU.</td>
    </tr>
    <tr>
      <td><code>name</code></td>
      <td>Required. The product name.</td>
    </tr>
    <tr>
      <td><code>brand</code></td>
      <td>Optional. The product's brand, vendor, or manufacturer.</td>
    </tr>
    <tr>
      <td><code>categories</code></td>
      <td>Optional. An array of categories associated with the product (e.g. shoes, vitamins, books, videos).</td>
    </tr>
    <tr>
      <td><code>price</code></td>
      <td>Required. The price of a single product.</td>
    </tr>
    <tr>
      <td><code>inventory</code></td>
      <td>Optional. Integer. The currently available inventory of the product.</td>
    </tr>
    <tr>
      <td><code>product_url</code></td>
      <td>Optional. A URL to the site containing product details.</td>
    </tr>
    <tr>
      <td><code>image_url</code></td>
      <td>Optional. A direct URL to an image of the  product. We recommend using an image type that is supported by modern email clients (e.g. JPEG, GIF, PNG). For best display results, image size should be consistent across all products.</td>
    </tr>
  </tbody>
</table>