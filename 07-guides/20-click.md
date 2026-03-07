# Click

The **Click** action block is one of the most fundamental interactions in doppelganger. It simulates a left-click from a user's mouse on a specific element on the webpage. This is essential for interacting with buttons, links, dropdown menus, checkboxes, and any other clickable interface element.

## 1. How the Click Action Works

When the task executes a **Click** block, the automated browser locates the target element on the page and dispatches a click event to it. If the element is not immediately visible, doppelganger will attempt to scroll it into view before clicking.

### Configuration

- **Action**: `click`
- **Selector**: The CSS selector of the target element you want to click (e.g., `#submit-button`, `.nav-link`, `a[href="/login"]`). This is required.
- **Wait**: (Optional) A delay in seconds to wait _after_ the click has been performed. This can be useful for allowing simple animations or transitions to finish, though using a **Wait for Selector** block is generally more robust for page loads or asynchronous actions.

## 2. Common Scenarios

Here are typical situations where you use the **Click** action block:

### Submitting Forms

After filling out inputs using the **Type** action, you use **Click** to submit the form.

- **Action**: `click`
- **Selector**: `button[type="submit"]`

### Navigating Menus and Links

Use **Click** to navigate through a site by interacting with navigation menus or hyperlinks.

- **Action**: `click`
- **Selector**: `.top-nav > li:nth-child(2) > a`

### Interacting with Toggles and Checkboxes

You can click on checkboxes, radio buttons, or toggle switches to change their state.

- **Action**: `click`
- **Selector**: `#agree-to-terms-checkbox`

### Handling Popups and Modals

If a popup or modal appears during your task, you can use **Click** to dismiss it or accept its prompt. Often used in conjunction with an **If** block to check if the modal exists.

- **Action**: `click`
- **Selector**: `.modal-close-btn`

## 3. Best Practices

- **Use Reliable Selectors**: Ensure your CSS selectors are robust and unlikely to change. Prefer IDs (`#my-button`) or specific data attributes (`[data-test-id="submit"]`) over generic classes or complex hierarchical paths.
- **Dynamic Elements**: If the element you want to click doesn't exist immediately (e.g., it appears after an AJAX request), precede the **Click** action with a **Wait for Selector** action targeting the same element.
- **Context within Loops**: When used inside a **For Each** loop, leaving the selector blank will click the current item being iterated over by the loop.

## 4. Troubleshooting Clicks

Sometimes a click might seem to do nothing. This can happen for a few reasons:

- **Element is hidden or covered**: Ensure the element is visible and not obscured by another element (like a sticky header or a cookie banner).
- **Event propagation**: Some websites use complex event handling. If a standard click fails, you might need to try triggering the click using a **JavaScript** block: `document.querySelector('selector').click();`
- **Navigation interference**: If a click triggers a page navigation, ensure your next action waits for the new page to load properly.
