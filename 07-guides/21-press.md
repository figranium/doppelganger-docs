# Press

The **Press** action block allows your task to simulate pressing a specific key on the keyboard. This is essential for interactions that don't rely solely on mouse clicks or typing entire strings, such as navigating menus with arrow keys, submitting forms via the `Enter` key, or closing modals using `Escape`.

## 1. How the Press Action Works

When the task executes a **Press** block, the browser simulates a full keystroke (down, up) of the designated key. You can also specify an element to focus on before pressing the key.

### Configuration

- **Action**: `press`
- **Key**: The name of the keyboard key you want to press (e.g., `Enter`, `Tab`, `Escape`, `ArrowDown`, `Space`). This is required.
- **Selector**: (Optional) The CSS selector of an element to focus on _before_ pressing the key. If left blank, the key will be pressed on whatever element currently has focus (or the document body).

## 2. Common Scenarios

Here are typical situations where you use the **Press** action block:

### Submitting Forms without a Button

Often, typing into a search input and pressing `Enter` is faster or more reliable than finding and clicking the submit button.

- **Action**: `type` (into `.search-input` with the value "shoes")
- **Action**: `press`
- **Key**: `Enter`
- **Selector**: `.search-input` (Ensure focus is still on the input)

### Closing Modals and Popups

Many dialogs or lightboxes can be closed quickly by simulating the `Escape` key.

- **Action**: `press`
- **Key**: `Escape`

### Navigating Dropdowns and Lists

You can use the arrow keys to move through custom dropdown menus or long lists of items.

- **Action**: `click` (to open the dropdown)
- **Action**: `press`
- **Key**: `ArrowDown` (to highlight the first item)
- **Action**: `press`
- **Key**: `Enter` (to select it)

### Tabbing through Forms

To quickly move focus between input fields without needing a selector for each one, use the `Tab` key.

- **Action**: `press`
- **Key**: `Tab`

## 3. Best Practices

- **Specify Focus When Necessary**: If you need a keypress to affect a specific component (like scrolling a custom div with arrow keys), use the **Selector** field to focus it first. Otherwise, the keystroke might just scroll the main page or be ignored.
- **Valid Key Names**: Ensure you are using valid key identifiers recognized by modern browsers (e.g., `ArrowLeft`, `PageUp`, `Home`, `End`). Standard characters (like `a`, `B`, `1`) work too, but the **Type** block is usually better for text input.
- **Combine with Type**: Often used immediately after a **Type** block to confirm an entry.

## 4. Troubleshooting Keypresses

If a **Press** action doesn't seem to work:

- **Missing Focus**: The key event might be going to the wrong element or the document body. Try explicitly setting the **Selector** field to the element you expect to react to the keypress.
- **Custom Implementations**: Some websites handle key events in non-standard ways (e.g., listening for `keydown` but ignoring `keyup`). If a simple `press` fails, you might need a more advanced approach using a **JavaScript** block to dispatch custom keyboard events.
- **Timing**: If the page is still animating or loading after a previous action, the focus might be lost before the key is pressed. Consider adding a small **Wait** or **Wait for Selector** before the **Press** block.
