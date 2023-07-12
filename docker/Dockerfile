FROM ubuntu:22.04

ARG NIGHTLY_TOOLCHAIN_VERSION=2023-04-25
WORKDIR /root

# Install prerequisites
RUN apt update -y && apt upgrade -y
RUN apt install -y build-essential cmake curl git xz-utils wget

# Install Rust and toolchains
RUN wget https://sh.rustup.rs/rustup-init.sh
RUN chmod +x rustup-init.sh
RUN ./rustup-init.sh -y
ENV PATH="/root/.cargo/bin:$PATH"
RUN rustup toolchain add nightly
RUN rustup target add wasm32-unknown-unknown --toolchain nightly
ARG TARGET="rustc -Vv | grep 'host: ' | sed 's/^host: \(.*\)$/\1/'"
RUN rustup toolchain install nightly-$NIGHTLY_TOOLCHAIN_VERSION --component llvm-tools-preview
RUN rustup target add wasm32-unknown-unknown --toolchain nightly-$NIGHTLY_TOOLCHAIN_VERSION
RUN rm -rf /root/.rustup/toolchains/nightly-$(eval ${TARGET})
RUN ln -s /root/.rustup/toolchains/nightly-$NIGHTLY_TOOLCHAIN_VERSION-$(eval ${TARGET}) /root/.rustup/toolchains/nightly-$(eval ${TARGET})
RUN rm -f rustup-init.sh
ENV CARGO_NET_GIT_FETCH_WITH_CLI=true
ENV CARGO_REGISTRIES_CRATES_IO_PROTOCOL=sparse
ENV RUSTUP_HOME=/root/.rustup

# Install Node.js and required packages
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash -
RUN apt install -y nodejs
RUN npm install --global yarn

# Install Gear node binary
RUN curl https://get.gear.rs/vara-testnet-v1.2-x86_64-unknown-linux-gnu.tar.xz | tar -xJC /usr/bin
ENV GEAR_NODE_PATH=/usr/bin/gear
