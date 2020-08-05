![logo](logo.png)

[![Build Status](https://travis-ci.org/mybee/zlog.svg?branch=master)](https://travis-ci.org/mybee/zlog) [![Coverage Status](https://coveralls.io/repos/github/mybee/zlog/badge.svg?branch=master)](https://coveralls.io/github/mybee/zlog?branch=master) [![GoDoc](https://godoc.org/github.com/mybee/zlog?status.svg)](https://godoc.org/github.com/mybee/zlog) [![Go Report Card](https://goreportcard.com/badge/github.com/mybee/zlog)](https://goreportcard.com/report/github.com/mybee/zlog) [![license](https://img.shields.io/github/license/mybee/zlog.svg)](https://github.com/mybee/zlog)

# zlog

Just Log Basic On [zerolog](https://github.com/rs/zerolog)

## Install

```shell
$ go get -u github.com/mybee/zlog
```

## Demo

```go
package main

import (
	"fmt"
	"os"

	"github.com/mybee/zlog"
	"github.com/pkg/errors"
)

func init() {

	zlog.NewBasic(os.Stdout, zlog.WithColor(), zlog.WithDebug())
	// zlog.NewJSONLog(os.Stdout)
}

func main() {
	zlog.ZInfo().
		Int("z", 100-1).
		Msg("just do it")

	zlog.ZDebug().
		Float64("f", 3.1415926).
		Msgf("hello %s", "zlog")

	var err error

	err = doit()
	if err != nil {
		zlog.ZError().Stack().Err(err).Msg("[doit] some error")
	}

	err = doErr()
	if err != nil {
		zlog.ZError().Err(err).Msg("[do error]")
	}

}

func doit() error {
	err := doErr()
	if err != nil {
		return errors.Wrap(err, "just error")
	}
	return nil
}

func doErr() error {
	return fmt.Errorf("some error")
}
```


