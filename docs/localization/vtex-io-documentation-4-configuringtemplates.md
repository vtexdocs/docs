---
title: "4. Configuring templates"
slug: "vtex-io-documentation-4-configuringtemplates"
hidden: false
createdAt: "2020-06-03T16:02:44.335Z"
updatedAt: "2024-11-27T13:38:35.073Z"
category: "Storefront Development"
excerpt: "Learn how to manage templates and customize your Store Theme."
---

In this guide, you'll learn how to customize your store theme by managing templates that define the structure of your website pages. Templates declare `JSON` blocks that, once rendered, determine the set of components for your website pages, such as the homepage, product page, search results page, etc.

The [Store Theme](https://developers.vtex.com/docs/guides/vtex-io-documentation-store-theme) app already implements basic templates for each page of your store, defined within its `blocks.json` or `blocks.jsonc` files. These templates enable your store to display VTEX Store Framework default components, even if you haven’t made any custom configurations in the code. By managing templates, you can create a custom theme for your website by adding or removing blocks to meet your business needs.

## Before you begin

<Steps>

### Learn about the JSON block concept

Familiarize yourself with the concept of a `JSON` block - the smallest Store Framework abstraction of React components displayed on the user interface. Thus, blocks are self-contained pieces of code, exported to the platform by independent apps, that determine how components are rendered on your website.

Blocks are imbued with higher flexibility, allowing you to achieve complex scenarios and specific component behaviors by configuring their properties (*props*) or even declaring them in other blocks. In practice, when you edit your theme's code using the Store Theme app, you're directly modifying blocks that will become your store's page components when rendered.

> ℹ To add a new component to a page, you simply declare a new block in the corresponding template. Similarly, removing a block from a template will exclude its associated component from the page.

### Get to know the property (prop) concept

To manage your templates efficiently, be familiar with the concept of `properties` (*prop*), which define the performance and visual identity of the component rendered in the interface. The more props a block has, the more flexible its configuration becomes for the end user.

Every JSON is defined using `{ }`, with keys and values that together specify its properties, representing its inherent characteristics. See the example below:

```json
{
 "name": "Pedro",
 "height": 1.90
}
```

In the example above, `name` and `height` are the object's keys, and their respective values are `Pedro` and `1.90`.

The `key + value` pair constitutes the property (or *prop*) of the JSON, defining its essential characteristics.

> ℹ The key and value can also be called, respectively, property name and property value.

### Understand the block composition

When a block is being developed, the composition definition indicates how the block’s content is structured or how it interacts with other components. There are 3 types of composition definitions:

- `blocks`: Have a fixed position on the store’s page irrespective of where they were declared in the code, leading to a preordained position on the UI.
- `children`: Do not have a fixed position on the store’s page, which means that how they’re declared in the code directly impacts the page position. The `children` block declared first will be at the top of the page, followed by the second one below it, and so on.
- `slots`: Placeholders within a block that enable the insertion of dynamic content. It is useful for flexible component design where content can be passed into specific slots, enabling the customization or reuse of a block with different content.

According to their composition, the listed blocks will determine whether they should be declared in the parent block's `blocks` list or in its `children` list when building a single component on the UI.

> ℹ You can find out which composition a block has by looking at its code in the exporting app's `interfaces.json` file.

</Steps>

> ℹ Learn more about these and other relevant concepts in [Composition](https://developers.vtex.com/docs/guides/vtex-io-documentation-composition), [Interfaces](https://developers.vtex.com/docs/guides/vtex-io-documentation-interface), [Properties](https://developers.vtex.com/docs/guides/vtex-io-documentation-properties), and [Slots](https://developers.vtex.com/docs/guides/vtex-io-documentation-slots).

## Instructions

### Declaring blocks in your Store Theme app

Declare all your blocks in the `blocks.jsonc` file, or create as many files and folders as needed within the `store` folder to organize store blocks and templates. You can also declare blocks in the `blocks` subfolder. The only difference is that `jsonc` files allow you to add comments to the code.

Since blocks are pieces of code exported by VTEX Store Framework apps, whenever a block is used in your theme, the app behind it must be declared in your Store Theme [dependencies](https://developers.vtex.com/docs/guides/vtex-io-documentation-dependencies/) list.

The `dependencies` object within the `manifest.json` file of your Store Theme app specifies the names and versions of various apps. These apps are pre-listed, as the default Store Theme code already defines templates that use blocks exported by them.

When declaring a new block in your Store Theme app, check if the app blocking it is listed as a dependency. If not, open the `manifest.json` file and add the app name and desired version to the `dependencies` list, following this format: `"vtex.{appName}": "{majorVersion}.x"`.

> ⚠ Replace the values between the curly braces based on your scenario.

### Managing blocks in your theme

To better understand how to manage blocks within your Store Theme app, follow the steps below to see the structure of the predefined homepage template:

1. Open the Store Theme app using the code editor of your choice.
2. Go to `store` and then `blocks`.
3. Access `home` and then `home.jsonc`. You'll see a result similar to the following:

```json
{
  "store.home": {
    "blocks": [
      "list-context.image-list#demo",
      /* You can make references to blocks defined in other files.
       * For example, `flex-layout.row#deals` is defined in the `deals.json` file. */
      "flex-layout.row#deals",
      "rich-text#shelf-title",
      "flex-layout.row#shelf",
      "info-card#home",
      "rich-text#question",
      "rich-text#link",
      "newsletter"
    ]
  },

  "shelf#home": {
    "blocks": ["product-summary.shelf"]
  },

  "product-summary.shelf": {
    "children": [
      "product-summary-name",
      "product-summary-description",
      "product-summary-image",
      "product-summary-price",
      "product-summary-sku-selector",
      "product-summary-buy-button"
    ]
  },

  "list-context.image-list#demo": {
    "children": ["slider-layout#demo-images"],
    "props": {
      "height": 720,
      "images": [
        {
          "image": "https://storecomponents.vteximg.com.br/arquivos/banner-principal.png",
          "mobileImage": "https://storecomponents.vteximg.com.br/arquivos/banner-principal-mobile.jpg"
        },
        {
          "image": "https://storecomponents.vteximg.com.br/arquivos/banner.jpg",
          "mobileImage": "https://storecomponents.vteximg.com.br/arquivos/banner-principal-mobile.jpg"
        }
      ]
    }
  },
  "slider-layout#demo-images": {
    "props": {
      "itemsPerPage": {
        "desktop": 1,
        "tablet": 1,
        "phone": 1
      },
      "infinite": true,
      "showNavigationArrows": "desktopOnly",
      "blockClass": "carousel"
    }
  },

  "rich-text#shelf-title": {
    "props": {
      "text": "## Summer",
      "blockClass": "shelfTitle"
    }
  },
  "flex-layout.row#shelf": {
    "children": ["list-context.product-list#demo1"]
  },
  "list-context.product-list#demo1": {
    "blocks": ["product-summary.shelf"],
    "children": ["slider-layout#demo-products"],
    "props": {
      "orderBy": "OrderByTopSaleDESC"
    }
  },
  "slider-layout#demo-products": {
    "props": {
      "itemsPerPage": {
        "desktop": 5,
        "tablet": 3,
        "phone": 1
      },
      "infinite": true,
      "fullWidth": true,
      "blockClass": "shelf"
    }
  },

  "info-card#home": {
    "props": {
      "id": "info-card-home",
      "isFullModeStyle": false,
      "textPosition": "left",
      "imageUrl": "https://storecomponents.vteximg.com.br/arquivos/banner-infocard2.png",
      "headline": "Clearance Sale",
      "callToActionText": "DISCOVER",
      "callToActionUrl": "/sale/d",
      "blockClass": "info-card-home",
      "textAlignment": "center"
    }
  },

  "rich-text#question": {
    "props": {
      "text": "**This is an example store built using the VTEX platform.\nWant to know more?**",
      "blockClass": "question"
    }
  },

  "rich-text#link": {
    "props": {
      "text": "\n**Reach us at**\nwww.vtex.com.br",
      "blockClass": "link"
    }
  },

  "product-summary-buy-button": {
    "props": { 
      "displayBuyButton": "displayButtonAlways"
    }
  }
}
```

As you can see above, the default `store.home` homepage template declares the following blocks:

- `list-context.image-list#demo`
- `flex-layout.row#deals`
- `rich-text#shelf-title`
- `flex-layout.row#shelf`
- `info-card#home`
- `rich-text#question`
- `rich-text#link`
- `newsletter`

