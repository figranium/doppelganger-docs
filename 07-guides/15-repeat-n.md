# Repeat N

The **Repeat N** action block repeatedly executes a sequence of actions a specific number of times. This is ideal for situations where you need to perform an operation a known, fixed number of times.

## 1. Why Use Repeat N?

The **Repeat N** block is perfect for predictable, fixed-length loops.
- **Fixed Iterations**: You know exactly how many times an action needs to happen (e.g., click a "Next" button exactly 3 times, or scrape exactly 5 pages of results).
- **Simplifying Repetitive Tasks**: Avoid copying and pasting the same action blocks multiple times in your task sequence.
- **Controlled Execution**: It's safer than a `while` loop when you want a strict limit on repetitions and don't want to risk an infinite loop.

## 2. Setting Up the Repeat N Block

The **Repeat N** block has a very simple configuration.

### Configuration

- **Value**: The number of times the block of actions inside it should be repeated. This must be a positive integer (e.g., `5`, `10`).

## 3. Common Scenarios

### Paginating a Specific Number of Times

If you want to extract data from the first 3 pages of a search result.

- **Action**: `repeat`
  - Value: `3`
  - Inside the block:
    - **Action**: `javascript` (to extract data)
    - **Action**: `click` (Selector: `.next-page-button`)
    - **Action**: `wait_selector` (Wait for next page to load)

### Retrying an Action

You can combine **Repeat N** with conditional logic to attempt an action a few times before giving up.

- **Action**: `repeat`
  - Value: `3`
  - Inside the block:
    - **Action**: `click` (Selector: `#retry-button`)
    - **Action**: `wait` (Value: `2`)

## 4. Best Practices

- **Avoid Infinite Loops (Implicitly)**: Unlike a `while` loop, **Repeat N** has a built-in exit condition. It will always finish after N iterations.
- **Use for Predictable Outcomes**: Only use **Repeat N** when you are certain the number of repetitions is correct. If the number of pages might change, a `while` loop with a condition checking for a "Next" button might be more robust.
- **Nested Blocks**: You can nest other logic blocks (`if`, `foreach`, even another `repeat`) inside a **Repeat N** block to build complex workflows.
