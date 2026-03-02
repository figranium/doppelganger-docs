# On Error

In automated workflows, things don't always go according to plan. Elements might load slowly, popups could block the screen, or network requests may time out. The **On Error** block in Doppelganger provides a robust mechanism to handle these unexpected situations gracefully, preventing your tasks from failing completely.

## 1. Understanding Error Handling

The **On Error** block acts like a `try/catch` mechanism in traditional programming. It allows you to define a specific sequence of actions that will only execute if an error occurs within the main execution flow.

### How it Works

1.  **Main Flow Execution**: Your task executes its actions sequentially.
2.  **Error Detection**: If an action fails (e.g., a "Wait for Selector" times out or an element cannot be clicked), the task execution pauses.
3.  **On Error Trigger**: If an **On Error** block is present, execution immediately jumps to the actions defined within it.
4.  **Recovery or Stop**: Inside the On Error block, you can attempt to resolve the issue (e.g., close a popup) and resume, or log the failure and cleanly stop the task.

## 2. Implementing the On Error Block

The **On Error** block is added to your task like any other action.

### Configuration

-   **Action**: **On Error** (`on_error`)

Any actions placed *inside* this block will become your error recovery sequence.

## 3. Common Error Recovery Strategies

Here are a few common scenarios where the **On Error** block is invaluable:

### Handling Unexpected Popups

Sometimes, a promotional popup or cookie banner might obscure the element you're trying to interact with.

-   **Main Flow**: Try to click a 'Submit' button.
-   **On Error Flow**:
    -   Use a **Wait for Selector** (with a short timeout) to check for a common popup close button (e.g., `.close-btn`).
    -   If found, **Click** it to dismiss the popup.
    -   Use a **Start Task** block (or simply let the flow resume if structured correctly) to retry the original action.

### Retrying Failed Navigations

Network instability can cause page loads to fail.

-   **Main Flow**: **Navigate To** a URL.
-   **On Error Flow**:
    -   Wait for a few seconds using the **Wait** block.
    -   Attempt the **Navigate To** action again.

### Graceful Shutdowns

If an error is unrecoverable, you might want to log the current state before stopping.

-   **On Error Flow**:
    -   Take a **Screenshot** to capture the exact visual state of the page at the moment of failure.
    -   Use the **Stop Task** block with a `failure` status to formally end the process and notify the system.

## 4. Debugging Error Workflows

When developing complex error handling logic, visual feedback is crucial. You can utilize **Headful Debugging** or **Headful Execution** to watch the browser interact with the page in real-time.

By running the task in a Headful environment, you can clearly see *why* an action failed (e.g., an element wasn't visible) and verify that your **On Error** logic correctly triggers and attempts recovery.

*Note: "Headful" refers to the execution environment where the browser UI is visible, aiding in observation and debugging. It is not a task mode itself.*
