# Server LCD-Display
Send local IP address from main NIC and current loadavg or a custom message to LCD display

![](https://github.com/Sebidev/server_lcd-display/blob/main/images/1685800997132.jpg)

### What do you need
Beetle USB ATMEGA32U4 Mini Development Board Module (you can also use any other microcontroller that is compatible with the Arduino Framework)

HD44780 1602 LCD Display Module Bundle with I2C Interface 2x16 Character

Order both, solder them together, firmware for the microcontroller and the program for the computer/server and a circuit diagram can all be found here in the repository.

Python 3 for computer/server program and VSCode with PlatformIO you need them to be able to build the firmware for the microcontroller.

The Python program only works on Linux not on Windows or MacOS. I have tested it on Arch Linux, Debian, Rocky Linux and on Ubuntu.

### First steps
Clone repository
```
git clone https://github.com/Sebidev/server_lcd-display
```
Open VSCode and install PlatformIO. Open the repository as a project with PlatformIO and if necessary edit the platformio.ini file according to the microcontroller you are using. And now just build the PlatformIO project and flash the firmware on them microcontroller.

```
pip install -r requirements.txt
sudo dmesg | grep tty
python server-lcddisplay.py -sp <YOU-SERIALPORT> -n <YOU-NIC> #Output with local IP address from NIC and loadavg send to the LCD-Display
python server-lcddisplay.py -sp <YOU-SERIALPORT> -m <"YOU-MESSAGE"> #Only custom message send to LCD-Display
```

with cronjob you can run the python program every minute or hour in my example, cronjob runs my Python program once every 1 minute.
```
sudo echo "*/1 * * * * <YOU-USER> /bin/python /<YOU-PATH>/server-lcddisplay.py <YOU-SERIALPORT> -n <YOU-NIC>" > /etc/crontab
sudo systemctl start cronie.service
```
