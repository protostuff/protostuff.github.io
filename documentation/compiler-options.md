---
layout: page
title: Compiler Options
permalink: /documentation/compiler-options/
---

Note that value (key:value) for some options are optional. The option `generate_field_map:false` 
does not disable the option - remove the entry instead to disable.

In maven, you would declare the key:value as:

```xml
<property>
  <name>Foo.implements_declaration</name> <!-- key -->
  <value>implements com.example.Bar</value> <!-- value -->
</property>
```

# All generators


`compile_imports` : `true|false|recursive` - after the target proto is compiled, compile the 
imported protos as well. If recursive, the imported protos of it's imported protos will be 
compiled as well (so on and so forth). 

`header_source_path` - the source path (org/example/foo.proto) will be printed (as a comment) 
in the header. By default, it only prints the name (foo.proto)

`${oldPackage} = ${newPackage}` - the matching package will be used for the compiled output.
Useful to group certain protos together for certain scenarios (E.g  moving packages to 
`${gwtpackage}.client`).

`underscore_on_vars` - if you have fields named after java keywords (`package`, `default`, 
etc), enable this option to avoid the clash (appends an underscore).
Best to avoid using keywords.  Who knows, you might be writing (in the future via reflection) 
to json output with its field names.

# java_bean

`generate_field_map` - generates a mapping between the field number and field name.
If on, you can serialize json encoded messages writing either its field name or field number.

```java
boolean numeric = false;
JsonIOUtil.writeTo(out, message, numeric);
```

`generate_pipe_schema` - generates a pipe schema for transcoding an input to a different output.

`alphanumeric` - requires the `generate_field_map` option to be on. The field names will be 
its field number prefixed by "f".  (e.g "f1")

`separate_schema` - statically declared schema (lite at runtime). Especially great for 
environments like android or j2me

`builder_pattern` - _well not really the builder pattern_. Setters will return the instance.

`generate_helper_methods` - additional helper methods for repeated fields

`primitive_numbers_if_optional` - uses primitive numbers (no auto-boxing) if the field is optional.

`${message.name}.implements_declaration = implements com.example.Foo` - matching message will 
implement the given interface.

`${message.name}.extends_declaration = extends com.example.Bar` - matching message will extend
the given class.

# gwt_overlay

`numeric` - the encoded property name of a message is referenced by its field number.
`{"firstName":"John","lastName":"Doe"}` is json-serialized as `{"1":"John","2":"Doe"}`

`alphanumeric` - the encoded property name of a message is referenced by its field number prefixed 
by "f". `{"firstName":"John","lastName":"Doe"}` is json-serialized as `{"f1":"John","f2":"Doe"}`.

`plain_overlay` - simply generate plain overlays that basically returns the property without checks.
By default, the gwt overlays generated will return the field's default values if null, as configured
on the .proto file.

`dev_mode` - additional code for overlays with enums to work on hosted mode.

`use_global_json` - the `parse` and `stringify` method would delegate to `$wnd.JSON.parse` and 
`$wnd.JSON.stringify` respectively.

`generate_helper_methods` - additional helper methods for repeated fields.

`${message.name}.implements\_declaration = implements com.example.Foo` - matching message will
implement the given interface. Note that gwt overlays can implement interfaces if gwt-2.0 +

# java_v2protoc_schema

`generate_field_map` - generates a mapping between the field number and field name.
If on, you can serialize json encoded messages writing either its field name or field number.

```java
boolean numeric = false;
JsonIOUtil.writeTo(out, message, numeric);
```

`enums_by_name` - serialize enums using their name instead of their number.

# java_bean_me

a variant of `java_bean` compiler that produces j2me-compatible messages/schemas.
