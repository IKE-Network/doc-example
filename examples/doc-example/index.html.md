---
date_published: 2026-05-08
date_modified: 2026-05-08
canonical_url: https://github.com/IKE-Network/doc-example/index.html
---

# doc-example

A standalone reference project demonstrating an IKE consumer whose **primary deliverable is a published document** rather than a JAR. Inherits `ike-parent` from `ike-platform`, uses the `ike-doc` custom packaging contributed by `ike-doc-maven-plugin` from `ike-docs`, and exercises the full multi-renderer pipeline (HTML, Prawn PDF, FOP PDF).

| Coordinate | Value |
| --- | --- |
| Group ID | `network.ike.examples` |
| Artifact | `doc-example` |
| Packaging | `ike-doc` |
| Parent | `network.ike.platform:ike-parent` |

## [#role-in-the-ike-ecosystem](#role-in-the-ike-ecosystem)Role in the IKE Ecosystem

This project is the canonical template for an **IKE deliverable that is itself a published document**. The companion project [example-project](https://ike.network/example-project/)[1] is the template for a **JAR + docs** deliverable. Together they cover the two common shapes of IKE consumer:

| Template | When to copy from it |
| --- | --- |
| `doc-example` | You’re shipping a published document as the primary deliverable — a guide, specification, manual, or reference. No Java compile path. Uses `<packaging>ike-doc</packaging>`. |
| [example-project](https://ike.network/example-project/)[1] | You’re shipping a JAR (a library, a CLI, a service) AND want rendered docs alongside it. |

For the workspace-aggregator template, see [ike-example-ws](https://ike.network/ike-example-ws/)[2].

## [#why-ike-doc-packaging](#why-ike-doc-packaging)Why `ike-doc` Packaging

The `ike-doc` lifecycle (provided by `ike-doc-maven-plugin` via `<extensions>true</extensions>` in `ike-parent`) is purpose-built for documentation modules:

- No compile, test, or jar phases — skips all Java-related lifecycle bindings.
- Primary artifact is a **ZIP** of the AsciiDoc sources.
- Rendering is handled by the inherited `doc-pipeline` profile from `ike-parent`, file-activated by the presence of `src/docs/asciidoc/`.
- Classified ZIPs (`html`, `pdf`, `asciidoc`) are attached by `maven-assembly-plugin` and deployed to Nexus as separate artifacts so consumers can pick the format they want.

Do not use `<packaging>jar</packaging>` for a doc-only module — it produces an empty JAR. Do not use `<packaging>pom</packaging>` — it disables renderers via the `pom-skip-renderers` profile.

## [#release-cascade-position](#release-cascade-position)Release Cascade Position

```
ike-tooling -> ike-docs -> ike-platform -> [doc-example, example-project] -> ike-example-ws
```

`doc-example` releases after `ike-platform` (whose `ike-parent` this project inherits) and after `ike-docs` (whose `ike-doc-maven-plugin` provides the AsciiDoc render pipeline declared at `5` in `ike-parent’s `<pluginManagement>`). Source-payload artifacts attach as `<classifier>adoc</classifier>` post-`IKE-Network/ike-issues#321`.

## [#renderer-pipelines](#renderer-pipelines)Renderer Pipelines

`doc-example` exercises the full set of PDF renderers IKE supports. All start from the same AsciiDoc source under `src/docs/asciidoc/`.

| Renderer | Path | Activation |
| --- | --- | --- |
| HTML | `target/generated-docs/html/` | Default; always built. |
| Prawn PDF | `target/generated-docs/pdf-prawn/doc-example.pdf` | `-Dike.pdf.prawn`. Ruby-based, fast, sensible defaults. |
| FOP PDF | `target/generated-docs/pdf-fop/doc-example.pdf` | `-Dike.pdf.fop`. Java-based, XSL-FO via DocBook intermediate. |

For a deeper tour of each pipeline, see the renderer documentation on [the IKE Docs site](https://ike.network/ike-docs/)[3].

## [#project-structure](#project-structure)Project Structure

```
doc-example/
├── pom.xml                              (1)
├── src/
│   ├── docs/asciidoc/                   (2)
│   │   ├── index.adoc                   (3)
│   │   └── chapters/
│   └── site/                            (4)
│       ├── asciidoc/index.adoc
│       ├── resources/css/site.css
│       └── site.xml
└── target/
    ├── doc-example-1-SNAPSHOT.zip       (5)
    └── generated-docs/
        ├── html/                        (6)
        ├── pdf-prawn/
        └── pdf-fop/
```

Inherits `ike-parent`. Declares `<packaging>ike-doc</packaging>`. The IKE doc pipeline source. File-activated profile in `ike-parent` triggers AsciiDoc rendering. Master document. Includes are conventionally under `chapters/`. The Maven Site Plugin source — what generates this site you’re reading. Distinct from `src/docs/asciidoc/` (the deliverable). Primary artifact: ZIP of the AsciiDoc sources, deployed to Nexus. Rendered outputs as classified ZIPs.  

## [#build-commands](#build-commands)Build Commands

```
# HTML only (default):
mvn clean verify

# With Prawn PDF:
mvn clean verify -Dike.pdf.prawn

# With FOP PDF:
mvn clean verify -Dike.pdf.fop

# All renderers:
mvn clean verify -Dike.pdf.prawn -Dike.pdf.fop

# Generate this site (Maven Site Plugin):
mvn site
```

## [#inheritance-pattern](#inheritance-pattern)Inheritance Pattern

```
<parent>
    <groupId>network.ike.platform</groupId>
    <artifactId>ike-parent</artifactId>
    <version>6</version>
</parent>

<groupId>network.ike.examples</groupId>
<artifactId>doc-example</artifactId>
<version>1-SNAPSHOT</version>
<packaging>ike-doc</packaging>
```

After inheriting, the project gets — for free — GPG signing via Bouncy Castle, the AsciiDoc documentation pipeline, dependency-version management for the IKE ecosystem, and the `extensions=true` declarations needed to activate `ike-doc` packaging.

## [#what-to-copy-when-starting-a-new-project](#what-to-copy-when-starting-a-new-project)What to Copy When Starting a New Project

When creating a new IKE document project, copy the following:

| File / Directory | Purpose |
| --- | --- |
| `pom.xml` | Parent declaration, `<packaging>ike-doc</packaging>`, group/artifact coordinates. Adjust group ID and artifact name only. |
| `src/docs/asciidoc/` | Documentation source. Edit `index.adoc` and add `chapters/` includes as needed. This is the deliverable. |
| `src/site/` | Maven Site Plugin source. Update `site.xml` (project name, repo URL) and `asciidoc/index.adoc` for your project. Keep the Forest-theme `site.css` and `ike-logo.svg` for visual consistency with the rest of the IKE ecosystem. |

## [#resources](#resources)Resources

| Resource | URL |
| --- | --- |
| Source repository | [https://github.com/IKE-Network/doc-example](https://github.com/IKE-Network/doc-example)[4] |
| Cross-project issue tracker | [https://github.com/IKE-Network/ike-issues](https://github.com/IKE-Network/ike-issues)[5] |
| IKE Network landing page | [https://ike.network/](https://ike.network/)[6] |
| IKE Docs (renderer pipelines, ike-doc-maven-plugin) | [https://ike.network/ike-docs/](https://ike.network/ike-docs/)[3] |
| IKE Platform (parent POM, BOM, workspace plugin) | [https://ike.network/ike-platform/](https://ike.network/ike-platform/)[7] |
| Sibling: code+docs template | [https://ike.network/example-project/](https://ike.network/example-project/)[1] |
| Sibling: workspace-aggregator template | [https://ike.network/ike-example-ws/](https://ike.network/ike-example-ws/)[2] |
