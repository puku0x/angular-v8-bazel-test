# WARNING: This file is generated and it's not meant to be edited.
# Before making any changes, please read Bazel documentation.
# https://docs.bazel.build/versions/master/be/workspace.html
# The WORKSPACE file tells Bazel that this directory is a "workspace", which is like a project root.
# The content of this file specifies all the external dependencies Bazel needs to perform a build.

####################################
# ESModule imports (and TypeScript imports) can be absolute starting with the workspace name.
# The name of the workspace should match the npm package where we publish, so that these
# imports also make sense when referencing the published package.
workspace(name = "bzl_app")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

RULES_NODEJS_VERSION = "0.18.6"
RULES_NODEJS_SHA256 = "1416d03823fed624b49a0abbd9979f7c63bbedfd37890ddecedd2fe25cccebc6"
http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "%s" % RULES_NODEJS_SHA256,
    url = "https://github.com/bazelbuild/rules_nodejs/releases/download/%s/rules_nodejs-%s.tar.gz" % (RULES_NODEJS_VERSION, RULES_NODEJS_VERSION),
)


####################################
# Load and install our dependencies downloaded above.

load("@build_bazel_rules_nodejs//:defs.bzl", "check_bazel_version", "node_repositories", "yarn_install")
# 0.18.0 is needed for .bazelignore
check_bazel_version("0.18.0")
node_repositories()
yarn_install(
    name = "npm",
    data = ["//:angular-metadata.tsconfig.json"],
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
)

load("@npm//:install_bazel_dependencies.bzl", "install_bazel_dependencies")
install_bazel_dependencies()

load("@npm_bazel_karma//:package.bzl", "rules_karma_dependencies")
rules_karma_dependencies()

load("@io_bazel_rules_webtesting//web:repositories.bzl", "web_test_repositories")
web_test_repositories()

load("@npm_bazel_karma//:browser_repositories.bzl", "browser_repositories")
browser_repositories()

load("@npm_bazel_typescript//:defs.bzl", "ts_setup_workspace")
ts_setup_workspace()

load("@npm_angular_bazel//:index.bzl", "ng_setup_workspace")
ng_setup_workspace()