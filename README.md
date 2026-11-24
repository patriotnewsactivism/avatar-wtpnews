# avatar.wtpnews.org

Live page for the Marcus Cole AI anchor at https://avatar.wtpnews.org.

- `index.html` — the served page. Requests avatar `marcus_cole_v2` from the
  LiveTalking server, speaks via `/speak` with a `/human` fallback, and
  carries the confidential-source disclosure ("Marcus never reveals a
  confidential source").
- The page's WebRTC config points at the TURN server on
  `turn:hermes.wtpnews.org:3478` (user `wtpnews`). The TURN credential in
  the page is the current one, rotated on 2026-11-24 after the previous
  credential was found in cleartext. If the credential ever needs rotating
  again, update `/etc/turnserver.conf` on Hermes first, restart coturn,
  then update this file — never commit a retired credential.

## Deploy

Deploy is a manual copy into the Caddy volume on Contabo
(`apex-contabo-caddy-1`, volume `apex-contabo_caddy-config`,
`/config/avatar/index.html`), then verify
`https://avatar.wtpnews.org` serves the new page. Do not edit the
bind-mounted Caddyfile with `sed -i` (inode replacement hides the edit
from the container); truncate in place or restart the container instead.
