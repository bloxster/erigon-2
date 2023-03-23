
# Getting started

In order to use Erigon, the software must first be installed. There are several ways Erigon can be installed depending on the operating system and the user's choice of installation method, for example using a package manager, container or building from source.

## System Requirements

For an Archive node of Ethereum Mainnet it is recommended ≥ 3TB of storage space: 1.8TB state (as of March 2022), 200GB temp files (can symlink or mount folder <datadir>/temp to another disk).

- Ethereum Mainnet Full node ( see --prune* flags): 400Gb (April 2022).
- Goerli Full node (see --prune* flags): 189GB on Beta, 114GB on Alpha (April 2022).
- Gnosis Chain Archive: 370GB (January 2023).
- BSC Archive: 7TB. BSC Full: 1TB.
- Polygon Mainnet Archive: 5TB. Polygon Mumbai Archive: 1TB.

As a storage mean it is reccomended to have SSD or NVMe disk. HDD is not reccomended because it will cause Erigon to always stay *N* blocks behind chain tip, but not fall behind. Furthermore, SSD performance deteriorates when close to capacity. 

*🔬 More details on disk storage [here](https://erigon.substack.com/p/disk-footprint-changes-in-new-erigon?s=r) and [here](https://ledgerwatch.github.io/turbo_geth_release.html#Disk-space).*

CPU: 64-bit architecture

RAM: ≥16GB

On Linux: kernel > v4

[Golang](https://go.dev/doc/install) version ≥ 1.18; [GCC](https://go.dev/doc/install/gccgo) 10+ or [Clang](https://clang.llvm.org).

## Installing Erigon

For building the latest stable release (this will be suitable for most users just wanting to run a node):

```bash
git clone --branch stable --single-branch https://github.com/ledgerwatch/erigon.git
cd erigon
make erigon
```

You can check the [list of releases](https://github.com/ledgerwatch/erigon/releases) for release notes.

For building the bleeding edge development branch:

```bash
git clone --recurse-submodules https://github.com/ledgerwatch/erigon.git
cd erigon
git checkout devel
make erigon
```
  
## Windows
  
Windows users may run erigon in 3 possible ways:

- Build executable binaries natively for Windows
- Use Docker
- Use WSL (Windows Subsystem for Linux)

### Build executable binaries natively for Windows
  
Using provided wmake.ps1 PowerShell script. Usage syntax is the same as make command so you have to run .\wmake.ps1 [-target] <targetname>. Example: .\wmake.ps1 erigon builds erigon executable. All binaries are placed in .\build\bin\ subfolder. There are some requirements for a successful native build on windows :

- Git for Windows must be installed. If you're cloning this repository is very likely you already have it
- GO Programming Language must be installed. Minimum required version is 1.18
- GNU CC Compiler at least version 10 (is highly suggested that you install chocolatey package manager - see following point)
- If you need to build MDBX tools (i.e. .\wmake.ps1 db-tools) then Chocolatey package manager for Windows must be installed. By Chocolatey you need to install the following components : cmake, make, mingw by choco install cmake make mingw. Make sure Windows System "Path" variable has: ``C:\ProgramData\chocolatey\lib\mingw\tools\install\mingw64\bin``

.. note::
  Important note about Anti-Viruses During MinGW's compiler detection phase some temporary executables are generated to test compiler capabilities. It's been reported some anti-virus programs detect those files as possibly infected by Win64/Kryptic.CIS trojan horse (or a variant of it). Although those are false positives we have no control over 100+ vendors of security products for Windows and their respective detection algorithms and we understand this might make your experience with Windows builds uncomfortable. To workaround the issue you might either set exclusions for your antivirus specifically for build\bin\mdbx\CMakeFiles sub-folder of the cloned repo or you can run erigon using the following other two options

### Use Docker

See [docker-compose.yml](https://github.com/ledgerwatch/erigon/blob/devel/docker-compose.yml)

### Use WSL (Windows Subsystem for Linux)

.. note::
  WSL Version 2 is the only version supported

Under this option you can build Erigon just as you would on a regular Linux distribution. You can point your data also to any of the mounted Windows partitions ( eg. ``/mnt/c/[...]``, ``/mnt/d/[...]`` etc) but in such case be advised performance is impacted: this is due to the fact those mount points use ``DrvFS`` which is a network file system and, additionally, MDBX locks the db for exclusive access which implies only one process at a time can access data. This has consequences on the running of ``rpcdaemon`` which has to be configured as Remote DB even if it is executed on the very same computer. If instead your data is hosted on the native Linux filesystem non limitations apply. Please also note the default WSL2 environment has its own IP address which does not match the one of the network interface of Windows host: take this into account when configuring NAT for port 30303 on your router.
