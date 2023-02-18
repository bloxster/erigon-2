Usage
=====

### Getting Started

For building the latest stable release (this will be suitable for most users just wanting to run a node):

```sh
git clone --branch stable --single-branch https://github.com/ledgerwatch/erigon.git
cd erigon
make erigon
./build/bin/erigon
```

You can check [the list of releases](https://github.com/ledgerwatch/erigon/releases) for release notes.

For building the bleeding edge development branch:

```sh
git clone --recurse-submodules https://github.com/ledgerwatch/erigon.git
cd erigon
git checkout devel
make erigon
./build/bin/erigon
```

Default `--snapshots` for `mainnet`, `goerli`, `gnosis`, `bsc`. Other networks now have default `--snapshots=false`. Increase
download speed by flag `--torrent.download.rate=20mb`. <code>🔬 See [Downloader docs](./cmd/downloader/readme.md)</code>

Use `--datadir` to choose where to store data.

Use `--chain=gnosis` for [Gnosis Chain](https://www.gnosis.io/), `--chain=bor-mainnet` for Polygon Mainnet, and `--chain=mumbai` for Polygon Mumbai.
For Gnosis Chain you need a [Consensus Layer](#beacon-chain-consensus-layer) client alongside Erigon (https://docs.gnosischain.com/node/guide/beacon).

Running `make help` will list and describe the convenience commands available in the [Makefile](./Makefile).



.. _installation:

Installation
------------

To use Lumache, first install it using pip:

.. code-block:: console

   (.venv) $ pip install lumache

Creating recipes
----------------

To retrieve a list of random ingredients,
you can use the ``lumache.get_random_ingredients()`` function:

.. autofunction:: lumache.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`lumache.get_random_ingredients`
will raise an exception.

.. autoexception:: lumache.InvalidKindError

For example:

>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']

