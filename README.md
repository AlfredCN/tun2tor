# tun2tor

[![Build Status](https://travis-ci.org/iCepa/tun2tor.svg?branch=master)](https://travis-ci.org/iCepa/tun2tor)

`tun2tor` is a Rust library that creates a `utun` (userspace tunnel) interface, and connects it to to a stream-based proxy like `tor`. It is primarily intended to be embedded in the [iCepa](https://github.com/iCepa/iCepa) project, but it can also be used as a standalone utility.

`tun2tor` only compiles for macOS and iOS, although Linux support is almost there.

[API Documentation](https://conradev.github.io/tun2tor)

## Running

Running `tun2tor` as a standalone utility is primarily useful for debugging at the moment. Here is how to get it running:

```bash
$ git clone --recursive https://github.com/iCepa/tun2tor.git
$ cd tun2tor
$ cargo build
$ sudo target/debug/tun2tor
```

```bash
$ tor --DnsPort 12345
```

Running it requires root privileges in order to create a `utun` interface. `tun2tor` is currently hardcoded in [`main.rs`](https://github.com/iCepa/tun2tor/blob/master/src/main.rs) to create an interface with an IP address of `172.30.20.1`, look for a SOCKS proxy at `127.0.0.1:9050`, and look for a DNS server at `127.0.0.1:12345`.

In order to route traffic through the interface, you need to modify the route table:

```bash
$ sudo route add 8.8.8.8 172.30.20.1
$ dig @8.8.8.8 facebookcorewwwi.onion
```
