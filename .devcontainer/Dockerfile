# Use Ubuntu 22.04 as base
FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    git \
    gdb \
    pkg-config

RUN apt-get update && apt-get install -y --no-install-recommends \
    libnats-dev \
    libzmq3-dev \
    libsocketcan-dev \
    libcurl4-openssl-dev \
    libyaml-dev \
    libelf-dev \
    libbsd-dev

RUN apt-get update && apt-get install -y --no-install-recommends \
    can-utils \
    fonts-powerline \
    pipx \
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
