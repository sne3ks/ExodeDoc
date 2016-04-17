#Sensor

## Ultrasonic sensor HCSR04
```python
board=Board('/path/to/your/board')

sensor= HCSR04(echo=11, trig=12)

def printValue(obj):
    print(obj.cm+" cm")

sensor.attachEvent('update', printValue, sensor)
sensor.read()

>> 23.0 cm

sensor.read(100)
>> 20.5 cm
>> 20.9 cm
>> 34.5 cm
...
sensor.stopRead()

```
<p align="center"><img src="https://brainy-bits.com/wp-content/uploads/2014/12/schematic-HCSR04.png" ></p>
[HCSR04 datasheet](https://docs.google.com/document/d/1Y-yZnNhMYy7rwhAgyL_pfa39RsB-x2qR4vP8saG73rE/edit)

**HCSR04's event** :

Event | Description
------|------------
**update** | the sensor've read a new value

###HCSR04(echo, trig)
Init a HCR04 sensor.

* **echo** : the Echo's pin number
* **trig** : the Trig's pin number

###read(period)
Read the distance of the nearest object by bouncing soundwaves off of it

* **period** : the period between each readings, if is not set (or equal to 0), the HCSR04'll read only one time.

###stopRead()
Stop the reading from the HCSR04

###HCR04.cm
The distance of the nearest object (cm) (updated during the last reading)

*cm= round(duration/58.2, 2) calculate with the speed of sound*

###HCR04.duration
Width (ms) of the last Echo pulse

*read the datasheet for more informations**
