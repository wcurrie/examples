package(default_visibility = ["//visibility:public"])

load("@bazel_tools//tools/jdk:default_java_toolchain.bzl", "default_java_toolchain")

default_java_toolchain(
    name = "toolchain",
    bootclasspath = ["@bazel_tools//tools/jdk:platformclasspath9"],
    # override jvm_opts to avoid defaults that include -Xbootclasspath/p
    # avoids failed: Worker process returned an unparseable WorkResponse!
    jvm_opts = [
    ],
    source_version = "10",
    target_version = "10",
)

