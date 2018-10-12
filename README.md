>Documentation
```
https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/Documentation/networking/ip-sysctl.txt
https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/Documentation/filesystems/proc.txt
```
>File Handle Limits
```
# increase maximum filedescriptors
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

-- Disable the TCP timestamps option for better CPU utilization:
net.ipv4.tcp_timestamps=0

-- Enable the TCP selective acks option for better throughput
net.ipv4.tcp_sack=1

-- 

# maximum Linux TCP buffer sizes

For 1GE: set max to 16MB

# Network Core
-- sometimes an application can handle huge buffers. To increase the maximum buffer size for all sockets / connections

For 1GB:
net.core.rmem_max = 16777216 - maximum receive window 
net.core.wmem_max = 16777216 - maximum send window
net.core.rmem_default = 16777216
net.core.wmem_default = 16777216
net.core.optmem_max = 16777216

For 10GB:
net.core.rmem_max = 33554432 - maximum receive window
net.core.wmem_max = 33554432 - maximum send window
net.core.rmem_default = 33554432
net.core.wmem_default = 33554432
net.core.optmem_max = 33554432

-- When a system is under heavy load and an interface receives a lot of packets, then the Kernel might not process them fast enough. You can increase the number of packets hold in the queue (backlog)

net.core.netdev_max_backlog = 5000 - Increase the maximum length of processor input queues

# IPv4

-- Enable low latency mode for TCP
net.ipv4.tcp_low_latency=1

-- To get better throughput in a network, it might make sense to enable TCP window scaling as defined in RFC1323:
net.ipv4.tcp_window_scaling = 1

-- Some applications support higher read and write buffers for sockets. The buffer size parameters are defined by 3 values (min, default, max)

For 1Gb:
net.ipv4.tcp_rmem = 4096 87380 16777216 - memory reserved for TCP rcv buffers
net.ipv4.tcp_wmem = 4096 16384 16777216 - memory reserved for TCP snd buffers

For 10Gb:
net.ipv4.tcp_rmem = 4096 87380 33554432 - memory reserved for TCP rcv buffers
net.ipv4.tcp_wmem = 4096 65536 33554432 - memory reserved for TCP snd buffers

-- You can do that by ignoring ICMP broadcasts, which will protect you from ICMP floods. We also ignore bogus responses to broadcast frames (violation against RFC1122),

net.ipv4.icmp_echo_ignore_broadcasts = 1
net.ipv4.icmp_ignore_bogus_error_responses = 1

-- SYN floods are a type of DDoS and can harm your system. To protect from it you should enable SYN cookies, resize the SYN backlog (queue size) and reduce SYN/ACK

net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_max_syn_backlog = 2048
net.ipv4.tcp_synack_retries = 3

-- To log packets with impossible addresses simply enable
net.ipv4.conf.all.log_martians = 1
net.ipv4.conf.default.log_martians = 1

-- To disable IP source routing (SRR), so that nobody can tell us which path a packet should take

net.ipv4.conf.all.accept_source_route = 0
net.ipv4.conf.default.accept_source_route  = 0

-- By default, routers router everything and even packages which don’t belong to their network(s). To avoid that we’ve to make sure strict reverse path filtering is enabled as defined in RFC3704:

net.ipv4.conf.all.rp_filter = 1
net.ipv4.conf.default.rp_filter = 1

-- Disable (ICMP) redirects at all. Please note that the send_redirects parameters should be enabled on routers:
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.default.accept_redirects = 0
net.ipv4.conf.all.secure_redirects = 0
net.ipv4.conf.default.secure_redirects = 0
net.ipv4.conf.all.send_redirects = 0        # Don't disable this on routers!
net.ipv4.conf.default.send_redirects = 0    # Don't disable this on routers!

-- disable IPv4 forwarding on non-routing systems:
net.ipv4.ip_forward = 0

# IPv6
-- Those who don’t use IPv6 at all should disable it:
net.ipv6.conf.all.disable_ipv6 = 1

-- On non-routing systems you should disable router solicitations
net.ipv6.conf.default.router_solicitations = 0
net.ipv6.conf.all.router_solicitations = 0

-- You should also don’t accept routing preferences from router advertisements
net.ipv6.conf.default.accept_ra_rtr_pref = 0
net.ipv6.conf.all.accept_ra_rtr_pref = 0

-- Don’t try to learn prefix information in router advertisements:
net.ipv6.conf.default.accept_ra_pinfo = 0
net.ipv6.conf.all.accept_ra_pinfo = 0

-- Don’t accept hop limits from router advertisements:
net.ipv6.conf.default.accept_ra_defrtr = 0
net.ipv6.conf.all.accept_ra_defrtr = 0

-- Disable IPv6 auto configuration, so that no unicast addresses can automatically be configured on your interface from a router advertisement
net.ipv6.conf.default.autoconf = 0
net.ipv6.conf.all.autoconf = 0

-- If you don’t want your system to be verbose about its neighbours, you should disable neighbour solicitations at all:
net.ipv6.conf.default.dad_transmits = 0
net.ipv6.conf.all.dad_transmits = 0

-- Unless you need more than one global unicast address, you should fix the number of assigned global unicast addresses per interface to 1

net.ipv6.conf.default.max_addresses = 1
net.ipv6.conf.all.max_addresses = 1

```
