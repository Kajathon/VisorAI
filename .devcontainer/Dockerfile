# Use an official lightweight Python runtime as a parent image
FROM openjdk:11-jre-slim

# Set environment variables for non-interactive (non-tty) operation
ENV DEBIAN_FRONTEND=noninteractive

# Install required packages, set locale, and clean up
RUN apt-get update && \
    apt-get install -y curl unzip zip locales && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8

# Set environment variables for locale
ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=en_US.UTF-8

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
RUN bash -c "source $SDKMAN_DIR/bin/sdkman-init.sh && sdk install kotlin"

# Set the entrypoint to kotlin compiler
ENTRYPOINT ["kotlinc"]
