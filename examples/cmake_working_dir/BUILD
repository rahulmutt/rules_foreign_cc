load("@rules_cc//cc:defs.bzl", "cc_test")
load("@rules_foreign_cc//tools/build_defs:cmake.bzl", "cmake_external")

filegroup(
    name = "sources",
    srcs = glob(["source_root/**"]),
)

cmake_external(
    name = "liba",
    lib_source = ":sources",
    # This demonstrates the usage of the working directory:
    # the directory where the "main" CMakeLists.txt file resides.
    working_directory = "cmake_dir",
)

cc_test(
    name = "test_lib",
    srcs = [
        "test_liba.cpp",
    ],
    deps = [
        ":liba",
    ],
)
