# Golang Helpers for Network Testing

[![GoDoc](https://pkg.go.dev/badge/github.com/bassosimone/netstub)](https://pkg.go.dev/github.com/bassosimone/netstub) [![Build Status](https://github.com/bassosimone/netstub/actions/workflows/go.yml/badge.svg)](https://github.com/bassosimone/netstub/actions) [![codecov](https://codecov.io/gh/bassosimone/netstub/branch/main/graph/badge.svg)](https://codecov.io/gh/bassosimone/netstub)

The `netstub` Go package contains small helpers for testing networking code.

For example:

```Go
import (
	"context"
	"errors"
	"net"

	"github.com/bassosimone/netstub"
	"github.com/stretchr/testify/assert"
	"github.com/stretchr/testify/require"
)

// Create a Dialer that always fails with a mocked error.
dialer := &netstub.FuncDialer{
	DialContextFunc: func(ctx context.Context, network, address string) (net.Conn, error) {
		return nil, errors.New("mocked error")
	},
}

// Use the dialer in code under test.
conn, err := dialer.DialContext(context.Background(), "tcp", "example.com:80")

// Verify the test.
require.Error(t, err)
assert.Nil(t, conn)
```

## Installation

To add this package as a dependency to your module:

```sh
go get github.com/bassosimone/netstub
```

## Development

To run the tests:
```sh
go test -v .
```

To measure test coverage:
```sh
go test -v -cover .
```

## License

```
SPDX-License-Identifier: GPL-3.0-or-later
```

## History

Adapted from [ooni/probe-cli](https://github.com/ooni/probe-cli/tree/v3.20.1/internal/mocks).
