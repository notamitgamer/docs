# Veyrix IDE

_v1.1.0 — Stable_

Veyrix is a lightweight, offline-first Progressive Web App (PWA) that turns your browser into a highly responsive code editor. It's designed to run smoothly in strict or restricted browser environments, keeping all processing and storage entirely client-side with no backend server.

## Why use it

- **Absolute privacy** — your files never leave your device; everything is saved in the browser's local IndexedDB unless you explicitly use cloud share
- **Blazing fast** — bypasses heavy virtual DOMs in favor of a vanilla JavaScript architecture, so it runs smoothly on low-end devices
- **True offline mode** — install as a PWA and write code anywhere, no internet connection required
- **Built-in time machine** — save snapshots of your files to instantly roll back to previous versions, no Git setup needed

## Core technology stack

| Component | Version | Role |
|---|---|---|
| Ace Editor | v1.32.6 | Core text engine |
| IndexedDB | — | Local persistence layer |
| LZ-String | v1.5.0 | URL compression (local share) |
| Firebase | v11.6.1 | Cloud share (loaded on demand only) |

Veyrix bypasses Virtual DOM overhead entirely — it uses a vanilla JS monolithic state architecture paired directly with the Ace Editor engine, rather than a framework like React or Vue.

## Getting started

Visit the live site to start using Veyrix IDE immediately — no installation required. To install as a PWA, tap the menu button and select **Install Web App**; it then runs fullscreen without browser toolbars.

## Explore the docs

- [Usage Guide](usage-guide.md) — files, editing, snapshots, sharing
- [Architecture & State Management](architecture.md) — state singleton, IndexedDB schema, cloud sync strategy
- [Security & Threat Model](security.md) — zero-knowledge password hashing, what's and isn't protected
- [Veyrix Web (Multi-File IDE)](veyrix-web.md) — the separate multi-file environment, live preview engine, ZIP export
- [Performance & Error Handling](performance.md) — benchmarks vs. VS Code Web / CodeSandbox, failure modes
- [Limitations & Roadmap](roadmap.md)
- [FAQ](faq.md)

## Support & contact

- General inquiries: mail@amit.is-a.dev
- Important matters: amitdutta4255@gmail.com
- Developer portfolio: [amit.is-a.dev](https://amit.is-a.dev)

## Legal disclaimer & licensing

Veyrix IDE and its documentation are provided "as is" under the **Apache License 2.0**, without warranty of any kind, express or implied. The creator reserves the right to modify or permanently discontinue the project at any time without prior notice, is not responsible for data loss, service interruptions, or damages arising from use of the software, and places sole responsibility for local data management on the user.
