load(
    "//bazel:envoy_build_system.bzl",
    "envoy_cc_test",
    "envoy_cc_test_library",
    "envoy_package",
)
load(
    "quiche.bzl",
    "envoy_quiche_platform_impl_cc_test_library",
)

licenses(["notice"])  # Apache 2

envoy_package()

envoy_cc_test(
    name = "http2_platform_test",
    srcs = ["http2_platform_test.cc"],
    external_deps = ["quiche_http2_platform"],
    deps = [
        "//source/common/quic/platform:quiche_flags_impl_lib",
        "//test/test_common:logging_lib",
        "//test/test_common:utility_lib",
        "@com_github_google_quiche//:http2_test_tools_random",
    ],
)

envoy_cc_test(
    name = "quic_platform_test",
    srcs = select({
        "//bazel:linux": ["quic_platform_test.cc"],
        "//conditions:default": [],
    }),
    copts = select({
        "//bazel:windows_x86_64": [],
        "//conditions:default": ["-Wno-unused-parameter"],
    }),
    data = ["//test/extensions/transport_sockets/tls/test_data:certs"],
    external_deps = ["quiche_quic_platform"],
    tags = ["nofips"],
    deps = [
        "//source/common/memory:stats_lib",
        "//source/common/quic/platform:quiche_flags_impl_lib",
        "//test/common/buffer:utility_lib",
        "//test/common/stats:stat_test_utility_lib",
        "//test/extensions/transport_sockets/tls:ssl_test_utils",
        "//test/mocks/api:api_mocks",
        "//test/test_common:logging_lib",
        "//test/test_common:threadsafe_singleton_injector_lib",
        "//test/test_common:utility_lib",
        "@com_github_google_quiche//:epoll_server_lib",
        "@com_github_google_quiche//:quic_core_error_codes_lib",
        "@com_github_google_quiche//:quic_core_quic_epoll_clock_lib",
        "@com_github_google_quiche//:quic_core_types_lib",
        "@com_github_google_quiche//:quic_platform_expect_bug",
        "@com_github_google_quiche//:quic_platform_mock_log",
        "@com_github_google_quiche//:quic_platform_test",
        "@com_github_google_quiche//:quic_platform_test_output",
        "@com_github_google_quiche//:quic_platform_thread",
        "@com_github_google_quiche//:quiche_common_mem_slice_storage",
        "@com_github_google_quiche//:quiche_common_platform_system_event_loop",
    ],
)

envoy_cc_test_library(
    name = "epoll_server_platform_impl_lib",
    hdrs = [
        "epoll_address_test_utils_impl.h",
        "epoll_bug_impl.h",
        "epoll_expect_bug_impl.h",
        "epoll_export_impl.h",
        "epoll_logging_impl.h",
        "epoll_ptr_util_impl.h",
        "epoll_test_impl.h",
        "epoll_thread_impl.h",
        "epoll_time_impl.h",
    ],
    external_deps = ["abseil_time"],
    deps = [
        ":quiche_expect_bug_impl_lib",
        ":quiche_thread_impl_lib",
        "//envoy/network:address_interface",
        "//source/common/quic/platform:quic_base_impl_lib",
        "//test/test_common:environment_lib",
    ],
)

envoy_quiche_platform_impl_cc_test_library(
    name = "quiche_common_platform_epoll_impl_lib",
    hdrs = ["quiche_epoll_impl.h"],
    tags = ["nofips"],
    deps = ["@com_github_google_quiche//:epoll_server_lib"],
)

envoy_quiche_platform_impl_cc_test_library(
    name = "quiche_expect_bug_impl_lib",
    hdrs = ["quiche_expect_bug_impl.h"],
    tags = ["nofips"],
    deps = [
        "@com_github_google_quiche//:quic_platform_base",
        "@com_github_google_quiche//:quic_platform_mock_log",
    ],
)

envoy_quiche_platform_impl_cc_test_library(
    name = "quiche_mock_log_impl_lib",
    hdrs = ["quiche_mock_log_impl.h"],
    tags = ["nofips"],
    deps = ["@com_github_google_quiche//:quic_platform_base"],
)

envoy_quiche_platform_impl_cc_test_library(
    name = "quiche_thread_impl_lib",
    hdrs = ["quiche_thread_impl.h"],
    tags = ["nofips"],
    deps = [
        "//envoy/thread:thread_interface",
        "//source/common/common:assert_lib",
        "//test/test_common:thread_factory_for_test_lib",
    ],
)

envoy_quiche_platform_impl_cc_test_library(
    name = "quiche_test_output_impl_lib",
    srcs = ["quiche_test_output_impl.cc"],
    hdrs = ["quiche_test_output_impl.h"],
    tags = ["nofips"],
    deps = [
        "//test/test_common:file_system_for_test_lib",
        "@com_github_google_quiche//:quic_platform_base",
        "@com_github_google_quiche//:quiche_common_platform",
    ],
)

envoy_quiche_platform_impl_cc_test_library(
    name = "quiche_test_impl_lib",
    hdrs = ["quiche_test_impl.h"],
    deps = ["//source/common/common:assert_lib"],
)

envoy_quiche_platform_impl_cc_test_library(
    name = "quiche_test_helpers_impl_lib",
    hdrs = ["quiche_test_helpers_impl.h"],
    deps = [
        ":quiche_expect_bug_impl_lib",
    ],
)
