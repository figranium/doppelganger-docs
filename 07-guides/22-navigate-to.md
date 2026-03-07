# Navigate To

The **Navigate To** action block is used to directly change the URL of the automated browser. This allows your task to jump directly to a specific page or start a new sequence of actions without relying on clicking links from an existing page.

## 1. How the Navigate To Action Works

When the task executes a **Navigate To** block, the browser initiates a standard page load for the provided URL. The task will wait until the basic page load event finishes before moving to the next block.

### Configuration

- **Action**: `navigate`
- **Value**: The full URL you want the browser to visit (e.g., `https://example.com/login`, `https://example.com/search?q=laptops`). You can include `{$variables}` to build dynamic URLs.

## 2. Common Scenarios

Here are typical situations where you use the **Navigate To** action block:

### Starting a New Flow

Instead of relying on the initial task URL, a task can begin by explicitly navigating to a login screen or a dashboard.

- **Action**: `navigate`
- **Value**: `https://dashboard.example.com`

### Parameterized Searches

If a site uses URL parameters for search queries, it's often faster to build the URL and navigate directly rather than filling out search forms.

- **Action**: `navigate`
- **Value**: `https://shop.example.com/products?category={$category}&sort=price_asc`

### Recovering from Errors

In an **On Error** block, you might want to restart a process by navigating back to the home page or previous step before retrying.

- **Action**: `navigate`
- **Value**: `https://example.com/start-over`

## 3. Best Practices

- **Include the Protocol**: Always provide a complete URL including `http://` or `https://`. Relative paths (like `/about`) will not work reliably unless handled explicitly by JavaScript.
- **Dynamic URLs**: Use the variable syntax (e.g., `{$query}`) to inject runtime data into the URL string.
- **Combine with Waits**: Even though `navigate` waits for the basic load, modern single-page applications (SPAs) often render content asynchronously _after_ the initial load. It's almost always a good idea to follow a **Navigate To** block with a **Wait for Selector** block targeting a key element on the new page.

## 4. Troubleshooting Navigation

If a **Navigate To** action seems to fail or hang:

- **Invalid URLs**: Ensure the URL is correctly formatted and accessible. Check for typos or missing parameters.
- **Timeouts**: If the target server is slow to respond, the navigation might time out. You might need to handle this with an **On Error** block.
- **Redirections**: The browser will automatically follow standard HTTP redirects. If the final URL is different from what you expected, the site might be redirecting based on authentication or geographical location.
