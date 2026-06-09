load(
    "@com_googlesource_gerrit_bazlets//:gerrit_plugin.bzl",
    "gerrit_plugin",
    "gerrit_plugin_tests",
)
load("@rules_java//java:defs.bzl", "java_library")
load("@rules_jvm_external//:defs.bzl", "artifact")
load(
    "@com_googlesource_gerrit_bazlets//tools:runtime_jars_allowlist.bzl",
    "runtime_jars_allowlist_test",
)
load(
    "@com_googlesource_gerrit_bazlets//tools:runtime_jars_overlap.bzl",
    "runtime_jars_overlap_test",
)
load(
    "@com_googlesource_gerrit_bazlets//tools:in_gerrit_tree.bzl",
    "in_gerrit_tree_enabled",
)

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
    name = "owners-common-api_tests",
    srcs = glob(["src/test/java/**/*.java"]),
    plugin = PLUGIN,
    deps = [
        artifact(
            "org.easymock:easymock",
            repository_name = EXT_REPO,
        ),
    ],
)

runtime_jars_allowlist_test(
    name = "check_owners-common-api_third_party_runtime_jars",
    allowlist = ":owners-common-api_third_party_runtime_jars.allowlist.txt",
    hint = ":check_owners-common-api_third_party_runtime_jars_manifest",
    target = ":owners-common-api__plugin",
)

runtime_jars_overlap_test(
    name = "no_overlap_with_gerrit",
    against = "//:release.war.jars.txt",
    hint = "Exclude overlaps via maven.install(excluded_artifacts=[...]) and re-run this test.",
    target = ":owners-common-api__plugin",
    target_compatible_with = in_gerrit_tree_enabled(),
)
