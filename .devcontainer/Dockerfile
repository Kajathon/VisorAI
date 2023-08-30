FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=non-interactive

RUN ln -fs /usr/share/zoneinfo/America/New_York /etc/localtime
RUN apt-get update && apt-get install -y tzdata
RUN dpkg-reconfigure --frontend noninteractive tzdata

RUN apt-get update && apt-get install -y \
    git \
    curl \
    unzip \
    vim

RUN apt-get update && apt-get install -y openjdk-11-jdk

RUN apt-get update && apt-get install -y python3 python3-pip

RUN mkdir -p /usr/local/android-sdk/cmdline-tools && cd /usr/local/android-sdk/cmdline-tools && \
    curl -o sdk-tools.zip https://dl.google.com/android/repository/commandlinetools-linux-7302050_latest.zip && \
    unzip sdk-tools.zip && rm sdk-tools.zip

ENV ANDROID_HOME /usr/local/android-sdk
ENV PATH $PATH:$ANDROID_HOME/cmdline-tools/tools/bin:$ANDROID_HOME/platform-tools

RUN yes | sdkmanager --licenses

RUN sdkmanager "platform-tools" "platforms;android-30" "build-tools;30.0.2"

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /app

CMD [ "bash" ]
