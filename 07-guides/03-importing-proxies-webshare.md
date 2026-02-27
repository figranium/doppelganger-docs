# Importing Proxies into Doppelganger: Webshare

Doppelganger supports rotating through a list of proxies or using a single backconnect (rotating) proxy. This guide explains how to get your proxies from Webshare and import them correctly.

## 1. Exporting from Webshare

1. Log in to your [Webshare Dashboard](https://dashboard.webshare.io/).
2. Navigate to **Proxy** > **List** in the sidebar.
3. Click the **Download** button or use the **Copy** feature.
4. **Important: Check the format.** Doppelganger's importer expects one of the following formats:
   - `host:port:username:password` (Standard Webshare format)
   - `protocol://username:password@host:port` (URL format)
   
   Ensure your Webshare download configuration matches the `IP:Port:Username:Password` order.

## 2. Importing into Doppelganger

### Option A: Bulk Import (Recommended for lists)
1. Open Doppelganger and go to **Settings** > **Proxies**.
2. Click the **Import** button.
3. Select the `.txt` file you downloaded from Webshare.
4. Doppelganger will automatically parse the lines and add them to your list.

### Option B: Manual Add (Recommended for Backconnect/Rotating Proxies)
If you are using Webshare's **Backconnect** (rotating) proxy (e.g., `p.webshare.io`):
1. In **Settings** > **Proxies**, enter the server (e.g., `p.webshare.io:80`).
2. Enter your **Username** and **Password**.
3. Check the **Rotating pool** box.
   - This tells Doppelganger that this single address provides a pool of IPs.
   - You can optionally set the **Estimated size** to help the system manage session health.
4. Click **Add Proxy**.

## 3. Using Your Proxies

- **Set Default**: Click the **Star** icon next to a proxy to make it the default for all new tasks.
- **Rotation Mode**: Choose between **Round Robin** (sequential) or **Random** rotation.
- **Task Specific**: You can override the proxy settings within a specific task's configuration if needed.


> *Tip: If your proxies are IP-authorized instead of password-authorized, you only need to provide the `host:port` and ensure your server's IP is whitelisted on Webshare.*
