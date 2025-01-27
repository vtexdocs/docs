---
title: Cart
createdAt: "2025-01-16T14:47:00.000Z"
---

The Cart module offers functionalities to manage the store's shopping cart. It handles large orders and complex ecommerce operations, such as marketplace integration, coupons, gift options, and promotions.

## Cart data storage

Cart data is saved in the browser’s [IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API), ensuring that users' carts persist even when they close the browser and is structured as follows.

![Cart SDK Architecture](https://vtexhelp.vtexassets.com/assets/docs/src/Cart___74c390e654f666b3a2adb7b6a0b5ecf7.png)

## Cart modes

The Cart module provides two modes:

- [**Pure**](#pure-mode) (default) - Works on the client side, stores cart data locally, and works offline. It lacks server-side validation and may not handle complex cases like unavailable items. It is ideal for basic cart functionality.

- [**Optimistic**](#optimistic-mode) - Handles complex ecommerce operations like unavailable items. Validates the cart state on the server using debounced requests

## Pure mode

The Pure mode stores cart data locally in the browser. This allows users to add or remove items and keep their carts even if they close the browser. However, it cannot validate items on the server side.

The Pure cart can also work offline. However, it can't automatically fix mistakes. For example, if a customer tries to add an out-of-stock item, the cart won't stop them. It will still show the item as added, even though it's not available to buy.

### Implementing Pure mode

To implement the Pure cart mode, follow these steps:

1. Wrap your app with the `CartProvider` component.
2. Access the cart using the `useCart` hook:

    ```tsx
    import { CartProvider, useCart } from '@faststore/sdk'

    // In the App's root component:
    const App = ({ children }) => {
    return <CartProvider>{children}</CartProvider>
    }

    // In your component:
    const MyComponent = () => {
    const { items } = useCart()

    return <div>Number of items on cart: {items.length}</div>
    }
    ```

## Optimistic mode

The Optimistic mode validates the cart state on the server and can handle edge cases like unavailable items. For example, if a customer tries to add an out-of-stock product, Optimistic mode will check with the store's system. If the product is not available, it will be removed from the cart and let the customer know.

This feature can be implemented in the `optimistic` mode via a callback function, `validateCart`,  that allows developers to make requests and cause side effects to the cart. If the function returns `null`, the cart behavior does not change. However, if you opt to change the state of the cart to handle some specific side effect, they must return the new cart state on the callback function.

### Implementing Optimistic mode

To implement the Optimistic cart mode, follow these steps:

1. Use the `CartProvider` component with the `optimistic` mode.
2. Implement the `validateCart` function to handle server-side validation:

    ```tsx
    import { CartProvider, useCart, Cart } from '@faststore/sdk'

    // In the App's root component:
    const validateCart = async (cart: Cart) => {
    const response = await fetch(...)

    if (response) {
        return response
    }

    return null
    }

    const App = ({children}) => {
    return <CartProvider mode="optimistic" onValidateCart={validateCart}>{children}</CartProvider>
    }

    // In your component:
    const MyComponent = () => {
    const { items, isValidating } = useCart()

    if (isValidating) {
        return <div>Cart is validating</div>
    }

    return <div>Number items in cart: {items.length}</div>
    }
    ```
