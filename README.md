# softether_exporter
Prometheus exporter of SoftEther VPN server

[![Build Status](https://travis-ci.org/dalance/softether_exporter.svg?branch=master)](https://travis-ci.org/dalance/softether_exporter)
[![Crates.io](https://img.shields.io/crates/v/softether_exporter.svg)](https://crates.io/crates/softether_exporter)

## Description

softether_exporter is a prometheus exporter for SoftEther VPN server.
The provided metrics are below.

```
softether_online
softether_sessions
softether_sessions_client
softether_sessions_bridge
softether_users
softether_groups
softether_mac_tables
softether_ip_tables
softether_logins
softether_outgoing_unicast_packets
softether_outgoing_unicast_bytes
softether_outgoing_broadcast_packets
softether_outgoing_broadcast_bytes
softether_incoming_unicast_packets
softether_incoming_unicast_bytes
softether_incoming_broadcast_packets
softether_incoming_broadcast_bytes
```

Each metrics has `hub` label. For example, outgoing unicast packet rate of HUB1 is below.

```
rate(softether_outgoing_unicast_packets{hub="HUB1"}[1m])
```

## Install
Download from [release page](https://github.com/dalance/softether_exporter/releases/latest), and extract to any directory ( e.g. `/usr/local/bin` ).
See the example files: `example/softether_exporter.service` and `example/config.toml`

If the release build doesn't fit your environment, you can build and install from source code.

```
cargo install softether_exporter
```

## Requirement

softether_exporter uses `vpncmd` or `vpncmd.exe` to access SoftEther VPN server.
The binary can be got from [SoftEther VPN Download](http://www.softether-download.com/?product=softether).

## Usage

```
softether_exporter [config_file]
```

The format of `config_file` is below.

```
listen_port = 9411                    # listen_port of expoter ( 9411 is the default port of softether_exporter )
listen_port = 9999                    # listen_port of expoter
vpncmd      = "/usr/local/bin/vpncmd" # path to vpncmd binary
server      = "localhost:8888"        # address:port of SoftEther VPN server

[[hubs]]
name     = "HUB1" # HUB name
password = "xxx"  # HUB password

[[hubs]]
name     = "HUB2"
password = "yyy"
```
