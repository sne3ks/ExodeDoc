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
>> searchMyBoard()
>> ['/dev/tty.wchusbserial1420' , '/dev/tty.HC-06-DevB']
>>
```

If you use OSx or Linux, you've to know that a device connected to your computer
is interpreted like a file for your OS. And it's trought this "file" that Exode communicate
with the Arduino board. You can find this file into this repertory ```\dev```

But you're really lucky today because Exode can find the path of your board it-self like
a good guy, *notice that you've to install Exode on your board before*.
**searchMyBoard()** return all board connected with Exode installed on.

### Your first script
```python
from Exode import *

uno = ArduinoUno('/path/to/your/board')

led = Led(13,'OUTPUT')
uno.add(led)

led.blink(500)
```
