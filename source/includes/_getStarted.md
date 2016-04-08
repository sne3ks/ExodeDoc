#Get Started

You're going to need :

- **An Arduino board**
- **Linux or OS X** (Window may work)
- **Python 3**
- **[Arduino Software](https://www.arduino.cc/en/Main/Software)** (only to install Exode on your board)

### Install Exode on your board

First of all, you've to load Exode on your device. That'll be the only time that
you'll have to compile a source code on your board.

1. Download [ExodeArduinoCore](https://github.com/sne3ks/ExodeArduinoCore) sources or ```git clone https://github.com/sne3ks/ExodeArduinoCore.git```

2. Open Arduino Software and [install ArduinoThread library](https://www.arduino.cc/en/Guide/Libraries).

3. Open ```ExodeArduinoCore\main\main.ino``` with the Arduino Software, verify and load the code on your board

### Install Exode on your computer

1. simple ```sudo pip3 install Exode```

<aside class="notice">
If pip3 is not installed, go here
</aside>

### Your first script
```python
from Exode import *

uno = ArduinoUno('/dev/tty.wchusbserial1420')

led = Led(13,'OUTPUT')
uno.add(led)

led.blink(500)
```
1. You can now create a python's script and start to code with Exode.
