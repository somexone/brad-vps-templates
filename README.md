# brad-vps-templates

Custom Portainer v2 template catalog for Dockhand and an existing VPS running
Docker Compose with Traefik v3.

## Templates

- **Brad VPS - Secure Web App** runs an arbitrary HTTP application behind
  Traefik with HTTPS on `websecure`, the `letsencrypt` certificate resolver,
  and the `crowdsec@file,authentik-forward-auth@file` middleware chain. Set
  `APP_NAME`, `APP_IMAGE`, `APP_HOST`, and `APP_PORT`.
- **Brad VPS - Secure Web App + Storage** provides the same secure web
  routing and adds configurable persistent storage. `APP_DATA` defaults to
  `./data`, and `APP_DATA_PATH` defaults to `/config`.
- **Brad VPS - Internal Container** is a minimal private container with no
  Traefik labels and no published host ports. Set `APP_NAME` and `APP_IMAGE`.

The secure web templates use the existing external Docker network named
`proxy`. Before deploying them, that network and the referenced Traefik
file-provider middlewares (`crowdsec@file` and
`authentik-forward-auth@file`) must already exist on the VPS. The secure web
templates expect the existing `websecure` entrypoint and `letsencrypt`
certificate resolver. The catalog does not deploy anything or contain
credentials.

The catalog is defined in `templates.json` and references the Compose files
from the `main` branch through `raw.githubusercontent.com`.
