# Merging Data

The **Merge** action block allows you to combine multiple arrays, objects, or primitive values into a single output within your task. This is extremely useful when you have collected pieces of data from different steps (e.g., scraping multiple pages or performing sequential API calls) and need to consolidate them into one unified payload for further processing or export.

## 1. How the Merge Action Works

The **Merge** block takes a list of values or variables and merges them together. The type of merging performed depends on the types of the inputs:

- **Arrays**: If multiple arrays are provided, they are concatenated into a single flat array.
- **Objects**: If multiple objects are provided, their properties are combined into a single object. If there are overlapping keys, the properties from the object provided later in the list will overwrite those from earlier objects.
- **Mixed/Primitives**: If a mix of arrays, objects, or primitive values is provided, they are typically gathered into an array, or handled according to the specific context.

### Configuration Options

- **Value**: A comma-separated list of values or variables to merge. You can reference variables using the `{$variableName}` syntax or access the output of the previous block using `{$block.output}`.
- **Target Variable**: (Optional) The name of a new or existing variable where the merged result will be stored. If left blank, the merged result is available in `block.output` for the immediate next step.

## 2. Basic Examples

### Merging Arrays

Suppose you have scraped two lists of products and stored them in variables:
- `productsPage1`: `[{"id": 1, "name": "Item A"}, {"id": 2, "name": "Item B"}]`
- `productsPage2`: `[{"id": 3, "name": "Item C"}]`

To combine these:
- **Action**: `merge`
- **Value**: `{$productsPage1}, {$productsPage2}`
- **Target Variable**: `allProducts`

The `allProducts` variable will now contain:
`[{"id": 1, "name": "Item A"}, {"id": 2, "name": "Item B"}, {"id": 3, "name": "Item C"}]`

### Merging Objects

Suppose you have extracted user profile data in two steps:
- `basicInfo`: `{"name": "Alice", "role": "Admin"}`
- `contactInfo`: `{"email": "alice@example.com", "phone": "555-1234"}`

To combine these into a single profile object:
- **Action**: `merge`
- **Value**: `{$basicInfo}, {$contactInfo}`
- **Target Variable**: `userProfile`

The `userProfile` variable will now contain:
`{"name": "Alice", "role": "Admin", "email": "alice@example.com", "phone": "555-1234"}`

## 3. Using the Previous Output

Often, you might want to merge the result of the immediately preceding block with existing data.

For example, if the previous block fetched additional details for an item, and you want to merge it with a base item stored in `currentItem`:
- **Action**: `merge`
- **Value**: `{$currentItem}, {$block.output}`
- **Target Variable**: `currentItem`

This will effectively update `currentItem` with the newly fetched details.

## 4. Combining with Other Actions

The **Merge** action is commonly used in conjunction with looping structures like **For Each** or **While**.

A typical pattern for gathering data across a loop is:
1. Initialize an empty array variable before the loop (e.g., `set` action: `allData` = `[]`).
2. Inside the loop, extract some data (e.g., using a **JavaScript** block or API call).
3. Use a **Merge** block inside the loop to append the new data to the accumulator array:
   - **Value**: `{$allData}, {$block.output}`
   - **Target Variable**: `allData`

By effectively using the **Merge** block, you can easily organize and structure the data collected throughout your automated tasks.
