load("@bazel_skylib//rules:build_test.bzl", "build_test")
load("@rules_cc//cc:defs.bzl", "cc_test")
load("@rules_foreign_cc//tools/build_defs:cmake.bzl", "cmake_external")

cmake_external(
    name = "liba",
    cmake_options = ["-GNinja"],
    # Demonstrate non-alphanumeric name
    lib_name = "liba++",
    lib_source = "//cmake_synthetic/liba:a_srcs",
    make_commands = [
        "ninja",
        "ninja install",
    ],
    postfix_script = "cp $$INSTALLDIR$$/lib/liba.a $$INSTALLDIR$$/lib/liba++.a",
)

cmake_external(
    name = "libb",
    cmake_options = ["-GNinja"],
    lib_source = "//cmake_synthetic/libb:b_srcs",
    make_commands = [
        "ninja",
        "ninja install",
    ],
    deps = [":liba"],
)

cmake_external(
    name = "lib_with_duplicate_transitive_bazel_deps",
    cache_entries = {
        "LIBA_DIR": "$$EXT_BUILD_DEPS$$",
        "LIBB_DIR": "$$EXT_BUILD_DEPS$$",
    },
    cmake_options = ["-GNinja"],
    lib_name = "libc",
    lib_source = "//cmake_synthetic/libc:c_srcs",
    make_commands = [
        "ninja",
        "ninja install",
    ],
    deps = [
        "//cmake_synthetic/liba:lib_a_bazel",
        "//cmake_synthetic/libb:lib_b_bazel",
    ],
)

build_test(
    name = "test_bazel_transitive_deps",
    targets = [":lib_with_duplicate_transitive_bazel_deps"],
)

cc_test(
    name = "test_libs",
    srcs = [
        "test_libb.cpp",
    ],
    deps = [
        # liba should come from transitive dependencies
        ":libb",
    ],
)
