# CareRoute Auth & Data API — Docs (public)

Public-facing docs site for the CareRoute mobile backend API. This is a
**docs-only mirror**, published via GitHub Pages so the mobile team (and anyone
else who needs it) can browse the API without repo access to the private
application source.

- **[openapi.yaml](openapi.yaml)** — OpenAPI 3.1 spec: every route, request/response
  schema, status code, and the `bearerAuth` (Firebase ID token) requirement, plus
  notes on the custom-token → ID-token exchange flow and known API limitations.
- **[index.html](index.html)** — a single-file Swagger UI page (loads
  `swagger-ui-dist` from the jsDelivr CDN, no build step) that renders
  `openapi.yaml`.

## Source of truth

The actual API source lives in the private `careroute-firebase` repo, at
`functions/src/index.ts` (and `otp.ts` / `credentials.ts` / `salesforce.ts`). This
repo's `docs/` folder there is the working copy that gets edited first; this
public repo is a **manually synced publish target** — when the spec changes,
copy the updated `docs/openapi.yaml` (and `index.html`, if it changes) here and
push. There's no automation wiring the two together yet.

## Viewing it locally

```bash
npx serve .
# or
python -m http.server 8000
```

Then open the printed URL — Swagger UI fetches `openapi.yaml` via `fetch()`,
which browsers block on a bare `file://` page, so it needs to be served over
HTTP even locally.

## Published at

https://jerehlomak.github.io/careroute-api-docs/ (once GitHub Pages is enabled
on this repo, Settings → Pages → Deploy from a branch → `main` / `/ (root)`).
