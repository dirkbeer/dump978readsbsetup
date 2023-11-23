# dump978readsbsetup

acci:
* You don’t use readsb, you use dump978.  You also have to serialize each dongle and define in readsb and dump978 configs which is used for each.
* don’t know how well the dongle and software handle it, both tools reading at the same time

https://github.com/flightaware/dump978
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

![image](https://github.com/dirkbeer/dump978readsbsetup/assets/6425332/eb7fe416-e638-472d-9610-a493dfa4ee1a)

sudo apt install soapysdr-tools

SoapySDRUtil --find

![image](https://github.com/dirkbeer/dump978readsbsetup/assets/6425332/68c0aa73-6350-4790-b253-7eec707d38bd)

![image](https://github.com/dirkbeer/dump978readsbsetup/assets/6425332/ce13a27a-ca0f-4538-931e-9cd42bbbcf7a)


```
