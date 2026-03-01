# Chaining Tasks

Automating complex workflows sometimes requires breaking down processes into smaller, manageable tasks. The **Start Task** block in Doppelganger allows you to trigger another task from within the current task, enabling you to build modular and reusable workflows.

## 1. Why Chain Tasks?

Chaining tasks is useful in several scenarios:

- **Modularity**: Create a reusable "Login" task and trigger it from various other scraping or agent tasks.
- **Organization**: Break down a massive, multi-step process into logical, smaller tasks.
- **State Management**: Run tasks sequentially, ensuring one process finishes completely before the next begins.

## 2. Using the Start Task Block

The **Start Task** block is straightforward to implement.

### Configuration

- **Action**: **Start Task** (`start`)
- **Task**: The ID of the target task you want to trigger.

When the executor reaches the **Start Task** block, it will automatically initiate the specified task.

## 3. Session State and Execution

When chaining tasks, it's important to understand how state is handled:

- **Shared State**: If you are reusing a session (e.g., after logging in), ensure `statelessExecution` is set to **false** on both the initiating task and the target task. This allows the newly started task to inherit the cookies and session state from `storage_state.json`.
- **Debugging**: If a chained task isn't working as expected, you can use Headful Execution on the target task independently to visually inspect the problem before integrating it into the chain.

## 4. Example: Modular Login and Scrape

A common pattern is to log in first, then scrape data:

1. **Task A (Login Task)**:
   - Navigates to the login page.
   - Enters credentials and submits the form.
   - Verifies the login was successful and saves the session.
2. **Task B (Scrape Task)**:
   - Uses the **Start Task** block to trigger Task A.
   - Waits for Task A to complete.
   - Navigates to the target data page (using the shared session).
   - Extracts the required information.

This approach keeps your scraping logic separate from your authentication logic, making both easier to maintain.
