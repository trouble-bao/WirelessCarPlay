# WirelessCarPlay
Wireless CarPlay for CarPlay enabled cars

# Basics

Assume that you have Carplay enabled car (full list of car models can be
found here: https://www.apple.com/ios/carplay/available-models/). But most
of them only allow you to use wired connection. It's OK during long distance
trips (you can power up your battery) but very inconvenient when driving short
journeys.

# Idea behind this code

The whole idea is to use Raspberry Pi hardware which will be connected to the USB
port (Carplay enabled port) and your iPhone will use Bluetooth and WiFi connection to the RPi.
This software will take care of BLE and WiFi connection and pass all data to
your head unit via USB port.


# build environment

1. 编译mDNSResponder
```
执行编译：

cd mDNSResponder/mDNSPosix
make os=linux
sudo make install

```

2. 编译CarPlay so
执行编译
```
cd source/PlatformPOSIX
make os=linux

rm -rf WirelessCarPlay/source/build/Debug-linux/
make os=linux debug=1 verbose=1
cp -f WirelessCarPlay/source/build/Debug-linux/*.so WirelessCarPlay/source/Examples/
```
3. 编译Examples AppleCarplay_AppStub.c demo
```
export LD_LIBRARY_PATH=WirelessCarPlay/source/Examples:$LD_LIBRARY_PATH
gcc AppleCarPlay_AppStub.c ../Platform/*.c -L.  -lCoreUtils -lpthread -lAirPlay -lAirPlaySupport -lAudioConverter -lScreenStream -lAudioStream   -I../Sources -I../AccessorySDK/Support/ -I../build/Debug-linux/ -I../Support -I../Platform -fPIC
```
