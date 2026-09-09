# ascend-oci-adapter

`ascend-oci-adapter` is the standalone Ascend provider used by
[inclusionAI/sandboxd](https://github.com/inclusionAI/sandboxd). It discovers
physical Ascend devices through the pinned MindCluster `ascend-common` code and
returns OCI device, mount, and environment candidates over a small JSON CLI
protocol. sandboxd retains allocation, lease, validation, and OCI lifecycle
ownership.

## Build

The adapter requires Linux, CGO, and a C compiler. It loads the host's
`libdcmi.so` at runtime through `dlopen`.

```bash
git submodule update --init --recursive
make build
```

## CLI

```text
ascend-oci-adapter version  --output=json
ascend-oci-adapter discover --output=json
ascend-oci-adapter edits    --input=- --output=json
```

Requests are read from stdin and responses are written to stdout. Diagnostics
are written to stderr. The first release preserves sandboxd protocol schema 1
and provider version `mindcluster-ee074e93`.

## Release bundle

```bash
make release VERSION=v0.1.0
```

The bundle contains the binary and the licenses required for redistribution.
AKernel pins the release URL and SHA-256; the trusted Ascend mount allowlist
remains in sandboxd/AKernel.
