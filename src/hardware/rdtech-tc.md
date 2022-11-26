# Using the RDTech TC66C With sigrok

References:
- Sigrok Device Page: https://www.sigrok.org/wiki/RDTech_TC66C
- Commit that added support: https://sigrok.org/gitweb/?p=libsigrok.git;a=commit;h=cae33a58743e408a602771d6924ee8c271326f47

The latest version of Sigrok available on Ubuntu 22.04 doesn't currently support
this device. So we need to build from source to be able to use it.

Here's the steps I cobbled together to do that on my machine.

```bash

#!/bin/bash
set -euo pipefail

# Based off of the notes for the Twinkie device located here:
# https://www.chromium.org/chromium-os/twinkie/build-sigrok-and-pulseview-from-sources/

sudo apt-get install gcc g++ libtool automake autoconf libftdi-dev libusb-1.0-0-dev libglib2.0-dev check libzip-dev
sudo apt-get install libzip-dev libglibmm-2.4-dev doxygen swig3.0 libhidapi-dev libserialport-dev libieee1284-3-dev
sudo apt-get install qtbase5-dev qtbase5-dev-tools libqt5svg5-dev cmake
sudo apt-get install libboost-filesystem-dev libboost-serialization-dev

git clone git://sigrok.org/libsigrok
git clone git://sigrok.org/libsigrokdecode
git clone git://sigrok.org/sigrok-cli
git clone git://sigrok.org/pulseview

cd libsigrok
./autogen.sh
./configure --prefix=/usr
make install

cd ../libsigrokdecode/
./autogen.sh
./configure --prefix=/usr
make install

cd ../sigrok-cli/
./autogen.sh
./configure --prefix=/usr
make install

cd ../pulseview/
cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr .
make install
```


Example scanning for devices:

```bash
$ sigrok-cli -d rdtech-tc:conn=/dev/ttyACM0 --scan
The following devices were found:
rdtech-tc - RDTech TC66 1.17 [S/N: 00034756] with 6 channels: V I D+ D- E0 E1
```

Example showing a device:

```bash
$ sigrok-cli -d rdtech-tc:conn=/dev/ttyACM0 --show
Driver functions:
    Energy meter
Scan options:
    conn
    serialcomm
rdtech-tc - RDTech TC66 1.17 [S/N: 00034756] with 6 channels: V I D+ D- E0 E1
Supported configuration options:
    continuous: on, off
    limit_samples:
    limit_time:
```

Example collecting samples:

```bash
sigrok-cli -d rdtech-tc:conn=/dev/ttyACM0 --samples 1
V: 8.9669 V
I: 136.75 mA
D+: 0.62 V
D-: 0.61 V
E0: 2.683 Wh
E1: 0 mWh
```
