## gobroadcast

[![MIT License](https://img.shields.io/badge/license-MIT-9370d8.svg?style=flat)](https://opensource.org/licenses/MIT)

This package provides an implementation of the fan-out pattern.

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