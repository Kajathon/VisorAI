# Base image
FROM openjdk:11-jdk-slim

# Set environment variables to non-interactive (this prevents some prompts)
ENV DEBIAN_FRONTEND=non-interactive

# Install necessary packages
RUN apt-get update && apt-get install -y \
    curl \
    unzip \
    sudo && \
    rm -rf /var/lib/apt/lists/*

# Create a non-root user named "kotlindev"
RUN adduser --disabled-password --gecos "" kotlindev && \
    echo "kotlindev:kotlindev" | chpasswd && \
    adduser kotlindev sudo

# Switch to the non-root user
USER kotlindev
ENV HOME /home/kotlindev
WORKDIR $HOME

# Install SDKMAN and Kotlin as the kotlindev user
RUN curl -s https://get.sdkman.io | bash
SHELL ["/bin/bash", "-c"]
RUN source "$HOME/.sdkman/bin/sdkman-init.sh" && sdk install kotlin

ENTRYPOINT [ "bash", "-c", "source $HOME/.sdkman/bin/sdkman-init.sh && kotlinc" ]
