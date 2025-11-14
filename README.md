# Vinea APIs

[![Buf CI](https://github.com/vinea-dev/apis/actions/workflows/buf-ci.yaml/badge.svg)](https://github.com/vinea-dev/apis/actions/workflows/buf-ci.yaml)
[![Go SDK Generation](https://github.com/vinea-dev/apis/actions/workflows/gengo-generator.yaml/badge.svg)](https://github.com/vinea-dev/apis/actions/workflows/gengo-generator.yaml)
[![Python SDK Generation](https://github.com/vinea-dev/apis/actions/workflows/genpy-generator.yaml/badge.svg)](https://github.com/vinea-dev/apis/actions/workflows/genpy-generator.yaml)

This repository contains the Protobuf definitions for the Vinea project's APIs.

## Overview

This repository serves as the central source of truth for all API contracts within the Vinea ecosystem. It uses [Buf](https://buf.build/) to manage and lint the Protobuf definitions, ensuring consistency and quality.

The APIs are organized into different services, each with its own versioned Protobuf package.

## APIs

### Edge API (`edge.v1alpha1`)

The Edge API is designed for edge devices to connect to the Vinea platform and receive jobs.

- **Service:** `EdgeAPI`
- **RPCs:**
    - `Register`: Allows an edge agent to register with the server and receive a unique agent ID.
    - `Subscribe`: A long-polling RPC for agents to subscribe to and receive jobs from the server.

### Foobar API (`foobar.v1alpha1`)

The Foobar API is a simple example service.

- **Service:** `FoobarAPI`
- **RPCs:**
    - `Echo`: A simple RPC that echoes the request ID in the response.

## Usage

### Prerequisites

To work with this repository, you need to have the following tools installed:

- [Go](https://golang.org/)
- [Buf](https://buf.build/docs/installation)

You can install the required version of `buf` by running:

```bash
make tools
```

### Linting

To lint the Protobuf definitions, run the following command:

```bash
buf lint
```

### Code Generation

To generate code from the Protobuf definitions, you can use `buf generate`. The code generation is configured in `buf.gen.yaml`.

```bash
buf generate
```

This will generate code based on the templates defined in `buf.gen.yaml`.

## Generated SDKs

The generated SDKs for Go and Python are automatically published to their respective repositories.

### Go SDK

The Go SDK is published to [github.com/vinea-dev/gengo](https://github.com/vinea-dev/gengo).

To use the Go SDK, add it as a dependency to your `go.mod` file:

```bash
go get github.com/vinea-dev/gengo
```

You can then import the generated packages in your Go code:

```go
import (
    "github.com/vinea-dev/gengo/edge/v1alpha1"
    "github.com/vinea-dev/gengo/foobar/v1alpha1"
)
```

### Python SDK

The Python SDK is published to [github.com/vinea-dev/genpy](https://github.com/vinea-dev/genpy).

To use the Python SDK, install it using `pip`:

```bash
pip install git+https://github.com/vinea-dev/genpy.git
```

You can then import the generated modules in your Python code:

```python
from edge.v1alpha1 import edge_api_pb2
from foobar.v1alpha1 import foobar_pb2
```

## Contributing

Contributions are welcome! Please feel free to open an issue or submit a pull request.
