# While

When automating browser interactions, you often encounter situations where you need to repeat a sequence of actions until a specific condition is met. The **While** action block allows you to loop through actions dynamically, making it ideal for tasks like pagination or waiting for complex state changes.

## 1. Why Use a While Loop?

Unlike a fixed **Repeat N** block, a **While** loop doesn't require you to know in advance how many times the loop should run. It evaluates a condition before every iteration:
- If the condition is true, the loop executes its inner actions.
- If the condition is false, the loop ends, and execution continues to the next block.

This is particularly useful when scraping lists of unknown length, clicking "Load More" buttons, or navigating through paginated results until a "Next" button is no longer available.

## 2. Setting Up the Condition

The **While** block requires a JavaScript expression to evaluate. This expression determines whether the loop should continue running.

### Configuration

- **Condition**: A JavaScript expression (e.g., `exists('.next-page-btn')`).
- **Value**: (Optional) Max iterations to prevent infinite loops (e.g., `50`).

You can use helper functions like `exists('[your-css-selector]')` to check if an element is present in the DOM.

## 3. Example: Handling Pagination

A common use case is clicking a "Next Page" button as long as it exists:

1. Add a **While** block.
2. Set the **Condition** to `exists('[your-next-button-selector]')`.
3. Inside the loop, add a **Click** block targeting `[your-next-button-selector]`.
4. Add a **Wait for Selector** block or a fixed **Wait** to ensure the next page loads before the loop restarts.
5. The loop will automatically end when the next button is no longer found.

By setting a maximum iteration count in the **Value** field, you can ensure your task doesn't run forever if the page structure changes unexpectedly.
