load("@rules_foreign_cc//tools/build_defs:cmake.bzl", "cmake_external")

cmake_external(
    name = "hello_world",
    binaries = select({
        "//:macos": ["CMakeHelloWorld"],
        "//:windows": ["CMakeHelloWorld.exe"],
        "//conditions:default": ["CMakeHelloWorld"],
    }),
    cmake_options = ["-GNinja"],
    lib_source = "@cmake_hello_world_variant_src//:all",
    make_commands = [
        "ninja",
        "ninja install",
    ],
)

filegroup(
    name = "binary",
    srcs = [":hello_world"],
    output_group = select({
        "//:macos": "CMakeHelloWorld",
        "//:windows": "CMakeHelloWorld.exe",
        "//conditions:default": "CMakeHelloWorld",
    }),
)

sh_test(
    name = "test_hello_world",
    srcs = ["test_hello_world.sh"],
    args = ["$(location :binary)"],
    data = [":binary"],
    deps = ["@bazel_tools//tools/bash/runfiles"],
)
