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

## Led
```python
uno = Board('/dev/tty.HC-06-DevB')

led13 = Led(13)
led14 = Led(14)

uno.add(led13)
uno.add(led14)

led13.blink(250)
led14.blink(500)
```
*parent : [DigPin](#digital)*

inherit all methods from digPin

### Led(pin)
Setup a Led

* **pin** : the pin number

### blink(period)
Init a blink on the led

* **period** : the blink period

### stopBlink()
Stop blink

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


## ppmPin
```python
board=Board('/path/to/your/board')

ppm= ppmPin(15)
ppm.write(1500)

delay(1000)
ppm.stop()
```
*parent : [Obj](#object)*

more informations about **ppm signal** [here](http://skymixer.net/electronics/84-rc-receivers/78-rc-ppm-signal)

### ppmPin(pin, us=1500)
Setup a ppm signal on the Pin

* **pin** : the pin number
* **us** : the value (us), if not set the default value'll be 1500

### write(us)
Change the ppm value

* **us** : the value (us)

### stop()
Stop the ppm signal on the pin
