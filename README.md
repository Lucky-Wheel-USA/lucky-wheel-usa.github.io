# Lucky wheel: remote spin page

Static page served by GitHub Pages at https://lucky-wheel-usa.github.io/.

A lucky wheel board makes the link on its "Vòng quay" page: `https://lucky-wheel-usa.github.io/#b=<board id>&k=<key>`.
The part after `#` never leaves the phone. The page and the board meet on public MQTT brokers
(`broker.hivemq.com`, backup `broker.emqx.io`) on `lucky-wheel/<id>/s` (state) and `lucky-wheel/<id>/c` (commands).
Every message is AES-128-GCM encrypted with the key from the link, so the brokers only see ciphertext.

The page is one file (`index.html`) with no external scripts. The firmware side is `usermods/lucky_wheel/lucky_remote.h`.
