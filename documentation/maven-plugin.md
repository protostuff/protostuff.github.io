---
layout: page
title: Protostuff maven plugin
permalink: /documentation/maven-plugin/
redirect_from: "/documentation/compiler-maven/"
---

### Overview

The Protostuff Maven Plugin generates Java or any other language sources from `.proto` files using extensible code 
generator based on [StringTemplate](http://www.stringtemplate.org/). The following examples describe the basic usage 
of the plugin.

The following default directory structure of the project is assumed:

```    
<project root>
├───pom.xml
└───src
    └───main
        └───proto
            └───foo.proto
```

Protocol buffer definitions location is configurable, but we recommend to use `src/main/proto/` directory. 
Any subdirectories under `src/main/proto/` are treated as package structure for protobuf definition imports. 

### pom.xml setup

Minimal configuration:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>io.protostuff.examples</groupId>
    <artifactId>protostuff-hello-world</artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
        <dependency>
            <groupId>io.protostuff</groupId>
            <artifactId>protostuff-core</artifactId>
            <version>1.3.5</version>
        </dependency>
    </dependencies>
    
    <build>
        <plugins>
            <plugin>
                <groupId>io.protostuff</groupId>
                <artifactId>protostuff-maven-plugin</artifactId>
                <version>1.3.5</version>
                <configuration>
                    <protoModules>
                        <protoModule>
                            <source>src/main/proto</source>
                            <outputDir>target/generated-sources/proto</outputDir>
                            <output>java_bean</output>
                        </protoModule>
                    </protoModules>
                </configuration>
                <executions>
                    <execution>
                        <id>generate-sources</id>
                        <phase>generate-sources</phase>
                        <goals>
                            <goal>compile</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

</project>
```

### Code Generation

If you configured `protostuff-maven-plugin` as described above, then sources are generated automatically each time
when you build project.

```
$ mvn clean install
```

You can explicitly invoke the plugin via:

```
$ mvn protostuff:compile
```

You can skip the compilation by specifying the property:

```
-Dprotostuff.compiler.skip=true
```
