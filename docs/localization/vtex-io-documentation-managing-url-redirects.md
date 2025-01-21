---
title: "Managing URL redirects"
slug: "vtex-io-documentation-managing-url-redirects"
hidden: false
createdAt: "2020-06-03T16:02:44.302Z"
updatedAt: "2024-11-25T18:10:16.429Z"
excerpt: "Learn how to manage your store's URL redirects to prevent 404 errors."
---

URL redirection is a method used to forward website visitors and search engines from one URL to another. It might be useful when you need to move content to a new URL, remove an old product page, or direct users from a specific region to a custom page. Implementing the appropriate redirects can improve the user experience by preventing visitors from encountering 404 error pages.

Check the following sections to learn how to [create](#creating-url-redirects), [remove](#deleting-url-redirects), and [verify](#verifying-url-redirects) URL redirects for your store.

## Before you begin

1. [Install the VTEX IO Command-Line Interface (CLI)](https://developers.vtex.com/docs/guides/vtex-io-documentation-vtex-io-cli-installation-and-command-reference).
2. [Install the `redirects` plugin for the VTEX IO CLI](https://developers.vtex.com/docs/guides/vtex-io-documentation-vtex-io-cli-plugins#installing-a-plugin):

  ```sh
  vtex plugins install redirects
  ```

## Creating URL redirects

1. Using the [CSV file template](#csv-file-template) as a reference, create a `.csv` file containing the redirects you want to create.
2. Save the file with a name of your choice.
3. Open the terminal and log in to your VTEX account.
4. Import the redirects into your account by running the following command:
- *Replace `{CSVpath}` with the path to your `.csv` file.*

    ```sh
    vtex redirects import {CSVpath}
    ```

Once your file is processed, the redirects will take effect. Please keep in mind that this may take some time.

## Deleting URL redirects

1. Using the [CSV file template](#csv-file-template) as a reference, create a `.csv` file containing the redirects you want to delete.
2. Save the file with a name of your choice.
3. Open the terminal and log in to your VTEX account.
4. Delete the redirects from your account by running the following command:
- *Replace `{CSVpath}` with the path to your `.csv` file.*

    ```sh
    vtex redirects delete {CSVpath}
    ```

## Verifying URL redirects

1. Open the terminal and log in to your VTEX account.
2. Retrieve the full list of your store's redirects into a `.csv` file by running the command below.
- *Replace `{fileName}` with a name of your choice.*

    ```sh
    vtex redirects export {fileName}.csv
    ```

After running this command, a file named `{fileName}.csv` containing your store redirects will be created in your current directory.

Check the [CSV file template](#csv-file-template) to understand the meaning of each field in the generated `.csv` file.

## CSV file template

To create or delete URL redirects in your store, you must create a `.csv` file as in the example below.

![redirects](https://cdn.jsdelivr.net/gh/vtexdocs/dev-portal-content@main/images/redirects.png)

Make sure the file contains a row with four columns and the following values:

| Property name | Description                                                                                   | Example                   |
| ------------- | --------------------------------------------------------------------------------------------- | ------------------------- |
| `from`        | Original path.                                                                                | `/blouse/p`               |
| `to`          | Relative path or full URL to which you want to redirect your visitors.                        | `/shirts/p` |
| `type`        | Redirect type. It can be `TEMPORARY` or `PERMANENT`                                                     | `TEMPORARY`               |
| `endDate`     | **Only for `TEMPORARY` redirects**. Expiration date of the redirect in the format `mm/dd/yyyy`. | `5/20/2020`               |

> ⚠️ Don't edit this row. Otherwise, you won't be able to create or delete redirects.

Under the first row of your `.csv` file, enter the `from`, `to`, `type`, and `endDate` values for the redirects you want to create or delete, as in the following example:

![redirects2](https://cdn.jsdelivr.net/gh/vtexdocs/dev-portal-content@main/images/redirects2.png)

Keep in mind:

- The `from` column only accepts relative paths.
- The `to` column accepts relative paths (e.g., `/shirts/p`) or full URLs (e.g., `https://myotherstore.com`).

> ⚠️ You can't create redirects using wildcards or variables. You must specify each redirect using relative paths or full URLs.
  
- `TEMPORARY` redirects receive the `302` status code, while `PERMANENT` redirects receive the `301` status code.
- The `endDate` must be left empty if the redirect is `PERMANENT`.

<div style="text-align: right"><a href="#creating-url-redirects">Creating URL redirects 🔼</a></div>
<div style="text-align: right"><a href="#deleting-url-redirects">Removing URL redirects 🔼</a></div>
<div style="text-align: right"><a href="#verifying-url-redirects">Verifying URL redirects 🔼</a></div>
