# Action Blocks

In "Agent" mode, tasks are built from a sequence of actions. These actions are executed sequentially by the browser.

## Basic Actions

### **Click**
Simulates a left-click on an element. Use this to interact with buttons, links, or any clickable item.
*   **Selector**: The CSS selector of the target element (e.g., `#btn`, `.link`).
*   **Wait**: Optional delay (in seconds) after clicking.

### **Type**
Types text into an input field. Use this for filling out forms or search bars.
*   **Selector**: The target input (e.g., `input[name="q"]`).
*   **Value**: The text to type. Can include `{$variables}`.
*   **Mode**: `Replace` (clears existing text) or `Append` (adds to end).

### **Wait**
Pauses execution for a fixed duration. Use this when you need a simple delay, though **Wait for Element** is often more reliable.
*   **Value**: Duration in seconds (e.g., `2.5`).

### **Wait for Element** (`wait_selector`)
Waits until a specific element appears in the DOM. Use this to ensure the page has loaded the content you need before proceeding.
*   **Selector**: The element to wait for.
*   **Value**: Timeout in seconds (default: 30).

### **Press Key** (`press`)
Simulates a keyboard key press. Use this for navigation keys like `Enter`, `Tab`, or `Escape`.
*   **Key**: The key name (e.g., `Enter`, `Tab`, `Escape`, `ArrowDown`).
*   **Selector**: (Optional) Focus this element before pressing.

### **Scroll**
Scrolls the page or a specific element. Use this to reveal content that loads on scroll (lazy loading).
*   **Selector**: (Optional) The element to scroll. If empty, scrolls the window.
*   **Value**: Pixels to scroll (e.g., `500`) or specific commands (`bottom`, `top`).

### **Hover**
Moves the mouse cursor over an element. Use this to trigger dropdown menus or tooltips.
*   **Selector**: The target element.

### **Navigate**
Redirects the browser to a new URL. Use this to start a flow or move to a different page.
*   **Value**: The full URL (e.g., `https://example.com/login`).

## Logic & Flow Control

### **Condition** (`if` / `else` / `end`)
Conditional execution block. Use this to handle dynamic situations, like closing a popup only if it appears.
*   **Condition**: A JavaScript expression (e.g., `exists('.error')`).
*   **Selector**: (Structured mode) Target element.
*   **Operator**: `equals`, `contains`, `exists`, etc.

### **While Loop** (`while` / `end`)
Repeats a block of actions while a condition is true. Use this for pagination or waiting for a specific state change.
*   **Condition**: Same as `if`.
*   **Value**: (Optional) Max iterations to prevent infinite loops.

### **Loop Elements** (`foreach` / `end`)
Iterates over a list of elements. Use this to scrape lists of items, like search results or product cards.
*   **Selector**: The elements to iterate (e.g., `.product-item`).
*   **Var Name**: Variable to store the current element index/data.

### **Repeat** (`repeat` / `end`)
Repeats a block N times. Use this when you know exactly how many times an action needs to happen.
*   **Value**: Number of repetitions.

## Advanced Actions

### **Run JavaScript** (`javascript`)
Executes custom JavaScript in the browser context. Use this for complex logic, data extraction, or interactions not supported by other blocks.
*   **Value**: The JS code (e.g., `return document.title;`).
*   **Output**: The return value is stored in `block.output` for subsequent steps.

### **Screenshot**
Takes a screenshot at the current state. Use this for debugging or keeping records of the task execution.
*   **Value**: (Optional) Filename suffix.
*   **Selector**: (Optional) Capture only this element.

### **Stop**
Immediately stops the task execution. Use this to end the task early based on a condition (e.g., login success).
*   **Value**: Exit status (e.g., `success`, `failure`).

### **Set Variable** (`set`)
Updates a runtime variable. Use this to store calculations or flags for later use.
*   **Var Name**: The variable to update (e.g., `counter`).
*   **Value**: The new value (can be a JS expression).

### **Wait for Downloads** (`wait_downloads`)
Waits for file downloads to complete. Use this after clicking a download button to ensure the file is saved.
*   **Value**: Timeout in seconds.

### **Error Handler** (`on_error`)
Defines a block of actions to run if an error occurs in the main flow. Use this to implement retry logic or graceful failures (try/catch).
