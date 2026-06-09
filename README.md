# Gerrit Owners-Common-API Plugin

This repository contains the basic infrastructure and API for building and running
two separate plugins, `owners` and `owners-autoassign`.

It provides the ability to parse the OWNERS file format and it's parsing across
branches and repositories.

## Building the plugins

This plugin is built with Bazel in Gerrit tree

Create symbolic links of the owners-common-api folderd and of the
external_plugin_deps.bzl file to the Gerrit source code /plugins directory.

Then build the owners-common-api plugin with the usual Gerrit
plugin compile command.

Example:

```
  git clone https://gerrit.googlesource.com/plugins/owners-common-api
  git clone --recurse-submodules https://gerrit.googlesource.com/gerrit
  cd gerrit/plugins
  ln -s ../../owners/owners-common-api .
  ln -sf owners-common-api/external_plugin_deps.bzl.MODULE.bazel .
  cd ..
  bazel build plugins/owners-common-api
```

The output is created in

```
  bazel-bin/plugins/owners-common-api/owners-common-api.jar
```

To execute the tests run:

```
  bazel test plugins/owners-common-api/...
```

This project can be imported into the Eclipse IDE:

Add the plugin name to the `CUSTOM_PLUGINS` (and in case when you want to run
tests from the IDE to `CUSTOM_PLUGINS_TEST_DEPS`) in Gerrit core in
`tools/bzl/plugins.bzl` file and run:

```
  ./tools/eclipse/project.py
```

