# Using thyrlian's Android SDK as the base image
FROM thyrlian/android-sdk:latest

# Set environment variables to non-interactive (this prevents some prompts)
ENV DEBIAN_FRONTEND=non-interactive

# Set timezone data
RUN ln -fs /usr/share/zoneinfo/America/New_York /etc/localtime
RUN apt-get update && apt-get install -y tzdata
RUN dpkg-reconfigure --frontend noninteractive tzdata

# Install additional tools if required
RUN apt-get update && apt-get install -y \
    git \
    curl \
    unzip \
    vim

# Install Java (if not included in the base image or if you need a different version)
RUN apt-get update && apt-get install -y openjdk-11-jdk
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk-amd64

# Install Python for backend operations
RUN apt-get update && apt-get install -y python3 python3-pip

# Clean up for reducing image size
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set the working directory
WORKDIR /app

# Default command
CMD [ "bash" ]
