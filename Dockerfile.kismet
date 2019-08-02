FROM danilonc/kali
MAINTAINER danilonc

RUN wget -O - https://www.kismetwireless.net/repos/kismet-release.gpg.key | apt-key add - && \
    echo 'deb https://www.kismetwireless.net/repos/apt/git/kali kali main' | tee /etc/apt/sources.list.d/kismet.list && \
    DEBIAN_FRONTEND=noninteractive apt-get update -y && \
    DEBIAN_FRONTEND=noninteractive apt-get install -qqy kismet
