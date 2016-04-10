#Pin
*[Arduino's official tutorial about pins](https://www.arduino.cc/en/Tutorial/DigitalPins)*
## Digital Pin
```python
  uno = Board('/path/to/your/board')

  pin=DigPin(13,'OUTPUT')
  pin.write('HIGH')
  pin.switch()

  pin.periodicSwitch(500)
  pin.stopPeriodicSwitch()

  pin.mode('INPUT')
  pin.read()
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



```
### DigPin(pin, Mode)
Setups your pin

* **pinNumber** : the number of the pin whose mode you wish to set
* **Mode** : the pin's behaviour 'OUTPUT' or 'INPUT'

### .mode(Mode)
Changes your pin's behaviour

* **Mode** : the pin's behaviour 'OUTPUT' or 'INPUT'

### .write(Lvl)
Writes a HIGH or a LOW value to a digital pin. [go here](https://www.arduino.cc/en/Reference/DigitalWrite) for more
informations.

* **Lvl** : 'HIGH',1 or 'LOW',0

### .swith()
Switches the digital pin value 'LOW' to 'HIGH' or 'HIGH' to 'LOW'

### .periodicSwitch(period)
Switches the pin value periodically

* **period** : in ms the interval between each switching, if is not set it'll be 100ms

### .stopPeriodicSwitch()
Stop the pin's periodic switch

### .read()
Reads the value from your pin

### .listen(period)
Reads the value from your pin periodically

* **period** : in ms the interval between each reading, if is not set it'll be 100ms

### .stopListen()
Stops the pin's listening

### .attachEvent(event, callback, args)
The callback function will be executed when the given event is dispatched

* **event** : the event's name "switch","on","off"
* **callback** : a callback function
* **args** : a list of arguments

### .detachEvent(event)
Remove the callback function on the given event

* **event** : the event's name "switch", "on", "off"

## analog

## ppm
