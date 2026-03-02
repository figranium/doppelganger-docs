# Wait for Selector

When automating browser interactions, timing is everything. Web pages are dynamic, and elements often load asynchronously after the initial page load. The **Wait for Selector** action block ensures your task doesn't try to interact with an element before it's actually ready on the page.

## 1. Why Use Wait for Selector?

Using a generic **Wait** block (e.g., waiting for exactly 5 seconds) is usually a bad practice:
- If the page loads in 1 second, you waste 4 seconds.
- If the page takes 6 seconds to load, your task fails.

**Wait for Selector** dynamically pauses the task execution until a specific element appears in the Document Object Model (DOM). This makes your tasks faster, more reliable, and less prone to flakiness caused by network speeds.

## 2. Setting Up the Wait

To use this block, you need to provide the CSS selector of the element you are waiting for.

### Configuration

- **Selector**: The CSS selector of the element you expect to appear (e.g., `#success-message`, `.product-list-item`, `button[type="submit"]`).
- **Value**: The maximum time to wait, in seconds. If the element doesn't appear within this time, the task will throw an error and fail (unless handled by an **On Error** block). The default timeout is usually 30 seconds.

## 3. Common Scenarios

Here are some typical situations where you should use **Wait for Selector**:

### Waiting for a Page Transition

After clicking a "Login" or "Submit" button, the browser usually redirects to a new page. You should wait for an element that only exists on the new page before proceeding.

- **Action**: `click` (on `#login-button`)
- **Action**: `wait_selector`
- **Selector**: `#dashboard-welcome-message`
- **Value**: `15`

### Waiting for Asynchronous Data (AJAX)

Many modern websites load data in the background (like infinite scrolling or loading search results). When you trigger a search or scroll down, you must wait for the new elements to render.

- **Action**: `type` (into `.search-bar` with the value "laptops")
- **Action**: `press` (Key: `Enter`)
- **Action**: `wait_selector`
- **Selector**: `.search-result-item`

### Waiting for Popups or Modals

When you click an element that opens a modal window, it might take a fraction of a second to animate into view. Waiting for the modal ensures you don't interact with it prematurely.

- **Action**: `click` (on `#open-settings`)
- **Action**: `wait_selector`
- **Selector**: `.settings-modal.is-visible`

## 4. Best Practices

- **Use Specific Selectors**: Avoid using overly generic selectors that might match elements already on the page. You want to ensure you are waiting for the *new* element that indicates the action is complete.
- **Handling Failures**: Consider wrapping potentially flaky operations inside an **If** block checking for the element's existence, or using an **On Error** block to gracefully handle timeouts if the element never appears.
- **Wait for Visibility**: Note that `wait_selector` generally waits for the element to exist in the DOM. If an element is in the DOM but hidden via CSS (`display: none`), you may need to ensure your selector targets the visible state, or use JavaScript conditions to wait for true visibility.
