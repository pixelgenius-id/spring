# Vexanium Node (Spring)

1. [Branches](#branches)
2. [Supported Operating Systems](#supported-operating-systems)
3. [Build and Install from Source](#build-and-install-from-source)
4. [Bash Autocomplete](#bash-autocomplete)

Vexanium Node is a C++ implementation of the Vexanium blockchain protocol, based on [AntelopeIO/spring](https://github.com/AntelopeIO/spring) v1.2.2 with Savanna consensus support. It contains blockchain node software and supporting tools for block producers and developers.

## Vexanium Customizations
Changes applied on top of Spring v1.2.2:

- System account: `eosio` → `vexcore`
- System account prefix: `eosio.*` → `vex.*` (`vex.token`, `vex.msig`, `vex.prods`, `vex.null`, `vex.code`, etc.)
- Core token symbol: `SYS` → `VEX`
- Public key prefix: `EOS` → `VEX`
- Genesis key: Vexanium mainnet initial key (`VEX6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV`)
- Default data/config dir: `~/.local/share/vexcore/`
- Default wallet dir: `~/vex-wallet/`
- EOS VM OC whitelist default: `vexcore` suffix
- Privileged account name guard prefix: `vex.` (was `eosio.`)

## Branches
Use the `vexanium` branch for Vexanium mainnet production. This branch tracks Spring v1.2.2 + Vexanium-specific changes.

## Supported Operating Systems
- Ubuntu 22.04 Jammy
- Ubuntu 20.04 Focal

## Build and Install from Source

### Prerequisites
- C++20 compiler and standard library
- CMake 3.16+
- LLVM 11 (Linux only)
- libcurl 7.40.0+
- git, GMP, Python 3, python3-numpy, zlib

### Step 1 - Clone
```bash
git clone --recursive https://github.com/pixelgenius-id/spring.git
cd spring
git checkout vexanium
git submodule update --init --recursive
```

### Step 2 - Install Dependencies

```bash
sudo apt-get update
sudo apt-get install -y \
        build-essential \
        cmake \
        git \
        libcurl4-openssl-dev \
        libgmp-dev \
        llvm-11-dev \
        python3-numpy \
        file \
        zlib1g-dev
```

On Ubuntu 20.04, also install gcc-10:
```bash
sudo apt-get install -y g++-10
```

### Step 3 - Build

```bash
mkdir -p build && cd build

# Ubuntu 20.04
cmake -DCMAKE_C_COMPILER=gcc-10 -DCMAKE_CXX_COMPILER=g++-10 \
      -DCMAKE_BUILD_TYPE=Release \
      -DLLVM_DIR=/usr/lib/llvm-11/lib/cmake/llvm ..

# Ubuntu 22.04
cmake -DCMAKE_BUILD_TYPE=Release \
      -DLLVM_DIR=/usr/lib/llvm-11/lib/cmake/llvm ..

make -j$(nproc) nodeos cleos keosd
```

### Step 4 - Verify
```bash
./programs/nodeos/nodeos --full-version
```

### Step 5 - Install
```bash
sudo cp programs/nodeos/nodeos /usr/local/bin/
sudo cp programs/cleos/cleos /usr/local/bin/
sudo cp programs/keosd/keosd /usr/local/bin/
```

## Bash Autocomplete
```bash
sudo cp programs/cleos/bash-completion/completions/cleos /etc/bash_completion.d/
sudo cp programs/spring-util/bash-completion/completions/spring-util /etc/bash_completion.d/
```

## Upstream
This repository is a fork of [AntelopeIO/spring](https://github.com/AntelopeIO/spring). Security patches and upstream improvements can be merged from the upstream `release/1.2` branch.
