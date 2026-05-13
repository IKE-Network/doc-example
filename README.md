# IKE Documentation Example

[![License](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)
[![Documentation](https://img.shields.io/badge/docs-ike.network%2Fdoc--example-blue)](https://ike.network/doc-example/)
[![IKE Network](https://img.shields.io/badge/IKE-Network-green)](https://ike.network/)

A standalone documentation-only project that demonstrates the IKE
AsciiDoc pipeline. Use this as a template for creating new
documentation projects.

- **Artifact**: `network.ike.examples:doc-example`
- **Packaging**: `pom` with `<classifier>adoc</classifier>` source attachment
- **Parent**: `network.ike.platform:ike-parent`

## Quick Start

```bash
# HTML only:
mvn clean verify

# HTML + Prawn PDF:
mvn clean verify -Dike.pdf.prawn

# HTML + FOP PDF:
mvn clean verify -Dike.pdf.fop
```

## Creating a New Documentation Project

### 1. Create `pom.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.1.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.1.0
         http://maven.apache.org/xsd/maven-4.1.0.xsd">
    <modelVersion>4.1.0</modelVersion>

    <parent>
        <groupId>network.ike.platform</groupId>
        <artifactId>ike-parent</artifactId>
        <version>54</version>
        <relativePath/>
    </parent>

    <groupId>com.example</groupId>
    <artifactId>my-docs</artifactId>
    <version>1.0.0-SNAPSHOT</version>
    <!-- Classifier-canonical doc shape (ike-issues#321): pom
         packaging with the asciidoc source attached as
         <classifier>adoc</classifier> by ike-parent's
         doc-pipeline profile. -->
    <packaging>pom</packaging>

    <name>My Documentation Project</name>

    <!-- Required (ike-issues#383): declare the gh-pages publish
         location explicitly. ike-parent's inherited template
         points to the in-reactor location and a build enforcer
         fails consumers that don't override. -->
    <distributionManagement>
        <site>
            <id>ike-site</id>
            <url>https://ike.network/${project.artifactId}/</url>
        </site>
    </distributionManagement>

    <dependencies>
        <dependency>
            <groupId>network.ike.tooling</groupId>
            <artifactId>ike-build-standards</artifactId>
            <classifier>claude</classifier>
            <type>zip</type>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>network.ike.docs</groupId>
            <artifactId>minimal-fonts</artifactId>
            <type>zip</type>
        </dependency>
    </dependencies>
</project>
```

### 2. Create `src/docs/asciidoc/index.adoc`

```asciidoc
= My Document Title
:author: Your Name
:revnumber: {project-version}
:revdate: {docdate}
:doctype: book
:toc: left
:toclevels: 3
:sectnums:
:icons: font
:source-highlighter: coderay

== First Chapter

Your content here.
```

### 3. Build

```bash
# HTML only:
mvn clean verify

# HTML + Prawn PDF:
mvn clean verify -Dike.pdf.prawn

# HTML + FOP PDF:
mvn clean verify -Dike.pdf.fop
```

### 4. Customize the Theme

To override the default IKE theme, create `src/theme/ike-default-theme.yml`
in your project and add this property to your `pom.xml`:

```xml
<properties>
    <asciidoc.theme.directory>${project.basedir}/src/theme</asciidoc.theme.directory>
</properties>
```

### 5. Add Diagrams

The IKE diagram standard prefers **PlantUML** for most cases
and **GraphViz** when layout precision matters. Both render
server-side via Kroki — no local tools needed. Mermaid is
intentionally not part of the recommended toolset.

```asciidoc
.Build pipeline
[plantuml]
----
@startuml
left to right direction
rectangle "Source" as A
rectangle "Build" as B
rectangle "Output" as C
A --> B --> C
@enduml
----
```

See [`IKE-DIAGRAMS.md`](https://ike.network/ike-tooling/ike-build-standards/IKE-DIAGRAMS.html)
for the diagram test (when a diagram earns its place), tool
selection (PlantUML diagram-type matrix, when to use GraphViz),
and authoring conventions.

### 6. Use Koncept Macros

Reference formally identified terminology with `k:Name[]`:

```asciidoc
The Koncept k:DiabetesMellitus[] is a metabolic disorder.
```

### 7. Required Artifacts on Nexus

For a standalone project, these artifacts must be released (or
installed to your local Maven repository):

- `network.ike.platform:ike-parent` (the parent POM)
- `network.ike.platform:ike-bom` (optional — BOM for version alignment)
- `network.ike.docs:ike-doc-maven-plugin` (`idoc:*` render and packaging goals)
- `network.ike.docs:ike-doc-resources`
- `network.ike.docs:minimal-fonts`
- `network.ike.docs:docbook-xsl`
- `network.ike.docs:koncept-asciidoc-extension`
- `network.ike.tooling:ike-build-standards`
- `network.ike.tooling:ike-maven-plugin`

## Output Locations

| Format | Path |
|--------|------|
| HTML | `target/generated-docs/html/index.html` |
| Self-contained HTML | `target/generated-docs/html-single/{artifactId}.html` |
| Prawn PDF | `target/generated-docs/pdf-prawn/{artifactId}.pdf` |
| FOP PDF | `target/generated-docs/pdf-fop/{artifactId}.pdf` |
| Prince PDF | `target/generated-docs/pdf-prince/{artifactId}.pdf` |
| AH PDF | `target/generated-docs/pdf-ah/{artifactId}.pdf` |
| WeasyPrint PDF | `target/generated-docs/pdf-weasyprint/{artifactId}.pdf` |
| XEP PDF | `target/generated-docs/pdf-xep/{artifactId}.pdf` |

## Links

- **Documentation:** [`https://ike.network/doc-example/`](https://ike.network/doc-example/)
- **Workspace:** [`IKE-Network/ike-example-ws`](https://ike.network/ike-example-ws/) — clone the workspace to build doc-example alongside example-project and the integration tests
- **Issues:** [`IKE-Network/ike-issues`](https://github.com/IKE-Network/ike-issues) (cross-project tracker)
- **Source:** [`IKE-Network/doc-example`](https://github.com/IKE-Network/doc-example)
