# Copyright 2017-present The Material Components for iOS Authors. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
# implied.
# See the License for the specific language governing permissions and
# limitations under the License.

load(
    "//:material_components_ios.bzl",
    "mdc_examples_objc_library",
    "mdc_extension_objc_library",
    "mdc_objc_library",
    "mdc_public_objc_library",
    "mdc_snapshot_objc_library",
    "mdc_snapshot_test",
    "mdc_unit_test_suite",
)
load("@build_bazel_rules_swift//swift:swift.bzl", "swift_library")

licenses(["notice"])  # Apache 2.0

mdc_public_objc_library(
    name = "Snackbar",
    bundles = [":Bundle"],
    sdk_frameworks = [
        "CoreGraphics",
        "QuartzCore",
        "UIKit",
    ],
    deps = [
        "//components/AnimationTiming",
        "//components/Buttons",
        "//components/OverlayWindow",
        "//components/Typography",
        "//components/private/Application",
        "//components/private/KeyboardWatcher",
        "//components/private/Overlay",
        "@material_internationalization_ios//:MDFInternationalization",
    ],
)

filegroup(
    name = "BundleFiles",
    srcs = glob([
        "src/MaterialSnackbar.bundle/**",
    ]),
)

objc_bundle(
    name = "Bundle",
    bundle_imports = [":BundleFiles"],
)

mdc_extension_objc_library(
    name = "ColorThemer",
    deps = [
        ":Snackbar",
        "//components/schemes/Color",
    ],
)

mdc_extension_objc_library(
    name = "FontThemer",
    deps = [
        ":Snackbar",
        "//components/Themes",
    ],
)

mdc_extension_objc_library(
    name = "TypographyThemer",
    deps = [
        ":Snackbar",
        "//components/schemes/Typography",
    ],
)

mdc_examples_objc_library(
    name = "ObjcExamples",
    deps = [
        ":ColorThemer",
        ":Snackbar",
        ":TypographyThemer",
        "//components/Buttons",
        "//components/Collections",
        "//components/Palettes",
        "//components/Typography",
        "//components/private/Overlay",
        "//components/schemes/Color",
        "//components/schemes/Typography",
    ],
)

mdc_objc_library(
    name = "private",
    hdrs = native.glob(["src/private/*.h"]),
    includes = ["src/private"],
    visibility = ["//visibility:private"],
)

swift_library(
    name = "unit_test_swift_sources",
    srcs = glob(["tests/unit/*.swift"]),
    copts = [
        "-swift-version",
        "4.2",
    ],
    visibility = ["//visibility:private"],
    deps = [
        ":ColorThemer",
        ":Snackbar",
        ":TypographyThemer",
        ":private",
    ],
)

mdc_objc_library(
    name = "unit_test_sources",
    testonly = 1,
    srcs = native.glob([
        "tests/unit/*.m",
        "tests/unit/*.h",
        "tests/unit/supplemental/*.m",
        "tests/unit/supplemental/*.h",
    ]),
    sdk_frameworks = [
        "UIKit",
        "XCTest",
    ],
    visibility = ["//visibility:private"],
    deps = [
        ":ColorThemer",
        ":FontThemer",
        ":Snackbar",
        ":private",
    ],
)

mdc_unit_test_suite(
    name = "unit_tests",
    deps = [
        ":unit_test_sources",
        ":unit_test_swift_sources",
    ],
)

mdc_snapshot_objc_library(
    name = "snapshot_test_lib",
    deps = [
        ":Snackbar",
        ":private",
    ],
)

mdc_snapshot_test(
    name = "snapshot_tests",
    deps = [
        ":snapshot_test_lib",
    ],
)
