FROM nvidia/opencl

RUN DEBIAN_FRONTEND=non-interactive apt-get update -qqy && DEBIAN_FRONTEND=non-interactive apt-get -qqy install magic-wormhole tcpdump tshark p7zip-full wget curl cmake build-essential make libssl-dev zlib1g-dev libcurl4-openssl-dev git aria2 tmux vim

WORKDIR /opt
RUN wget https://hashcat.net/files/hashcat-5.1.0.7z && 7z x hashcat-5.1.0.7z && rm -rf hashcat-5.1.0.7z

# Download all workdlists from wpa-sec.stanev.org/?my_dicts
RUN  mkdir /wordlist && \
     chmod 777 /wordlist
WORKDIR /wordlist
RUN curl https://wpa-sec.stanev.org/\?dicts  | egrep -io 'href[^>]*>' | egrep -oi 'https.*gz' | xargs -n1  wget

# Download netgear killer and other default psk generators
RUN git clone https://github.com/soxrok2212/PSKracker.git

# Download ptwiki wordlist
RUN aria2c --seed-time=0 'aria2c 'magnet:?xt=urn:btih:RM5672AK4GBORY3RI5E2JR6EJGCUYEHA&dn=uniq_most_common_ptwiki_words.txt&xl=183599639&tr=udp://tracker.opentrackr.org:1337/announce''

# Download rockyou.txt
RUN wget http://downloads.skullsecurity.org/passwords/rockyou.txt.bz2

# Download probable wordlist
RUN git clone https://github.com/berzerk0/Probable-Wordlists.git

# Install hcxtools
WORKDIR /opt/
RUN git clone https://github.com/ZerBea/hcxtools.git && cd hcxtools && make && make install

# Install hashcat tools git
WORKDIR /opt/
RUN git clone https://github.com/hashcat/hashcat.git && cd hashcat && make && make install

WORKDIR /opt/
RUN git clone https://github.com/hashcat/maskprocessor.git && cd maskprocessor/src && make && install -m 755 *.bin /usr/local/bin/

WORKDIR /opt/
RUN git clone https://github.com/hashcat/hashcat-utils.git && cd hashcat-utils/src && make && install -m 755 *.bin *.pl /usr/local/bin/

WORKDIR /opt/
RUN git clone https://github.com/hashcat/princeprocessor.git && cd princeprocessor/src && make && install -m 755 *.bin /usr/local/bin/

WORKDIR /opt/
RUN git clone https://github.com/hashcat/kwprocessor.git && cd kwprocessor && make && install -m 755 kwp /usr/local/bin/

WORKDIR /opt/
RUN git clone https://github.com/hashcat/statsprocessor.git && cd statsprocessor/src && make && install -m 755 *.bin /usr/local/bin/

RUN wget https://raw.githubusercontent.com/ZerBea/hcxtools/master/usefulscripts/hcxgrep.py -O /usr/local/bin/hcxgrep.py && chmod a+x /usr/local/bin/hcxgrep.py

# Set the locale
#RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && locale-gen
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8  

WORKDIR /root/
RUN wget https://gist.githubusercontent.com/DaniloNC/33e8c44e3ed669f02ff9def29d61e267/raw/5d88836b884167ab59d7dd7afc28a1e1e76ae12c/crack_wpa.sh && chmod a+x crack_wpa.sh
