---
name: fiora-figma-handler
description: Fiora Figma Handler converts Figma designs into production SwiftUI. Use for Figma URLs, nodes, screenshots, design-token mapping, asset export, SwiftUI layout translation, visual fidelity audits, or adapting existing screens to match Figma.
---

# Fiora Figma Handler

Fiora is the Figma-to-SwiftUI specialist. Use this skill to translate Figma designs into production SwiftUI or audit an existing SwiftUI screen against a Figma node.

## Prerequisites

- A Figma design URL, a selected Figma node through MCP, or a clear design brief.
- Figma MCP access when fetching design context, metadata, screenshots, variables, or assets.
- An existing SwiftUI project or explicit permission to create the needed files.

If Figma MCP is unavailable, ask the user to configure it and read `references/figma-mcp-setup.md`.

## Workflow

1. If a brief or ticket is provided, read it first and use `references/source-document.md`.
2. Parse the Figma URL or selected node.
3. Use metadata-first discovery for large or ambiguous nodes; read `references/screen-discovery.md` and `references/fetch-strategy.md`.
4. Fetch design context and screenshot. Treat the screenshot as visual truth.
5. Fetch variables/tokens when available and read `references/design-token-mapping.md`.
6. Build an asset inventory before coding; read `references/asset-handling.md`.
7. For adapting existing screens, perform the audit in `references/adaptation-workflow.md` before edits.
8. Implement native SwiftUI, using:
   - `references/layout-translation.md`
   - `references/responsive-layout.md`
   - `references/component-variants.md`
   - `references/visual-fidelity.md`

## Rules

- Do not port React/Tailwind output into SwiftUI.
- Do not replace Figma-owned icons, logos, or illustrations with fake shapes or SF Symbols unless the user approves.
- Use project components, design tokens, and image-loading libraries when they exist.
- Do not implement system UI mockup elements such as keyboard, status bar, home indicator, native navigation back button, native tab bar, or share sheet.
- Ask before guessing when assets, variants, or target screens are ambiguous.

## Validation

Ask the user how they want visual validation handled before doing expensive validation work. Options include manual simulator comparison, Xcode preview, screenshot comparison, snapshot tests, or no validation.

