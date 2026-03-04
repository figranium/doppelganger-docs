# Stop Task

The **Stop Task** block in Doppelganger provides a way to gracefully or forcefully terminate the execution of a task before it reaches the end of its defined sequence.

## 1. Why Use Stop Task?

- **Early Exit**: If a certain condition is met (e.g., finding the desired data on the first page), there's no need to continue running the rest of the task.
- **Error Handling**: When combined with an **If** block or **On Error** block, it can be used to abort the task and report a `failure` status if something critical goes wrong (e.g., unable to log in).
- **Conditional Success**: To stop a task and mark it as a `success` based on runtime logic without executing the remaining blocks.

## 2. Using the Stop Task Block

### Configuration

- **Action**: **Stop Task** (`stop`)
- **Value**: The exit status to report when stopping. This is typically set to `success` or `failure`.

When the executor reaches the **Stop Task** block, it immediately halts any further actions in the current task and updates the task's execution record with the provided status.

## 3. Common Scenarios

### Stopping After a Successful Action

Sometimes, a task's only purpose is to perform a check or establish a session.

1. Navigate to the target page and perform the necessary actions.
2. Use an **If** block to check if the action was successful (e.g., checking if a specific element `[your-success-selector]` exists).
3. Inside the **If** block, add a **Stop Task** block with the Value set to `success`.
4. Optionally, add an **Else** block with a **Stop Task** block set to `failure` if the action didn't succeed.

### Terminating on Critical Error

When a required element fails to load, continuing the task might result in cascading errors or wasted resources.

1. Use an **If** block to check if an essential element is missing or an error message `[your-error-selector]` is displayed.
2. Inside the block, add a **Stop Task** block.
3. Set the **Value** to `failure` so you can easily identify failed runs in the execution history.

## 4. Interaction with Other Blocks

- **On Error**: If you catch an error using an **On Error** block, you can perform some cleanup (like taking a **Screenshot**) and then use **Stop Task** to officially end the execution with a `failure` status.
- **While Loops**: If you need to break out of a **While** loop and end the entire task simultaneously, **Stop Task** is the most direct method.
- **Start Task**: If task A uses **Start Task** to run task B, and task B hits a **Stop Task** block, only task B stops. Task A will resume execution once task B concludes, receiving the exit status from task B.
