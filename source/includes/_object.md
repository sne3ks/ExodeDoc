# BoardObject
*parent : AbstractObj*

Each component connected to your board are represented by an abstract BoardObject.
All Exode's objects have theses utilities :

* Setup on the board
* Event manager
* Log system
* UI interface

## Setup on the board

### obj.on(board)
```python
board-0= Board('/path/to/your/board-0')

#There's only one board connected,
#obj1'll be setup on board-0
obj1=Led(13)
obj1.board
>> "Board-0"

board-1= Board('/path/to/your/board-1')

#There's two board connected, we've to specify on which board setup
#our obj
obj2=Led(13).on(board-1)

```
Setup obj on the board

* **board** : A board object

*If there's only one board connected, Exode will automatically call obj.on().
Else, if there's more than one board you've to call obj.on()*

## Event manager
```python
uno = Board('/path/to/your/board')

pin=DigPin(13,'OUTPUT')

def switcheCallback():
  print("Hey Hey !")

pin.attachEvent("switch",switcheCallback)
pin.listen()

>>0
>>0
>>1 #lvl switched here
>>"Hey Hey !"
>>1
>>0
>>"Hey Hey !"
...

pin.detachEvent("switch")

>>0
>>1
>>0

```

Event manager lets you add/delete callback functions associated with the object's events.
Theses functions will be call when their associated event is dispatched.  

### obj.attachEvent(event, callback, \*args)
The callback function with the given args will be executed when the event is dispatched.

* **event** : the event name
* **callback** : a function
* **args** : arguments used by the function

### obj.detachEvent(event)
Delete the callback function associated to the event

* **event** : the event name

## Log system
```python
uno = Board('/path/to/your/board')

pin=DigPin(13,'OUTPUT')
pin.log(" hello world !")

#in log file
>> "2016-04-06 19:13:47,408 - Exode.Core - DEBUG -"..
>> .. " OBJC - Board-0.digPin(13) hello world !"

```
Object can write a message in the log file

### obj.log(msg)
write a message in the log file

* **msg** : a string

## UI interaction
Board object can interact with UI component

### obj.setColor(color)
Change the ui object color

* **color** : an array of 4 numbers from 0 to 1 *(e.g. [0,1,0.3, 1] [r,g,b, a])*

### obj.getValue(name)
Return a value

* **name** : the value's name

### obj.setValue(value, name)
Update a value

* **value** : a value
* **name** : the name of the value to change

### obj.getUIXView()
Return a string representation of the object, styled with markdown

# DataObject

Mother class for object generating data. *(e.g. analog, E/R)*

### obj.setPlot(plot)
set a plot to the obj, data generating will be write on this plot.
