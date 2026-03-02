# On Error

In complex automation tasks, failures are inevitable. Elements might not load in time, network requests can fail, or target websites may change their structure unexpectedly. The **On Error** (`on_error`) block in Doppelganger provides a way to gracefully handle these failures and implement custom recovery or fallback logic.

## 1. Why Use the On Error Block?

The **On Error** block is essential for building robust and resilient workflows. It allows you to:

- **Implement Retry Logic**: Automatically retry a failed action before giving up.
- **Graceful Failures**: Prevent the entire task from crashing if a non-critical step fails.
- **Alternative Paths**: Execute a different sequence of actions if the primary sequence encounters an error.
- **Error Logging**: Capture screenshots or variable states when something goes wrong for easier debugging in Headful Debugging or API execution logs.

## 2. Using the On Error Block

The **On Error** block functions similarly to a `try...catch` statement in programming. It defines a set of actions that should be executed if any action within the main flow of the current scope fails.

### Configuration

- **Action**: **On Error** (`on_error`)
- **Block Content**: Place the recovery actions inside this block.

When the executor encounters an error in a preceding action (within the same scope), it immediately jumps to the **On Error** block and executes its contents.

## 3. Best Practices and Execution

When implementing error handling, keep these concepts in mind:

- **Scope Matters**: An **On Error** block typically handles errors that occur before it within the same logical block (or the entire task if placed at the top level).
- **Preventing Infinite Loops**: If your recovery logic includes retrying a step, ensure you use a **Set Variable** block to track retry attempts and limit them, preventing an infinite loop.
- **State Management**: Use the **On Error** block to reset the state. For example, if a multi-step form fails, the error handler might navigate back to the start of the form.

## 4. Example: Fallback Navigation

A common use case is attempting to click a specific element and falling back to a different approach if it fails:

1. **Wait for Selector**: Wait for the primary `#quick-login` button.
2. **Click**: Click `#quick-login`.
3. **On Error**:
   - **Navigate**: Go to the standard login page (`/login`).
   - **Type**: Enter username.
   - **Type**: Enter password.
   - **Click**: Click `#submit-login`.

By incorporating the **On Error** block, your agent tasks become significantly more reliable when facing real-world web variability.
