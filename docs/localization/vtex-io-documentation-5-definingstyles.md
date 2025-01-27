---
title: "5. Defining styles"
slug: "vtex-io-documentation-5-definingstyles"
hidden: false
createdAt: "2020-08-11T07:03:18.383Z"
updatedAt: "2024-11-28T18:48:33.390Z"
category: "Storefront Development"
excerpt: "Learn how to set specific styles for your store components to enhance your store's user experience."
---

After understanding blocks and templates and how they render interface components, this guide will show you how to customize them to match your store identity.

The Store Theme allows you to:

- [Set a default style for all your store components](#setting-a-default-style-for-all-store-components)
- [Set a specific style for a component type or a single component](#setting-a-specific-style-for-a-component-type-or-a-single-component)

## Setting a default style for all store components

To set the default style for your store, you can use the `style.json` file in the `style` folder of the Store Theme app. This single file allows you to customize the appearance of your store by modifying the default definitions declared within it. This approach avoids the need to customize individual components on each page.

For example, you can set the default theme background color to blue by changing the `semanticColors` block's `base` property:

```json
"semanticColors": {
  "background": {
    "base": "#00BFFF",
    "base--inverted": "#03044e",
    "action-primary": "#0F3E99",
    "action-secondary": "#eef3f7",
    "emphasis": "#f71963",
    "disabled": "#f2f4f5",
    "success": "#8bc34a",
    "success--faded": "#eafce3",
    "danger": "#ff4c4c",
    "danger--faded": "#ffe6e6",
    "warning": "#ffb100",
    "warning--faded": "#fff6e0",
    "muted-1": "#727273",
    "muted-2": "#979899",
    "muted-3": "#cacbcc",
    "muted-4": "#e3e4e6",
    "muted-5": "#f2f4f5"
  },
}
```

> ⚠ The `styles.json` file only accepts [HEX values](https://www.w3schools.com/html/html_colors_hex.asp) to set a color. Using other formats, such as RGB, may break the PWA module.

For detailed instructions on customizing your theme, see the [VTEX Styleguide](https://styleguide.vtex.com/#/Styles), a comprehensive CSS framework with guidelines for defining component styles. It includes a detailed explanation of the `styles.json` file structure to help you in your customizations.

## Setting a specific style for a component type or a single component

The `style.json` file enables more generic customization of your store visual style and can be useful in most scenarios.

If you want to create a more distinctive store identity with certain elements featuring unique styles different from the default theme, consider this scenario: Imagine your store primarily uses blue as its main color, but you want the text components (created by `rich-text` blocks) to display in red. To make only one specific text component red while keeping the rest in the default blue color, you can achieve this advanced customization by overriding the default styles defined in `styles.json`. This can be done using CSS handles and the `blockClass` prop.

To apply advanced customization to your store style, see the guide [Using CSS Handles for store customization](https://developers.vtex.com/docs/guides/vtex-io-documentation-using-css-handles-for-store-customization/).
