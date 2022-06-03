import RPi.GPIO as GPIO
import time


TRIG = 4
ECHO = 17
RED_LED = 26
pwm = None
INTERVAL = 5

def distanceInit():
	print('Distance Measurement In Progress')
	GPIO.setmode(GPIO.BCM)
	GPIO.setup(TRIG,GPIO.OUT)
	GPIO.setup(ECHO,GPIO.IN)


def distanceStart():
	
	GPIO.output(TRIG,True)
	time.sleep(0.00001)
	GPIO.output(TRIG,False)

	
	while GPIO.input(ECHO) == 0:
		pass
	pulse_start = time.time()

	
	while GPIO.input(ECHO) == 1:
		pass
	pulse_end = time.time()

	
	pulse_duration = pulse_end - pulse_start
	distance = pulse_duration * 17150
	distance = round(distance,2)
	
	return distance


def ledStart():
	global pwm
	GPIO.setup(RED_LED, GPIO.OUT)
	pwm = GPIO.PWM(RED_LED,60)
	
	
	pwm.start(0)
	for i in range(3):
		
		for i in range(101):
			
			pwm.ChangeDutyCycle(i)
			time.sleep(0.02)

		
		for i in range(100,-1,-1):
			pwm.ChangeDutyCycle(i)
			time.sleep(0.02)
	pwm.stop()


try:
	distanceInit()
	while True:
		distance = distanceStart()
		print("Distance:{}cm".format(distance))
		if distance < 10:
			ledStart()
		time.sleep(INTERVAL)
except KeyboardInterrupt:
	if pwm != None:
		pwm.stop()
	GPIO.cleanup()
