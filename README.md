# circuit-breaker

[![Build Status](https://img.shields.io/github/actions/workflow/status/user/circuit-breaker/ci.yml?branch=main)]()
[![Go Version](https://img.shields.io/badge/go-1.22+-blue.svg)]()
[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

Circuit breaker implementation with half-open state and bulkhead isolation — designed for production workloads with a focus on reliability and developer ergonomics.

## Features

- **Minimal Allocations** — Designed to minimize GC pressure in hot paths
- **Zero Dependencies** — No external packages required for core functionality
- **Graceful Shutdown** — Clean shutdown handling with configurable drain timeout
- **High Performance** — Optimized for low-latency, high-throughput workloads
- **Context Support** — Full context.Context propagation for cancellation and deadlines

## Installation

```bash
go get github.com/user/circuit-breaker@latest
```

## Usage

```go
package main

import (
	"fmt"
	"github.com/user/circuit-breaker"
)

func main() {
	client := circuitbreaker.New(
		circuitbreaker.WithTimeout(30 * time.Second),
	)

	result, err := client.Run(context.Background())
	if err != nil {
		log.Fatal(err)
	}

	fmt.Println(result)
}
```

## Configuration

Configuration can be provided via environment variables, a config file, or programmatically.

| Variable | Description | Default |
|----------|-------------|--------|
| `CIRCUIT_BREAKER_TIMEOUT` | Request timeout in seconds | `30` |
| `CIRCUIT_BREAKER_RETRIES` | Number of retry attempts | `3` |
| `CIRCUIT_BREAKER_LOG_LEVEL` | Log verbosity (debug, info, warn, error) | `info` |

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
