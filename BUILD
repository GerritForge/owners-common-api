load("//tools/bzl:junit.bzl", "junit_tests")
load("//tools/bzl:plugin.bzl", "PLUGIN_DEPS", "PLUGIN_DEPS_NEVERLINK", "PLUGIN_TEST_DEPS", "gerrit_plugin")

gerrit_plugin(
    name = "owners-common-api",
    srcs = glob([
        "src/main/java/**/*.java",
    ]),
    manifest_entries = [
        "Implementation-Title: Gerrit OWNERS api plugin",
        "Implementation-URL: https://gerrit.googlesource.com/plugins/owners",
        "Gerrit-PluginName: owners-api",
        "Gerrit-Module: com.googlesource.gerrit.owners.api.OwnersApiModule",
    ],
    resources = glob(["src/main/**/*"]),
    deps = [
        "@jackson-annotations//jar",
        "@jackson-core//jar",
        "@jackson-databind//jar",
        "@jackson-dataformat-yaml//jar",
        "@snakeyaml//jar",
    ],
)

junit_tests(
    name = "owners-common-api_tests",
    srcs = glob([
        "src/test/java/**/*.java",
    ]),
    jvm_flags = [
        "--add-opens=java.base/java.lang=ALL-UNNAMED",
        "--add-opens=java.base/java.util=ALL-UNNAMED",
        "--add-opens=java.base/java.util.stream=ALL-UNNAMED",
    ],
    visibility = ["//visibility:public"],
    deps = PLUGIN_DEPS + PLUGIN_TEST_DEPS + [
        ":owners-common-api__plugin",
        "@easymock//jar",
        "@javassist//jar",
        "@powermock-api-easymock//jar",
        "@powermock-api-support//jar",
        "@powermock-core//jar",
        "@powermock-module-junit4-common//jar",
        "@powermock-module-junit4//jar",
        "@powermock-reflect//jar",
    ],
)
