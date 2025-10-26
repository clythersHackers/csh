# Use Ubuntu 22.04 as base
FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    libcurl4-openssl-dev \
    git \
    build-essential \
    libsocketcan-dev \
    can-utils \
    libzmq3-dev \
    libyaml-dev \
    pkg-config \
    fonts-powerline \
    pipx \
    libelf-dev \
    libbsd-dev \
    python3-dev \
    python3-venv \
    ninja-build \
    && rm -rf /var/lib/apt/lists/*

# Add pipx binaries to PATH
ENV PATH="/root/.local/bin:${PATH}"

# Install Meson (using pipx, as their docs specify)
RUN pipx install meson

# Clone the CSH repository with submodules
WORKDIR /opt
RUN git clone --recurse-submodules https://github.com/clythersHackers/csh.git

# Build stage
WORKDIR /opt/csh
# the default ninja build only installs to ~/.local
RUN ./configure && ./install \
    && cp /root/.local/bin/* /usr/local/bin/

# Optional: default entrypoint to launch CSH
ENTRYPOINT ["/usr/local/bin/csh"]

# Default working directory
WORKDIR /workspace
