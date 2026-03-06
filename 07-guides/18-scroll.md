# Scroll

In modern web pages, content is frequently hidden below the initial viewport, loading dynamically only as the user scrolls downwards (a technique known as infinite scrolling or lazy loading). The **Scroll** block in figranium simulates human scrolling behavior, allowing you to access this obscured content.

## 1. Understanding the Scroll Block

The **Scroll** block performs a scrolling action within the browser context. You can instruct it to scroll a specific element (like a scrollable container) or the entire window.

### Configuration

The Scroll block is configured using the following parameters:

-   **Selector**: (Optional) The CSS selector of the specific element to scroll (e.g., `[your-css-selector]`). If left empty, the block will scroll the main browser window.
-   **Value**: This determines *how* the scroll occurs. It accepts:
    -   A numeric value representing the number of pixels to scroll downwards (e.g., `500`). Negative numbers are not supported for scrolling upwards.
    -   The keyword `bottom` to attempt scrolling to the absolute bottom of the container or page.
    -   The keyword `top` to attempt scrolling to the absolute top of the container or page.

## 2. Common Use Cases

### Loading Infinite Scroll Content

Many social media feeds and e-commerce product lists employ infinite scrolling. To scrape all available items, you must repeatedly scroll the page.

1.  Use a **While** loop with a condition checking if more items are loading or if a "loading" indicator is present.
2.  Inside the loop, place a **Scroll** block with the Value set to a reasonable pixel amount (e.g., `800`) or the keyword `bottom`.
3.  Add a **Wait** block or a **Wait for Selector** block inside the loop after the scroll to give the new content time to load before the next iteration.

### Scrolling within a Specific Container

Sometimes, the main page doesn't scroll, but a specific `div` or panel within the page does (e.g., a modal window containing a long list of options).

1.  Identify the CSS selector of the scrollable container (e.g., `[your-container-selector]`).
2.  Add a **Scroll** block.
3.  Set the **Selector** field to the container's selector.
4.  Set the **Value** as needed (pixels, `bottom`, or `top`).

## 3. Debugging Scroll Actions

If the Scroll block doesn't seem to have an effect, consider the following:

-   **Headful Execution**: Run the task in a Headful environment to visually verify if the page is actually scrolling.
-   **Wrong Selector**: Ensure the selector points to the element that actually handles the scrolling overflow (often the element with `overflow-y: scroll` or `overflow-y: auto` in CSS), not just an element inside it. If you meant to scroll the whole page, ensure the selector field is completely empty.
-   **Timing Issues**: The site might require a slight delay after scrolling before it registers the movement and begins fetching new content. Ensure you have adequate `Wait` or `Wait for Selector` blocks in place.
