load("@rules_cc//cc:defs.bzl", "cc_binary", "cc_library")

cc_library(
    name = "base",
    srcs = glob(
        [
            "src/*.c",
            "src/hashkit/nc_hashkit.h",
            "src/event/nc_event.h",
            "src/proto/nc_proto.h",
        ],
        exclude = ["src/test_all.c, src/nc.c"],
    ) + ["config.h"],
    hdrs = glob(["src/*.h"]),
    copts = [
        "-Isrc",
        "-I.",
        "-Isrc/hashkit",
        "-Isrc/event",
        "-Isrc/proto",
        "-Icontrib/yaml-0.2.5/include",
        "-DHAVE_CONFIG_H",
        "-D_GNU_SOURCE",
    ],
    deps = [
        "//contrib/yaml-0.2.5:yaml",
    ],
)

cc_library(
    name = "hashkit",
    srcs = glob([
        "src/hashkit/*.c",
        "src/hashkit/nc_hashkit.h",
    ]) + ["config.h"],
    hdrs = glob(["src/hashkit/*.h"]),
    copts = [
        "-Isrc",
        "-I.",
        "-Isrc/hashkit",
        "-Isrc/event",
        "-Isrc/proto",
        "-DHAVE_CONFIG_H",
    ],
    deps = [
        ":base",
    ],
)

cc_library(
    name = "event",
    srcs = glob([
        "src/event/*.c",
        "src/event/nc_event.h",
    ]) + ["config.h"],
    hdrs = glob(["src/hashkit/*.h"]),
    copts = [
        "-Isrc",
        "-I.",
        "-Isrc/hashkit",
        "-Isrc/proto",
        "-DHAVE_CONFIG_H",
    ],
    deps = [
        ":base",
    ],
)

cc_library(
    name = "proto",
    srcs = glob([
        "src/proto/*.c",
        "src/proto/nc_proto.h",
    ]) + ["config.h"],
    hdrs = glob(["src/hashkit/*.h"]),
    copts = [
        "-Isrc",
        "-I.",
        "-Isrc/hashkit",
        "-Isrc/event",
        "-Isrc/proto",
        "-DHAVE_CONFIG_H",
    ],
    deps = [
        ":base",
    ],
)

cc_binary(
    name = "twemproxy",
    srcs = glob(
        [
            "config.h",
            "src/nc.c",
        ],
        exclude = ["src/test_all.c"],
    ),
    copts = [
        "-Isrc",
        "-I.",
        "-Isrc/hashkit",
        "-Isrc/event",
        "-Isrc/proto",
        "-Icontrib/yaml-0.2.5/include",
        "-DHAVE_CONFIG_H",
        "-D_GNU_SOURCE",
    ],
    linkopts = ["-lpthread"],
    deps = [
        ":base",
        ":event",
        ":hashkit",
        ":proto",
        "//contrib/yaml-0.2.5:yaml",
    ],
)

cc_binary(
    name = "test_all",
    srcs = glob(
        [
            "config.h",
            "src/test_all.c",
        ],
    ),
    copts = [
        "-Isrc",
        "-I.",
        "-Isrc/hashkit",
        "-Isrc/event",
        "-Isrc/proto",
        "-Icontrib/yaml-0.2.5/include",
        "-DHAVE_CONFIG_H",
        "-D_GNU_SOURCE",
    ],
    linkopts = ["-lpthread"],
    deps = [
        ":base",
        ":event",
        ":hashkit",
        ":proto",
        "//contrib/yaml-0.2.5:yaml",
    ],
)
