👷‍♂️🚧 - WORK IN PROGRESS -
please check back in a few days! -MH 10/27/24
---

# HomeBrew Fermentation Chamber Dashboard
HomeBrew is an open-source project that allows homebrewers to monitor and control fermentation chamber conditions in real-time through the local network.
The project is written in / based on python and assumes you are building a fermentation chamber yourself. The dashboard enables selecting recipies, monitoring & logging of temperature, fermentation progress (coming soon), humidity (coming soon), and fan status, along with data logging and chart visualization. 
This project is designed for Raspberry Pi and compatible hardware, providing a scalable and customizable system for managing fermentation environments.

### Used in current personal setup:
- Raspberry Pi 4 B 2GB
- 4x 80x80mm USB Fans
- 4x DS18B20 Temperture Sensors + 1x 10k Resistor

The chamber itself is build from an old fridge and a 45W Greenhouse Heater. Fridge & Heater are controlled through a STC-1000 220V unit. So far the STC-1000 is **not** connected to the Pi.

## Features
### Real-Time Temperature Monitoring:
- Tracks four different temperatures: Ambient / Room Temp, Top & Bottom Temp within Fermentation Chamber, and the Brew Temperatur.
### Fan Control: 
- Automatically toggles fans within the chamber on/off based on a temperature threshold (bottom vs top) to maintain an even fermentation environment.
### Data Visualization: 
- Live(!) charts to display temperature fluctuations and other fermentation conditions over time. Including fan activity, fermentation / yeast activities and door open/close states
### Historical Log Storage: 
- Fermentation logging can be stopped, paused & re-started. HomeBrew maintains log files of each fermentation session for future reference and analysis.
### Web-Based Dashboard: 
- Accessible through any browser with a responsive and interactive dashboard.

## Prerequisites
- Raspberry Pi with Raspbian OS (or compatible hardware)
- USB temperature sensors compatible with the w1thermsensor library
- uhubctl installed on your Raspberry Pi for USB power control
- Python 3.7 or later
- Virtual environment setup


## Installation
1. Clone this repository:
`git clone https://github.com/yourusername/homebrew_fermentation_chamber.git`
`cd homebrew_fermentation_chamber`

2. Create and activate a virtual environment:
`python3 -m venv homebrew_venv`
`source homebrew_venv/bin/activate`

3. Install the required dependencies:
`pip install -r requirements.txt`

4. Install w1thermsensor and configure USB control:
Ensure that `uhubctl` is installed, then install the `w1thermsensor library` within the virtual environment:
`pip install w1thermsensor`

5. Usage
Start the Flask app:
`flask run --host=0.0.0.0 --port=5001`
Access the Dashboard: Visit `http://127.0.0.1:5001` or `http://homebrew.local` (if configured) in your web browser.

## Dashboard Overview:

### Header
- Start/Stop Button & Animation show you if monitoring/logging is active and into which fermentation log the data is written.
- Allows to start a new fermentation log for a new brew.
### Time Information
- shows the current time and estimated (minimum) and the fermentation time (delta oldest & newest data point)
- shows the minimum required fermentation time in days (according to selected recipe - see Setup & Settings)
- Gives Delta between minimum required and current fermentation time -> minimum time left in fermentation
### Temperture Information
- quick and easy temperature overview and provides max & min recorded temps and the average temp within the chamber
- Also provides an overview of the goal fermentation teemp (according to selected recipe - see Setup & Settings) and the actual average brew temperature
### Brew Temperture Over Time
- chart displaying the temp_brew over (all) logged time and shows (if selected) the expected goal fermentation temp
- auto updates / live, when current selected fermentation log is the log in which HomeBrew is logging

### Setup & Settings
- allows you to select both a recipe and fermentation log
- allows changes (CRU) to recipe csv file.
### Fermentation Data Graph
- core chart of the dashboard, showing data for 300 time stamps.
- By default all data is shown: fermentation goal temp, brew temp, ambeint temp, bottom temp, top temp, interruptions (fermentation activity), door open/closed, fan on/off
- Clicking a line (in legend, bottom of chart) shows/hides the data
- if more than 300 time stamps are present, slider activates and allow scrolling back in time (right to left); the chart auto updates and recenters to the most recent 300 entries, when new data is written to the selected file
### Test & Debug
- allows to test & debug temperature sensors

## Configuration
# Environment Variables
You may configure certain parameters in config.py to customize your setup.

TEMP_THRESHOLD: Temperature difference in °C to activate the fan.
DATA_INTERVAL: Interval in seconds between data logging points.

## Contributing
We welcome contributions! 
To get started, fork this repository, improve the code and submit a pull request. Please ensure any changes include necessary documentation updates and have been tested thoroughly.

## License
This project is licensed under the MIT License. See LICENSE for details.

## Support
For issues or questions, please create a new issue in the GitHub repository.

---

Happy Brewing, Happy Coding
and obviously: Cheers! 🍻
