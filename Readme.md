# Intro
This is a demo to integrate nvml with bazel and hermetic cc toolchain.

# Note
1. this demo is not work, build will fail and throw errors:
```bash
# bazel build @com_github_nvidia_go_nvml//examples/devices  --config=linux-amd64
INFO: Analyzed target @@gazelle~~go_deps~com_github_nvidia_go_nvml//examples/devices:devices (88 packages loaded, 15653 targets configured).
ERROR: /data/build/bazel-local-cache/8c12620ae33a989236acb551c5cda37d/external/gazelle~~go_deps~com_github_nvidia_go_nvml/pkg/nvml/BUILD.bazel:3:11: GoCompilePkg external/gazelle~~go_deps~com_github_nvidia_go_nvml/pkg/nvml/nvml.a failed: (Exit 1): builder failed: error executing GoCompilePkg command (from target @@gazelle~~go_deps~com_github_nvidia_go_nvml//pkg/nvml:nvml) bazel-out/k8-opt-exec-ST-13d3ddad9198/bin/external/rules_go~~go_sdk~go_sdk/builder_reset/builder compilepkg -sdk external/rules_go~~go_sdk~go_sdk -installsuffix linux_amd64 -src ... (remaining 75 arguments skipped)

Use --sandbox_debug to see verbose messages from the sandbox and retain the sandbox build root for debugging
error: unsupported linker arg: --unresolved-symbols
compilepkg: error running subcommand external/hermetic_cc_toolchain~~toolchains~zig_sdk/tools/x86_64-linux-gnu.2.19/c++: exit status 1
Target @@gazelle~~go_deps~com_github_nvidia_go_nvml//examples/devices:devices failed to build
Use --verbose_failures to see the command lines of failed build steps.
```
2. local un-hermetic cc toolchain works fine.
```bash
# bazel build @com_github_nvidia_go_nvml//examples/devices
WARNING: Build options --action_env, --extra_toolchains, --features, and 2 more have changed, discarding analysis cache (this can be expensive, see https://bazel.build/advanced/performance/iteration-speed).
INFO: Analyzed target @@gazelle~~go_deps~com_github_nvidia_go_nvml//examples/devices:devices (56 packages loaded, 15671 targets configured).
INFO: Found 1 target...
Target @@gazelle~~go_deps~com_github_nvidia_go_nvml//examples/devices:devices up-to-date:
  bazel-bin/external/gazelle~~go_deps~com_github_nvidia_go_nvml/examples/devices/devices_/devices
INFO: Elapsed time: 15.690s, Critical Path: 14.35s
INFO: 6 processes: 3 internal, 3 linux-sandbox.
INFO: Build completed successfully, 6 total actions
```