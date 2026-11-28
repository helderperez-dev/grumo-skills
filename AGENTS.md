# Grumo Skills

This repository distributes Agent Skills for the Grumo ecosystem.

Rules for contributors and agents:

- Treat `helderperez-dev/grumo` and `helderperez-dev/grumo-store` as implementation sources of truth.
- Do not invent public Grumo APIs. Verify current code before documenting a symbol.
- Keep `SKILL.md` files concise and link to supporting references.
- Preserve architectural distinctions: Runtime owns semantics/authority; Store owns durable mechanics.
- Prefer native Store primitives over compatibility KV encodings.
- Do not claim distributed guarantees that are not implemented and tested.
- When a public Grumo API changes, update the corresponding skill in the same development cycle.
