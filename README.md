# Zoup
[![Go Reference](https://pkg.go.dev/badge/github.com/vite-cloud/go-zoup.svg)](https://pkg.go.dev/github.com/vite-cloud/go-zoup)
[![Tests](https://github.com/vite-cloud/go-zoup/actions/workflows/tests.yml/badge.svg)](https://github.com/vite-cloud/go-zoup/actions/workflows/tests.yml)
[![codecov](https://codecov.io/gh/vite-cloud/go-zoup/branch/main/graph/badge.svg?token=2EBL0P4UN6)](https://codecov.io/gh/vite-cloud/go-zoup)

Zoup is like Zap but probably way slower and with a completely different architecture.

## Getting started

```go
zoup := zoup.FileWriter{os.Stdout}

zoup.Write(zoup.InfoError, "hello world", zoup.Fields{
"foo": "bar",
})
```

Prints out
```
_stack=main.go:6 _time="2022-05-27 11:06:21" level=info message="hello world" foo=bar
```

> A larger stack follows the following pattern: `file:line;file:line;file:line`

And that's it! Zoup uses writers to write the same log to multiple outputs. That means you can not customize what comes
out only where it comes out.

Under the hood, Zoup uses [logfmt](https://www.brandur.org/logfmt) to format logs.

It includes the following fields:
* `_stack`: the last 3 lines on the stack
* `_time`: the time the log was written
* `level`: the log level
* `message`: the log message

## Writers

* `FileWriter`: writes to a file
* `CompositeWriter`: writes to multiple writers
* `MemoryWriter`: writes to an array (for testing)

