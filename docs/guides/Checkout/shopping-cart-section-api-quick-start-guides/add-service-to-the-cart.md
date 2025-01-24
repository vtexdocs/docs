---
title: "Add a service (offering) to a shopping cart"
slug: "add-service-to-the-cart"
hidden: false
createdAt: ""
updatedAt: ""
hidePaginationPrevious: false
hidePaginationNext: false
---
A service, also known as an offering, is an item that may come with a product, optionally and with an additional cost. It is used to assign a value of an additional service to an SKU, as a gift packaging.

You can add a service to a shopping cart by using the [Checkout API](https://developers.vtex.com/docs/api-reference/checkout-api). To do so, follow the sections below.

## Checking if a cart product has a service attached to it

First, you must check if a product has a service available attached to it. This way, you know the options of service you can add to the item in the shopping cart.

You must use the [Cart simulation](https://developers.vtex.com/docs/api-reference/checkout-api#post-/api/checkout/pub/orderForms/simulation?endpoint=post-/api/checkout/pub/orderForms/simulation) endpoint and send the `skuId`, `seller` and `quantity` in the request body, as the code example below.

```json
{    "items": [
        {
            "id": "30",
            "quantity": 1,
            "seller": "1"
        }
    ]
}
```

In the response body, you must check if the `offerings` object presents the following information, as in the example below:

```json
    "offerings": [
        {
            "type": "Removal of additional old appliance",
            "id": "1",
            "name": "Removal of additional old appliance",
            "allowGiftMessage": false,
            "attachmentOfferings": ["Name", "Info"],
            "price": 2999
        }
    ]
```

If the `offerings` array presents this information, the SKU has a service associated with it. You will use the `id` value in the next step.

>ℹ️ If you have multiple services associated with the product, all of them will be returned in the `offerings` array.

## Adding a service to a product

You can add a service to an item in the shopping cart by using the checkout [`orderForm`](https://developers.vtex.com/docs/guides/orderform-fields).

To do so, you must add the item to the cart using the [Add cart items](https://developers.vtex.com/docs/api-reference/checkout-api#post-/api/checkout/pub/orderForm/-orderFormId-/items) endpoint.

Then, you must send the service `id` from the previous step in the desired `item` by using the request body of the `POST` `https://{accountName}.{environment}.com/api/checkout/pub/orderForm/{orderFormId}/items/{itemPosition}/offerings` request:

```json
{
    "id": "1"
}
```

The expected response is the `orderForm` structure with the `offerings` array with the service information inside it, as the code below:

```json
    "offerings": [
        {
            "type": "Removal of additional old appliance",
            "id": "1",
            "name": "Removal of additional old appliance",
            "allowGiftMessage": false,
            "attachmentOfferings": ["Name", "Info"],
            "price": 2999
        }
    ]
```

### Adding more than one service to a product

If you need to add more than a service to a specific product, you must add more units of the product that the service is attached to. To do so, you must follow the steps below:

1. Update the product you want to add the service to have `"quantity": 1`. Use the  [Handle cart items](https://developers.vtex.com/docs/api-reference/checkout-api#patch-/api/checkout/pub/orderForm/-orderFormId-/items?endpoint=patch-/api/checkout/pub/orderForm/-orderFormId-/items) endpoint with the following request body:

```json
{    
    "orderItems": [
        {
            "index": 0,
            "quantity": 1
        }
    ]
}
```
2. Attach the `offering` to the `item` in the shopping cart. Use the `POST` `https://{accountName}.{environment}.com/api/checkout/pub/orderForm/{orderFormId}/items/{itemPosition}/offerings` request as the previous section:

```json
{
    "id": "1"
}
```
3. Update the `quantity` back to the previous value, sending the `noSplitItem` field as `true` in the [Handle cart items](https://developers.vtex.com/docs/api-reference/checkout-api#patch-/api/checkout/pub/orderForm/-orderFormId-/items?endpoint=patch-/api/checkout/pub/orderForm/-orderFormId-/items) endpoint in the request body. This field will make sure the items do not split the configuration, making it possible to have the same `quantity` of products and services.

```json
    "orderItems": [
        {
            "index": 0,
            "quantity": 4
        }
    ],
    "noSplitItem": true
```

## Removing a service (offering) from a shopping cart

To remove a service (offering), you must use the `POST` `https://{accountName}.{environment}.com/api/checkout/pub/orderForm/{orderFormId}/items/{itemPosition}/offerings/{serviceId}/remove` endpoint with the service `id` in the request body:

```json
{
    "id": "1" 
}
```

The expected response is the `orderForm` structure with the `offerings` array empty, like the example below:

```json
    "offerings": []
```
