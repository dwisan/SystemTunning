> Linux TCP Tunning
```
maximum Linux TCP buffer sizes

For 1GE: set max to 16MB

net.ipv4.tcp_window_scaling = 1
net.core.rmem_max = 16777216 - maximum receive window
net.core.wmem_max = 16777216 - maximum send window
net.ipv4.tcp_rmem = 4096 87380 16777216 - memory reserved for TCP rcv buffers
net.ipv4.tcp_wmem = 4096 16384 16777216 - memory reserved for TCP snd buffers

For 1GE: set max to 32M or 54M

net.ipv4.tcp_window_scaling = 1
net.core.rmem_max = 33554432 - maximum receive window
net.core.wmem_max = 33554432 - maximum send window
net.ipv4.tcp_rmem = 4096 87380 33554432 - memory reserved for TCP rcv buffers
net.ipv4.tcp_wmem = 4096 65536 33554432 - memory reserved for TCP snd buffers

```
