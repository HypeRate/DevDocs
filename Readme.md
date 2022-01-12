# HypeRate DevDocs

## What will happen at the first february weekend?

On the first weekend in february we will switch the old and the new API.

For testing purposes we set up another host which can be used for testing.

At the said weekend we will switch some DNS entries and let all the traffic route to the new host. This host will only serve the new API - so you need to make sure that you got your own websocket key on our [Discord](https://discord.gg/75jcqvuHAH) through the ticket system.

**IMPORTANT: Do not switch the domains! They old one will remain active after moving the DNS entries!**

**Only use the new domain for testing purposes - it won't be accessible after said weekend.**

## I don't have a compatible device! What should I do?

The new API sends sends a random heartbeat between 1 and 10 every second to the `internal-testing` device id.

## Old API

URL: `wss://app.hyperate.io/socket/websocket`

Authentication: None required

## New API

URL: `wss://app.hyperate.io/socket/websocket?token=<MY-WEBSOCKET-KEY>`

Authentication: Websocket key required

## Required websocket messages

### Join Channel

You need to join the appropiate channel before any data will be send to your client.

To do this you need to send the following JSON message:

```json
{
  "topic": "hr:<ID>",
  "event": "phx_join",
  "payload": {},
  "ref": 0
}
```

This would be the correct message to join the "internal-testing" channel:

```json
{
  "topic": "hr:internal-testing",
  "event": "phx_join",
  "payload": {},
  "ref": 0
}
```

### Send heartbeat

Phoenix expects that you send the heartbeat every 30 seconds otherwise the connection will be closed.

```json
{
  "topic": "phoenix",
  "event": "heartbeat",
  "payload": {},
  "ref": 0
}
```
