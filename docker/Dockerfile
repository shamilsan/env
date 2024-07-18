FROM --platform=linux/amd64 ubuntu:24.04

ARG RUST_TOOLCHAIN_VERSION=stable
WORKDIR /root

# Install prerequisites
RUN apt update -y && apt upgrade -y
RUN apt install -y build-essential cmake curl git xz-utils wget binaryen

# Install Rust and toolchains
RUN wget https://sh.rustup.rs/rustup-init.sh
RUN chmod +x rustup-init.sh
RUN ./rustup-init.sh -y
ENV PATH="/root/.cargo/bin:$PATH"
RUN rustup default $RUST_TOOLCHAIN_VERSION
RUN rustup target add wasm32-unknown-unknown
RUN rm -f rustup-init.sh
ENV CARGO_NET_GIT_FETCH_WITH_CLI=true
ENV CARGO_REGISTRIES_CRATES_IO_PROTOCOL=sparse
ENV RUSTUP_HOME=/root/.rustup

# Install Node.js and required packages
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash -
RUN apt install -y nodejs
RUN npm install --global yarn

# Install Gear node binary
RUN curl https://get.gear.rs/gear-v1.4.2-x86_64-unknown-linux-gnu.tar.xz | tar -xJC /usr/bin
ENV GEAR_NODE_PATH=/usr/bin/gear
