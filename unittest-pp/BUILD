subinclude("///cc//build_defs:cc")

github_repo(
    name = "unittest_cpp",
    repo = "unittest-cpp/unittest-cpp",
    hashes = ["3ba4f8b6c6e75ca8c79dd6008c78e95fb08554fbf2e0f1195fb78a4bf5a8a805"],
    build_file = "unittest.build",
    revision = "v2.0.0",
    strip_prefix = "unittest-cpp-2.0.0",
)


filegroup(
    name = "srcs",
    srcs = ["unittest_main.cc", "///unittest-pp/unittest_cpp//:unittest_cpp_srcs"],
)

filegroup(
    name = "hdrs",
    srcs = ["///unittest-pp/unittest_cpp//:unittest_cpp_hdrs"],
)

cc_library(
    name = "main",
    srcs = [":srcs"],
    hdrs = [":hdrs"],
    visibility = ["PUBLIC"],
    includes = ["."],
)
