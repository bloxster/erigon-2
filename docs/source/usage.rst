Usage
=====

Erigon is a full modular client which allows its use from a service with all the options included to a setup of services splitted among different processes, machines or remote servers according to user preferences.

Monolithic Client
------------------

To use Erigon as a monolithic service simply launch

``./build/bin/erigon``

Default ``--snapshots`` for ``mainnet``, ``goerli``, ``gnosis``, ``bsc``. Other networks now have default ``--snapshots=false``. Increase
download speed by flag ``--torrent.download.rate=20mb``. <code>🔬 See [Downloader docs](./cmd/downloader/readme.md)</code>

Use ``--datadir`` to choose where to store data.

Use ``--chain=gnosis`` for `Gnosis Chain<https://www.gnosis.io/>`_, ``--chain=bor-mainnet`` for Polygon Mainnet, and ``--chain=mumbai`` for Polygon Mumbai.
For Gnosis Chain you need a Consensus Layer client alongside Erigon <https://docs.gnosischain.com/node/guide/beacon>.

Running ``make help`` will list and describe the convenience commands available in the [Makefile](./Makefile).
