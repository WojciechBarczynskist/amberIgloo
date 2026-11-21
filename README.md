# amberIgloo

![CI](https://img.shields.io/github/actions/workflow/status/WojciechBarczynskist/amberIgloo/ci.yml?branch=main&label=CI) ![Go](https://img.shields.io/badge/go-1.21+-00ADD8) ![GoDoc](https://img.shields.io/badge/godoc-reference-00ADD8) ![License](https://img.shields.io/github/license/WojciechBarczynskist/amberIgloo?color=blue)

amberIgloo is a lightweight Go HTTP microservice built with the standard library and gorilla/mux. It exposes /api/health for health checks and /api/items for CRUD operations, with thread-safe in-memory storage, request logging middleware, panic recovery middleware, and graceful shutdown on SIGINT/SIGTERM. Ships with a multi-stage Dockerfile and CI pipeline.

## Table of Contents

- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Running Tests](#running-tests)
- [Contributing](#contributing)
- [Changelog](#changelog)
- [License](#license)

## Features

- /api/items endpoint with thread-safe in-memory CRUD storage (sync.RWMutex)
- Multi-stage Dockerfile: golang:1.21-alpine builder, alpine:3.19 final
- HTTP server with gorilla/mux routing and standard net/http handlers
- Request logging middleware with method, path, and duration
- Panic recovery middleware with stack trace printing

## Philosophy

amberIgloo was built with the following principles:

- **Simplicity**: Minimal dependencies, clear code, easy to understand and modify
- **Correctness**: Comprehensive tests, type safety, and proper error handling
- **Performance**: Efficient algorithms, minimal overhead, fast startup
- **Maintainability**: Clean structure, documentation, and consistent code style

The goal is to provide a solid foundation that you can build upon, not a black box you have to work around.

## Prerequisites

- Go 1.21 or higher
- Docker (optional, for containerized deployment)

## Installation

```bash
go get https://github.com/WojciechBarczynskist/amberIgloo
# or build from source
git clone https://github.com/WojciechBarczynskist/amberIgloo.git
cd amberIgloo && go build -o bin/server cmd/server/main.go
# or run with Docker
docker build -t amberIgloo . && docker run -p 8080:8080 amberIgloo
```

## Usage

```bash
# Run the server (defaults to :8080)
go run cmd/server/main.go
# => Server starting on :8080

# Build a production binary
go build -o bin/server cmd/server/main.go

# Run with a custom port
PORT=3000 ./bin/server

# Health check
curl http://localhost:8080/api/health
# => {"status":"ok","timestamp":"2024-01-15T10:30:00Z"}

# Run tests
go test ./... -v

# Build with Docker
docker build -t amberIgloo .
docker run -p 8080:8080 amberIgloo
```

## Project Structure

```
amberIgloo/
├── cmd/server/main.go
├── internal/
│   ├── handler/handler.go
│   └── middleware/middleware.go
├── go.mod  go.sum  Dockerfile  Makefile  .env.example
├── README.md  LICENSE  CHANGELOG.md  CONTRIBUTING.md  CODE_OF_CONDUCT.md
├── .github/
│   ├── workflows/ci.yml
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   └── feature_request.md
│   └── PULL_REQUEST_TEMPLATE.md
└── .gitignore
```

## Running Tests

```bash
go test ./... -v
# with coverage
go test ./... -cover -coverprofile=coverage.out
```

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

Quick start:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Make your changes and run tests (see [Running Tests](#running-tests) above)
4. Commit with a clear message: `git commit -am 'Add: my feature'`
5. Push to your fork: `git push origin feature/my-feature`
6. Open a Pull Request

Please ensure all tests pass before submitting a pull request.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for a list of changes and version history.

## License

This project is licensed under the MIT -- see the [LICENSE](LICENSE) file for details.

Copyright (c) 2026 zara silva.
