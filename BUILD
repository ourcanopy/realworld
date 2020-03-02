load("@bazel_gazelle//:def.bzl", "gazelle")
load("@build_bazel_rules_nodejs//:index.bzl", "nodejs_binary")

load("@npm//@ourcanopy/sapper:index.bzl", "sapper")

gazelle(
    name = "gazelle",
    prefix = "github.com/ourcanopy/realworld",
)

filegroup(
    name = "config",
    srcs = ["package.json", "rollup.config.js"],
)

filegroup(
  name = "source",
  srcs = glob(["src/**"])
)

filegroup(
    name = "static",
    srcs = glob(["static/**"])
)

_BUILD_DEPS = [
    "@npm//@ourcanopy/sapper",
    "@npm//rollup",
    "@npm//rollup-plugin-node-resolve",
    "@npm//rollup-plugin-replace",
    "@npm//rollup-plugin-commonjs",
    "@npm//rollup-plugin-svelte",
    "@npm//rollup-plugin-babel",
    "@npm//rollup-plugin-terser",
    "@npm//rollup-plugin-copy",
]

_LIVE_DEPS = [
    "@npm//body-parser",
    "@npm//compression",
    "@npm//express-session",
    "@npm//marked",
    "@npm//node-fetch",
    "@npm//polka",
    "@npm//session-file-store",
    "@npm//sirv",
]

sapper(
  name = "bundle",
  output_dir = 1,
  args = [
    "build",
    "$(RULEDIR)/bundle"
  ],
  data = [
    ":config",
    ":source",
    ":static",
  ] + _BUILD_DEPS + _LIVE_DEPS,
)

nodejs_binary(
  name = "binary",
  entry_point = ":bundle",
  data = [":bundle"] + _LIVE_DEPS,
)
