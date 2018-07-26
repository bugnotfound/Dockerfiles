FROM kalilinux/kali-linux-docker:latest
MAINTAINER danilonc

# Update Kali
RUN apt-get update -y && apt-get dist-upgrade -y && apt-get autoremove -y

# Install Tools
RUN apt-get update -y && apt-get dist-upgrade -y && apt-get install nmap zmap masscan -y
