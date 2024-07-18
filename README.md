# Gear Envinronment

Development environment for building smart contracts.

# Usage

0. Install [Docker](https://docs.docker.com/engine/install/).

1. Pull and run Docker container:

    ```shell
    docker pull ghcr.io/gear-foundation/gear-env:stable
    docker run --rm --name gear-env -itd ghcr.io/gear-foundation/gear-env:stable bash
    ```

2. Prepare smart contract for building (here we use [`dapp-template`](https://github.com/gear-foundation/dapp-template) for example):

    ```shell
    git clone https://github.com/gear-foundation/dapp-template.git --depth 1
    docker cp ./dapp-template gear-env:/root
    ```

3. Build smart contract on the Docker container:

    ```shell
    docker exec -itw /root/dapp-template gear-env cargo build --release
    ```

4. Copy build artifacts back to the local machine:

    ```shell
    docker cp gear-env:/root/dapp-template/target/wasm32-unknown-unknown/release/. ./
    ```

5. Stop the Docker container after using:

    ```shell
    docker stop gear-env
    ```

# Contents

## v1.4.2 (latest stable)

- Based on Ubuntu 24.04 LTS
- Stable Rust toolchain: `v1.79.0` (`129f3b996 2024-06-10`)
- Node.js: `v20.15.1`
- Yarn: `v1.22.22`
- Gear node binary: `1.4.2-13d95cf3388`

## v1.0.2

- Based on Ubuntu 22.04 LTS
- Stable Rust toolchain: `v1.74.0` (`79e9716c9 2023-11-13`)
- Nightly Rust toolchain: `v1.74.0-nightly` (`203c57dbe 2023-09-17`)
- Node.js: `v18.17.1`
- Yarn: `v1.22.21`
- Gear node binary: `v1.0.2-d02d306f97c`

## v0.1.4

- Based on Ubuntu 22.04 LTS
- Stable Rust toolchain: `v1.74.0` (`79e9716c9 2023-11-13`)
- Nightly Rust toolchain: `v1.75.0-nightly` (`fcab24817 2023-10-13`)
- Node.js: `v18.17.1`
- Yarn: `v1.22.21`
- Gear node binary: `v1.0.1-a3fe307bd8e`

## v0.1.2

- Based on Ubuntu 22.04 LTS
- Stable Rust toolchain: `v1.74.0` (`79e9716c9 2023-11-13`)
- Nightly Rust toolchain: `v1.71.0-nightly` (`f5559e338 2023-04-24`)
- Node.js: `v18.17.1`
- Yarn: `v1.22.21`
- Gear node binary: `v0.2.2-946ac47439c`

## v0.1.1

- Based on Ubuntu 22.04 LTS
- Stable Rust toolchain: `v1.70.0` (`90c541806 2023-05-31`)
- Nightly Rust toolchain: `v1.71.0-nightly` (`f5559e338 2023-04-24`)
- Node.js: `v18.16.0`
- Yarn: `v1.22.19`
- Gear node binary: `v0.1.6-78dfa07ed34`

## v0.1.0

- Based on Ubuntu 22.04 LTS
- Rust toolchain: `v1.69` (`stable`) and `v1.70.0-nightly` (`2023-03-14`)
- Node.js: `v18.16`
- Yarn: `v1.22`
- Gear node binary: `v0.1.4-5c685d0`

# Build and run Docker container locally

```shell
git clone https://github.com/gear-foundation/gear-env.git
cd gear-env
```

```shell
docker build -t gear-env docker
docker run --rm --name gear-env -itd gear-env bash
```

# License

The source code is licensed under the [MIT license](LICENSE).
