---
title: "Search"
slug: "search-overview"
---

The `Search` module helps create and manage faceted store search experiences. The module allows users to filter products by attributes like brand, price, or features. These filters generate unique URLs (facet states) for each combination, enabling:

- Easy navigation: Allows users to revisit previous searches using their browser history.
- Improved filtering experience: Selecting or removing filters updates the URL without reloading the page.
- SEO-friendly: Unique URLs for each search state help with search engine optimization.

![Faceted Search](https://vtexhelp.vtexassets.com/assets/docs/src/FacetedSearch___7d5958d80e6945f07dae5f9f7d2ac8d4.jpg)

The `Search` module relies on the following parts:

- [`SearchProvider`](https://github.com/vtex/faststore/blob/master/packages/sdk/src/search/Provider.tsx) component and [`useSearch`](https://github.com/vtex/faststore/blob/master/packages/sdk/src/search/useSearch.ts) hook: Defines the search state (selected filters, sort criteria, etc.) and functions to change it (select/remove filters, change sort).
- [`serializer`](https://github.com/vtex/faststore/blob/master/packages/sdk/src/search/serializer.ts): Parses URLs to create a serialized URL for every filter combination.

## `SearchProvider`

The `SearchProvider` component defines the structure of a faceted search state and provides functions to change that state. This component exposes the `State` interface that allows you to access and modify the following search variables:

| Variable     | Type       | Description   |
| ---------------- | ------------ | ----------------- |
| `base`           | `string`     | Base URL path to be ignored by the search context. Use `/en` to ignore the locale-specific part of the URL in the search context. |
| `page`           | `number`     | Index of the current page in the pagination context. Use `0` if it's the first page in the pagination result and `1` if it's the second. |
| `selectedFacets` | `Facet[]`    | All selected facets. |
| `sort`           | `SearchSort` | Selected sorting criteria for the search (e.g., ascending/descending price, number of reviews)  |
| `term`           | `string`     | Terms of the full text search. |

The `SearchProvider` also provides functions to change the facet state:

- `setFacet` - Selects a facet by its key.
- `toggleFacet` - Replace a selected facet with its key.
- `removeFacet` - Remove the selected facet with its value.

For more information about this component, see the [`SearchProvider`](/TBD) guide.

## `serializer`

The `serializer` file handles parsing URLs and creating serialized URLs representing specific filter combinations.

## Use cases

The `Search` module is versatile for ecommerce applications, especially for creating dynamic product search interfaces. Key features include sorting, filtering by facets like price or category, and generating unique URLs for search states, enhancing user experience and SEO.

For more examples, refer to the FastStore repository in the [`search` tests folder](https://github.com/vtex/faststore/tree/master/packages/sdk/test/search).

### Brand filtering

In this use case, the `SearchProvider` and a checkbox component create a filter for the `faststore` brand. When a user selects or deselects the checkbox for this brand, the search state is updated via the `toggleFacet` function, which adds or removes the brand filter from the current search context.

This interaction automatically updates the URL and redirects the user to a new results page that reflects the selected filter criteria. The `itemsPerPage` prop ensures that a consistent number of products (12) are shown per page, offering a customizable and user-friendly shopping experience.

```tsx
import { SearchProvider, parseSearchState } from '@faststore/sdk'

function Page() {
  const params = useMemo(() => parseSearchState(new URL(window.href)), [])

  return (
    <SearchProvider
      onChange={(url: URL) => (window.location.href = url.href)}
      itemsPerPage={12}
      {...params}
    >
      <Checkbox />
    </SearchProvider>
  )
}

function Checkbox() {
  const { toggleFacet } = useSession()

  return (
    <input
      type="checkbox"
      onChange={() => toggleFacet({ key: 'brand', value: 'faststore' })}
    />
  )
}
```

The `Page` component parses the search state from the URL and passes it to `SearchProvider`, which manages the faceted search context. When the checkbox is clicked, the URL is updated with the selected filter and redirects to the corresponding results page. The `itemsPerPage` prop ensures 12 products are displayed per page.
