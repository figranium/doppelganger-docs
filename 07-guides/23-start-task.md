# Start Task

The **Start Task** action block allows you to compose modular workflows by triggering the execution of another doppelganger task from within the current one. This enables you to reuse common sequences (like logging in or configuring a session) across multiple different scraping or automation flows.

## 1. How the Start Task Action Works

When the task executes a **Start Task** block, it essentially hands over control to the specified target task. The browser session, cookies, and local storage are preserved and passed to the new task, allowing it to continue seamlessly from the exact state the current task left off.

### Configuration

- **Action**: `start`
- **Task**: The ID of the task you want to trigger. In the Editor, this is usually selected from a dropdown list of available tasks. This is required.

## 2. Common Scenarios

Here are typical situations where you use the **Start Task** action block:

### Reusable Login Flows

Instead of copying and pasting the login steps (typing username/password, handling 2FA, waiting for the dashboard) into every task that requires authentication, you can create a single "Login Task".

- **Task A (Login Task)**: Navigates to `/login`, fills credentials, submits, and waits for success.
- **Task B (Scrape Data)**: The first block is a **Start Task** pointing to Task A. After Task A completes successfully, Task B continues to navigate and extract data, already authenticated.

### Multi-Step Data Pipelines

You might have a master task that orchestrates several sub-tasks to gather complex information.

- **Master Task**:
  1. Starts "Search Items Task" (which populates an array of links).
  2. Iterates over those links.
  3. Inside the loop, uses **Start Task** to run "Extract Item Details Task" for each link.
  4. Merges the results.

### Conditional Execution

You can trigger different flows based on the state of the page using an **If** block.

- **Action**: `if` (condition: `exists('.captcha-wall')`)
- **Action**: `start` (Task: "Solve Captcha Flow")
- **Action**: `end`
- **Action**: `start` (Task: "Main Scraping Flow")

## 3. Best Practices

- **Pass State Securely**: Because the browser session is shared, variables defined in the calling task might not be automatically available in the started task unless explicitly passed or stored in a way the new task can access (like local storage or a shared database, depending on your setup).
- **Keep Sub-tasks Focused**: Tasks designed to be started by others should be small, focused on a single responsibility (e.g., "Accept Cookies", "Login", "Scrape Profile"). This makes them easier to debug and reuse.
- **Handle Errors Gracefully**: If a started task fails, the calling task will also fail unless the **Start Task** block is wrapped in an **On Error** block. Ensure your sub-tasks have robust error handling so they don't break the entire pipeline unexpectedly.

## 4. Troubleshooting Task Starts

If a **Start Task** action doesn't seem to work:

- **Missing Task ID**: Ensure the target task actually exists and the ID is correct. If the target task was deleted, the action will fail.
- **Circular Dependencies**: Avoid starting Task A from Task B, and then starting Task B from Task A. This will create an infinite loop that will eventually crash the execution or timeout.
- **Unexpected State**: The started task assumes the browser is in a specific state. If the calling task navigated away or altered the page unexpectedly before starting the sub-task, the sub-task's selectors might fail. Always ensure the "handoff" point is well-defined.
