# dump978readsbsetup

https://github.com/wiedehopf/readsb

```
git clone https://github.com/flightaware/dump978.git

sudo apt update && sudo apt full-upgradey

sudo apt-get install \
  build-essential \
  libboost-system-dev \
  libboost-program-options-dev \
  libboost-regex-dev \
  libboost-filesystem-dev \
  libsoapysdr-dev

cd dump978
make

./dump978-fa --sdr driver=rtlsdr


```
