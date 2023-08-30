# Use an official Ubuntu 22.04 as the base image
FROM ubuntu:22.04

# Set environment variables for non-interactive (non-tty) operation
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y curl unzip zip git repo sudo openjdk-11-jdk && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Add a new user and group 'kotlindev'
RUN groupadd kotlindev && \
    useradd -ms /bin/bash -g kotlindev kotlindev

# Set up environment variables for SDKMAN
ENV SDKMAN_DIR /home/kotlindev/.sdkman

# Install SDKMAN as kotlindev user
RUN su - kotlindev -c "curl -s https://get.sdkman.io | bash"

# Switch to kotlindev user
USER kotlindev
WORKDIR /home/kotlindev

# Install Kotlin using SDKMAN
RUN bash -c "source $SDKMAN_DIR/bin/sdkman-init.sh && sdk install kotlin && sdk install gradle"

# Set the entrypoint to kotlin compiler
ENTRYPOINT ["kotlinc"]
