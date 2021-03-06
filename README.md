# Logr [![Build Status](https://travis-ci.com/activeshadow/logr.svg?branch=master)](https://travis-ci.com/activeshadow/logr)

Some different implementations of the
[go-logr/logr](https://github.com/go-logr/logr) logging interface.

Currently there's only a *standard* implementation ([stdlogr](stdlogr)) using
`fmt` that prints logs to `STDOUT` in
[logfmt](http://godoc.org/github.com/kr/logfmt).

## stdlogr

The `stdlogr` uses `fmt` to print logs to `STDOUT` in
[logfmt](http://godoc.org/github.com/kr/logfmt). Error logs get printed even
if the `InfoLogger` is disabled.

Example:

```
package main

import (
  "errors"

  "actshad.dev/logr/stdlogr"
)

func main() {
  // Create new "foo" logger that's enabled and has a verbosity level of 1.
  logger := stdlogr.New("foo", true, 1)
  logger.Info("is this working?", "working", true)

  foobarLogger := logger.WithName("bar")
  err := errors.New("this is an error")
  foobarLogger.Error(err, "what about this logger?", "hello", "world!")

  logger.V(1).Info("verbosity 1 log")
  logger.V(2).Info("verbosity 2 log")
}
```

Output:

```
level=info ts=1534767423 name=foo msg="is this working?" working=true
level=error ts=1534767423 name=foo.bar msg="what about this logger?" hello=world! error="this is an error"
level=info ts=1534767423 name=foo msg="verbosity 1 log" v=1
```

## License

```
MIT License

Copyright (c) 2018

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
