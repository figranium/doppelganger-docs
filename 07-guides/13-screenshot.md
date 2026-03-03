# Screenshot

The **Screenshot** action block captures a snapshot of the current state of the browser window. This is an invaluable tool for debugging, creating audit trails, or verifying visual elements during a task execution.

## 1. Why Use Screenshot?

Visual confirmation can be just as important as the data you extract. You might use the **Screenshot** block to:
- **Debugging**: If a task fails unexpectedly, a screenshot taken just before the failure can help you understand what the browser was seeing.
- **Auditing**: Keep a visual record of actions performed, such as confirming a successful form submission or a completed transaction.
- **Verification**: Ensure that a page has loaded correctly or that specific elements are visible before proceeding with complex interactions.

## 2. Setting Up the Screenshot

The **Screenshot** block provides a few options to customize how and what you capture.

### Configuration

- **Value**: (Optional) A filename suffix. This helps you identify specific screenshots if you take multiple during a single task execution. For example, using `before-login` will result in a filename like `timestamp-before-login.png`.
- **Selector**: (Optional) If you only want to capture a specific element on the page, provide its CSS selector here (e.g., `#invoice-details`, `.product-image`). If left blank, the block will capture the entire visible viewport.

## 3. Common Scenarios

### Full Page Capture

To capture everything currently visible in the browser window, simply add a **Screenshot** block without specifying a selector.

- **Action**: `screenshot`
- **Value**: `full-page-view`

### Element-Specific Capture

When you only care about a particular part of the page, such as a chart or a specific table, use the **Selector** field.

- **Action**: `screenshot`
- **Selector**: `.financial-summary-chart`
- **Value**: `q3-summary`

### Capturing State Changes

A common pattern is to take a screenshot before and after a significant action to verify the change.

- **Action**: `click` (on `#submit-order`)
- **Action**: `wait_selector` (Selector: `#order-confirmation`)
- **Action**: `screenshot`
- **Value**: `order-success`

## 4. Best Practices

- **Timing is Crucial**: Always ensure the page or element you want to capture is fully loaded before taking the screenshot. Use the **Wait for Selector** block beforehand to avoid capturing blank or partially loaded pages.
- **Meaningful Names**: Use descriptive suffixes in the **Value** field so you can easily understand what each screenshot represents when reviewing task results.
- **Storage Considerations**: Remember that screenshots consume storage space. Use them strategically rather than taking a screenshot after every single minor step.
