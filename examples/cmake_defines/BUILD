load("@rules_foreign_cc//tools/build_defs:cmake.bzl", "cmake_external")

cmake_external(
    name = "lib_a",
    lib_source = ":lib_a_sources",
    static_libraries = select({
        "//:windows": ["lib_a.lib"],
        "//conditions:default": ["liblib_a.a"],
    }),
    deps = [":lib_b"],
)

cmake_external(
    name = "lib_b",
    defines = ["FOO"],
    lib_source = ":lib_b_sources",
    static_libraries = select({
        "//:windows": ["lib_b.lib"],
        "//conditions:default": ["liblib_b.a"],
    }),
)

filegroup(
    name = "lib_a_sources",
    srcs = ["lib_a/{}".format(s) for s in ["CMakeLists.txt", "lib_a.cpp"]],
)

filegroup(
    name = "lib_b_sources",
    srcs = ["lib_b/{}".format(s) for s in ["CMakeLists.txt", "lib_b.cpp"]],
)
