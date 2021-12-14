```golang
import (
    "log"
    "github.com/Ansen/latency"
)

func main() {
    duration := latency.Latency("localAddr", "1.1.1.1", "443")
    log.Println("Latency: ", duration)

}
```

The `sudo` is needed to open a raw socket. If you know how to do this with capabilities, please do tell.

`latency` can also run in _auto_ mode, where it tests a range of well known sites (which will be geo-balanced), and some servers in specific locations. It's fun, try it! `sudo latency -a`

`latency` sends a TCP SYN packet (the opening of the three-way handshake) to a remote host on port 80. That host will respond with either a RST (if the port is closed), or a SYN/ACK (if the port is open). Either way, we time how long it takes between sending the SYN and receiving the response. That's your network latency.

There are of course many other ways to measure this ([mtr](https://en.wikipedia.org/wiki/MTR_%28Software%29) is nice), but this is a fun exercise in using raw sockets and binary encoding in Go.

License: GPL.
