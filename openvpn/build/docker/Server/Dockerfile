FROM ubuntu:18.04

RUN apt-get update && apt-get install -y \
        liblz4-dev               \
        liblzo2-dev              \
        libpam-dev               \
        libssl-dev               \
        libtool                  \
        libtool-bin              \
        cmake                    \
        make                     \
        autoconf                 \
        python                   \
        git                      \
        curl                     \
        nano                     \
        libpam0g-dev             \
        unzip                    \
        net-tools                \
        pkg-config               \
        wget                     \
        nsis                     \
        gcc-mingw-w64            \
        man2html                 \
        dos2unix                 \
        ninja-build
        
RUN cd /opt && \
        git clone --recurse-submodules https://github.com/geovandro/PQCrypto-VPN.git || true

RUN cd /opt/PQCrypto-VPN/openvpn/build && python build.py

RUN cd / && tar xvzf /opt/PQCrypto-VPN/openvpn/build/pq-openvpn-linux-staged.tar.gz

RUN mkdir /usr/local/openvpn/etc/keys 

RUN cp /opt/PQCrypto-VPN/openvpn/config/server.ovpn /usr/local/openvpn/etc

RUN cp /opt/PQCrypto-VPN/openvpn/config/sample-certs/picnic-CA.crt /usr/local/openvpn/etc/keys && \
    cp /opt/PQCrypto-VPN/openvpn/config/sample-certs/picnic-server.key /usr/local/openvpn/etc/keys && \
    cp /opt/PQCrypto-VPN/openvpn/config/sample-certs/picnic-server.crt /usr/local/openvpn/etc/keys && \
    cp /opt/PQCrypto-VPN/openvpn/config/sample-certs/dh2048.pem /usr/local/openvpn/etc/keys


# If all steps complete successfully, the following installers should be available:
# Linux: /opt/PQCrypto-VPN/openvpn/build/pq-openvpn-linux-staged.tar.gz
