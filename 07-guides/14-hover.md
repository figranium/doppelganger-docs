# Hover

In many modern websites, interacting with elements requires more than just a simple click. Some elements only become visible or interactable when you move the mouse pointer over a specific area. The **Hover** block in Doppelganger allows you to simulate this mouse movement.

## 1. Understanding the Hover Block

The **Hover** block triggers a `mouseenter` and `mouseover` event on a target element. This is essential for navigating menus, revealing tooltips, or loading dynamic content that relies on hover states.

### Configuration

The Hover block requires a single configuration:

-   **Selector**: The CSS selector of the target element you want to hover over (e.g., `[your-css-selector]`).

## 2. Common Use Cases

### Revealing Dropdown Menus

Many navigation bars use hover states to reveal sub-menus. If you need to click a link inside a dropdown, you must first hover over the parent menu item.

1.  Add a **Hover** block targeting the main menu item (e.g., `[your-menu-selector]`).
2.  Add a **Wait for Selector** block targeting the sub-menu item to ensure the animation has finished and the element is visible.
3.  Add a **Click** block targeting the newly revealed sub-menu item.

### Triggering Tooltips

If your task involves extracting data that is only visible in a tooltip (like a full title or a descriptive text), hovering is necessary.

1.  Add a **Hover** block targeting the element that triggers the tooltip.
2.  Use a **Wait for Selector** to ensure the tooltip is present in the DOM.
3.  Extract the data from the tooltip element.

## 3. Debugging Hover Interactions

If a hover action isn't behaving as expected, you can use **Headful Execution** or **Headful Debugging** to observe the browser's behavior in real-time.

By running the task in a Headful environment, you can visually confirm if the mouse pointer moves to the correct location and if the desired element responds to the hover event.

*Note: "Headful" refers to the execution environment where the browser UI is visible, aiding in observation and debugging. It is not a task mode itself.*
