# Lucky wheel: remote spin page

Static page served by GitHub Pages at https://lucky-wheel-usa.github.io/.

A lucky wheel board makes the link on its "Vòng quay" page: `https://lucky-wheel-usa.github.io/#b=<board id>&k=<key>`.
The part after `#` never leaves the phone. The page and the board meet on public MQTT brokers
(`broker.hivemq.com`, backup `broker.emqx.io`) on `lucky-wheel/<id>/s` (state) and `lucky-wheel/<id>/c` (commands).
Every message is AES-128-GCM encrypted with the key from the link, so the brokers only see ciphertext.

Mobile carriers block the brokers' WebSocket ports (8884, 8084), so the page first connects to the relay
`wss://lucky-relay.lucky-wheel-usa.workers.dev/hivemq` (or `/emqx`) on port 443: a Cloudflare Worker (`relay/`) that
pipes the bytes to the broker's TCP port 1883, for pages of this site only. Deploy it with `npx wrangler deploy` in
`relay/`. `test.html` shows which ports a network lets through.

The page is one file (`index.html`) with no external scripts. The firmware side is `usermods/lucky_wheel/lucky_remote.h`.
