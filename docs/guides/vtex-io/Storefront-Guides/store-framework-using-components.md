---
title: "Using components"
slug: "store-framework-using-components"
hidden: false
createdAt: "2025-01-21T16:36:39.917Z"
updatedAt: ""
excerpt: "Discover how components in VTEX IO Store Framework enable you to build your storefront, from basic elements to advanced customizations." 
---

Components are building blocks used to create storefronts and admin apps. They are built on the [VTEX IO development platform](https://developers.vtex.com/docs/guides/vtex-io-documentation-what-is-vtex-io) using [React](https://react.dev/) technology.

These components are modular, reusable pieces of code that encapsulate specific features and can be combined to create complex user interfaces. They range from basic elements, such as buttons and forms, to more complex ones, such as product carousels and navigation bars. Conceptually, components resemble JavaScript functions: they take arbitrary inputs, referred to as `props`, and return React elements that articulate what should be displayed on the screen.

You can use our [native components](#native-components), customize them as needed, or even [create your own components](#custom-components) to meet the specific needs of your projects on the VTEX IO platform.

In the guides of this section, you will explore how to leverage components to create customizable storefronts.

## Before you begin

<Steps>

### Develop your Store Theme

Make sure your store has a [Store Theme](https://developers.vtex.com/docs/guides/vtex-io-documentation-store-theme) developed following the [Storefront](https://developers.vtex.com/docs/guides/getting-started-3) guide.

### Check the builders

Check if the builders are properly installed in your Store Theme. To use builders, your account must have at least version `vtex.builder-hub@0.293.4` installed. Also, you need to specify them in the app's `manifest.json` file. Learn more in [Builders](https://developers.vtex.com/docs/guides/vtex-io-documentation-builders).

You must have at least the following builders configured:

- [store builder](https://developers.vtex.com/docs/guides/vtex-io-documentation-store-builder): Enables the development of Store Framework storefronts.
- [react builder](https://developers.vtex.com/docs/guides/vtex-io-documentation-react-builder): Used to develop apps with [React](https://react.dev/) when your project requires customized frontend solutions.

### Learn about VTEX IO apps

Familiarize yourself with [VTEX IO apps](https://developers.vtex.com/docs/vtex-io-apps) and learn how to build custom solutions following the guide [Storefront apps](https://developers.vtex.com/docs/guides/vtex-io-documentation-1-developing-storefront-apps-using-react-and-vtex-io).

</Steps>

## Essential concepts

A deep understanding of native and custom components is important for using them more effectively.

### Native components

Within the VTEX IO ecosystem, different types of components address different aspects of store development. Below are the main types of components:

- [**Basic components**](https://developers.vtex.com/docs/guides/basic-components): Reusable UI elements such as buttons, forms, input fields, and other fundamental interface elements. These components provide the building blocks for creating more complex UI elements and features.

The [Product Summary](https://developers.vtex.com/docs/apps/vtex.product-summary) exemplifies a basic storefront component, summarizing essential product information like name, price, and image, which can be seamlessly integrated into other store blocks, such as the [Shelf](https://developers.vtex.com/docs/apps/vtex.shelf).

- [**Store Components**](https://developers.vtex.com/docs/guides/store-components): Collection of components that can be used to create or extend other VTEX apps, aiming to improve the functionality and appearance of the storefront. They cover a range of elements, including product displays, navigation bars, checkout processes, and category pages. Some components in this collection offer advanced features, such as product recommendations, search filters, and personalized content delivery.

### Custom components

When building a [store theme](https://developers.vtex.com/docs/guides/vtex-io-documentation-6-buildingyourownstoretheme), you can leverage existing VTEX IO apps or create custom apps to add new components and extend the platform features.

See our guide about how to [develop an app](https://developers.vtex.com/docs/guides/vtex-io-documentation-developing-an-app).

## Guides in this section

<Flex>

<WhatsNextCard
title="Building a horizontal Product Summary"
description="Discover the process of building a horizontal Product Summary."
linkTo="https://developers.vtex.com/docs/guides/vtex-io-documentation-building-a-horizontal-product-summary"
linkTitle="See more"
/>

<WhatsNextCard
title="Building a Shelf"
description="Understand how to build and customize shelves to display products on your store’s pages."
linkTo="https://developers.vtex.com/docs/guides/vtex-io-documentation-building-a-shelf"
linkTitle="See more"
/>

<WhatsNextCard
title="Configuring custom images for the SKU Selector"
description="Learn how to customize the images for your SKU Selector."
linkTo="https://developers.vtex.com/docs/guides/vtex-io-documentation-configuring-custom-images-for-the-sku-selector"
linkTitle="See more"
/>

<WhatsNextCard
title="Creating a native form for your store users"
description="Discover how to customize and integrate forms directly on your store."
linkTo="https://developers.vtex.com/docs/guides/vtex-io-documentation-creating-a-native-form-for-your-store-users"
linkTitle="See more"
/>

<WhatsNextCard
title="Creating a product availability form"
description="Learn how to create a product availability form with this step-by-step guide."
linkTo="https://developers.vtex.com/docs/guides/vtex-io-documentation-creating-a-product-availability-form"
linkTitle="See more"
/>

<WhatsNextCard
title="Using Sandbox blocks"
description="Learn how to use Sandbox blocks to test different components in a safe environment."
linkTo="https://developers.vtex.com/docs/guides/vtex-io-documentation-using-sandbox-blocks"
linkTitle="See more"
/>

<WhatsNextCard
title="Using the Assets Builder"
description="Explore how to manage assets in your VTEX IO projects using the Assets builder."
linkTo="https://developers.vtex.com/docs/guides/vtex-io-documentation-using-the-assets-builder"
linkTitle="See more"
/>

</Flex>
