>File Handle Limits
```
fs.file-max = 100000
```
> Socket Tuning
```
# Use the full range of ports.
net.ipv4.ip_local_port_range = 1024 65535

# Enables fast recycling of TIME_WAIT sockets.
net.ipv4.tcp_tw_recycle = 1

# Allow reuse of sockets in TIME_WAIT state for new connections
net.ipv4.tcp_tw_reuse = 1

# Increase the number of outstanding syn requests allowed.
net.ipv4.tcp_max_syn_backlog = 4096
net.ipv4.tcp_syncookies = 1

# The maximum number of "backlogged sockets".  Default is 128.
net.core.somaxconn = 1024

# maximum Linux TCP buffer sizes

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
