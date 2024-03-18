# What's NextEPC

NextEPC is an Open Source implementation of the 4G/5G 3GPP core network. NextEPC includes the Mobility Management Entity
(MME), Serving Gateway (SGW), Packet Data Network Gateway (PGW), Home Subscriber Server (HSS), and Policy and Charging
Rules Functions (PCRF).

For More, Please visit [NextEPC Opensource Project Website](https://nextepc.org).

# What's This Repo

This repo is a modified NextEPC versin for FreeBSD 13. Which have been test.

It will be used for CityU 2023 fall CityUCS5296CloudComputing Group Project with other optimaztion.


# Installation and Configuration

```
# Install mongodb and MongoDB C Driver
doas pkg install mongodb44-4.4.26
doas pkg install libmongocrypt
mkdir -p data/db
mongod --dbpath data/db

# Set loopback interfaces up
doas ifconfig lo0 alias 127.0.0.2 netmask 255.255.255.255
doas ifconfig lo0 alias 127.0.0.3 netmask 255.255.255.255
doas ifconfig lo0 alias 127.0.0.4 netmask 255.255.255.255
doas ifconfig lo0 alias 127.0.0.5 netmask 255.255.255.255
doas sysctl -w net.inet.ip.forwarding=1

# Define a TUN device
doas ifconfig tun create

# Install dependencies
doas pkg install git gcc bison gsed pkgconf autoconf \
         automake libtool gnutls libgcrypt \
         libidn libyaml
# Build
git clone https://github.com/kunlunh/nextepc
cd nextepc
autoreconf -iv
./configure --prefix=`pwd`/install
make -j `nproc`
make install

# Run
nextepc-epcd

# Install NextEPC WebUI
doas pkg install node npm

cd webui
npm install
npm run dev

```


## License

Opensource NextEPC files are made available under the terms of the GNU Affero General Public License (GNU AGPLv3).

