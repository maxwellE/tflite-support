load("@build_bazel_rules_android//android:rules.bzl", "android_library")
load("@org_tensorflow//tensorflow/lite/java:aar_with_jni.bzl", "aar_with_jni")
load("@org_tensorflow//tensorflow/java:build_defs.bzl", "JAVACOPTS")

package(
    default_visibility = ["//tensorflow_lite_support:users"],
    licenses = ["notice"],  # Apache 2.0
)

exports_files([
    "AndroidManifest.xml",
])

filegroup(
    name = "object_detector_src",
    srcs = glob(["**/*.java"]),
)

android_library(
    name = "object_detector",
    srcs = glob(["*.java"]) + [
        "//tensorflow_lite_support/java/src/java/org/tensorflow/lite/task/vision/core:base_vision_api_src",
    ],
    javacopts = JAVACOPTS,
    manifest = "AndroidManifest.xml",
    deps = [
        "//tensorflow_lite_support/java:tensorflowlite_support_java",
        "//tensorflow_lite_support/java/src/java/org/tensorflow/lite/task/core:base_task_api",
        "//tensorflow_lite_support/java/src/native/task/vision/detector:object_detector_native",
        "@com_google_auto_value",
        "@org_checkerframework_qual",
        "@org_tensorflow//tensorflow/lite/java:tensorflowlite_java",
    ],
)

# AAR target for OSS release.
#
# bazel build -c opt --config=monolithic --config=android_arm64 --fat_apk_cpu=x86,x86_64,arm64-v8a,armeabi-v7a \
#   tensorflow_lite_support/java/src/java/org/tensorflow/lite/task/vision/detector:object-detector
aar_with_jni(
    name = "object-detector",
    android_library = ":object_detector",
)
