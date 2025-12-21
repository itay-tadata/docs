# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Repository overview

- This repo is a Mintlify documentation starter kit for the Tadata docs.
- The docs site is configured primarily through `docs.json` at the repo root and content markdown files (to be added) referenced by that configuration.

## Development commands

All local development is driven by the Mintlify CLI and the `docs.json` at the repo root.

- **Install Mintlify CLI (once per machine)**
  - `npm i -g mint`
- **Run local docs preview** (from the repo root, where `docs.json` lives)
  - `mint dev`
  - The site is served at `http://localhost:3000`.
- **Update Mintlify CLI** (useful if `mint dev` stops working as expected)
  - `mint update`

There are currently no repository-specific build, lint, or test commands defined in this repo beyond what the Mintlify CLI provides.

## Deployment and publishing

- Production deployment is handled by Mintlify via their GitHub app.
- When the Mintlify GitHub app is installed and connected to this repo, changes merged to the default branch are automatically deployed to the live docs.

## High-level architecture and structure

### Mintlify configuration (`docs.json`)

`docs.json` is the central configuration file for the docs site. It controls:

- **Branding and theming**
  - `theme`: Mintlify theme key (currently `"mint"`).
  - `name`: Site name (`"Tadata"`).
  - `colors`: Primary/light/dark colors for the theme.
  - `logo`: Paths to light/dark logo assets.
  - `favicon`: Path to the site favicon.
- **Global navigation and layout**
  - `navigation.tabs`: Top-level tabs in the docs UI.
    - Each tab contains `groups`, and each group lists `pages` by slug (e.g. `"getting-started/welcome"`).
    - Each page slug is expected to correspond to a markdown/MDX file in the repo with the same path structure (e.g. `getting-started/welcome.mdx` or `.md`).
  - `navigation.global.anchors`: Global links (e.g. a "Platform" link pointing to `https://app.tadata.com`).
- **Navbar configuration**
  - `navbar.links`: Secondary links (e.g. a `Support` mailto link).
  - `navbar.primary`: Primary call-to-action button (currently labeled `Platform`, linking to `https://app.tadata.com`).
- **Contextual options**
  - `contextual.options`: List of tools/services (e.g. `copy`, `view`, `chatgpt`, `claude`, `cursor`, etc.) that Mintlify exposes in code or content blocks for quick actions.
- **Footer configuration**
  - `footer.socials`: Links to external properties such as X/Twitter, GitHub, and LinkedIn.

### Content organization

- The logical structure of the docs is defined by `navigation.tabs[].groups[].pages` in `docs.json`.
- Each page entry (e.g. `"guides/using-connectors"`) is expected to map to a corresponding content file in the repository following the same folder/slug pattern.
- Groups are organized by topic areas already encoded in `docs.json`, such as:
  - `Getting Started` (introductory docs)
  - `Guides` (how-to documents)
  - `Authentication`
  - `Connectors`
  - `Optimization`
  - `Recipes` (scenario-based examples)

### How configuration and content work together

- `docs.json` defines the information architecture (what sections exist, how they are labeled, and how they appear in navigation).
- Content files (markdown/MDX) implement the actual documentation for each slug referenced in `docs.json`.
- Changing the structure of the docs (adding/removing groups, tabs, or pages) is done by editing `docs.json`; the corresponding content files must then exist at matching paths so that Mintlify can render them without 404s.

This division of responsibilities—`docs.json` for structure and site configuration, markdown/MDX files for content—should be kept in mind when modifying or extending the documentation.