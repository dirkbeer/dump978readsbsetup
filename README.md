# dump978readsbsetup

acci:
* You don’t use readsb, you use dump978.  You also have to serialize each dongle and define in readsb and dump978 configs which is used for each.
* don’t know how well the dongle and software handle it, both tools reading at the same time

https://github.com/flightaware/dump978
https://github.com/flightaware/dump1090.git
https://github.com/wiedehopf/readsb

```bash
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

sudo systemctl stop readsb

./dump978-fa --sdr driver=rtlsdr
```

![image](https://github.com/dirkbeer/dump978readsbsetup/assets/6425332/7a51f102-eb44-45a5-8cf2-ad0fbc1887d4)

```bash
sudo apt install soapysdr-tools

SoapySDRUtil --find
```

![image](https://github.com/dirkbeer/dump978readsbsetup/assets/6425332/20f7aa11-4bc2-4bdc-af70-7c4936883a70)

```bash
./dump978-fa --sdr driver=rtlsdr,serial=00000001
```

![image](https://github.com/dirkbeer/dump978readsbsetup/assets/6425332/d44e9429-3882-4d51-8359-ec4134833dc5)

Try sending data directly from dump978 to readsb:

```bash
./dump978-fa --sdr driver=rtlsdr,serial=00000001 --raw-port 30978 &
```
```bash
readsb --net-only --net-connector 127.0.0.1,30978,raw_in
```
![image](https://github.com/dirkbeer/dump978readsbsetup/assets/6425332/eed3ba03-7b8f-4b8e-80ba-8a976a041c3a)

Works, but not receiving any messages, let's stop this and try using dump1090 instead.

```
Ctrl-c
fg
Ctrl-c
```

```bash
cd
git clone https://github.com/flightaware/dump1090.git
cd dump1090
make

./dump1090 --device-type rtlsdr --net --net-ro-port 30002 &
```
```bash
readsb --net-only --net-connector 127.0.0.1,30002,raw_in
```
