# Processing CSV Data

The **CSV** action block allows you to parse comma-separated values (CSV) into structured data (an array of rows) directly within your task. This is particularly useful when you need to read bulk data from a file or external source and iterate over it.

## 1. How the CSV Action Works

The **CSV** block takes a string of CSV formatted text and converts it into a JavaScript array of objects, where the keys are the column headers.

- **Value**: The raw CSV text you want to parse.

### Using `block.output`

If you leave the **Value** field blank, the CSV block will automatically attempt to use the output from the _previous_ block (`block.output`). This makes it easy to chain actions, such as downloading a CSV file or fetching CSV text via an API, and immediately parsing it.

## 2. Basic Example

Suppose you have the following CSV text:

```csv
name,role,email
Alice,Admin,alice@example.com
Bob,User,bob@example.com
```

### Step 1: Input the CSV

- **Action**: `csv`
- **Value**:
  ```csv
  name,role,email
  Alice,Admin,alice@example.com
  Bob,User,bob@example.com
  ```

### Step 2: Accessing the Result

After the CSV block executes, `block.output` will contain an array of objects:

```json
[
  { "name": "Alice", "role": "Admin", "email": "alice@example.com" },
  { "name": "Bob", "role": "User", "email": "bob@example.com" }
]
```

## 3. Iterating Over Parsed CSV Rows

The most common use case for parsing CSV data is to iterate over the rows and perform actions for each row. You can achieve this using the **For Each** action block.

### Step 1: Parse the CSV

- **Action**: `csv`
- **Value**: (Your CSV data or leave blank to use previous output)

### Step 2: Store the Parsed Data (Optional but Recommended)

It's often helpful to store the parsed array in a variable before iterating over it.

- **Action**: `set`
- **Var Name**: `userData`
- **Value**: `{$block.output}`

### Step 3: Iterate with For Each

- **Action**: `foreach`
- **Selector**: Leave blank or use it for specific iterations (if dealing with complex structures). For variables, use the variable in a custom iteration logic, or standard For Each setup depending on your task's structure.
- **Var Name**: `row`

### Step 4: Use Row Data Inside the Loop

Inside the loop, you can access the current row's data using the variable you defined (e.g., `row`).

- **Action**: `type`
- **Selector**: `#email-input`
- **Value**: `{$row.email}`

## 4. Combining with Other Actions

You can combine the **CSV** action with actions like **JavaScript** or **Merge** to further process the data. For instance, you could use a JavaScript block to filter the parsed CSV rows before iterating over them.

```javascript
// Filter the parsed CSV (assuming it's in a variable called 'csvData')
return variables.csvData.filter((row) => row.role === "Admin");
```

By leveraging the CSV block, you can easily integrate external data sources into your automated tasks.
