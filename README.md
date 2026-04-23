# IKE Documentation Example

A standalone documentation-only project that demonstrates the IKE
AsciiDoc pipeline. Use this as a template for creating new
documentation projects.

- **Artifact**: `network.ike.examples:doc-example:1-SNAPSHOT`
- **Packaging**: `ike-doc` (external consumer)
- **Parent**: `network.ike.platform:ike-parent:1`

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
         http://maven.apache.org/xsd/maven-4.1.0.xsd"
         root="true">
    <modelVersion>4.1.0</modelVersion>

    <parent>
        <groupId>network.ike.platform</groupId>
        <artifactId>ike-parent</artifactId>
        <version>1</version>
    </parent>

    <groupId>com.example</groupId>
    <artifactId>my-docs</artifactId>
    <version>1.0.0-SNAPSHOT</version>
    <packaging>ike-doc</packaging>

    <name>My Documentation Project</name>

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

The pipeline supports Mermaid, PlantUML, and GraphViz via Kroki
server-side rendering. No local tools needed.

```asciidoc
[mermaid]
....
graph LR
    A[Source] --> B[Build] --> C[Output]
....
```

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
- `network.ike.docs:ike-doc-maven-plugin` (provides `ike-doc` packaging)
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
