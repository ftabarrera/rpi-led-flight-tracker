# rpi-led-flight-tracker
Track the aircraft flying above you using a Raspberry Pi, RTL-SDR, and an LED matrix

![Example of the flight tracker running on raspberry pi](https://github.com/Weslex/rpi-led-flight-tracker/blob/main/example_img.png)

## Installation
- First clone this repository
```
    git clone https://github.com/Weslex/rpi-led-flight-tracker && cd rpi-led-flight-tracker
```

- Install dump1090 and rpi-rgb-led-matrix
```
    git clone https://github.com/antirez/dump1090 && cd dump1090
    make
    cd ..

    git clone https://github.com/hzeller/rpi-rgb-led-matrix
    sudo apt-get update && sudo apt-get install python3-dev cython3 -y
    make build-python 
    sudo make install-python
    cd ..

```
- Create Python Environment and Install Packages
```
    python -m venv FlightTrackerEnv
    source FlightTrackerEnv
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






