# Base image
FROM openjdk:11-jdk-slim

# Set environment variables to non-interactive (this prevents some prompts)
ENV DEBIAN_FRONTEND=non-interactive

# Install necessary packages and Kotlin
RUN apt-get update && apt-get install -y \
    curl \
    unzip \
    sudo && \
    curl -s https://get.sdkman.io | bash && \
    bash -c "source $HOME/.sdkman/bin/sdkman-init.sh && sdk install kotlin"

# Create a non-root user named "kotlindev"
RUN useradd -m kotlindev && \
    echo "kotlindev:kotlindev" | chpasswd && \
    adduser kotlindev sudo

# Switch to the non-root user
USER kotlindev

# Set the user's home directory and the work directory
ENV HOME /home/kotlindev
WORKDIR $HOME

# Set up SDKMAN and Kotlin for the kotlindev user
RUN curl -s https://get.sdkman.io | bash && \
    bash -c "source $HOME/.sdkman/bin/sdkman-init.sh && sdk install kotlin"

# Any additional setup or installations can be added here...

ENTRYPOINT [ "bash", "-c", "source $HOME/.sdkman/bin/sdkman-init.sh && kotlinc" ]
