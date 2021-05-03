# Lorri environment

You need to have lorri installed, and the lorri daemon started.  When you first change into this directory, you'll need to authorize the direnv with `direnv allow`.

This user environment gets further than the nix-shell (because the .envrc alters the LD_LIBRARY_PATH) but still bails out on the same error.

```bash
douglas:~/src/nixos-bazel-userenv-example/lorri$ bazel build proto/...

Starting local Bazel server and connecting to it...
DEBUG: /home/douglas/.cache/bazel/_bazel_douglas/651ab3c7437336fbdd156a0df96f9a5d/external/bazel_gazelle/internal/go_repository.bzl:189:18: org_golang_x_net: gazelle: finding module path for import golang.org/x/sys/windows: exit status 1: package golang.org/x/sys/windows: build constraints exclude all Go files in /home/douglas/.cache/bazel/_bazel_douglas/651ab3c7437336fbdd156a0df96f9a5d/external/bazel_gazelle_go_repository_cache/pkg/mod/golang.org/x/sys@v0.0.0-20201119102817-f84b799fce68/windows
INFO: Analyzed 3 targets (143 packages loaded, 8408 targets configured).
INFO: Found 3 targets...
ERROR: /home/douglas/src/nixos-bazel-userenv-example/lorri/proto/BUILD.bazel:17:17: Generating into bazel-out/k8-fastbuild/bin/proto/example_go_proto_/github.com/dmayle/nixos-bazel-userenv-example/lorri/proto failed (Exit 1) go-protoc-bin failed: error executing command bazel-out/k8-opt-exec-2B5CBBC6-ST-c3a8cc05bdea9a638dbef813eeba1ffe0dfa7d81daedbab406d39b734127c092/bin/external/io_bazel_rules_go/go/tools/builders/go-protoc-bin_/go-protoc-bin -protoc ... (remaining 16 argument(s) skipped)

Use --sandbox_debug to see verbose messages from the sandbox
bazel-out/k8-opt-exec-2B5CBBC6/bin/external/com_google_protobuf/protoc: error while loading shared libraries: libstdc++.so.6: cannot open shared object file: No such file or directory
2021/05/03 14:18:22 error running protoc: exit status 127
INFO: Elapsed time: 110.832s, Critical Path: 18.47s
INFO: 496 processes: 496 linux-sandbox.
FAILED: Build did NOT complete successfully
```
With detailed debugging statements:
```bash
douglas:~/src/nixos-bazel-userenv-example/lorri$ bazel --sandbox_debug build proto/...

```
