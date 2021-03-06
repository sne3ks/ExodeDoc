#Introduction

### Well, What is it ?
> Blink two led asynchronously

```python

from Exode import *
uno = Board('/dev/tty.HC-06-DevB')

led13 = Led(13)
led14 = Led(14)

uno.add(led13)
uno.add(led14)

led13.blink(250)
led14.blink(500)

```
Exode is a Python's library for communication between
Arduino microcontroller boards and a connected computer.
Write Python script and take control on your board using a serial IO.

### Fast and Intuitive

Exode was designed to simplify the development of Arduino projects. The library
takes advantages from the clear and light Python's syntax.

Once your Arduino connected to your device (computer, Rasberry Pi, smartphone ..)
using a serial IO (usb/bluetooth), you're now allowed to have remote interactions
with your board.

You microcontroller become a simple slave, let your computer process the most
complex tasks. You may add artificial intelligence algorithm in your projects...

### Powerfull tools


Many of Arduino components are implemented in Exode, that's way you can directly
manipulate them with Python.

Exode use event-driven programming to manage the interactions between the differents
components plugged on your board, or your computer.

Furthermore, the Exode's kernel is based on an asynchronous processes,
greatly simplifying your project !!

### User Interface

<p align="center"><img src="images/showcase.gif" ></p>

Interact with your board easily through UI components :

* Visualize data
* Send data
* Event-driven applications
