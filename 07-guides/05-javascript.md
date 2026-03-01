# JavaScript

The **JavaScript** action block allows you to execute custom JavaScript in the browser context of your task. Use this block for complex logic, advanced data extraction, or specialized interactions that are not supported by standard action blocks.

## Basic Usage

When adding a JavaScript block, you will provide the JavaScript code to run. This code is executed directly in the browser context.

- **Value**: The JS code to run.

### Return Values and `block.output`

Any value returned from your custom JavaScript is automatically captured and stored. It will be available to subsequent steps in the variable `block.output`.

**Example:**
```javascript
// Extracting the page title
return document.title;
```
If you run this code in a JavaScript block, the page title will be saved to `block.output`. You can then use this output in a "Set Variable" block, or any other block that accepts variables (e.g., `{$block.output}`).

## Common Use Cases

### Advanced Data Extraction
While the standard extraction tools work for most scenarios, you may need to scrape data from complex DOM structures, handle Shadow DOM elements, or format data before saving it.

```javascript
// Extracting a list of items into an array of objects
const items = Array.from(document.querySelectorAll('.product-item')).map(item => {
  return {
    name: item.querySelector('.title')?.innerText || 'No title',
    price: item.querySelector('.price')?.innerText || '0.00'
  };
});
return items;
```

### Complex Interactions
You can use JavaScript to simulate complex user interactions, trigger specific events, or manipulate the DOM directly.

```javascript
// Scrolling to the bottom of a specific scrollable container
const container = document.querySelector('.chat-history');
if (container) {
  container.scrollTop = container.scrollHeight;
}
return true;
```

### Interacting with the Page Environment
Since the code runs in the context of the page, you have full access to the `window` and `document` objects, as well as any global variables or functions defined by the website.

```javascript
// Accessing a global variable defined by the site
if (window.__INITIAL_STATE__) {
  return window.__INITIAL_STATE__.userData;
}
return null;
```

## Tips for Success

- **Keep it focused**: Try to keep your JavaScript blocks focused on a single task, such as extracting a specific piece of data or triggering a specific interaction.
- **Return data cleanly**: Always return clean, structured data (like strings, numbers, arrays, or objects) that can be easily used by subsequent blocks in your task.
- **Error handling**: Consider wrapping your code in `try...catch` blocks to handle unexpected situations gracefully, especially when querying the DOM.
