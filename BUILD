load(
    "@com_googlesource_gerrit_bazlets//:gerrit_plugin.bzl",
    "gerrit_plugin",
    "gerrit_plugin_tests",
)
load("@rules_java//java:defs.bzl", "java_library")
load("@rules_jvm_external//:defs.bzl", "artifact")

EXT_REPO = "owners-common-api_plugin_deps"

EXT_DEPS = [
    "com.fasterxml.jackson.core:jackson-databind",
    "com.fasterxml.jackson.dataformat:jackson-dataformat-yaml",
]

PLUGIN = "owners-common-api"

gerrit_plugin(
    name = PLUGIN,
    srcs = glob([
        "src/main/java/**/*.java",
    ]),
    manifest_entries = [
        "Implementation-Title: Gerrit owners-common-api plugin",
        "Implementation-URL: https://gerrit.googlesource.com/plugins/owners",
        "Gerrit-PluginName: owners-common-api",
        "Gerrit-Module: com.googlesource.gerrit.owners.api.OwnersApiModule",
    ],
    deps = [
        artifact(
            c,
            repository_name = EXT_REPO,
        )
        for c in EXT_DEPS
    ],
)

gerrit_plugin_tests(
    name = "owners-common-api_test",
    srcs = glob(["src/test/java/**/*.java"]),
    plugin = PLUGIN,
    deps = [
        artifact(
            "org.easymock:easymock",
            repository_name = EXT_REPO,
        ),
    ],
)
