# Grumo Skills

Official Agent Skills for the **Grumo ecosystem**.

This repository packages reusable development guidance for AI coding agents so they understand how to build with Grumo, evolve Grumo Framework, and work on Grumo Store without rediscovering the architecture or falling back to generic framework patterns.

## Included skills

### `grumo-development`

For application development with Grumo:

- Model and UUIDv7 identity
- `field()`, indexes, unique constraints and defaults
- typed relationships
- validation
- Runtime vs Store ownership
- Jobs, Events, Streams, Topics and Objects
- agents and autonomous systems
- Grumo application anti-patterns

### `grumo-core-development`

For contributors changing Grumo Framework itself:

- canonical execution lifecycle
- Runtime authority
- Store ownership
- adapter design
- Store Python binding boundary
- framework CI and release gates
- architectural invariants

### `grumo-store-development`

For development of Grumo Store:

- Rust core
- native Store primitives
- cross-domain transactions
- PyO3 Python binding
- Python API design
- Store packaging and releases

### Focused production skills

- `grumo-production-deployment` — secure configuration, health/readiness,
  provenance, and rollback evidence.
- `grumo-component-authoring` — semantic, accessible, token-based UI work.
- `grumo-store-backup-recovery` — backup, restore, compaction, quota, and
  disaster-recovery operations.

## Use today with VS Code / GitHub Copilot

Clone the repository:

```bash
git clone git@github.com:helderperez-dev/grumo-skills.git
cd grumo-skills
```

### Install globally for Copilot

macOS / Linux:

```bash
bash scripts/install.sh copilot
```

Preview an installation without changing the destination:

```bash
bash scripts/install.sh --dry-run project ~/code/grumo
```

Normal installations stage existing skills and automatically restore them if
copying a later skill fails.

This installs into:

```text
~/.copilot/skills/
├── grumo-development/
├── grumo-core-development/
└── grumo-store-development/
```

Reload VS Code after the first installation if necessary.

### Install into one project only

For example, inside the Grumo Framework checkout:

```bash
bash scripts/install.sh project ~/code/grumo
```

The skills are copied to:

```text
<project>/.github/skills/
```

### Generic agent location

For agents that discover skills from `~/.agents/skills`:

```bash
bash scripts/install.sh agents
```

### Windows / PowerShell

Global Copilot installation:

```powershell
.\scripts\install.ps1 -Target copilot
```

Project installation:

```powershell
.\scripts\install.ps1 -Target project -ProjectPath C:\code\grumo
```

## Using the skills

A skills-capable agent may discover a skill automatically from its description.

You can also explicitly tell the coding agent which Grumo skill to use.

Examples:

```text
Use the grumo-development skill and build a Customer model with indexed email lookup.
```

```text
Use grumo-core-development. Review this change and make sure it preserves Runtime ownership of Store.
```

```text
Use grumo-store-development. Expose this new Rust primitive through the Python binding.
```

When the client exposes slash-command style skill invocation, the corresponding names are:

```text
/grumo-development
/grumo-core-development
/grumo-store-development
```

## Repository layout

```text
grumo-skills/
├── .github/
│   └── skills/
│       ├── grumo-development/
│       │   ├── SKILL.md
│       │   └── references/
│       ├── grumo-core-development/
│       │   ├── SKILL.md
│       │   └── references/
│       └── grumo-store-development/
│           ├── SKILL.md
│           └── references/
├── scripts/
│   ├── install.sh
│   └── install.ps1
├── AGENTS.md
└── README.md
```

## Source-of-truth strategy

This repository is the **distribution repository**.

The intended long-term ownership model is:

```text
helderperez-dev/grumo
  ├── grumo-development
  └── grumo-core-development

helderperez-dev/grumo-store
  └── grumo-store-development

             ↓ sync/release

helderperez-dev/grumo-skills
  └── distribution for coding agents
```

This keeps architectural guidance versioned near the implementation while providing one convenient installation repository.

## Core philosophy

> Do not implement a generic industry pattern merely because it is familiar. First determine whether Grumo already has a native primitive or architectural rule for the problem.

The primary architectural rules are:

1. Runtime owns semantics and authority.
2. Store owns durable mechanics.
3. AI is Compute, not a second Runtime.
4. Effect != Observation.
5. Prefer local-first mechanics.
6. One Runtime process owns one Store writer.
7. Prefer native Store primitives over compatibility encodings.
8. Python typing expresses data semantics.
9. `field()` expresses persistence metadata.
10. `relation()` expresses relationships and lifecycle policy.
11. Do not claim distributed guarantees that Grumo does not implement and test.
12. Add operational complexity only when a real product requirement demands it.

## Updating

After pulling a newer version of this repository, reinstall:

```bash
git pull
bash scripts/install.sh copilot
```

The installer replaces only the Grumo skill directories it owns.
