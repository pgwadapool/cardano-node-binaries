# Build notes

Cardano 1.35.0-rc3 binaries built via Ubuntu 20.04 (glibc-2.31)

Contains network config and alonzo genesis files for mainnet and testnet.

## Requires libsodium and secp256k1

### Instructions to install libsodium

Create a working directory for your builds:

```
mkdir -p ~/src

cd ~/src
```

Download and install libsodium:

```
git clone https://github.com/input-output-hk/libsodium

cd libsodium

git checkout 66f017f1

./autogen.sh

./configure

make

sudo make install
```

Add the following to your .bashrc file and source it:

```
echo "export LD_LIBRARY_PATH="/usr/local/lib:$LD_LIBRARY_PATH"" >> ~/.bashrc

echo "export PKG_CONFIG_PATH="/usr/local/lib/pkgconfig:$PKG_CONFIG_PATH"" >> ~/.bashrc

source ~/.bashrc
```

### Instructions to install secp256k1

Ensure the following are installed if on Ubuntu

```
sudo apt install autoconf automake libtool
```

Create a working directory if you have not already

```
mkdir -p ~/src
cd ~/src
```

Download and install secp256k1

```
git clone https://github.com/bitcoin-core/secp256k1.git

cd secp256k1

git reset --hard $SECP256K1_REF

./autogen.sh

./configure  --enable-module-schnorrsig --enable-experimental

make

sudo make install
```

For those who run cardano-node as a systemd service, run the following:

```
sudo ldconfig
```

This ensures the system is aware of libsodium and secp256k1 (not just at the user level).
