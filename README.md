# rpi-led-flight-tracker
Track the aircraft flying above you using a Raspberry Pi, RTL-SDR, and an LED matrix

![Example of the flight tracker running on raspberry pi](https://github.com/Weslex/rpi-led-flight-tracker/blob/main/example_img.png)

Add these beforehand if running fresh minimal rebuild
```
sudo apt install -y python3-pip git cmake libusb-1.0-0-dev build-essential pkg-config python3-dev cython3
```

Then run the following so you can have rtl-sdr
```
git clone git://git.osmocom.org/rtl-sdr.git
cd rtl-sdr
mkdir build
cd build
cmake ../ -DINSTALL_UDEV_RULES=ON
make
sudo make install
sudo ldconfig
cd ~
```
#In my Blacklist FIle, /etc/modprobe.d/blacklist I have tried saving both of the following individually with
sudo nano /etc/modprobe.d/rtl-sdr.conf

blacklist RTL28xxU
blacklist RTL2832U
blacklist dvb_usb_rtl28xxu

## Installation
- First clone this repository
```
git clone https://github.com/ftabarrera/rpi-led-flight-tracker.git && cd rpi-led-flight-tracker
```

- Install dump1090 and rpi-rgb-led-matrix
```
git clone https://github.com/antirez/dump1090 && cd dump1090
make
cd ..

git clone https://github.com/hzeller/rpi-rgb-led-matrix && cd rpi-rgb-led-matrix
make build-python 
sudo make install-python
cd ..
mv rpi-rgb-led-matrix rpi_rgb_led_matrix

```
- Create Python Environment and Install Packages
```
python -m venv FlightTrackerEnv
source FlightTrackerEnv/bin/activate
pip install -r requirements.txt
```

## Usage
- The easiest way to configure the flight tracker is to modify "run_flight_tracker.py"
    - Set the display variables for your particular display
    - Set base_latitude and base_longitude values to where you would like the center of the display to base_longitude

- Start up dump1090
```
./dump1090/dump1090 --interactive --net
```

- With dump1090 still running, start the flight tracker (must be run as root)
```
sudo FlightTrackerEnv/bin/python3.11 run_flight_tracker.py
```






