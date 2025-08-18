# .devcontainer configuration for Mortar project
# Uses Go 1.24.2

FROM golang:1.24.2


# Install common tools and Docker (official instructions)
RUN apt-get update && \
    apt-get install -y \
    ca-certificates \
    curl \
    gnupg \
    lsb-release \
    git \
    bash && \
    rm -rf /var/lib/apt/lists/*

# Add Docker’s official GPG key
RUN install -m 0755 -d /etc/apt/keyrings && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg && \
    chmod a+r /etc/apt/keyrings/docker.gpg

# Set up the Docker repository
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list

# Install Docker Engine, CLI, and containerd
RUN apt-get update && \
    apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin && \
    rm -rf /var/lib/apt/lists/*

# Install Task
RUN sh -c "$(curl --location https://taskfile.dev/install.sh)" -- -d -b /bin v3.42.1


# Install runtime dependencies
RUN apt-get update && apt-get install -y \
    libsdl2-dev \
    libsdl2-ttf-dev \
    libsdl2-image-dev \
    libsdl2-gfx-dev

# Set default shell to bash
SHELL ["/usr/bin/bash", "-c"]

# Set up a non-root user (optional)
WORKDIR /workspace
RUN useradd -m vscode && chown -R vscode /workspace && usermod -aG docker vscode
# Install and configure sudo for vscode non-root user:
RUN apt-get update && \
    apt-get install -y sudo && \
    echo "vscode ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    rm -rf /var/lib/apt/lists/*
USER vscode
SHELL ["/usr/bin/bash", "-c"]