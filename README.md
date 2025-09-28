> [!NOTE]
> - This project uses a Raspberry Pi 4. The 4GB model is recommended.
> - This project cannot run without the virtual environment and dependencies required. It is recommended to use the .venv folder provided in this repository.

> [!TIP]
> - Each python file has a specific `.sh` and `.service` file to help it run asynchronously in the raspberry pi via shell scripts.
> - The `.sh` files also output a log for debugging.

# Real-Time Attendance Monitoring System (RTAMS) Control and Interface scripts
- Scripts for the functions and API calls of RTAMS. 

## Python code

### clock.py
- Uses the `time`, `datetime`, and `rpi_lcd` libraries to get the exact time based on the raspberry pi's current time, and displays it on the LCD.

### nfc-poll.py
- Uses the `py532lib`, `rpi_lcd`, `logging` and `time` libraries to fetch the data from the NFC card and print it on the lcd. The `logging` library will log a message to the console with the `INFO` level, along with the NFC card's `uid` (unique ID).
- Basically, this scans the NFC cards (restarts continuously every time an NFC card is tapped)

### run.py
- The main script that will run all the functions (at the time when this code was made, it was not yet converted to full OOP due to time constraints).
- Function that handles button presses, LCD display, and row selector (for updating the payload to the correct category).
- Payload updating via API calls in next.js.
- Scrolling text if it's too long for the LCD.
- LCD display for each action.
- Attendance tracking logic (time in and time out, checks if already logged for the specific category, if not, creates a new record).

## Service and Shell Scripts

### nfc_polling.service
- Service runner for the nfc polling shell script

### run_NFC.service
- Service runner for the main script

### sync_clock.service
- Service runner for syncing the raspberry pi's time to time servers via internet

### run_nfc_polling.sh
- Shell script that executes the `nfc-poll.py` script using the virtual environment, and outputs any errors to a log file

### run_script.sh
- Shell script that runs the main `run.py` python script using the virtual environment

### sync_clock.sh
- Shell script that will check network connectivity by pinging google.com. If connected to a wifi network, will fetch the date and time and syncrhonize the raspberry pi's clock.
