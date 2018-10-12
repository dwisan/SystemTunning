> Linux TCP Tunning
```
maximum Linux TCP buffer sizes

For 1GE: set max to 16MB

net.ipv4.tcp_window_scaling = 1
net.core.rmem_max = 16777216 //receive windows size
net.core.wmem_max = 16777216 //send windows size
net.ipv4.tcp_rmem = 4096 87380 16777216
net.ipv4.tcp_wmem = 4096 16384 16777216

For 1GE: set max to 32M or 54M

net.ipv4.tcp_window_scaling = 1
net.core.rmem_max = 33554432 //receive windows size
net.core.wmem_max = 33554432 //send windows size
net.ipv4.tcp_rmem = 4096 87380 33554432 // min, default, and max number of bytes
net.ipv4.tcp_wmem = 4096 65536 33554432 // min, default, and max number of bytes 

```
