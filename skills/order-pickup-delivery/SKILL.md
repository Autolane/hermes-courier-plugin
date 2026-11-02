---
name: order-pickup-delivery
description: Have an Autolane vehicle collect a restaurant pickup order and deliver it in Austin, Texas, using the Courier by Autolane tools. Use when the user asks for Autolane or Courier delivery of a pickup order in Austin, or asks about an Autolane delivery already placed.
compatibility: Needs the Courier by Autolane MCP server (https://mcp.goautolane.com/courier-mcp) connected in Hermes as `courier-by-autolane`, signed in with a mobile number on the invite list.
---

# Order a pickup delivery

The Courier tools (`mcp__courier_by_autolane__*`) describe the call order, and every response names the next call in `next_step`. Follow them. This skill covers what the tools can't.

## If the tools are missing

If no `mcp__courier_by_autolane__*` tool is available, or a call says to reconnect, tell the user to run this once and then start a new session:

    hermes mcp add courier-by-autolane --url https://mcp.goautolane.com/courier-mcp --auth oauth --connect-timeout 300

Hermes opens Autolane's "Link your phone" page, where the user enters a mobile number and the code Autolane texts. Scheduled and unattended runs can't sign in, so report it and stop. If the page says the service isn't available for the number, Courier is invite-only for now: point the user to https://goautolane.com/autolane-courier.

## Rules

- Austin, Texas only. Call `check_delivery` before checkout. After a decline, don't place the store order for Autolane delivery.
- Show the price, terms and consent text from `check_delivery` and get the user's yes before `reserve_delivery`.
- Get the user's approval for the Autolane fee before sending payment and before the store order is submitted.
- If the user drops the order after a reservation, call `cancel_delivery` so the vehicle is released.
- Never use Autolane for alcohol, tobacco or nicotine, pharmacy items, or anything that needs an ID or age check at pickup.
