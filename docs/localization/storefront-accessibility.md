---
title: "Accessibility"
slug: "storefront-accessibility"
hidden: false
createdAt: "2025-01-03T16:57:23.824Z"
updatedAt: ""
excerpt: "Make sure your store is accessible to all by following these best practices for ecommerce accessibility."
---

This guide presents accessibility best practices for building the storefront of your VTEX store based on the [Lighthouse accessibility score](https://developer.chrome.com/docs/lighthouse/accessibility/scoring).

Accessibility ensures that websites, tools, and technologies are usable by as many people as possible, including those with disabilities. It focuses on designing and developing content so anyone can perceive, understand, navigate, and interact with it.

This involves providing text alternatives for images, enabling keyboard navigation, and ensuring compatibility with assistive technologies. The aim is to create a digital environment where all users can access information and functionalities equally.

To learn more about strategies, standards, and resources to make your ecommerce accessible, refer to [W3C Web Accessibility Initiative (WAI)](https://www.w3.org/WAI/).

## Building your storefront

To guarantee accessibility in your store's storefront, implement Accessible Rich Internet Applications (ARIA) attributes correctly, along with other best practices, to ensure that all users can navigate and interact with your site.

>ℹ Learn more in [Lighthouse accessibility score](https://developer.chrome.com/docs/lighthouse/accessibility/scoring).

See below some key strategies for ensuring accessibility when developing your storefront.

### Use Semantic HTML tags

Always use semantic HTML tags when possible, as they help screen readers better interpret content.

- Use `<header>`, `<nav>`, `<main>`, `<footer>`, and other semantic elements to enhance accessibility with minimal extra effort.
- Use appropriate form elements, such as `<button>` for clickable items, `<input>` for input fields, and `<label>` for form labels.

### Add ARIA attributes

ARIA attributes improve accessibility by providing additional information to assistive technologies regarding the page structure, roles, states, and properties of elements. Below are the ARIA attributes that most impact the Lighthouse accessibility audit.

- `aria-label`: Provides a label for an element, typically when a visible label is absent or insufficient. It is especially useful for non-text elements like buttons with icons, form fields without labels, or complex controls. This attribute helps screen readers understand the purpose of an element.

```html
<button aria-label="Close modal">X</button>
```

- `aria-labelledby`: Associates an element with another element that serves as its label. This is particularly useful for linking descriptions or titles with non-text elements, such as in headings.

```html
<div aria-labelledby="sectionTitle">
  <h2 id="sectionTitle">Special Offers</h2>
  <p>Exclusive discounts available!</p>
</div>
```

- `aria-hidden`: Indicates that an element and its children are not visible or perceivable to assistive technologies. It is often used for purely decorative elements that don’t provide any meaningful information.

```html
<div aria-hidden="true">
  <img src="decorative-image.jpg" alt="" />
</div>
```html

- `aria-live`: Announcements dynamic content changes, particularly for live regions like notifications, error messages, or shopping cart updates. The value can be `polite` (announce after the current task) or `assertive` (announce immediately).

```html
<div aria-live="polite">
  Your cart has been updated.
</div>
```

- `role`: Defines the role of an element, helping screen readers understand its intended behavior. Common roles include `button`, `link`, `alert`, `dialog`, `navigation`, and more. Incorrect or missing roles can make it difficult for users to interact with dynamic content or custom UI elements, such as dropdowns or modals.

```html
<div role="dialog" aria-labelledby="dialogTitle">
  <h2 id="dialogTitle">Confirm Action</h2>
  <button>Close</button>
</div>
```

- `aria-expanded`: Indicates the expanded or collapsed state of elements like dropdowns, menus, or accordions.

```html
<button aria-expanded="false" aria-controls="menu">
  Toggle Menu
</button>
```

- `aria-describedby`: Provides additional descriptive text to an element, often used for form fields or controls that need extra context. The value of this attribute should reference the `id` of a related descriptive element.

```html
<label for="email">Email Address</label>
<input type="email" id="email" aria-describedby="emailHelp" />
<span id="emailHelp">We'll never share your email.</span>
```

- `aria-required`: Indicates that an input field is required before submitting a form. It is particularly useful for form fields.

```html
<input type="text" id="name" aria-required="true" />
```

- `aria-invalid`: Indicates that the value entered in a form field is invalid. For example, for showing form validation errors

```html
<input type="email" id="email" aria-invalid="true" />
```

- `aria-controls`: Identifies the elements that are controlled by the current element, like a button controlling a dropdown menu. It is especially useful in dynamic interfaces, as helps to clarify relationships between elements such as modals, menus, o carousels.

```html
<button aria-controls="dropdownMenu" aria-expanded="false">Open Menu</button>
```

- `area-checked`: Indicates the current state of a checkbox or a toggle. It can have values of `true`, `false`, or `mixed` for checkboxes.

```html
<input type="checkbox" aria-checked="false" />
```

#### Best practices for ARIA

- **Correct usage:** Make sure ARIA attributes are used where appropriate, but don’t overuse them. Native HTML elements, such as `<button>`, `<form>`, and `<input>`, are already accessible and don’t need ARIA roles or attributes.
- **ARIA IDs must be unique:** Ensure all ARIA IDs used are unique.
- **ARIA attributes are valid and error-free:** Verify that ARIA attributes (`aria-*`) have valid values and contain no spelling errors.
- **ARIA attributes correspond to their functions:** Ensure that the `aria-*` attributes are being used for the correct purpose and match the intended function.
- **ARIA roles and children must meet requirements:** Ensure that elements with specific ARIA roles (for example, `role="treeitem"`) contain the appropriate child roles as required.

### Multimedia 

- **Images have `alt` text:** All images must have descriptive `alt` attributes that provide meaningful content to users of screen readers.
- **`<input type="image">` elements have `alt` text:** Images used within form buttons, such as `<input type="image">` should also have descriptive `alt` text.
- **Videos contain a track element with captions:** All `<video>` elements must contain a `<track>` element with `kind="captions"` to provide captions for users with hearing impairments.

### Page structure

#### Buttons

- **Buttons must have an accessible name:** Buttons must have a clear, accessible name through the `aria-label`, text content, or associated `<label>` tags.
- **Button text must be understandable:** The text on buttons should clearly communicate the action they will perform.

#### Tables

- **Tables have headers:** Ensure `<td>` element in large tables is associated with one or more table headers (`<th>`).

#### Responsive viewport and scaling

**Do not use `[user-scalable="no"]` in `viewport` meta tag:** The `viewport` meta tag should not prevent users from zooming by setting `user-scalable="no"`. The maximum zoom level (`maximum-scale`) should be set to at least 5.

#### Performance

**Do not use `<meta http-equiv="refresh">`:** The `<meta http-equiv="refresh">` tag is used to automatically refresh or redirect a web page after a specified amount of time, and it is typically placed within the `<head>` section. The use of this meta tag may cause **disruption for screen readers users**, **loss of user context**, and **impact negatively the website’s SEO**.

## Accessibility in VTEX storefront technologies

To start building your storefront with VTEX, you can choose between [FastStore](https://developers.vtex.com/docs/guides/faststore) and [Store Framework](https://developers.vtex.com/docs/guides/store-framework).

>ℹ [Legacy CMS Portal](https://help.vtex.com/pt/tracks/cms--2YcpgIljVaLVQYMzxQbc3z/1oN446gRGcR2s70RvBCAmj) is no longer available to new stores starting to use VTEX.

See below the accessibility features available in which technology.

### FastStore

- **Lighthouse Metrics:** The accessibility score is monitored using Lighthouse metrics for key pages like Home, Product Detail Pages (PDP), and Product List Pages (PLP). Although the dashboard provides a basic accessibility score, more detailed insights can be found in the pull request (PR) analysis.

![lighthouse-faststore](https://cdn.jsdelivr.net/gh/vtexdocs/dev-portal-content@main/docs/guides/vtex-io/Storefront-Guides/images/lighthouse-faststore.png)

- **FastStore UI Component Library:** The components have been developed with accessibility in mind. Each component is designed to enhance accessibility, with sections highlighting best practices. Notable components include Dropdown, Hero, Button, and Checkbox, which include specific accessibility considerations.

### Store Framework

When developing your [Store Theme](https://developers.vtex.com/docs/guides/vtex-io-documentation-store-theme), follow the best practices outlined in the [Building your storefront](#building-your-storefront) section. Learn how to start developing yours in the [Getting started](https://developers.vtex.com/docs/guides/getting-started-3) tutorial.

When creating a [Storefront app](https://developers.vtex.com/docs/guides/vtex-io-documentation-1-developing-storefront-apps-using-react-and-vtex-io) to your store developed with Store Framework, prioritize accessibility within the creation process to improve the shopping experience for all users. To promote inclusion, key practices are:
  - Ensuring keyboard interactivity for all user actions.
  - Applying good color contrast in component styles.
  - Avoiding the use of HTML `<div>` elements where possible to enhance accessibility for screen readers and improve SEO.
