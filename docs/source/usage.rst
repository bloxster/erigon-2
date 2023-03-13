Usage
=====

Erigon is by default an "all in one binary" solution, but it's possible start any internal component as a separated processes: TxPool, JSON RPC layer (RPCDaemon), p2p layer (Sentry), history download layer (Downloader), consensus. Don't start services as separated processes unless you have clear reason for it: resource limiting, scale, replace by your own implementation, security. 

How to start Erigon's services as separated processes, see in docker-compose.yml.

Monolithic Client
------------------

To use Erigon as a monolithic service simply launch

``./build/bin/erigon``

Default ``--snapshots`` for ``mainnet``, ``goerli``, ``gnosis``, ``bsc``. Other networks now have default ``--snapshots=false``. Increase
download speed by flag ``--torrent.download.rate=20mb``. <code>🔬 See [Downloader docs](./cmd/downloader/readme.md)</code>

Use ``--datadir`` to choose where to store data.

Use ``--chain=gnosis`` for `Gnosis Chain <https://www.gnosis.io/>`_, ``--chain=bor-mainnet`` for Polygon Mainnet, and ``--chain=mumbai`` for Polygon Mumbai.
For Gnosis Chain you need a Consensus Layer client alongside Erigon (see `here <https://docs.gnosischain.com/node/guide/beacon>`_).

Running ``make help`` will list and describe the convenience commands available in the [Makefile](./Makefile).
