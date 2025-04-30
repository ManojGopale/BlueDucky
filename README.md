Forked from [https://github.com/pentestfunctions/BlueDucky](https://github.com/pentestfunctions/BlueDucky) and modified for my own usecases.

Additional uses cases for remote access of phone via Bluetooth vulnerability
1. Access personal email client on phone, and forward specific emails to yourself.
2. Accessing phone contacts on phone and call anyone.
3. Access messenger app on phone and send messages.
4. Access google maps.

🔗 [Youtube Video](https://www.youtube.com/watch?v=aCu8cRfEyM8): Demonstrates the vulenrability on an adrioid phone. 

Follow instructions.txt to install 
1. Kali linux in VMware
2. BlueDucky on Kali linux to run the bluetooth vulnerability.


start_bluetooth.sh --> Commands to start bluetooth service and toggle bluetooth on from terminal. 

## Introduction 📢
BlueDucky is a powerful tool for exploiting a vulnerability in Bluetooth devices. By running this script, you can:

1. 📡 Load saved Bluetooth devices that are no longer visible but have Bluetooth still enabled.
2. 📂 Automatically save any devices you scan.
3. 💌 Send messages via ducky script format to interact with devices.

### Setup Instructions for Debian-based 

```bash
# update apt
sudo apt-get update
sudo apt-get -y upgrade

# install dependencies from apt
sudo apt install -y bluez-tools bluez-hcidump libbluetooth-dev \
                    git gcc python3-pip python3-setuptools \
                    python3-pydbus

# install pybluez from source
git clone https://github.com/pybluez/pybluez.git
cd pybluez
sudo python3 setup.py install

# build bdaddr from the bluez source
cd ~/
git clone --depth=1 https://github.com/bluez/bluez.git
gcc -o bdaddr ~/bluez/tools/bdaddr.c ~/bluez/src/oui.c -I ~/bluez -lbluetooth
sudo cp bdaddr /usr/local/bin/
```
### Setup Instructions for Arch-based 

```bash
# update pacman & packages
sudo pacman -Syyu

# install dependencies
# since arch doesn't separate lib packages: libbluetooth-dev included in bluez package
sudo pacman -S bluez-tools bluez-utils bluez-deprecated-tools \
               python-setuptools python-pydbus python-dbus
               git gcc python-pip \

# install pybluez from source
git clone https://github.com/pybluez/pybluez.git
cd pybluez
sudo python3 setup.py install

# build bdaddr from the bluez source
cd ~/
git clone --depth=1 https://github.com/bluez/bluez.git
gcc -o bdaddr ~/bluez/tools/bdaddr.c ~/bluez/src/oui.c -I ~/bluez -lbluetooth
sudo cp bdaddr /usr/local/bin/
```

## Running BlueDucky
```bash
git clone https://github.com/pentestfunctions/BlueDucky.git
cd BlueDucky
sudo hciconfig hci0 up
python3 BlueDucky.py
```

alternatively,

```bash
pip3 install -r requirements.txt
```

## Operational Steps 🕹️
1. On running, it prompts for the target MAC address.
2. Pressing nothing triggers an automatic scan for devices.
3. Devices previously found are stored in known_devices.txt.
4. If known_devices.txt exists, it checks this file before scanning.
5. Executes using payload.txt file.
6. Successful execution will result in automatic connection and script running.

## Enjoy experimenting with BlueDucky! 🌟

## More resources
1. [Android keyboard shortcuts](https://support.databeat.net/en/useful-android-keyboard-shortcuts) - Navigate android device using keyboard
2. [Keyboard shortcuts for gmail](https://support.google.com/mail/answer/6594?hl=en&co=GENIE.Platform%3DAndroid&oco=1) - Navigate gmail on android phone using keyboard shortcuts and keys.
3. [Key mapping to Android](https://source.android.com/docs/core/interaction/input/keyboard-devices#hid-keyboard-and-keypad-page-0x07) - Map of hex values and corresponding keyboard keys. 






