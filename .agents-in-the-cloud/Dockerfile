FROM agents-in-the-cloud-workspace
# AgentsInTheCloud image version: 1

USER root

# Rust's native linker and the tools needed to fetch the toolchain.
RUN apt-get update \
 && apt-get install -y --no-install-recommends build-essential ca-certificates curl

USER agents-in-the-cloud

ENV CARGO_HOME=/home/agents-in-the-cloud/.cargo \
    RUSTUP_HOME=/home/agents-in-the-cloud/.rustup
ENV PATH="/home/agents-in-the-cloud/.cargo/bin:${PATH}"

# Install once in the image, rather than in each workspace's setup script.
# Keep the toolchain owned by the workspace user so rustup/cargo remain usable.
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs -o /tmp/install-rust.sh \
 && sh /tmp/install-rust.sh -y --no-modify-path --profile minimal \
      --default-toolchain stable --component rustfmt --component clippy \
 && rm /tmp/install-rust.sh \
 && rustc --version \
 && cargo --version
