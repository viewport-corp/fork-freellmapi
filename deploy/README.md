# Viewport Internal Overlay — freellmapi

Internal deployment overlay for [freellmapi](https://github.com/tashfeenahmed/freellmapi).
This directory adds only Viewport deployment config; the upstream project is untouched.

## What this is

A minimal, pinned, loopback-only deployment of freellmapi for **Viewport internal use**.
The upstream repo self-labels as **"personal experimentation only"**, so this overlay
keeps the service private (never internet-exposed) and pins a known image.

## Configuration

- **Image:** pinned to `ghcr.io/tashfeenahmed/freellmapi:v0.4.1` (no floating `:latest`).
- **Binding:** loopback-only — `127.0.0.1:${PORT:-3001}:3001`. Not reachable from the
  internet. Do **not** change `127.0.0.1` to `0.0.0.0`.
- **Data:** SQLite persisted in the `freellmapi-data` volume.
- **Secrets:** provided via `.env` (see `.env.example`). `ENCRYPTION_KEY` is **required**
  (64-char hex; generate with `openssl rand -hex 32`).

## Deploy (dokploy-new)

Deploy on **dokploy-new** using this fork as the git source:

- **Git source:** this fork (`viewport-corp/fork-freellmapi`)
- **Compose path:** `deploy/docker-compose.yml`
- Set `ENCRYPTION_KEY` (and any optional vars) in the environment / `.env`.

## Process

Follows the locked Viewport external-OSS process:
**fork → clone → upstream → viewport/deploy overlay → PR.**
