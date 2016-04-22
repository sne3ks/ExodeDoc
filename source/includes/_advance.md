#Advanced usage

## How it works ?

### How Exode send instructions ?

Exode sends byte arrays to the Arduino Board. Each array represents **an instruction**.
Byte arrays are constructed on this pattern

Byte position | Description
------------|------------
  **0**   | The instruction's length
  **1**   | The instruction's id
  **2 .. n** | The instruction's operands

When the board receives a byte array, the board will decode and execute it.

For example, here the byte array to write a 'HIGH' level on the pin 13

Byte position | Value |Description
------------|-------|---------
  0   | **\x03** |The instruction's length
  1   | **\x01** |The instruction's id
  2   | **'\r'** | pin 13
  3   | **'\x01'** | 'HIGH' *(or 1)*


### How Exode receive values ?

<aside class="warning">
  For the moment, exodeArduinoCore can only send unsigned int coded on 4 bytes with a little endian
</aside>

Some instructions wait from the board an answer, for example, digPin.read().
Exode works on an asynchronous process, that's why the answers don't come in the same
order than their request. To identify the request who is associated the incoming
answer, Exode uses a **key system**.

For example, here the byte array to read the pin 13 level

Byte position | Value |Description
------------|-------|---------
  0   | **\x03** |The instruction's length
  1   | **\x02** |The instruction's id
  2   | **'\r'** | pin 13
  3   | **'\x07'** | the key (here 7)

Board will answer

Byte position | Value |Description
------------|-------|---------
  0   | **\x07** |The instruction's key
  1   | **\x01** | the answer
  2   | **\x00** |
  3   | **\x00** |
  4   | **\x00** |


## Board's instructions
```python
  uno = Board('/path/to/your/board')

  #Example to turn-on a led using instructions
  uno.pinMode(13, "OUTPUT")
  uno.digitalWrite(13, "HIGH")

```

Here the full list of board's instructions

ID | Name | Description | Operands | Answer
---|------|-------------|----------|-------
0  | **pinMode(pin, mode, analogic=False)** | setup a pin | **pin**: pinNumber <br> **mode**: 1 or 0 (OUTPUT or INPUT) <br> **analogic**: if it's an analogic pin |
1  | **digitalWrite(pin, lvl)** | write a digital Value on a pin | **pin**: pinNumber <br> **lvl**: 1 or 0 (HIGH or LOW) |
2  | **digitalRead(pin, key)** | read a pin lvl | **pin**: pinNumber <br> **key**: request's key | *the pin lvl*
3  | **digitalSwitch(pin)** | switch a pin lvl | **pin**: pinNumber |
4  | **analogWrite(pin, value)** | write an analog value | **pin**: pinNumber <br> **value** : [0, 255] |
5  | **analogRead(pin, key)** | read the value on an analog pin | **pin**: Analogic pin number <br> **key**:  request's key | *the pin value*
6  | **addPPM(pin, us, key)** | init a PPM signal | **pin**: pin Number <br> **us** : signal value (us) <br> **key** : request's key | *the signal id*
7  | **removePPM(id)** | stop a PPM signal | **id**: the signal id |
8  | **writePPM(id, us)** | new PPM value | **id** : the signal id <br> **us** : signal value (us) |
9  | **pulse(pin ,us)** | send a pulse on a pin | **pin** : pin Number <br> **us** : pulse length (us) |
10 | **pulseIn** | read a pulseIn on a pin | **pin** : pin Number <br> **key** : request's key | *the pulse length*
14 | **reset** | reset the board | | |
15 | **checkExode** | check if exode is installed on the board | | *404 with the request's key 202*



## Listener
> Here a code to read a digital input

```python
uno = Board('/path/to/your/board')

# We setup the pin13
uno.pinMode(13, "INPUT")

# Define a callback function
def printLvl(value):
  print("the value on the pin is : "+str(value))

# Get a key
requestKey= uno.getKey()

# Init the listener and read the pin
uno.addListener(updateFunction=printLvl, key=requestKey)
uno.digitalRead(13, requestKey)

>> "the value on the pin is : 0"

```

To receive date from the board, Exode uses Listener. A Listener listens to the incoming data, when a value comes
with the excepted key, the listener will call a callback function with the incoming value as argument.

###Board.addListener(updateFunction, key, isInfinite=False)
To init a Listener on the board

* **updateFunction** : the callback function, call when board receive the excepted value
* **key** : the request's key
* **isInfinite** : indicate if we listen the board indefinitely or only once

###Board.getKey(self, excpt=[])
Return a available key

* **excpt** : optional, a list of value to be excluded


## boardThread
> Example of boardThread to read a value with the HCSR04 sensor

```python

uno = Board('/path/to/your/board')

# Setup trig(2) and echo(3) pin
uno.pinMode(2, 'OUTPUT')
uno.pinMode(3, 'INPUT')

# requestKey
readKey= uno.getKey()

# Init a thread
readThread= uno.newThread()
readThread.add("pulse", 2, 10)
readThread.add("pulseIn", 3, readKey)

# Prepare the listener
def printValue(value):
  print("duration : "+value)

board.addListener(key=readKey, updateFunction=printValue, isInfinite= True)

# Launch the thread every 1s
readThread.start(1000)

>> duration : 1455
>> duration : 3455
>> duration : 3234
...

readThread.stop()
```

Some instructions have to be call consecutively or to be repeated at regular intervals.
A BoardThread is a block of instructions load on the board, that will be executed consecutively
and/or at regular intervals

###Board.newThread()
Init a new thread on the board

###boardThread.add(name, \*args)
Add an instruction to the boardThread

* **name** : the instruction's name
* **args** : the instruction's arguments

###boardThread.start(period=0)
Start the thread

* **period** : the time period (ms) between each thread executions, if is not set or equal to 0 the thread will be
execute only once.

###boardThread.stop()
Stop the thread
