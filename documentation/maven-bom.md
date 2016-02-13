---
layout: page
title: Maven "Bill Of Materials"
permalink: /documentation/maven-bom/
---

It is possible to accidentally mix different versions of protostuff JARs when using Maven.
For example, you may find that a third-party library pulls in a transitive dependency to
an older release. If you forget to explicitly declare a direct dependency yourself, all
sorts of unexpected issues can arise.

To overcome such problems Maven supports [the concept of a "bill of materials" (BOM) dependency]
(http://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html).
You can import the `protostuff-bom` in your `<dependencyManagement>` section to
ensure that all protostuff dependencies (both direct and **transitive**) are at the same version:

~~~xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>io.protostuff</groupId>
            <artifactId>protostuff-bom</artifactId>
            <version>1.3.5</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
~~~

An added benefit of using the BOM is that you no longer need to specify the `<version>` attribute
when depending on protostuff artifacts:

~~~xml
<dependencies>
    <dependency>
        <groupId>io.protostuff</groupId>
        <artifactId>protostuff-api</artifactId>
    </dependency>
    <dependency>
        <groupId>io.protostuff</groupId>
        <artifactId>protostuff-core</artifactId>
    </dependency>
<dependencies>
~~~

