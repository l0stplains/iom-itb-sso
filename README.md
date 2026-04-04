# IOM ITB SSO

This folder is a self-contained Keycloak for IOM ITB SSO.

> [!NOTE]
> Please refer to [iom-itb-sso-poc](https://github.com/l0stplains/iom-itb-sso-poc) and [integration guide](https://github.com/l0stplains/iom-itb-sso-poc/blob/main/docs/SSO-INTEGRATION-GUIDE.md) for technical explanations.

Contents:
- keycloak/realm-export.json: realm definition
- keycloak/themes/iom-itb: login theme
- postgres/init.sql: postgres initialization for Keycloak DB
- docker-compose.local.yml: local stack for development
- docker-compose.prod.yml: production-oriented stack
- .env.example: environment template
- WORKFLOW.md: operational guide for typical SSO changes and Coolify deployment

## Local development quick start

1. Copy env template:

```bash
cp .env.example .env
```

2. Start local stack:

```bash
docker compose -f docker-compose.local.yml up --build
```

3. Open:
- Keycloak: http://localhost:8080
- Admin user: KEYCLOAK_ADMIN / KEYCLOAK_ADMIN_PASSWORD from .env

## Production with Docker Compose

1. Prepare .env with strong passwords and public URL.
2. Run:

```bash
docker compose -f docker-compose.prod.yml up -d
```

3. Put Keycloak behind reverse proxy/platform (Coolify in target setup).

## Notes

> [!IMPORTANT]
> Current domain values in this stack use `*.kirisame.jp.net` for staging/testing.
> Before moving to a new server or production domain, update all related URLs and settings, including:
> - `keycloak/realm-export.json` client URLs (`redirectUris`, `webOrigins`, `rootUrl`, `baseUrl`, `post.logout.redirect.uris`)
> - `.env` / Coolify variables (especially `KEYCLOAK_PUBLIC_URL`)
> - application-side OIDC config in frontend/backend repos (issuer/authority, redirect/logout URIs)

- The imported realm is iom-itb-sso.
- When changing realm-export.json, re-import behavior depends on your Keycloak state and existing DB data.
- For repeatable environments, keep realm JSON and env contract versioned.
