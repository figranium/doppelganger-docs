# For Each

## Description

The **For Each** action block allows you to iterate over a list of elements on a page. It executes the actions contained within the block once for every element that matches a specified selector.

## Use Case

This block is particularly useful for scraping lists of items, such as search results, product cards, or table rows. Instead of manually specifying each item, you can dynamically loop through them to extract data or perform actions on each individual item.

## Example Configuration

Let's say you want to interact with a list of links on a page. You can configure the **For Each** block as follows:

- **Selector**: `.link` (This will match all elements with the class `link`).
- **Var Name**: `currentItem` (This variable will hold the index/data of the current element being processed in the loop).

Inside the loop, you can add actions like **Click** or **Extract Text** and reference the `currentItem` variable if needed.
