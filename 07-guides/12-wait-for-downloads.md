# Wait for Downloads

When automating web interactions, downloading files is a common requirement. The **Wait for Downloads** action block ensures your task reliably pauses until all pending file downloads are completely finished and saved to disk.

## 1. How Wait for Downloads Works

When a task triggers a file download (for instance, by clicking a "Download CSV" or "Export" button), the browser initiates a background process to fetch the file. Because this happens asynchronously, a generic Wait block is often unreliable: if you wait 5 seconds but the download takes 10 seconds, your task will fail or miss the downloaded file entirely.

The **Wait for Downloads** block communicates directly with the browser to monitor the status of all active download streams. It dynamically pauses task execution until the browser reports that the download has completed successfully, making your automation both faster and more resilient to network fluctuations.

## 2. Configuration

To use this block, place it immediately after the action that triggers the download.

- **Value**: The maximum time to wait, in seconds. If the download does not complete within this time limit, the task will throw an error and fail (unless handled by an **On Error** block). A typical default timeout is 30 seconds, though large files may require a longer duration.

## 3. Usage Context

A standard flow involving file extraction typically looks like this:

### Step 1: Trigger the Download

Use a click action to interact with the button or link that initiates the file download.

- **Action**: `click`
- **Selector**: `.export-data-btn`

### Step 2: Wait for Downloads

Immediately following the click, insert the **Wait for Downloads** block.

- **Action**: `wait_downloads`
- **Value**: `60` *(Waits up to 60 seconds for the file)*

### Step 3: Accessing the Download

Once the download is complete, figranium automatically registers the file in the task's execution results. You can access downloaded files through the `downloads` array in the final execution result payload, which contains the file `name`, `url`, and local `path`.
