FROM ubuntu:22.04

WORKDIR /root

# Install prerequisites
RUN apt update -y && apt upgrade -y
RUN apt install -y curl xz-utils wget

# Install Rust and toolchains
RUN wget https://sh.rustup.rs/rustup-init.sh
RUN chmod +x rustup-init.sh
RUN ./rustup-init.sh -y
ENV PATH="/root/.cargo/bin:$PATH"
RUN rustup toolchain add nightly
RUN rustup target add wasm32-unknown-unknown --toolchain nightly
ARG TARGET="rustc -Vv | grep 'host: ' | sed 's/^host: \(.*\)$/\1/'"
RUN rustup toolchain install nightly-2023-03-14 --component llvm-tools-preview
RUN rustup target add wasm32-unknown-unknown --toolchain nightly-2023-03-14
RUN rm -rf /root/.rustup/toolchains/nightly-$(eval ${TARGET})
RUN ln -s ~/.rustup/toolchains/nightly-2023-03-14-$(eval ${TARGET}) ~/.rustup/toolchains/nightly-$(eval ${TARGET})

# Install Node.js and required packages
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash -
RUN apt install -y nodejs
RUN npm install --global yarn

# Install Gear node binary
RUN curl -fsSL https://get.gear.rs/vara-testnet-x86_64-unknown-linux-gnu.tar.xz | tar -xJC /usr/bin

# Configure cargo
RUN echo '[registries.crates-io]\nprotocol = "sparse"\n' > /root/.cargo/config.toml

# Install dev-utils
RUN apt install -y build-essential
