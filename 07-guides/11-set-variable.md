# Set Variable

The **Set Variable** action block allows you to store, update, or manipulate values during a task's execution. This is essential for keeping track of counters, storing extracted data temporarily, or creating dynamic conditions for your logic flows.

## 1. How Set Variable Works

Variables in a figranium task act as temporary storage containers. The **Set Variable** action lets you define a variable's name and assign it a value.

- **Var Name**: The name of the variable you want to create or update (e.g., `itemCount`, `pageTitle`, `isFinished`).
- **Value**: The data you want to store in the variable. This can be a static value or a dynamic JavaScript expression.

## 2. Using Static Values

You can use the **Set Variable** block to initialize a variable with a specific value.

### Example: Setting an initial counter

- **Action**: `set`
- **Var Name**: `currentPage`
- **Value**: `1`

This sets the variable `currentPage` to the number `1`. You can then use this variable in a **While** loop or a **Navigate** action to keep track of pagination.

## 3. Using Dynamic Expressions

The true power of the **Set Variable** block comes from its ability to evaluate JavaScript expressions. You can perform calculations, format strings, or access other variables and task outputs.

### Example: Incrementing a Counter

To increase a counter, you can reference the variable's current value in the **Value** field:

- **Action**: `set`
- **Var Name**: `currentPage`
- **Value**: `variables.currentPage + 1`

### Example: Storing Block Output

Many action blocks (like **JavaScript** or **CSV**) output data to a special variable called `block.output`. You can save this output to a named variable for later use.

- **Action**: `javascript`
  - Value: `return document.title;`
- **Action**: `set`
  - Var Name: `savedPageTitle`
  - Value: `block.output`

Now, the page's title is safely stored in `savedPageTitle`, and you can run other blocks without losing this information when `block.output` gets overwritten.

## 4. Using Variables in Other Blocks

Once you have set a variable, you can use it in other action blocks.

*   **In fields that support templates**: Use the `{$variableName}` syntax. For example, in a **Type** action, you could use `{$savedPageTitle}` to type out the title you extracted earlier.
*   **In conditions**: In an **If** or **While** block, you can reference variables directly using the `variables` object (e.g., `variables.currentPage < 5`).

## 5. Summary

The **Set Variable** block is a foundational tool for building complex, stateful tasks. By storing intermediate results and managing counters or flags, you can create robust workflows that handle dynamic scenarios efficiently.
