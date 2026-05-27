---
date_published: 2026-05-26
date_modified: 2026-05-26
canonical_url: https://ike.network/doc-example/dependency-info.html
---

# Maven Coordinates

## [Apache Maven](#apache-maven)

```
<dependency>
  <groupId>network.ike.examples</groupId>
  <artifactId>doc-example</artifactId>
  <version>33</version>
  <type>pom</type>
</dependency>
```

## [Apache Ivy](#apache-ivy)

```
<dependency org="network.ike.examples" name="doc-example" rev="33">
  <artifact name="doc-example" type="pom" />
</dependency>
```

## [Groovy Grape](#groovy-grape)

```
@Grapes(
@Grab(group='network.ike.examples', module='doc-example', version='33')
)
```

## [Gradle/Grails](#gradle-grails)

```
implementation 'network.ike.examples:doc-example:33'
```

## [Scala SBT](#scala-sbt)

```
libraryDependencies += "network.ike.examples" % "doc-example" % "33"
```

## [Leiningen](#leiningen)

```
[network.ike.examples/doc-example "33"]
```
