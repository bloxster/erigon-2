# Fundamentals

Erigon is an implementation of Ethereum (execution client with light client for consensus layer), on the efficiency frontier with high modularity. Archive Node by default.

# System Requirements

For an Archive node of Ethereum Mainnet we recommend >=3TB storage space: 1.8TB state (as of March 2022), 200GB temp files (can symlink or mount folder <datadir>/temp to another disk). Ethereum Mainnet Full node ( see --prune* flags): 400Gb (April 2022).

Goerli Full node (see --prune* flags): 189GB on Beta, 114GB on Alpha (April 2022).

Gnosis Chain Archive: 370GB (January 2023).

BSC Archive: 7TB. BSC Full: 1TB.

Polygon Mainnet Archive: 5TB. Polygon Mumbai Archive: 1TB.

SSD or NVMe. Do not recommend HDD - on HDD Erigon will always stay N blocks behind chain tip, but not fall behind. Bear in mind that SSD performance deteriorates when close to capacity.

RAM: >=16GB, 64-bit architecture.

Golang version >= 1.18; GCC 10+ or Clang; On Linux: kernel > v4

🔬 more details on disk storage [here](https://erigon.substack.com/p/disk-footprint-changes-in-new-erigon?s=r) and [here](https://ledgerwatch.github.io/turbo_geth_release.html#Disk-space).
