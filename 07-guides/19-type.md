# Type

The **Type** action block simulates keystrokes in an input field. It goes beyond merely setting a value; it mimics human typing by triggering appropriate keyboard events (like `keydown`, `keypress`, and `keyup`), which is essential for interacting with complex forms, search bars, and applications that rely on these events for validation or functionality.

## 1. Why Use Type?

While you might be tempted to use a JavaScript block to simply set `element.value = "text"`, the **Type** block is crucial for modern web applications. Many frontend frameworks (like React, Vue, or Angular) do not immediately recognize programmatic value changes. Simulating genuine keystrokes ensures that internal states are updated correctly, auto-complete suggestions are triggered, and validation rules are evaluated as if a real user were interacting with the page.

## 2. Setting Up the Action

To configure the **Type** block, you need to provide the target element and the text you want to type.

### Configuration

- **Selector**: The CSS selector for the input field or text area (e.g., `#username`, `input[name="q"]`, `textarea.comment-box`).
- **Value**: The exact text string to type. This can be static text or can include dynamic variables like `{$username}` or `{$block.output}`.
- **Mode**: Determines how the new text interacts with any existing text in the field.
  - **Append**: The new text is added to the end of any existing text already present in the field.
  - **Replace**: The field is completely cleared before the new text is typed. This is the most common use case for ensuring clean data entry.

## 3. Common Scenarios

Here are some typical situations where the **Type** block is indispensable:

### Filling Out Login Forms

When automating login flows, you need to enter credentials reliably into specific fields.

- **Action**: `type`
- **Selector**: `#email`
- **Value**: `user@example.com`
- **Mode**: `Replace`

Followed by:

- **Action**: `type`
- **Selector**: `#password`
- **Value**: `{$password_variable}`
- **Mode**: `Replace`

### Using Search Bars

Search bars often require keystrokes to trigger dynamic dropdown suggestions or live filtering.

- **Action**: `type`
- **Selector**: `input.search-input`
- **Value**: `automation tools`
- **Mode**: `Replace`

Followed by:

- **Action**: `press` (Key: `Enter`)

### Appending to Existing Text

Sometimes you want to add a suffix to a value already present, like adding a domain name to an input field pre-filled with a username.

- **Action**: `type`
- **Selector**: `#domain-suffix`
- **Value**: `@example.com`
- **Mode**: `Append`

## 4. Best Practices

- **Ensure the Element is Ready**: Before typing, it's highly recommended to use a **Wait for Selector** block targeting the same input element to ensure it is fully rendered and interactable.
- **Combining with Variables**: The `Value` field supports variable substitution. Use this to inject dynamic data retrieved from previous steps or external sources.
- **Handling Complex Interactions**: If the field requires special keys like `Tab`, `Enter`, or arrow keys after typing, follow the **Type** block immediately with a **Press** block.
- **Consider Stealth Options**: When running tasks in "Agent" mode with headful browser settings, remember that human-like typing delays and variations can be configured in the global stealth settings, further enhancing the simulation.
