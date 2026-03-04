# Type

The Type action block is one of the most fundamental ways to interact with a webpage in Doppelganger. It simulates typing text into an input field, such as a search bar, login form, or comment box.

## Configuration Options

When configuring a Type block, you need to specify the target element, the text to type, and how the typing should behave.

### 1. Selector

The CSS selector for the target input field where you want to type.

*   **Example:** `input[name="q"]` (for a common search input)
*   **Example:** `#email-address` (for an ID-based input)
*   **Example:** `.login-input.password` (for a class-based input)

*Tip: If you're unsure of the correct selector, use the "Visual" mode or Headful execution to inspect the element and identify a unique selector.*

### 2. Value

The text string you want to simulate typing into the targeted input field.

You can use static text or inject variables using the `{$variableName}` syntax.

*   **Static Example:** `hello world`
*   **Variable Example:** `{$searchQuery}`
*   **Mixed Example:** `Search for: {$searchQuery}`

### 3. Mode

The typing mode determines how the new text interacts with any existing text already present in the input field.

*   **Replace:** This is the default and most common mode. It clears any existing text in the input field before typing the new value. Use this when you want to ensure only your specific value is present (e.g., logging in, clearing a search bar).
*   **Append:** This mode adds the new text to the end of whatever is currently in the input field. Use this when you are building a string piece-by-piece or filling out a multi-part form field where some data is already pre-filled.

## Best Practices

*   **Wait for the Element:** While the Type block generally waits for the element to become interactive, it's often a good practice to precede a critical Type action (like a login) with a **Wait for Selector** block to ensure the page has fully loaded and the input is ready to receive text.
*   **Simulate Human Typing:** If you are running tasks where bot detection is a concern, ensure your `StealthConfig` has `naturalTyping` enabled. This adds slight, randomized delays between keystrokes to mimic human behavior more closely, rather than pasting the entire string instantly.
*   **Handling Dropdowns/Comboboxes:** For custom select menus or comboboxes that require you to type and then select from a list, you often need to chain actions: use a **Type** block to filter the options, followed by a **Wait for Selector** (for the dropdown list to appear), and finally a **Click** block to select the specific option.
