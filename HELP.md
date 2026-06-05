# Project Nahan (نهان) - User Walkthrough

This guide will walk you through accessing and managing your newly deployed Nahan gateway. 

## 1. Accessing the Dashboard

By default, your dashboard is mapped to the `/sync/dash` route. 
To access it, open your browser and navigate to:
`https://<YOUR_WORKER_DOMAIN>/sync/dash`

*(Note: If you visit the root domain or `/sync` via a web browser, the system will camouflage itself and show the Ubuntu/Docker website to trick network scanners).*

## 2. Authentication

When you open the dashboard, you will be greeted by the "Telemetry Hub" login screen.
*   **Default Master Key:** `admin`
*   Enter `admin` and click **Authenticate**.

*(If you see a red warning saying "⚠️ DB sync missing!", it means you haven't bound the `IOT_DB` KV namespace to your worker yet. Return to Cloudflare settings to bind it!)*

## 3. Using the Dashboard

The dashboard consists of 4 main tabs:

### 📡 Endpoints (Info)
This is where you retrieve your connection strings to import into your client application (like v2rayN, Nekobox, or Clash).
*   **Data Stream Link:** The direct URI format (e.g., `vless://...`). You can scan the QR code using your mobile device.
*   **Cloud Sync URL:** The base API path for direct Sub/Config syncing.

### 📊 Metrics (Network)
Displays basic network information about where your Cloudflare edge node is executing, including the Cloudflare Colo code and origin IP.

### ⚙️ System (Settings)
Here you can change core functionalities:
*   **Encoding Mode:** Choose `Alpha Mode` (VLESS) or `Beta Mode` (Trojan).
*   **Device UUID:** Your secret client password/UUID. If you leave this blank, the system auto-generates one.
*   **API Route:** Change this from `sync` to a hidden keyword (e.g., `my-secret-path`). Your dashboard will move to `/my-secret-path/dash`.
*   **Master Key:** Change the dashboard login password from `admin` to a secure phrase.

### 🌐 Network (Advanced)
Fine-tune your proxy properties:
*   **Resolver IP & Metric Node IP:** Useful if you are routing traffic through Cloudflare Pages or utilizing specific fallback IPs.
*   **Backup Relay IP:** If the main WebSocket connection drops, traffic falls back to this IP.
*   **Maintenance Hosts:** A comma-separated list of websites (e.g., `ubuntu.com, docker.com`). Unauthorized users scanning your domain will see these sites instead.

## 4. Applying Changes

After making changes in the **System** or **Advanced** tabs:
1. Click the blue **Update Config** button at the bottom of the screen.
2. The page will display "Syncing..." and then reload automatically.
3. *Important:* If you changed the **API Route**, the page will automatically redirect you to the new URL (e.g., `/<new-route>/dash`). Make sure to bookmark the new link!

## 5. Client Configuration

If you're importing this profile to a client (e.g., v2rayNG, Shadowrocket):
*   Navigate to the **Endpoints** tab.
*   Click **Copy** next to the Data Stream Link.
*   Import the link from your clipboard into your proxy client.
*   Ensure that your client is configured to allow `WebSocket (ws)` as the transport protocol, and `TLS` is active (if running on port 443).
