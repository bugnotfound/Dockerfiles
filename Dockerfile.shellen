FROM danilonc/keystone
MAINTAINER danilonc

WORKDIR /opt

# Update
RUN apt-get update -y && apt-get dist-upgrade -y && apt-get autoremove -y

# Install Tools
RUN apt-get update -y && apt-get dist-upgrade -y && apt-get install build-essential git cmake python3-dev python3-setuptools python-ipython tmux python3-pip python3-colorama python3-termcolor python3-terminaltables python3-pygments python3-prompt-toolkit -y

# Install shellen 
RUN pip3 install shellen

# Install kcshell
RUN pip3 install kcshell

# Default command
CMD /bin/bash
