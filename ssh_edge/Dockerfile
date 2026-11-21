# Base image updated by Renovate, update versionCompatibility on Alpine base bump
ARG BUILD_FROM=ghcr.io/home-assistant/base:3.24-2026.11.0@sha256:58422480a299b16b6ea376c2167463206d430619ed02b40cd687c8bd6875519e
FROM $BUILD_FROM

# Setup base
RUN \
    set -x \
    && apk add --no-cache \
        bash-completion \
        pulseaudio-utils \
        alsa-plugins-pulse \
        bluez \
        git \
        libuv \
        mosquitto-clients \
        nano \
        openssh \
        pwgen \
        tmux \
        ttyd \
        vim \
    && apk upgrade --no-cache \
        --repository=https://dl-cdn.alpinelinux.org/alpine/edge/main \
        $(apk info -q | grep '^openssh') \
    && ssh -V

# Add YAML highlighting for nano
ADD https://raw.githubusercontent.com/scopatz/nanorc/master/yaml.nanorc /usr/share/nano/yaml.nanorc
RUN sed -i 's/^#[[:space:]]*\(include "\/usr\/share\/nano\/\*\.nanorc".*\)/\1/' /etc/nanorc

# Use bash as default shell
RUN sed -i "s|/bin/sh|/bin/bash|" /etc/passwd

# Home Assistant CLI
ARG CLI_VERSION=5.7.0
ARG TARGETARCH
RUN \
    TARGETARCH="${TARGETARCH:-$(apk --print-arch)}" \
    && case "${TARGETARCH}" in \
            amd64|x86_64) CLI_ARCH="amd64" ;; \
            arm64|aarch64) CLI_ARCH="aarch64" ;; \
            *) echo "Unsupported TARGETARCH: ${TARGETARCH}" && exit 1 ;; \
        esac \
    && curl -Lso /usr/bin/ha \
        "https://github.com/home-assistant/cli/releases/download/${CLI_VERSION}/ha_${CLI_ARCH}" \
    && chmod a+x /usr/bin/ha \
    && /usr/bin/ha completion > /usr/share/bash-completion/completions/ha

# Copy data
COPY rootfs /

LABEL \
    org.opencontainers.image.title="Home Assistant App: Terminal & SSH (OpenSSH edge)" \
    org.opencontainers.image.description="Allow logging in remotely to Home Assistant using SSH" \
    org.opencontainers.image.source="https://github.com/tvup/ha-app-ssh-edge" \
    org.opencontainers.image.licenses="Apache License 2.0"
