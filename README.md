# nfq-go

nfq-go is a Go library that wraps libnetfilter_queue.

## Usage

### Import 

```go
import nfq "github.com/hownetworks/nfq-go"
```

### New

```go
queue, err := nfq.New(0, func(pkt nfq.Packet) {
  ...
})
```

### Give a Verdict

`NF_ACCEPT`

```go
err := pkt.Accept()
```

`NF_DROP`

```go
err := pkt.Drop()
```

`NF_REPEAT`

```go
err := pkt.Repeat()
```

`NF_QUEUE` to queue 5

```go
err := pkt.Queue(x)
```

### Modifying Packets

Use `WithData(data []byte)` and `WithMark(mark uint32)` to modify the packet's data and mark. Instead of modifying the original these methods return a new `Packet` and can be chained.

As an example, here's how to (re)queue the packet to queue number 5, this time its data set to `newData` and mark set to `1234`:

```go
err := pkt.WithData(newData).WithMark(1234).Queue(5)
```

### Close

```go
queue.Close()
```
