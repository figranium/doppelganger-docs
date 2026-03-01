# Conditional Logic (If / Else)

When building automated tasks, you often encounter situations where the flow needs to change based on what is happening on the page. For example, a popup might appear, or a specific element might only be visible for certain items.

The **If**, **Else**, and **End Block** actions allow your tasks to make these kinds of decisions dynamically during execution.

## 1. How Conditional Blocks Work

A conditional block evaluates a specific condition. If the condition is met, the actions inside the block are executed. If not, the actions are skipped (or the alternate `else` path is taken).

Every conditional flow requires at least an **If** block and an **End Block**.

- **If**: Starts the conditional block and defines the condition to check.
- **Else**: (Optional) Defines an alternate path to take if the initial condition is not met.
- **End Block**: Marks the end of the conditional logic.

## 2. Using the If Action

To start a conditional flow, add an **If** action block.

### Setting Up the Condition

The condition is defined using JavaScript expressions. You have access to built-in helper functions to check the state of the page.

- **Condition**: A JavaScript expression that evaluates to true or false.

#### Common Helper Functions

- `exists(selector)`: Returns true if an element matching the selector is currently in the DOM.
- `visible(selector)`: Returns true if the element is in the DOM and visible (not hidden via CSS or zero size).

**Example Condition:**
```javascript
exists('.modal-popup')
```
*This condition checks if an element with the class `modal-popup` is present.*

## 3. The Else Action

The **Else** action is used within an **If** / **End Block** structure. If the initial **If** condition evaluates to false, the task will jump to the **Else** action and execute the subsequent steps until it hits the **End Block**.

## 4. Closing with End Block

You must always close an **If** block (and its **Else** block, if used) with an **End Block**. This tells the task runner where the conditional logic finishes and where the main flow resumes.

## 5. Example: Closing a Dynamic Popup

Here is a common scenario: you are navigating a website, and occasionally a promotional popup appears. You want to close it if it's there, but continue normally if it's not.

### Step 1: Navigate

- **Action**: `navigate`
- **Value**: `https://example.com`

### Step 2: Start If Block

- **Action**: `if`
- **Condition**: `exists('.promo-popup')`

### Step 3: Close Popup (Inside If Block)

*(This action only runs if the popup exists)*

- **Action**: `click`
- **Selector**: `.promo-popup .close-btn`

### Step 4: End Conditional Block

- **Action**: `end`

### Step 5: Continue Flow

- **Action**: `click`
- **Selector**: `#main-content-link`

## 6. Variables in Conditions

You can also use runtime variables in your conditions. For example, if you stored a value in a previous step, you can check it.

- **Condition**: `variables.isLoggedIn === false`

By mastering conditional logic, you can build robust tasks that adapt to varying page structures and dynamic content.
