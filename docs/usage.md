# Usage


Erigon is by default an "all in one binary" solution, but it's possible start any internal component as a separated processes: TxPool, JSON RPC layer (RPCDaemon), p2p layer (Sentry), history download layer (Downloader), consensus layer.

Don't start services as separated processes unless you have clear reason for it: resource limiting, scale, replace by your own implementation, security. 

How to start Erigon's services as separated processes, see in docker-compose.yml.

## All-in-one Client

To use Erigon as a full single service launch:

```bash
./build/bin/erigon
```

Default ``--snapshots`` for ``mainnet``, ``goerli``, ``gnosis``, ``bsc``. Other networks now have default ``--snapshots=false``. Increase
download speed by flag ``--torrent.download.rate=20mb``.

*🔬 See [Downloader docs](./cmd/downloader/readme.md)*

Use ``--datadir`` to choose where to store data.

Use ``--chain=gnosis`` for [Gnosis Chain](https://www.gnosis.io), ``--chain=bor-mainnet`` for Polygon Mainnet, and ``--chain=mumbai`` for Polygon Mumbai.
For Gnosis Chain you need a Consensus Layer client alongside Erigon (see [here](https://docs.gnosischain.com/node/guide/beacon)).

Running ``make help`` will list and describe the convenience commands available in the ``Makefile``.

## RPC Daemon

As every other component, the Remote Procedure Call (RPC) can work inside Erigon or as an independent process.

### Built-in RPC server

To enable built-in RPC server: ``--http`` and ``--ws`` (sharing same port with http)

For example:
```bash
./build/bin/erigon --private.api.addr=localhost:9090 --http.vhosts="*" --http.addr="0.0.0.0" --http.api=eth,web3,net,debug,trace,txpool
```
Run Erigon on a remote server allowing connection from any host, enabling http api for eth, web3, net etc. To connect a remote wallet use IP address of the remote machine on the RPC URL. Default port is 8545 e.g. http://123.123.123.123:8545

### RPC as separate process

The RPC daemon can use the local database (with running Erigon or on snapshot of a database) or remote database (running on another server). 

**For local DB**

When running RPCDaemon on the same machine with Erigon add ``--datadir`` option specifying where Erigon data are stored, by default ``/home/admin/.local/share/erigon``.

```bash
./build/bin/erigon --private.api.addr=localhost:9090 --http=false

./build/bin/rpcdaemon --private.api.addr=localhost:9090 --http.vhosts="*" --http.addr="0.0.0.0" --http.api=eth,erigon,web3,net,debug,trace,txpool —-datadir=/home/admin/.local/share/erigon
```

**For remote DB**

This works regardless of whether RPC daemon is on the same computer with Erigon, or on a different one. They use TPC socket connection to pass data between them. To use this mode, run Erigon in one terminal window.

```bash
./build/bin/erigon --private.api.addr=localhost:9090 --http=false

./build/bin/rpcdaemon --private.api.addr=localhost:9090 --http.api=eth,erigon,web3,net,debug,trace,txpool
```
If the Erigon process is one machine and RPCDaemon is on another machine, use ``private.api.addr`` option for Erigon and open port 9090

```bash
./build/bin/erigon --private.api.addr=0.0.0.0:9090 --http=false --http.vhosts="*" --http.addr="0.0.0.0"
```

On the other machine

```bash
./build/bin/rpcdaemon --http.vhosts="*" --private.api.addr=123.123.123.123:9090 --http.api=eth,erigon,web3,net,debug,trace,txpool
```










