FROM ubuntu:20.04

ARG PULSAR_VERSION=2.5.2
ARG PULSAR_URL_PREFIX=https://archive.apache.org/dist/pulsar/pulsar-${PULSAR_VERSION}
ARG PULSAR_CLIENT=apache-pulsar-client.deb
ARG PULSAR_CLIENT_DEV=apache-pulsar-client-dev.deb
RUN set -x \
    && sed -i 's/archive.ubuntu.com/mirrors.huaweicloud.com/g' /etc/apt/sources.list \
    ## install by apt-get
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    build-essential cmake \
    libboost-dev libboost-filesystem-dev \
    liblz4-dev libsnappy-dev libzstd-dev liblog4cxx-dev \
    libmsgpack-dev libzookeeper-mt-dev libcpprest-dev libhdf5-dev \
    ca-certificates wget \
    ## install pulsar c++ client
    && mkdir -pv /tmp/pulsar/DEB \
    && cd /tmp/pulsar \
    && wget -q "${PULSAR_URL_PREFIX}/DEB/${PULSAR_CLIENT}" -P "DEB" \
    && wget -q "${PULSAR_URL_PREFIX}/DEB/${PULSAR_CLIENT}.sha512" -P "DEB" \
    && sha512sum -c "DEB/${PULSAR_CLIENT}.sha512" \
    && dpkg -i "DEB/${PULSAR_CLIENT}" \
    && wget -q "${PULSAR_URL_PREFIX}/DEB/${PULSAR_CLIENT_DEV}" -P "DEB" \
    && wget -q "${PULSAR_URL_PREFIX}/DEB/${PULSAR_CLIENT_DEV}.sha512" -P "DEB" \
    && sha512sum -c "DEB/${PULSAR_CLIENT_DEV}.sha512" \
    && dpkg -i "DEB/${PULSAR_CLIENT_DEV}" \
    && cd / \
    && rm -rf /tmp/pulsar \
    ## clean
    && apt-get autoremove -y ca-certificates wget \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

CMD ["/bin/bash"]