This means that your default store homepage will comprise the components defined by these blocks.

To build more complex components, the `home.jsonc` file includes each block’s declaration and configuration, using the block's props and, if necessary, other blocks.

>⚠ More than simply declaring a block in the block list template, you must also define its behavior when rendered as a component. To do this, use the block's props, as shown in the [Clarifying block naming and properties](#clarifying-block-naming-and-properties) section, and include other child blocks to configure it, as detailed in [Defining blocks composition](#defining-blocks-composition).

### Clarifying block naming and properties

Still in the `home.jsonc` file, use `ctrl+f` and search for the `rich-text#question` block. This block renders a component that displays markdown text to users.

```json
"rich-text#question": {
  "props": {
    "text": "**This is an example store built using the VTEX platform. Want to know more?**",
    "blockClass": "question"
  }
},
```

The `rich-text#question` block has two props: `text` and `blockClass`. The `text` prop specifies the content the component will display, while `blockClass` defines an ID used for customization.

To check the available props of the app behind the `rich-text` block, see the Configuration section within the [Rich Text](https://developers.vtex.com/docs/guides/vtex-rich-text) app documentation. Note that the exported block's name is simply `rich-text`, whereas Store Theme uses `rich-text#block`. This is because you can use a `#` symbol after the block's official name to easily identify it when inserting it into the theme's code and better organize the theme.

> ℹ All the props available to configure a block can be found in the documentation of its exporting app or in the block's own documentation (if applicable).

### Defining blocks composition

Still in the `home.jsonc`, search for the`shelf#home` block.

```json
"shelf#home": {
  "blocks": ["product-summary.shelf"]
},
```

Note that it declares another block to your `blocks` list, which in turn declares other blocks below in a list called `children`:

```json
"product-summary.shelf": {
  "children": [
    "product-summary-name",
    "product-summary-description",
    "product-summary-image",
    "product-summary-price",
    "product-summary-sku-selector",
    "product-summary-buy-button"
  ]
},
```

In the example above, `product-summary.shelf` requires other blocks as children, such as `product-summary-name`, to render the component properly.

> ℹ As previously mentioned, a component can be a crossroad for multiple blocks. Therefore, one of your theme blocks may need to list other blocks to achieve the desired rendering on the UI.

To build a component using multiple blocks, the main block can declare a `blocks` list, such as `shelf#home`, or a `children` list, as seen in the `product-summary.shelf` block.

As explained in [Understand block composition](#understand-block-composition), the choice between using a `blocks` or `children` list depends on the *composition* of the blocks being declared.
