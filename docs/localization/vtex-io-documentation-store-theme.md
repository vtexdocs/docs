---
title: "Store Theme"
slug: "vtex-io-documentation-store-theme"
hidden: false
createdAt: "2024-07-24T13:48:10.752Z"
updatedAt: "2024-12-03T15:29:21.377Z"
category: "Storefront development"
seeAlso:
  - "/docs/guides/vtex-io-documentation-manifest"
  - "/docs/apps/vtex.store-sitemap"
---

In [Store Framework](https://developers.vtex.com/docs/guides/store-framework), a Store Theme is a storefront template that shapes your store's appearance and functionality. It determines how each element of your store will be displayed on the storefront.

## Project structure

Although the structure of a Store Theme project may vary depending on its specific settings, it typically includes the following files and folders:

```txt mark=5,9,16
📂 STORE-THEME/
│
├── 📂 .github/
├── 📂 public/
├── 📂 store/
│   ├── 📂 blocks/
│   ├── 📄 blocks.jsonc
│   └── 📄 routes.json
├── 📂 styles/
│   ├── 📂 configs/
│   └── 📂 css/
├── 📄 .editorconfig
├── 📄 .gitignore
├── 📄 .vtexignore
├── 📄 CHANGELOG.md
├── 📄 manifest.json
├── 📄 package-lock.json
└── 📄 README.md
```

Some of these files and folders are essential for the theme to function correctly:

- **`/store` folder:** Contains the blocks, interfaces, and routes necessary to build the storefront.
- **`/styles` folder:** Contains the store visual elements, such as colors, typography, and other style-related settings.
- **`manifest.json` file:** Contains metadata about the app, including vendor, name, version, [dependencies](https://developers.vtex.com/docs/guides/vtex-io-documentation-dependencies/), and [builders](https://developers.vtex.com/docs/guides/vtex-io-documentation-builders/).

>⚠ For your project to work properly, you must have at least the `store` and `styles` builders configured within the `manifest.json` file.

Store Themes are [VTEX IO](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-io) apps that inherently use the [`store` builder](https://developers.vtex.com/docs/guides/vtex-io-documentation-store-builder). This builder allows you to link routes to templates, which consist of other reusable [components](https://developers.vtex.com/docs/guides/vtex-io-documentation-components) and layout [blocks](https://developers.vtex.com/docs/guides/vtex-io-documentation-composition) organized in the `/store` folder.

To export the CSS configurations in the `/styles` folder for your Store Framework blocks, Store Themes leverage the [`styles` builder](https://developers.vtex.com/docs/guides/vtex-io-documentation-styles-builder). This builder helps set a cohesive style for all components in your Store Theme app.

For more information about available builders, check this [list of builders](https://developers.vtex.com/docs/guides/vtex-io-documentation-builders#list-of-builders).

## Development tools

The VTEX IO platform facilitates the development of Store Themes by providing tools such as [VTEX IO CLI](https://developers.vtex.com/docs/guides/vtex-io-documentation-vtex-io-cli-installation-and-command-reference) and [workspaces](https://developers.vtex.com/docs/guides/vtex-io-documentation-creating-a-development-workspace) for developers, as well as content management with [Site Editor](https://developers.vtex.com/docs/guides/vtex-io-documentation-site-editor) for business users.

Store Themes can be customized by adding native [VTEX IO apps](https://developers.vtex.com/docs/vtex-io-apps) or developing [custom React components](https://developers.vtex.com/docs/guides/vtex-io-documentation-1-developing-storefront-apps-using-react-and-vtex-io) to meet business needs and enhance user experience.

Below are some available themes to get started:

- [Minimum Boilerplate Theme](#minimum-boilerplate-theme)
- [Store Theme](#store-theme)

## Available themes

### Minimum Boilerplate Theme

The [Minimum Boilerplate Theme](https://github.com/vtex-apps/minimum-boilerplate-theme) serves as a basic starting point for developers to create new storefronts on the VTEX IO platform. It offers a basic and functional structure that can be customized and expanded based on the project's specific needs.

The Minimum Boilerplate Theme should be used only when you want to start a new store theme without any pre-set configurations.

>ℹ️ Learn how to set this boilerplate in the [Minimum Boilerplate Theme](https://developers.vtex.com/docs/apps/vtex.minimumtheme) documentation.

### Store Theme

The [**Store Theme**](https://github.com/vtex-apps/store-theme) is a boilerplate with pre-set configurations to create a store using [VTEX IO](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-io).

![store-theme-gif](https://user-images.githubusercontent.com/67270558/169829563-6ac39b89-7c9e-4d5e-a2ac-c2139e70e34a.gif)

This boilerplate gives you a ready-to-go default storefront structure, including:

- **Pre-configured layouts:** A variety of files organized in different folders within the `/store/blocks` folder. These files combine our native [components](https://developers.vtex.com/docs/guides/vtex-io-documentation-components) to create templates for different parts of the store, such as the homepage, product details page, and order-placed page.
- **Default styles:** A customizable set of styles to achieve a professional look and feel without extensive custom styling.
- **Sitemap:** An example of a [Sitemap](https://github.com/vtex-apps/store-theme/blob/master/sitemap/sitemap.json) use case.

>ℹ️ Learn how to start a project with this boilerplate in the [Getting started](https://developers.vtex.com/docs/guides/getting-started-3) section.
