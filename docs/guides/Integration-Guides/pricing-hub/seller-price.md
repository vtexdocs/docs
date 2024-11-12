---
title: "B2B Seller Price"
slug: "seller-price"
hidden: false
createdAt: "2021-11-08T16:34:25.542Z"
updatedAt: "2022-06-13T16:08:09.500Z"
---

> This feature is in closed beta, available only for selected customers. If you have any questions, contact our [Support](https://help.vtex.com/support).

In B2B commerce, it is often necessary to offer personalized prices. For example, in the commercial relationship between a distributor (seller) and different supermarkets (buyers), there might be specific price deals in place for each supermarket. In this case, the distributor (seller) needs to set specific prices for each customer.

This scenario gets more complex when the seller’s products are offered in a B2B marketplace, since marketplaces usually centralize the relationship with customers.

Considering this, our B2B Seller Price feature allows sellers from B2B marketplaces to configure specific price tables for each customer, based on their email address, and apply these personalized prices using [Pricing Hub](https://developers.vtex.com/docs/guides/pricing-hub-overview). This feature works for all types of sellers in the B2B scenario, whether they are white label or not.

## How it works

The diagram below shows how the process works, after all the required [configurations](#setup).

![](https://user-images.githubusercontent.com/77292838/212167865-3a63bd16-669d-47ed-a6d5-5da730a052a9.png)

When a customer logs in on a B2B marketplace which has Pricing Hub enabled, it will make a `POST` [Get Prices](https://developers.vtex.com/docs/api-reference/pricing-hub#post-/api/pricing-hub/prices) request to the Pricing Hub API to fetch prices information from the B2B Seller’s external prices app. The app will then return the prices information in the response, applying the specific prices associated with each customer email, as set by the seller.


>ℹ️ You will need to create a custom component on the front end, in order to display the prices that the app delivers.
>
## Setup

To set up this process, the marketplace and each seller must follow the instructions below.

### Marketplace

The marketplace must follow the steps below to activate the B2B Seller Price:

1. Contact our [Support](https://help.vtex.com/support) and open a request to enable Pricing Hub on the marketplace and seller accounts.
2. Enable the use of external prices by the seller through the `PUT` [Configure External Price Source](https://developers.vtex.com/docs/api-reference/pricing-hub#put-/config) of the Pricing Hub API.
3. Allow VTEX to share customers’ email addresses with the seller. To do so, it is necessary to set `'AllowEmailSharing'` as the value for the TrustPolicy field in the `POST` [Create Seller](https://developers.vtex.com/docs/api-reference/marketplace-apis#post-/-accountName-.-environment-.com.br/api/seller-register/pvt/sellers) or `PUT` [Update Seller](https://developers.vtex.com/docs/api-reference/marketplace-apis#patch-/-accountName-.-environment-.com.br/api/seller-register/pvt/sellers/-sellerId-) endpoints.

>ℹ️ Make sure to manage the relationship between the marketplace’s catalog and the sellers’ catalogs on the Received SKUs page. Read the article on [Cataloging received SKUs](https://help.vtex.com/en/tutorial/manual-sku-cataloging--tutorials_396) for more information on this process.

### Seller

The B2B sellers – white label or not – who want to use this feature must follow the instructions below.

1. Configure specific price tables associated with the customers’ respective email addresses, either using the [Pricing API](https://developers.vtex.com/docs/guides/pricing-api-overview) or the [VTEX Admin panel](https://help.vtex.com/en/tutorial/configurar-price-tables-especificas--5S9oDOMHNmY4K0kAewAiWY).
2. Develop a VTEX IO app to allow querying price tables by email, integrating with external price systems, and install it in the master workspace.

   We offer a reference implementation template to simplify this process: [Node template](https://github.com/vtex/unilever-external-prices-node). This template app can be customized to use other price parameters, by following the instructions on the app repository.

   Make sure your app complies with the [specifications detailed in the Pricing Hub documentation](https://developers.vtex.com/docs/guides/pricing-hub-overview#specifications).

>⚠️ Pricing Hub only recognizes the master workspace. This means linking it to a test workspace will not work. For more information on the different types of workspaces, read our [Workspace](https://developers.vtex.com/docs/guides/vtex-io-documentation-workspace) documentation.

## Learn more

- [Pricing Hub - Overview](https://developers.vtex.com/docs/guides/pricing-hub-overview)
- [Pricing Hub - Get Prices](https://developers.vtex.com/docs/api-reference/pricing-hub#post-/api/pricing-hub/prices)
