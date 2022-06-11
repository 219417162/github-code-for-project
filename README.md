# github-code-for-project
import RPi.GPIO as GPIO
GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)
import time

trigger_pin = 18
echo_pin = 24
buzzer = 3
led1 = 2

GPIO.setup(trigger_pin,GPIO.OUT)
GPIO.setup(echo_pin,GPIO.IN)
GPIO.setup(led1,GPIO.OUT)
GPIO.setup(buzzer,GPIO.OUT)



while True:
    GPIO.output(trigger_pin, False)

    time.sleep(1)

    GPIO.output(trigger_pin, True)
    time.sleep(0.01)
    GPIO.output(trigger_pin, False)

    while GPIO.input(echo_pin)==0:
        pulse_start=time.time()

    while GPIO.input(echo_pin)==1:
        pulse_end=time.time()

    pulse_duration=pulse_end-pulse_start

    distance = pulse_duration*11150
    distance = round(distance,2)

    if distance > 20:
        GPIO.output(buzzer, GPIO.HIGH)
        GPIO.output(led1, GPIO.LOW)
        print("no one in the room")
    else:
        print("someone in the room")
        GPIO.output(buzzer, GPIO.LOW)
        GPIO.output(led1, GPIO.HIGH)
