---
title: "3. Creating a Store Theme project"
slug: "vtex-io-documentation-3-settingyourstoretheme"
hidden: false
createdAt: "2020-06-03T16:02:44.903Z"
updatedAt: "2025-01-28T18:00:46.857Z"
category: "Storefront Development"
excerpt: "Discover how to create your very first Store Framework storefront."
---

This guide explains how to start building a [Store Theme](https://developers.vtex.com/docs/guides/vtex-io-documentation-store-theme), a VTEX IO project that uses the [store builder](https://developers.vtex.com/docs/guides/vtex-io-documentation-store-builder) and Store Framework blocks to create the storefront of a VTEX store. The Store Theme defines the store visual and interactive elements, including layout, colors, typography, icons, and animations.

To kickstart our storefront project, we'll use a pre-defined [Store Theme boilerplate app](https://github.com/vtex-apps/store-theme), which simplifies the process of creating a custom Store Theme by providing pre-defined templates and styles. For more information about available themes, see the guide [Store Theme](https://developers.vtex.com/docs/guides/vtex-io-documentation-store-theme).

## Before you begin

<Steps>

### Have the Edtion Store app

Make sure your VTEX account has the Store Edition app installed, as recommended in this track's second step [Configuring your account](https://developers.vtex.com/docs/guides/vtex-io-documentation-2-prerequesites). Otherwise, you won't be able to successfully implement the VTEX Store Framework.

### Learn about the Store Theme app’s structure

Familiarize yourself with the Store Theme’s structure. Understanding the purpose of each file and folder will help you configure the store’s templates and visual theme according to your needs. Learn about in [Project structure](https://developers.vtex.com/docs/guides/vtex-io-documentation-store-theme#project-structure).

</Steps>

## Instructions

### Step 1 - Downloading the Store Theme app

The VTEX IO CLI simplifies starting a new VTEX IO project by providing a list of pre-defined app templates. In the following steps, we'll kickstart a new Store Theme project.

1. Using your terminal, navigate to an existing local directory where you want to copy the Store Theme:

 ```sh
 cd {folderName}
 ```

> ⚠ Replace `{folderName}` with the actual folder name where you want to copy the Store Theme boilerplate app.

2. Run the following command to clone the Store Theme boilerplate app in your folder:

 ```sh
 vtex clone https://github.com/vtex-apps/store-theme.git
 ```

3. Open the `store-theme` in the code editor of your preference.
4. Go to the `manifest.json` file and replace the predefined `vendor` value with the account name of the store you're developing. This will ensure that you can correctly publish your Store Theme app later.

### Step 2 - Linking your local code to the VTEX IO platform

Since the Store Theme boilerplate app already includes a default theme, you can immediately see how this theme affects your website frontend by following the instructions below:

1. Open the terminal and log in to your VTEX account.

```sh
 vtex login {accountName}
```

> ⚠ Replace `{accountName}` with the name of your VTEX account.

2. Create a [development workspace](https://developers.vtex.com/docs/guides/vtex-io-documentation-creating-a-development-workspace) by running the following command:

```sh
 vtex use {workspaceName}
```

> ⚠ Replace `{workspaceName}` based on your scenario.

3. Change to the `store-theme` directory.
4. Link the Store Theme app to the current workspace by running the following command:

 ```sh
  vtex link
 ```

The `vtex link` command sends your code to the platform, allowing you to see your changes in real time.

![VTEX link example](https://cdn.jsdelivr.net/gh/vtexdocs/dev-portal-content@main/images/link-store-theme.png)

By successfully running this command in your terminal, your local code is sent to the VTEX IO cloud-native infrastructure and reflected in the development workspace you're currently working in. Any changes made to your Store Theme app files will now be automatically reflected on your website in real time.

### Step 3 - Checking out your new Store Theme

To view your new Store Theme in action on your store's website, run the following command in your terminal:

```sh
 vtex browse
```

This command will open your browser with the workspace you're working on. Alternatively, you can navigate directly to `https://{workspaceName}--{accountName}.myvtex.com`, replacing the placeholders with your development workspace and VTEX account name.

Once you're logged in, you should see the following Store Theme rendered on your store's website:

![Store Theme](https://cdn.jsdelivr.net/gh/vtexdocs/dev-portal-content@main/images/vtex-io-documentation-3-settingyourstoretheme-3.png)

Now that your store is using a default theme code, you can start configuring the Store Theme app to match your store needs. This includes changing templates and customizing styles to create a unique identity for your store.

In the upcoming guides of this tutorial, you'll learn how to define templates by configuring and combining components for each store page, as well as declaring styles such as colors, typography scales, and spacing.
