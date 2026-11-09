# Ghost Docker

Configuration to run Ghost and its services with Docker Compose

## IPv6 networking

IPv6 networking is opt-in because it requires newer Docker and Docker Compose versions than the base setup. Enable it by including the IPv6 override file:

```sh
docker compose -f compose.yml -f compose.ipv6.yml up -d
```

## Public URL in a subdirectory

`DOMAIN` is the hostname Caddy serves. By default it is also Ghost's public
URL. If another proxy publishes Ghost at a subdirectory, keep `DOMAIN` as the
origin hostname and set `PUBLIC_URL` to the full canonical URL, including the
trailing slash:

```dotenv
DOMAIN=blog.example.com
PUBLIC_URL=https://example.com/blog/
```

Ghost then generates canonical links, assets, sitemaps and analytics requests
under `/blog/`, while Caddy can continue receiving origin traffic at
`blog.example.com`.

If `ADMIN_DOMAIN` is set, Ghost keeps the public subdirectory in the admin
path. With the example above, the admin URL is
`https://ADMIN_DOMAIN/blog/ghost/`. ActivityPub also needs the external proxy
to expose its root-level `/.well-known/*` and `/.ghost/activitypub/*` routes on
the public domain.

# Copyright & License 

Copyright (c) 2013-2026 Ghost Foundation - Released under the [MIT license](LICENSE).
