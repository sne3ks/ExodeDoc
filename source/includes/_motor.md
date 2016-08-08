#Motor

##Servo motor
```python
board= Board('/path/to/your/board-0')

servo= Servo(7)
servo.write(100)
servo.writeUs(1900)
servo.detach()

dangerousServo= Servo(8)
dangerousServo.secure(minAngle=75, maxAngle=105)
dangerousServo.calibrate(zeroUs=1500, angleToUs=7)
dangerousServo.write(100)

```

<p align="center"><img src="images/servo.png"><p>

*parent : [ppmPin](#ppmpin)*

### Servo(pin, angle=90, minAngle=0, maxAngle=180, zeroUs=1000, angleToUs=5.5555)
Setup a servo

* **pin** : the Servo's pin
* **angle** : servo's angle, default is 90
* **min/max Angle** : min/max Angle for your servo, defaults are 0 and 180
* **zeroUs** : the value in us of the angle 0° of your servo , default is 1000
* **angleToUs** : the value in us of 1° angle

### secure(minAngle=0, maxAngle=90)
Secure your servo setting the min/max value

* **min/max Angle** : min/max Angle for your servo, defaults are 0 and 180


### calibrate(zeroUs=1000, angleToUs=5.555)
Calibrate your servo

* **zeroUs** : the value in us of the angle 0° of your servo , default is 1000
* **angleToUs** : the value in us of 1° angle

### detach()
Detach your servo from its pin (stop the ppm)

### write(angle)
Write an angle on your servo

* **angle** : servo's angle

### writeUs(us)
Change the ppm signal value on the pin

* **us** : the value (us) of the ppm signal

##L298N Motor

```python
board= Board('/path/to/your/board-0')

motor=L298N_MOTOR(DC=8, IN1=7, IN2=6)
motor.runForward() # Motor run forward power 50%

motor.setSpeed(100) # Motor run forward power 100%
motor.stop() # Motor stop

motor.setSpeed(10) # Set the power to 10%
motor.setDirection('backward') # Set the direction on backward
motor.run() # Motor run backward power 10%


```
<p align="center"><img src="http://www.electromonde.com/image/data/composants2/schema%20ciruit%20lm298.png" ><p>

### L298N_MOTOR(DC, IN1, IN2, speed=50)
*parent : [BoardObject](#boardobject)

Setup a motor on the L298N

* **DC** : DC pin number
* **IN1** : IN1 pin number
* **IN2** : IN2 pin number
* **speed** : the motor's percentage of power (by default it's 50%)

### setSpeed(value)
Change the motor's speed

* **speed** : the motor's percentage of power (by default it's 50%)

### setDirection(value)
Change the motor direction

* **value** : 'forward'/1 or 'backward'/-1

### switch()
Switch the motor direction

### runForward()
Run forward the motor

### runBackward()
Run backward the motor

### run()
Run the motor with the last direction given

### stop()
Stop the motor
