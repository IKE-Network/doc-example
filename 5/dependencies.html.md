---
date_published: 2026-05-09
date_modified: 2026-05-09
canonical_url: https://github.com/IKE-Network/doc-example/dependencies.html
---

# Project Dependencies

## [compile](#compile)

The following is a list of compile dependencies for this project. These dependencies are required to compile and run the application:

| GroupId | ArtifactId | Version | Type | Licenses |
| --- | --- | --- | --- | --- |
| network.ike.docs | [minimal-fonts](https://github.com/IKE-Network/ike-minimal-fonts)[1] | 9 | zip | [SIL Open Font License 1.1](https://scripts.sil.org/OFL)[2] |

## [provided](#provided)

The following is a list of provided dependencies for this project. These dependencies are required to compile the application, but should be provided by default when using the library:

| GroupId | ArtifactId | Version | Classifier | Type | Licenses |
| --- | --- | --- | --- | --- | --- |
| network.ike.docs | [docbook-xsl](https://github.com/IKE-Network/ike-docbook-xsl)[3] | 9 | - | jar | [MIT License (DocBook XSL Stylesheets)](https://github.com/docbook/xslt10-stylesheets/blob/master/xsl/COPYING)[4][Apache License 2.0 (IKE Customization Layer)](https://www.apache.org/licenses/LICENSE-2.0)[5] |
| network.ike.docs | [ike-doc-resources](https://github.com/IKE-Network/ike-docs)[6] | 9 | - | jar | [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt)[7] |
| network.ike.tooling | [ike-build-standards](https://ike.network/ike-tooling/ike-build-standards/)[8] | 148 | asciidoctorconfig | zip | [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt)[7] |
| network.ike.tooling | [ike-build-standards](https://ike.network/ike-tooling/ike-build-standards/)[8] | 148 | built-with | zip | [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt)[7] |
| network.ike.tooling | [ike-build-standards](https://ike.network/ike-tooling/ike-build-standards/)[8] | 148 | claude | zip | [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt)[7] |
| network.ike.tooling | [ike-build-standards](https://ike.network/ike-tooling/ike-build-standards/)[8] | 148 | config | zip | [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt)[7] |
| network.ike.tooling | [ike-build-standards](https://ike.network/ike-tooling/ike-build-standards/)[8] | 148 | site-theme | zip | [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt)[7] |

# Project Transitive Dependencies

No transitive dependencies are required for this project.

# Project Dependency Graph

## [Dependency Tree](#dependency-tree)

- network.ike.examples:doc-example:pom:5 ** 
  
  | IKE Documentation Example |
  | --- |
  | **Description: **Documentation-only project demonstrating the IKE AsciiDoc pipeline. Exercises all diagram types, Koncept macros, typography, and layout features across all 6 PDF renderers. **URL: **[https://github.com/IKE-Network/doc-example](https://github.com/IKE-Network/doc-example)[9] **Project Licenses: **[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt)[7] |
  
    - network.ike.tooling:ike-build-standards:zip:claude:148 (provided) ** 
      
      | IKE Build Standards |
      | --- |
      | **Description: **Versioned Claude instruction files for IKE projects. Modular standards (Maven, Java, IKE-specific) distributed as a classified Maven artifact. **URL: **[https://ike.network/ike-tooling/ike-build-standards/](https://ike.network/ike-tooling/ike-build-standards/)[8] **Project Licenses: **[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt)[7] |
    - network.ike.tooling:ike-build-standards:zip:config:148 (provided) ** 
      
      | IKE Build Standards |
      | --- |
      | **Description: **Versioned Claude instruction files for IKE projects. Modular standards (Maven, Java, IKE-specific) distributed as a classified Maven artifact. **URL: **[https://ike.network/ike-tooling/ike-build-standards/](https://ike.network/ike-tooling/ike-build-standards/)[8] **Project Licenses: **[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt)[7] |
    - network.ike.docs:ike-doc-resources:jar:9 (provided) ** 
      
      | IKE Documentation Resources |
      | --- |
      | **Description: **Shared build resources for the IKE documentation pipeline: assembly descriptors, PDF themes, renderer configurations, SVGO configs, and AsciiDoc shared docinfo. **URL: **[https://github.com/IKE-Network/ike-docs](https://github.com/IKE-Network/ike-docs)[6] **Project Licenses: **[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt)[7] |
    - network.ike.docs:docbook-xsl:jar:9 (provided) ** 
      
      | IKE DocBook XSL Stylesheets |
      | --- |
      | **Description: **DocBook XSL 1.79.2 stylesheets with IKE FO customization layer. Ready-to-use artifact for the AsciiDoc → DocBook5 → XSL-FO → PDF pipeline. **URL: **[https://github.com/IKE-Network/ike-docbook-xsl](https://github.com/IKE-Network/ike-docbook-xsl)[3] **Project Licenses: **[MIT License (DocBook XSL Stylesheets)](https://github.com/docbook/xslt10-stylesheets/blob/master/xsl/COPYING)[4], [Apache License 2.0 (IKE Customization Layer)](https://www.apache.org/licenses/LICENSE-2.0)[5] |
    - network.ike.docs:minimal-fonts:zip:9 (compile) ** 
      
      | IKE Minimal Fonts |
      | --- |
      | **Description: **Minimal Noto font subset for IKE documentation (~4MB) **URL: **[https://github.com/IKE-Network/ike-minimal-fonts](https://github.com/IKE-Network/ike-minimal-fonts)[1] **Project Licenses: **[SIL Open Font License 1.1](https://scripts.sil.org/OFL)[2] |
    - network.ike.tooling:ike-build-standards:zip:site-theme:148 (provided) ** 
      
      | IKE Build Standards |
      | --- |
      | **Description: **Versioned Claude instruction files for IKE projects. Modular standards (Maven, Java, IKE-specific) distributed as a classified Maven artifact. **URL: **[https://ike.network/ike-tooling/ike-build-standards/](https://ike.network/ike-tooling/ike-build-standards/)[8] **Project Licenses: **[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt)[7] |
    - network.ike.tooling:ike-build-standards:zip:built-with:148 (provided) ** 
      
      | IKE Build Standards |
      | --- |
      | **Description: **Versioned Claude instruction files for IKE projects. Modular standards (Maven, Java, IKE-specific) distributed as a classified Maven artifact. **URL: **[https://ike.network/ike-tooling/ike-build-standards/](https://ike.network/ike-tooling/ike-build-standards/)[8] **Project Licenses: **[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt)[7] |
    - network.ike.tooling:ike-build-standards:zip:asciidoctorconfig:148 (provided) ** 
      
      | IKE Build Standards |
      | --- |
      | **Description: **Versioned Claude instruction files for IKE projects. Modular standards (Maven, Java, IKE-specific) distributed as a classified Maven artifact. **URL: **[https://ike.network/ike-tooling/ike-build-standards/](https://ike.network/ike-tooling/ike-build-standards/)[8] **Project Licenses: **[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0.txt)[7] |

# Licenses

**SIL Open Font License 1.1: **IKE Minimal Fonts

**Apache License, Version 2.0: **IKE Build Standards, IKE Documentation Example, IKE Documentation Resources

**MIT License (DocBook XSL Stylesheets): **IKE DocBook XSL Stylesheets

**Apache License 2.0 (IKE Customization Layer): **IKE DocBook XSL Stylesheets

# Dependency File Details

| Total | Size | Entries | Classes | Packages | Java Version | Debug Information |
| --- | --- | --- | --- | --- | --- | --- |
| docbook-xsl-9.jar | 25.8 MB | 1955 | 0 | 0 | - | - |
| ike-doc-resources-9.jar | 21.8 kB | 31 | 0 | 0 | - | - |
| minimal-fonts-9.zip | 3.1 MB | - | - | - | - | - |
| ike-build-standards-148-asciidoctorconfig.zip | 0.2 kB | - | - | - | - | - |
| ike-build-standards-148-built-with.zip | 3.5 kB | - | - | - | - | - |
| ike-build-standards-148-claude.zip | 81 kB | - | - | - | - | - |
| ike-build-standards-148-config.zip | 1.2 kB | - | - | - | - | - |
| ike-build-standards-148-site-theme.zip | 3.4 kB | - | - | - | - | - |
| 8 | 29 MB | 1986 | - | - | - | - |
| compile: 1 | compile: 3.1 MB | - | - | - | - | - |
| provided: 7 | provided: 25.9 MB | provided: 1986 | - | - | - |
