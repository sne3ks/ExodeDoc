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


If pip3 is not installed, go [here](https://pip.pypa.io/en/latest/installing/)

### Found the path to your Arduino
```bash
user$ python3
>> from Exode import *
>> BOARD.search()
>> ['/dev/tty.wchusbserial1420' , '/dev/tty.HC-06-DevB']
>>
```

If you use Osx or Linux, you've to know that a device connected to your computer
is interpreted like a file for your OS. And it's through this "file" that Exode communicates
with the Arduino board. You can find this file into this repertory ```\dev```

But you're really lucky today because Exode can find the path of your board like
a good guy, *notice that you've to install Exode on your board before*.
**BOARD.search()** return all board connected with Exode installed on.

### Your first script
```python
#1 Import
from Exode import *

#2 Connect
uno = Board('/path/to/your/board')

#3 Setup
led = Led(13)

#4 Do something awesome !!
led.blink(500)
```

* Firstly you have to **import Exode** ```from Exode import *```
* Then, **connect** your board giving its absolute path ``uno= Board('/path/to/your/board')```
* **Setup** your led, shields, servos... plugged on your Board ```led= Led(13)```
* Now you can **manipulate** them ! ```led.blink(500)```
