#Pin
*[Arduino's official tutorial about pins](https://www.arduino.cc/en/Tutorial/DigitalPins)*
## Digital
```python
  uno = Board('/path/to/your/board')

  pin=DigPin(13,'OUTPUT')
  pin.write('HIGH')
  pin.switch()

  pin.periodicSwitch(500)
  pin.stopPeriodicSwitch()

  pin.mode('INPUT')
  pin.read()
  pin._lvl
  >> 1

  pin.listen(1000)
  >> 1
  >> 1
  >> 0

  pin.stopListen()

  def switchedEvent():
    print("Hey Hey !")

  pin.attachEvent("switch",switchedEvent)
  pin.listen()

  >>0
  >>0
  >>1 #lvl switched here
  >>"Hey Hey !"
  >>1
  >>0
  >>"Hey Hey !"
  ...

  pin.detachEvent()

  >>1
  >>0
  >>0
  >>1

  digPinA0 = DigPin(0, 'OUTPUT', analogic=True)
  digPinA0.write("HIGH")

```
*parent : [Obj](#object)*

A digital pin.

**digPin's event** :

Event | Description
------|------------
**switch** | The value from the digPin've changed
**on** | The value from the digPin is 1
**off** | The value from the digPin is 0

### DigPin(pin, Mode, analogic=False)
Setups your pin

* **pinNumber** : the number of the pin whose mode you wish to set
* **Mode** : the pin's behaviour 'OUTPUT' or 'INPUT'
* **analogic** : optional parameter, set *True* if the pin is a physical analog Pin

### mode(Mode)
Changes your pin's behaviour

* **Mode** : the pin's behaviour 'OUTPUT' or 'INPUT'

### write(Lvl)
Writes a HIGH or a LOW value to a digital pin. [go here](https://www.arduino.cc/en/Reference/DigitalWrite) for more
informations.

* **Lvl** : 'HIGH',1 or 'LOW',0

### analogWrite(value)
Writes an analog value (PWM wave) to the pin. Arduino's documentation
[here](https://www.arduino.cc/en/Reference/AnalogWrite)

* **value** : an integer between 0 and 255

### switch()
Switches the digital pin value 'LOW' to 'HIGH' or 'HIGH' to 'LOW'

### periodicSwitch(period)
Switches the pin value periodically

* **period** : in ms the interval between each switching, if is not set it'll be 100ms

### stopPeriodicSwitch()
Stop the pin's periodic switch

### read()
Reads the value from your pin, then saves the value into **digPin.\_lvl**

### listen(period)
Reads the value from your pin periodically

* **period** : in ms the interval between each reading, if is not set it'll be 100ms

### stopListen()
Stops the pin's listening

## AnaPin
```python
board=Board('/path/to/your/board')

analog= AnaPin(5,'INPUT')

analog.read()
analog.value
>> 455

def printValue(pin):
  print(str(pin._pin)+": "+str(pin.value))

analog.attachEvent("update",printValue,analog)
analog.listen()

>> "5: 455"
>> "5: 430"
>> "5: 432"
>> "5: 100"
...

```
*parent : [Obj](#object)*

[An analog pin](https://www.arduino.cc/en/Tutorial/AnalogInputPins).

**AnaPin's event** :

Event | Description
------|------------
**update** | anaPin have read a new value

### anaPin(pin, mode)
Setup the analog pin.

* **pin** : the analog pin number
* **mode** : the pin's behaviour 'OUTPUT' or 'INPUT'

### mode(mode)
Changes your pin's behaviour

* **mode** : the pin's behaviour 'OUTPUT' or 'INPUT'

### read()
Reads the value from the pin, then saves the value into **anaPin.value**.
more informations [here](https://www.arduino.cc/en/Reference/RobotAnalogRead)

### listen(period)
Reads the value from your pin periodically

* **period** : in ms the interval between each reading, if is not set it'll be 100ms

### stopListen()
Stops the pin's listening


## PPM
