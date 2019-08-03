FROM archlinux/base
LABEL maintainer="danilonc"

# Dockerfile based on https://hub.docker.com/r/niklasheer/arch-yay/dockerfile

# Base installation
RUN pacman -Syyu --noconfirm --noprogressbar && \
    pacman -S --noconfirm --needed --noprogressbar \
    base-devel \
    ttf-roboto \
    jq \
    tar \
    wget

# Add user, group sudo
RUN /usr/sbin/groupadd --system sudo && \
    /usr/sbin/useradd -m --groups sudo user && \
    /usr/sbin/sed -i -e "s/Defaults    requiretty.*/ #Defaults    requiretty/g" /etc/sudoers && \
    /usr/sbin/echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Install yay latest version - https://github.com/Jguer/yay
RUN curl https://api.github.com/repos/Jguer/yay/releases/latest | jq '.["assets"] | map(select(.["browser_download_url"] | contains("x86_64")))[0]["browser_download_url"]' | xargs wget -O- | tar zx && \
    install -Dm755 yay*_x86_64/yay /usr/bin/ && \
    install -Dm644 yay*_x86_64/yay.8 /usr/share/man/man8/yay.8 && \
    rm -rf ./*yay*

USER user
WORKDIR /home/user
