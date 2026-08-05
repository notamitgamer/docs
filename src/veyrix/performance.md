---
label: Performance & Errors
icon: zap
order: 550
---

# Performance & Benchmarks

By stripping away Webpack overhead, Virtual DOM reconciliation, and heavy language servers, Veyrix operates on a fraction of the hardware requirements of modern cloud IDEs.

| Environment | Base RAM (idle) | Editor engine | Time to interactive |
|---|---|---|---|
| Veyrix IDE | ~30MB – 42MB | Ace Editor (vanilla) | < 0.5 seconds |
| VS Code Web | ~350MB+ | Monaco + Web Workers | 2.5 – 4 seconds |
| CodeSandbox | ~500MB+ | Monaco + Container VM | 4 – 8 seconds |

## Why it's better for mobile / low-end devices

- **Debounced I/O** — IndexedDB writes are debounced by 500ms, ensuring zero main-thread blockage during rapid typing
- **No Monaco overhead** — Monaco is powerful but struggles on low-end Androids due to heavy worker threading; Ace Editor is substantially lighter
- **Visual viewport anchoring** — PWA implementations often suffer layout thrashing when the soft keyboard appears; Veyrix anchors directly to the `window.visualViewport` API, freezing the reflow

# Error Handling Behavior

## "Incognito" / Private Mode restraints

Safari and Firefox frequently restrict or completely block IndexedDB access in Private Browsing. If `DB.init()` fails, Veyrix degrades gracefully to an in-memory volatile state. A UI toast warns the user that files will be lost when the tab closes, prompting manual downloads.

## DOMException: QuotaExceededError

Triggered when the device runs out of disk space, or the browser's origin quota is exceeded. Veyrix catches this in the `DB.save()` promise rejection, halting autosave and notifying the user to clear space or delete older snapshots.
