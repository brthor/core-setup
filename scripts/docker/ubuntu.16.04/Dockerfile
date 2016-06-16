#
# Copyright (c) .NET Foundation and contributors. All rights reserved.
# Licensed under the MIT license. See LICENSE file in the project root for full license information.
#

# Dockerfile that creates a container suitable to build dotnet-cli
FROM ubuntu:16.04

# Misc Dependencies for build
RUN apt-get update && \
    apt-get -qqy install \
        curl \
        unzip \
        gettext \
        sudo && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# This could become a "microsoft/coreclr" image, since it just installs the dependencies for CoreCLR (and stdlib)
RUN apt-get update && \
    apt-get -qqy install \
        libunwind8 \
        libkrb5-3 \
        libicu55 \
        liblttng-ust0 \
        libssl1.0.0 \
        zlib1g \
        libuuid1 \
        liblldb-3.6 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install Build Prereqs
RUN apt-get update && \
    apt-get -qqy install \
        debhelper \
        build-essential \
        devscripts \
        git \
        cmake \
        clang-3.5 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Use clang as c++ compiler
RUN update-alternatives --install /usr/bin/c++ c++ /usr/bin/clang++-3.5 100
RUN update-alternatives --set c++ /usr/bin/clang++-3.5

# Remove sudo password
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
RUN echo '%root ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Change permissions on these directories/files so any user can use them
RUN chmod -R a+rwx /usr/local
RUN chmod -R a+rwx /home
RUN chmod -R 755 /usr/lib/sudo

# Set working directory
WORKDIR /opt/code
