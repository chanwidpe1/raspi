import time 
import Adafruit_DHT
import datetime
Sensor = Adafruit_DHT.DHT11
GPIO = 17
h=0
t=0
while True:
    humidity, temperature = Adafruit_DHT.read_retry(Sensor,GPIO)
    if humidity is not None and temperature is not None:
        #print('Temp={0:0.1f}*C Humidity={1:0.1f}%'.format(temperature,humidity))
        h=humidity
        t=temperature
    else:
        print('Failed to get reading. Try again!')
    date=datetime.datetime.now()
    with open("Logger.txt", "a") as text_file:
        text_file.write("DetaTime: %s Humid: %.2f %% Temp: %.2f C\n" % (date.strftime("%Y-%M-%d : %H:%M:%S"),h,t))
        print("DetaTime: %s Humid: %.2f %% Temp: %.2f C" % (date.strftime("%Y-%M-%d : %H:%M:%S"),h,t))
    time.sleep(10)
