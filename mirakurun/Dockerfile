FROM node:12-buster-slim
EXPOSE 40772
ENV DOCKER="YES"
ENV DEV="libpcsclite-dev libboost*-dev libglib2.0-dev libusb-dev build-essential curl libssl-dev yasm libtool autoconf pkg-config gcc git g++ make automake"

RUN apt-get update && \
    apt-get -y install pcscd libpcsclite1 libccid pcsc-tools libboost-*1.67.0 && \
    apt-get -y install $DEV && \
\
# recpt1
#\
#    git clone https://github.com/stz2012/recpt1 /tmp/recpt1 && \
#    cd /tmp/recpt1/recpt1 && \
#    ./autogen.sh && \
#    ./configure && \
#    make && \
#    make install && \
\
# recfriio
\
    git clone https://github.com/masafm/recfriio.git /tmp/recfriio && \
    cd /tmp/recfriio/recfriior5 && \
    make && \
    make install && \
    ln -s /usr/local/bin/recfriio /usr/local/bin/recpt1 && \
# pm2
\
    npm install pm2 -g && \
\
# arib-b25-stream-test
\
    npm install arib-b25-stream-test -g --unsafe && \
\
# mirakurun
    npm install mirakurun -g --unsafe --production && \
\
# 不要なパッケージを削除
\
    apt-get -y remove $DEV && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/recpt1

WORKDIR /usr/local/lib/node_modules/mirakurun

ENTRYPOINT /etc/init.d/pcscd start && \
    npm start

