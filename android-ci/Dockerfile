FROM java:8
MAINTAINER cliffred

ENV ANDROID_SDK_VERSION 24.3.4

# Install Dependencies
RUN dpkg --add-architecture i386 && apt-get update && apt-get install -y --force-yes libc6-i386 lib32stdc++6 lib32gcc1 lib32ncurses5 lib32z1

# Install Android SDK
RUN cd /opt && wget --output-document=android-sdk.tgz --quiet http://dl.google.com/android/android-sdk_r$ANDROID_SDK_VERSION-linux.tgz && tar xzf android-sdk.tgz && rm -f android-sdk.tgz && chown -R root.root android-sdk-linux

# Setup environment
ENV ANDROID_HOME /opt/android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools

# Install sdk elements
RUN echo y | android update sdk --all --force --no-ui --filter tools,platform-tools,tools,build-tools-23.0.3,android-23,extra-android-support,extra-android-m2repository

# Cleaning
RUN apt-get clean

# GO to workspace
RUN mkdir -p /opt/workspace
WORKDIR /opt/workspace
