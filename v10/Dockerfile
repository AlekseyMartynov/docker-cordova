FROM ubuntu:focal

## JDK

RUN apt-get update && \
    apt-get install -y software-properties-common

RUN add-apt-repository -y ppa:openjdk-r/ppa && \
    apt-get update && \
    apt-get install -y openjdk-8-jdk

ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64

## Android SDK

RUN apt-get install -y wget unzip

ENV ANDROID_SDK_ROOT=/opt/android
ENV ANDROID_HOME=/opt/android

# https://developer.android.com/studio/#command-tools
RUN mkdir $ANDROID_SDK_ROOT && \
    cd $ANDROID_SDK_ROOT && \
    wget -O temp.zip https://dl.google.com/android/repository/commandlinetools-linux-6858069_latest.zip && \
    unzip temp.zip && \
    rm temp.zip

# https://stackoverflow.com/a/65262939
RUN cd $ANDROID_SDK_ROOT && \
    mv cmdline-tools latest && \
    mkdir cmdline-tools && \
    mv latest cmdline-tools

ENV PATH=$PATH:$ANDROID_SDK_ROOT/cmdline-tools/latest/bin

RUN yes | sdkmanager --licenses

ENV ANDROID_BUILD_TOOLS_VERSION=29.0.3

# https://developer.android.com/studio/releases/build-tools
RUN sdkmanager "build-tools;$ANDROID_BUILD_TOOLS_VERSION" "platforms;android-29"

ENV PATH=$PATH:$ANDROID_SDK_ROOT/platform-tools:$ANDROID_SDK_ROOT/build-tools/$ANDROID_BUILD_TOOLS_VERSION

## Node

RUN wget -O- https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get install -y nodejs

## Gradle

RUN apt-get install -y gradle

## Cordova

RUN npm i -g cordova@10
RUN cordova telemetry off

## Git

RUN apt-get install -y git

## Warm-up

RUN cordova create app1 com.example app1 && \
    cd app1 && \
    cordova platform add android && \
    cordova build && \
    cordova build --release && \
    cd .. && \
    rm -rf app1 && \
    gradle -stop
