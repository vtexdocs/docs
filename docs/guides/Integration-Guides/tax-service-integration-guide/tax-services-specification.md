---
title: "Specification"
slug: "tax-services-specification"
hidden: false
createdAt: "2020-09-01T16:35:02.523Z"
updatedAt: "2022-02-11T15:38:54.137Z"
---

In synchronous integration, VTEX’s [Checkout API](https://developers.vtex.com/docs/api-reference/checkout-api) triggers and sends a request to the external tax service API whenever there are changes to a shopper’s cart, such as adding or removing items.

To learn more about how to implement a client to connect your tax calculation provider to VTEX’s APIs, check the [Tax Service recipe](https://developers.vtex.com/docs/guides/tax-services-recipe) and [example](https://developers.vtex.com/docs/guides/tax-services-reference-implementation).

>⚠️ The timeout for the request is five seconds. There is no retry in case of timeout. If the external service that responds to the request times out constantly, the store will not be able to finish the order. If this integration is active, it applies to all stores in that account.

## Tax integration via Checkout API

You must activate the tax integration by configuring the `orderForm`, an object that stores contextual information about the order. This data is essential to the checkout process of the order.

Check the flow of `orderForm` configuration below:

![Tax integration flow](https://raw.githubusercontent.com/vtexdocs/dev-portal-content/main/images/tax-service-flow-specification.png)

### Get `orderForm`

To activate the tax integration, first it is necessary to get the current `orderForm` settings using the [Get `orderForm` configuration](https://developers.vtex.com/docs/api-reference/checkout-api#get-/api/checkout/pvt/configuration/orderForm?endpoint=get-/api/checkout/pvt/configuration/orderForm) endpoint.

In the endpoint response, the `taxConfiguration` object has the tax information that must be updated, as in the example below:  

```json
{
    "taxConfiguration": {
            "url": "https://{accountName}.myvtex.com/tax-service/order-tax",
            "authorizationHeader": "99b9935b048dfd86893d0bf9gas628849",
            "appId": "tradeincart",
            "isMarketplaceResponsibleForTaxes": false,
       ...
}
    
```

### Update `orderForm`

Then, Checkout settings must be updated using the [Update orderForm configuration](https://developers.vtex.com/docs/api-reference/checkout-api#post-/api/checkout/pvt/configuration/orderForm) endpoint.  

In the `taxConfiguration` object, it is important to update the following fields.

| Property name | Description| Example|
| ---------------------------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------|
| `url`                              | String of external API endpoint of the tax provider that the Checkout will query to receive the calculated taxes.| `"https://sandbox-rest.avatax.com/api/v2/transactions/create"`|
| `authorizationHeader`              | String that the Checkout will use in the `Authorization` header of calls to the external tax calculation API. This field can be used to define the access credentials for this API. | `"99b9935b048dfd86893d0bf9gas628849"`|
| `isMarketplaceResponsibleForTaxes` | Boolean that indicates whether the marketplace is responsible for calculating taxes for the products (`true`) or if the responsibility lies with the seller (`false`).          | `true`|

>⚠️ The `isMarketplaceResponsibleForTaxes` feature is not compatible with stores that have [Multilevel Omnichannel Inventory](https://help.vtex.com/en/tutorial/multilevel-omnichannel-inventory--7M1xyCZWUyCB7PcjNtOyw4) implemented.

Here is an example of the `taxConfiguration` object with the expected information:

```json
{
  "taxConfiguration": {
        "url": "{Tax provider URL}",
        "authorizationHeader": "{Tax provider authorization header}",
        "appId": "tradeincart",
        "isMarketplaceResponsibleForTaxes": true,
        ...
  },
  ...
}
```

>⚠️ You must send the entire `orderForm` in the request body in the [Update orderForm configuration](https://developers.vtex.com/docs/api-reference/checkout-api#post-/api/checkout/pvt/configuration/orderForm) endpoint.

After successfully submitting the request, the Tax API integration becomes active in synchronous mode.

>⚠️ When a purchase is made in a store, the location from which the order is shipped matters for tax calculation purposes. Because of this, when items from [White Label Sellers](https://help.vtex.com/en/tutorial/white-label-seller--5orlGHyDHGAYciQ64oEgKa) are part of an order, tax configuration for the marketplace (`seller 1`) is not taken into account for those items. Each seller must have its own tax service configuration in order for this type of integration function properly.


## Tax calculation request

The external tax calculation service must provide an endpoint, as the `https://sandbox-rest.avatax.com/api/v2/transactions/create` example, that will receive a `POST` request. In this request, Checkout provides a body in a specific format. This means that either the endpoint must be prepared to receive this body format, or the integration must contain a parser to adapt it to the correct format.  

Here is an example of that body sent by Checkout API:

```json
{
     "orderFormId": "e5098ad8c4jk490bb2f6f03400ac1413",
     "salesChannel": "1",
     "items": [
       {
         "id": "0",
         "sku": "26",
         "productId": "12",
         "ean": "12345678909123",
         "refId": "3432",
	       "categoryId": "3",
         "unitMultiplier": 1,
         "measurementUnit": "un",
         "targetPrice": 8.2,
         "itemPrice": 8.2,
         "quantity": 1,
         "discountPrice": 0,
         "dockId": "1125a08",
         "freightPrice": 0,
         "brandId": "2000002",
         "taxCode": "PC040210",
         "sellerId": "1"
       }
     ],
     "totals": [
       {
         "id": "Items",
         "name": "Items Total",
         "value": 820
       },
       {
         "id": "Discounts",
         "name": "Discounts Total",
         "value": 0
       },
       {
         "id": "Shipping",
         "name": "Shipping Total",
         "value": 0
       },
       {
         "id": "Tax",
         "name": "Tax Total",
         "value": 0
       }
     ],
     "clientEmail": "client@email.com",
     "shippingDestination": {
       "country": "BRA",
       "state": "RJ",
       "city": "Rio de Janeiro",
       "neighborhood": "Botafogo",
       "postalCode": "22250-905",
       "street": "Praia Botafogo"
     },
     "clientData": {
       "email": "client@email.com",
       "document": "12345678909",
       "documentType": "cpf",
       "clientProfileData": "12345678000100",
       "stateInscription": "12345678"
     },
     "paymentData": {
       "payments": [
         {
           "paymentSystem": "2",
           "bin": null,
           "referenceValue": 820,
           "value": 820,
           "installments": null
         }
       ]
     },
    "taxApp": {
        "fields": {
            "isTradeIn": "Yes",
            "productuid": "15216842581",
            "quoteuid": "29882961591",
            "condition": "working",
            "tradeInPrice": "220.00",
            "title": "ROG Phone II 512GB",
            "productIdApplied": "404",
            "uid": "29882961591",
            "taxBase": "1399.99"
        },
        "id": "tradeincart",
        "major": 1
    }
}
```

This body has the main fields:

| Field                 | Type   | Description                                                                                                                                                                 |
| --------------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `orderFormId`         | string | `orderform` ID.                                                                                                                                                             |
| `salesChannel`        | string | Trade policy ID.                                                                                                                                                      |
| `items`               | array  | List of objects which are the order products, where `dockId` is a field that refers to its identification on the Logistics system that contains information of its address. |
| `totals`              | array  | Total amount of the `orderForm`, divided into taxes, shipping, discounts, and the items prices.                                                                           |
| `clientEmail`         | string | Client's email. address.                                                                                                                                                     |
| `shippingDestination` | object | Shipping information. Mandatory. field.                                                                                                                                      |
| `clientData`          | object | Information regarding the client that placed the order.                                                                                                                     |
| `paymentData`         | object | Contains an array of payments, where there is information regarding the order payment.                                                                                      |
| `taxApp`              | object | Contains an object with custom fields specific to the tax application.                                                                                                      |


>⚠️  When marketplace provide orderform data to a tax provider installed on **white label seller** it has omit fields like `orderFormId` , `paymentData` and `taxApp` .


### Tax provider response to the request

In response to the request sent by Checkout, it is expected that the external tax provider API returns an array of products, each with its own array of taxes. See the example below:  

```json
[
    {
        "id": "0",
        "taxes": [
            {
                "name": "TAX 1",
                "description": "This tax represents a standard sales tax applied to the item.",
                "value": 3.48
            },
            {
                "name": "TAX 2",
                "description": "This tax is a special surcharge imposed by the government for environmental conservation purposes.",
                "value": 22
            }
        ]
    }
]
```

The following JSON represents a list of taxes associated with a particular item, with each tax defined by its name, description, and value:

| Field         | Type   | Description                                                                                       |
| ------------- | ------ | ------------------------------------------------------------------------------------------------- |
| `id`          | string | Request item index, which means the SKU's position on the `items` array sent by the request body. |
| `taxes`       | array  | List of all the taxes types for an SKU.|
| `name`        | string | Tax name that will appear on the checkout.|
| `description` | string | Informative field, which does not appear on the storefront.|
| `value`       | number | Absolute numeric value that will be added to the original price.|

In the example above, the only item in the items array has a cost of `10`, and, including the calculated taxes returned by the tax calculation tool, the total value would be `10 + 3.48 + 22 = 35.48`.

>ℹ️ If no taxes apply to the items in the order, the expected response is an empty array (`[]`).

For the Checkout API to interpret the request body, the `Content-type` must be set to `application/vnd.vtex.checkout.minicart.v1+json`.  

#### Jurisdiction fields

If you use [Avalara](https://www.avalara.com/us/en/index.html) as your tax calculation provider, response bodies can also include the following fields, which refer to the different jurisdictions that may apply according to location.

| Field       | Type   | Description|
| ----------- | ------ | --------------------------------------------------------- |
| `jurisType` | string | Type of jurisdiction that applies to calculation.         |
| `jurisCode` | string | Unique code that identifies the appropriate jurisdiction. |
| `jurisName` | string | Name of the jurisdiction that applies to the calculation. |

These fields are also read by Checkout and added to the `priceTag`.

Below is an example for values that may be contained in these fields, and you can [download all of the jurisdictions and respective codes used by Avalara](https://help.avalara.com/Avalara_AvaTax_Update/Download_jurisdiction_codes).

```json
{
    "Id": "0",  
    "taxes": [  
       {  
         "name": "NY STATE TAX: NEW YORK",  
         "description": "Srixon Q-Star Tour Golf Balls 5013392- Dozen Yellow",  
         "rate": 0.04,  
         "value": 1.4,  
         "jurisCode": "36",  
         "jurisType": "State",  
         "jurisName": "NEW YORK"  
       },  
       {  
         "name": "NY COUNTY TAX: ERIE",  
         "description": "Srixon Q-Star Tour Golf Balls 5013392- Dozen Yellow",  
         "rate": 0.0475,  
         "value": 1.66,  
         "jurisCode": "029",  
         "jurisType": "County",  
         "jurisName": "ERIE"  
       },  
       {  
         "name": "NY STATE TAX: NEW YORK (SHIPPING)",  
         "description": "freight",  
         "rate": 0.04,  
         "value": 0.17,  
         "jurisCode": "36",  
         "jurisType": "State",  
         "jurisName": "NEW YORK"  
       },  
       {  
         "name": "NY COUNTY TAX: ERIE (SHIPPING)",  
         "description": "freight",  
         "rate": 0.0475,  
         "value": 0.2,  
         "jurisCode": "029",  
         "jurisType": "County",  
         "jurisName": "ERIE"  
        }  
    ]  
}
```

By following these guidelines and leveraging the provided examples, you can incorporate tax integration into your VTEX platform.
