# Doc Example — Claude Standards

## Initial Setup — ALWAYS DO THIS FIRST

Run `mvn validate` before any other work. This unpacks current build
standards into `.claude/standards/`. Do not proceed without this step.

Because this repo has no sibling parent in its local reactor, Maven
resolves `network.ike.platform:ike-parent:1` and
`network.ike.docs:ike-doc-maven-plugin:1` directly from Nexus. If
those are not yet released (or not in your local repo), the build
will fail at project-load time.

After validate completes, read and follow these files in `.claude/standards/`:

- MAVEN.md — Maven 4 build standards (always read)
- IKE-MAVEN.md — IKE-specific Maven conventions (always read)
- IKE-DOC.md — Documentation project standards (always read)

Do NOT read JAVA.md or IKE-JAVA.md — this is a doc-only project with
no Java source code.

## Project Overview

Standalone documentation-only project. Inherits from
`network.ike.platform:ike-parent` and uses `ike-doc` custom packaging,
which is contributed to the lifecycle by `ike-doc-maven-plugin`
(from `ike-docs`) via `<extensions>true</extensions>` in
`ike-parent`'s `<pluginManagement>`.

- **Artifact**: `network.ike.examples:doc-example`
- **Packaging**: `ike-doc` (external consumer of the custom packaging)
- **Version**: `1-SNAPSHOT`

### Why `ike-doc` packaging here and not in ike-docs

The `ike-doc` packaging handler lives in `ike-doc-maven-plugin`
(inside `ike-docs`). It cannot be used inside `ike-docs` itself for
the same reason the plugin was split out: Maven resolves
`<extensions>true</extensions>` plugins at project-load time, before
the reactor builds its own modules, so a plugin-defining module
cannot use its own packaging.

External consumers (like this repo) have no such problem: the plugin
JAR is already in Nexus by the time Maven loads this project.

### Release Cascade Position

```
ike-tooling → ike-docs → ike-platform → [doc-example, example-project] → ike-example-ws
```

`doc-example` must release after `ike-platform`, which must release
after `ike-docs`.

## Key Build Commands

```bash
# HTML only:
mvn clean verify

# Prawn PDF:
mvn clean verify -Dike.pdf.prawn

# FOP PDF:
mvn clean verify -Dike.pdf.fop

# Multiple renderers:
mvn clean verify -Dike.pdf.prawn -Dike.pdf.fop
```

## Output Locations

- HTML: `target/generated-docs/html/index.html`
- PDF: `target/generated-docs/pdf-{renderer}/doc-example.pdf`
