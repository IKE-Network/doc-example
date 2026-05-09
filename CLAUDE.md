# doc-example

Standalone doc-only project. Inherits network.ike.platform:ike-parent directly from Nexus. Uses `<packaging>pom</packaging>` with asciidoc-source classifier (the canonical doc payload coordinate post-`IKE-Network/ike-issues#321`; classifier name will rename from `asciidoc` to `adoc` in the coordinated phase 3b release).

## Build Standards

Files in `.claude/standards/` are build artifacts unpacked from `ike-build-standards`. DO NOT edit or commit them. See the workspace root CLAUDE.md for details.

## Build

```bash
mvn clean verify -DskipTests -T4
```

## Key Facts

- GroupId: `network.ike.examples`
- Version: `1-SNAPSHOT`
- Uses `--enable-preview` (Java 25)
- BOM: imports `dev.ikm.ike:ike-bom` for dependency version management

## Prohibited Patterns

- **Never use `maven-antrun-plugin`** — use a proper Maven goal or `exec-maven-plugin`
- **Never use `build-helper-maven-plugin` for multi-execution property chaining** —
  write a proper Maven goal in `ike-maven-plugin`
- **Never embed shell commands inline in POM** — extract to a named script

See `.claude/standards/` (after `mvn validate`) for full standards.
See `CLAUDE-doc-example.md` for project-specific notes.
