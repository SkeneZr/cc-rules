# Test the way cc rules depend on one another; ideally we should be able to
# pick up all transitive dependencies correctly but compile the .o files independently.

subinclude("//build_defs:cc")

cc_library(
    name = "lib1",
    srcs = ["lib1.cc"],
    hdrs = ["lib1.h"],
)

cc_library(
    name = "lib2",
    srcs = ["lib2.cc"],
    hdrs = ["lib2.h"],
    visibility = ["//test/..."],
    deps = [
        ":lib1",
    ],
)

cc_test(
    name = "cc_deps_test",
    srcs = ["deps_test.cc"],
    deps = [
        ":lib2",
    ],
)

# TODO(peterebden): how to best do this kind of testing in a plugin?
# lib2 should express a direct dependency on lib1
# plz_e2e_test(
#     name = "cc_query_somepath_test_1",
#     cmd = "plz query somepath //test:lib2 //test:lib1",
#     expected_output = "cc_query_somepath_test_1.txt",
# )
#
# # lib2's object file should not have any dependency on lib1's though.
# plz_e2e_test(
#     name = "cc_query_somepath_test_2",
#     cmd = "plz query somepath //test:_lib2#cc //test:_lib1#cc",
#     expected_failure = True,
#     expected_output = "cc_query_somepath_test_2.txt",
# )

# These rules test that cc_library correctly accepts multiple srcs.
cc_library(
    name = "multisrc_lib",
    srcs = [
        "multisrc_1.cc",
        "multisrc_2.cc",
    ],
    hdrs = ["multisrc.h"],
)

cc_test(
    name = "cc_multisrc_test",
    srcs = ["cc_multisrc_test.cc"],
    deps = [":multisrc_lib"],
)

# This tests that cc_library works correctly with inputs that are multiple sources.
filegroup(
    name = "cc_multiple_srcs",
    srcs = [
        "multisrc_1.cc",
        "multisrc_2.cc",
    ],
)

cc_library(
    name = "multisrc_lib_2",
    srcs = [":cc_multiple_srcs"],
    hdrs = ["multisrc.h"],
)

cc_test(
    name = "cc_multisrc_test_2",
    srcs = ["cc_multisrc_test.cc"],
    deps = [":multisrc_lib_2"],
)
