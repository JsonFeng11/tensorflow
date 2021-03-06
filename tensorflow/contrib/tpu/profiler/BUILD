licenses(["notice"])  # Apache 2.0

load("//tensorflow/core:platform/default/build_config.bzl", "tf_proto_library")
load("//tensorflow/core:platform/default/build_config.bzl", "tf_proto_library_cc")
load("//tensorflow/core:platform/default/build_config.bzl", "tf_additional_all_protos")

tf_proto_library_cc(
    name = "tpu_profiler_proto",
    srcs = ["tpu_profiler.proto"],
    has_services = 1,
    cc_api_version = 2,
    cc_grpc_version = 1,
    protodeps = [":op_profile_proto"] + tf_additional_all_protos(),
    visibility = ["//visibility:public"],
)

cc_binary(
    name = "capture_tpu_profile",
    srcs = ["capture_tpu_profile.cc"],
    visibility = ["//tensorflow/contrib/tpu/profiler:__subpackages__"],
    deps = [
        ":op_profile_proto_cc",
        ":tpu_profiler_proto_cc",
        ":trace_events_proto_cc",
        ":trace_events_to_json",
        "//tensorflow/core:framework",
        "//tensorflow/core:framework_internal",
        "//tensorflow/core:lib",
        "//tensorflow/core:protos_all_cc",
        "//tensorflow/core/distributed_runtime/rpc:grpc_util",
        "@grpc//:grpc++_unsecure",
    ],
)

tf_proto_library(
    name = "trace_events_proto",
    srcs = ["trace_events.proto"],
    cc_api_version = 2,
    visibility = ["//visibility:public"],
)

cc_library(
    name = "trace_events_to_json",
    srcs = ["trace_events_to_json.cc"],
    hdrs = ["trace_events_to_json.h"],
    deps = [
        ":trace_events_proto_cc",
        "//tensorflow/core:lib",
        "@jsoncpp_git//:jsoncpp",
    ],
)

cc_test(
    name = "trace_events_to_json_test",
    srcs = ["trace_events_to_json_test.cc"],
    deps = [
        ":trace_events_to_json",
        "//tensorflow/core:lib",
        "//tensorflow/core:test",
        "//tensorflow/core:test_main",
        "@jsoncpp_git//:jsoncpp",
    ],
)

tf_proto_library_cc(
    name = "op_profile_proto",
    srcs = ["op_profile.proto"],
    cc_api_version = 2,
    visibility = ["//visibility:public"],
)
