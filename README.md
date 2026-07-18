## gobroadcast

[![Build Status](https://github.com/nitroshare/gobroadcast/actions/workflows/test.yml/badge.svg)](https://github.com/nitroshare/gobroadcast/actions/workflows/test.yml)
[![Coverage Status](https://coveralls.io/repos/github/nitroshare/gobroadcast/badge.svg?branch=main)](https://coveralls.io/github/nitroshare/gobroadcast?branch=main)
[![Go Reference](https://pkg.go.dev/badge/github.com/nitroshare/gobroadcast.svg)](https://pkg.go.dev/github.com/nitroshare/gobroadcast)
[![MIT License](https://img.shields.io/badge/license-MIT-9370d8.svg?style=flat)](https://opensource.org/licenses/MIT)

This package provides an implementation of the [fan-out pattern](https://en.wikipedia.org/wiki/Fan-out_(software)).

Sending on a channel in Go normally results in a single channel receiving the value, even if multiple goroutines are receiving on the channel. Instead, this package provides `Broadcaster`, which multiple goroutines can `Subscribe()` to and receive copies of data `Sent()`:

```golang
import "github.com/nitroshare/gobroadcast"

// Create the broadcaster
b := gobroadcast.New[int]()

// Subscribe to the broadcasts (returns a channel that receives them)
c := b.Subscribe()

// Broadcast values
b.Send(0)
b.Send(50)
b.Send(100)

// Unsubscribe from broadcasts
b.Unsubscribe(c)

// Shut down broadcaster (implicitly closing the channel for all subscribers)
b.Close()
```