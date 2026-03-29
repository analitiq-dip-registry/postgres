# Contributing

Thank you for your interest in contributing to the Analitiq connector registry. This guide explains how to add endpoints, improve existing connectors, and create new connectors for systems that don't have one yet.

## Before you start

- Install [Claude Code](https://claude.ai/code)
- Install the connector builder plugin:
  ```
  claude plugin add analitiq-dip-registry/analitiq-plugin-connector-builder
  ```
- Fork the connector repo you want to contribute to (or the [connector-template](https://github.com/analitiq-dip-registry/connector-template) for new connectors)

## Adding endpoints to an existing connector

1. Fork and clone the connector repo
2. Launch Claude in the repo directory
3. Tell it: *"Add an endpoint for [resource name]"*
4. The plugin will research the API documentation and generate the endpoint definition
5. Create a PR with the label `version:minor`

## Fixing or improving an existing connector or endpoint

1. Fork and clone the connector repo
2. Make your changes (fix auth details, correct schema fields, update documentation, etc.)
3. Create a PR with the label `version:patch`

For breaking changes to authentication or connector structure, use the label `version:major`.

## Creating a new connector

Before creating a new connector, check if one already exists at [github.com/analitiq-dip-registry](https://github.com/analitiq-dip-registry). Connectors are named `connector-{system-name}`.

If the connector doesn't exist:

1. Launch Claude anywhere
2. Tell it: *"I want to create a connector for [system name]"*
3. The plugin will interview you about the system, research its API documentation, and generate the full connector with all required files
4. Push the new repo to the `analitiq-dip-registry` GitHub org (or request access to do so)

No coding required — the plugin handles authentication research, endpoint schema generation, and file creation automatically.

## Pull request guidelines

- **All PRs must target the default branch** and pass CI checks before merging
- **Apply a version label** to every PR:
  - `version:minor` — new endpoints added
  - `version:patch` — fixes to existing definitions or documentation
  - `version:major` — breaking changes to authentication or connector structure
- **Do not manually edit** `definition/manifest.json` version or `CHANGELOG.md` version entries — a GitHub Action updates these automatically when the PR is merged
- **One connector per repo** — do not add multiple connectors to a single repository

## What the automated pipeline does

When a PR is merged with a version label:

1. The version in `definition/manifest.json` is bumped according to the label
2. A new entry is added to `CHANGELOG.md` with the PR title and date
3. The changes are committed and pushed automatically

If no version label is applied, the version is not changed.

## Repository structure

```
connector-{name}/
├── CLAUDE.md               # Agent reference for Claude Code
├── AGENTS.md               # Agent reference for other frameworks (identical to CLAUDE.md)
├── README.md               # Human documentation
├── CHANGELOG.md            # Version history (auto-updated on merge)
├── CONTRIBUTING.md         # This file
└── definition/             # Connector definition files
    ├── connector.json      # Authentication and connector config
    ├── manifest.json       # Endpoint manifest with version (auto-bumped on merge)
    └── endpoints/          # Individual endpoint JSON definitions
        └── {name}.json
```

## Feature requests and bug reports

If you have an idea for a new connector, want to request an endpoint, or found a bug, please [open a GitHub issue](https://github.com/analitiq-dip-registry/connector-template/issues) on the relevant connector repo. Use the issue to describe what you need and any context that would help.

## Questions?

If you're unsure about anything, open an issue on the connector repo or on the [connector builder plugin](https://github.com/analitiq-dip-registry/analitiq-plugin-connector-builder) repo.