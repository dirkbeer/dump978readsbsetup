# dump978readsbsetup

acci:
* You don’t use readsb, you use dump978.  You also have to serialize each dongle and define in readsb and dump978 configs which is used for each.
* don’t know how well the dongle and software handle it, both tools reading at the same time

https://github.com/flightaware/dump978

https://github.com/flightaware/dump1090

https://github.com/wiedehopf/readsb

*How to install dump978*
```bash
git clone https://github.com/flightaware/dump978.git

sudo apt update && sudo apt full-upgrade

sudo apt install \
  build-essential \
  libboost-system-dev \
  libboost-program-options-dev \
  libboost-regex-dev \
  libboost-filesystem-dev \
  libsoapysdr-dev

cd dump978
make
```

*How to install dump1090 (for testing)*
```bash
cd
git clone https://github.com/flightaware/dump1090.git
cd dump1090
make
```

*How to find your current devices and get device serial numbers*
```bash
sudo apt install soapysdr-tools
SoapySDRUtil --find
SoapySDRUtil --probe="driver=rtlsdr"
```

*How to send dump978 output to a specific port, for readsb to read*
```bash
./dump978-fa --sdr driver=rtlsdr,serial=00000001 --raw-port 30978 > /dev/null 2>&1 &
```
The ambersand at the end sends the command to run in the background so you can keep working in the terminal. Use `fg` to bring it back to the foreground, and then `Ctrl-c` to cancel it.

*How to send dump1090 output to a specific port, for readsb to read*
```bash
./dump1090 --device-type rtlsdr --net --net-ro-port 30002 --quiet &
```

*How to find out how readsb is set up by default, and how to control it*
```bash
cat /usr/lib/systemd/system/readsb.service
cat /etc/default/readsb
sudo systemctl stop readsb
```

*Simple readsb run for testing*
Set the port number to match whatever you have dump978 or dump1090 outputting to.
```bash
readsb --net-only --net-connector 127.0.0.1,30002,raw_in
```

*Full readsb run*
```bash
sudo nano /etc/default/readsb
```

```bash
#RECEIVER_OPTIONS="--device 0 --device-type rtlsdr --gain -10 --ppm 0"
RECEIVER_OPTIONS="--net-connector 127.0.0.1,30978,raw_in"
```


```bash
./dump978-fa --sdr driver=rtlsdr,serial=00000001 --raw-port 30978 > /dev/null 2>&1 &
sudo systemctl restart readsb
```
