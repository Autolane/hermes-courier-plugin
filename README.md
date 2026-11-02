# Courier by Autolane for Hermes

Restaurant pickup delivery in Austin, Texas. You place a pickup order with a restaurant or prepared-food store, and an Autolane vehicle collects it and brings it to you for a flat fee.

This is a portable Agent Plugins v1 package: `plugin.json`, `mcp.json` and one skill. It has no code and installs nothing. It points Hermes at Autolane's hosted MCP server, `https://mcp.goautolane.com/courier-mcp`.

## Install

1. `hermes plugins install courier-by-autolane --enable`
2. Sign in once:

       hermes mcp add courier-by-autolane --url https://mcp.goautolane.com/courier-mcp --auth oauth --connect-timeout 300

   Hermes opens Autolane's "Link your phone" page. Enter your mobile number and the 6-digit code Autolane texts you. When the page asks where Hermes runs, choose **On this computer**, then **Finish linking**. Keep all the tools Hermes lists.
3. Start a new session and ask: "Can Autolane deliver my pickup order from a taco shop on South Congress to 500 W 2nd St?"

Step 2 exists because Hermes doesn't yet sign in to a plugin's remote server. It adds the same server to `config.yaml`, where it replaces the plugin's entry. If you added Courier by hand from our docs before, delete that entry so the tools don't load twice.

Courier is invite-only for now. If your number isn't on the list, [join the waitlist](https://goautolane.com/autolane-courier).

## Approvals

`reserve_delivery`, `confirm_delivery`, `update_delivery` and `cancel_delivery` book, change or cancel a real delivery and take payment. The plugin asks Hermes to confirm each one with you, but the sign-in in step 2 replaces that setting. To keep it, add `trust: untrusted` under `mcp_servers.courier-by-autolane` in `config.yaml`. `check_delivery` and `get_delivery_status` only read.

## Data and privacy

Every tool call goes to Autolane at mcp.goautolane.com and carries store and drop-off addresses, your name, order details and the store's confirmation. Hermes stores and refreshes your Autolane sign-in. The plugin stores nothing and sends no telemetry. The tool list comes from Autolane's server and can change without a new plugin release.

To remove it: `hermes mcp remove courier-by-autolane`, then `hermes plugins disable courier-by-autolane`.

[Privacy policy](https://goautolane.com/privacy-policy) · [Terms of service](https://goautolane.com/terms-of-service) · Help: support@goautolane.com
