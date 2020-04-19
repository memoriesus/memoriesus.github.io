---
post: page
title: build iOS project using Bazel faster
tags: [Bazel,iOS]
comment: true 
---
# Bazel build system 
First of all, Bazel doesn't replace the **compiler**, it's a build system.
To use it , you must install Xcode because Bazel will need all the developer tools such as compilers, linkers, system frameworks embedded in Xcode toolchains.
The build system allows you to automate tasks, compile and execute tests in a deterministic environment.


# Workspace 
Once again, we will add in dependencies to our WORKSPACE file to retrieve the rules required for building an iOS project.

Open the WORKSPACE file and add the following.

`load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")
skylib_version = "0.8.0"
http_archive(
    name = "bazel_skylib",
    url = "https://github.com/bazelbuild/bazel-skylib/releases/download/{}/bazel-skylib.{}.tar.gz".format(skylib_version, skylib_version),
)
git_repository(
    name ="build_bazel_rules_apple",
    commit="1445924a158a89ad634f562c84a600a3435ef8c2",
    “remote="https://github.com/bazelbuild/rules_apple.git",
    )
    load(
    "@build_bazel_rules_apple//apple:repositories.bzl",
    "apple_rules_dependencies",
)
apple_rules_dependencies()
load(
    "@build_bazel_rules_swift//swift:repositories.bzl",
    "swift_rules_dependencies",
)
swift_rules_dependencies()
load(
    "@build_bazel_apple_support//lib:repositories.bzl",
    "apple_support_dependencies",
)
apple_support_dependencies()
<existing content omitted for brevity>
`

# How to apply it into iOS project
Within the project directory , create a BUILD file and add the following to it 
`load("@build_bazel_rules_apple//apple:ios.bzl", "ios_application")
load("@build_bazel_rules_swift//swift:swift.bzl", "swift_library")
swift_library(
    name = "Lib",
    srcs = [
        "AppDelegate.swift",
        "MainViewController.swift",
    ],
)
os_application(
    name = "exampleiOS",
    bundle_id = "top.marcsteven.exampleiOS",
    families = ["iphone"],
    infoplists = [":Info.plist"],
    minimum_os_version = "11.0",
    deps = [":Lib"],
)  `
Save the BUILD file and then do the command order as below:
`bazel build:exampleiOS`

