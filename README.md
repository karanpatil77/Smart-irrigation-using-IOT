# Smart Irrigation using IoT🤖

![Alt Text](https://github.com/karanpatil77/Smart-irrigation-using-IOT/blob/main/SmartIrrigation.gif)

BScIT final year project presenting an automatic irrigation system using IOT. 
The importance of building an automation system for an office, home or field is increasing day-byday. Automation makes an efficient use of the electricity, water and reduces much of the wastage.Smart water sprinkler irrigation system makes an efficient use of water for the growth of plants by which your indoor plant may never suffer the lack of water problems. 

## Requirents

**Hardware:** Raspberry Pi Zero w, Soil Moisture Sensor, DHT11 (Temperature/Humidity Sensor), 5V Relay, 3-6V Mini Micro Submersible Pump, 5v Power Supply (Any USB Cable+ USB Wall Charger), Flexible Water Line

**Programming Languages:** Python, Html, CSS

**Frameworks:** Flask(Python)

**OS:** Raspbian(linux), Windows

**Other:** Thingspeak API, IFTTT

## Circuit Diagram

<img src="https://github.com/karanpatil77/Smart-irrigation-using-IOT/blob/main/GPIO.jpg" alt="Circuit Diagram" width="700" height="300" align="center">


## Installation

Note: If you get the wiring exactly as described above, my code in the next section will work without any further modifications.

All files:
- water.py,
- web_plants.py,
- auto_water.py,
- temp.py
- main.html

Now lets get to the RPi terminal.

There are two parts to this setup. One file controls all the GPIO and circuit logic, and the other runs a local web server.

**GPIO Script**

Let's start with the code for controlling the GPIO. This requires the RPi.GPIO python library which can be installed on your Raspberry Pi as follows:

```bash
$> python3.4 -m pip install RPi.GPIO
```
With that installed, you should be able to use the water.py script found here.

You can test this is working correctly by running an interactive python session as follows:
```bash
$> python3.4
>>> import water
>>> water.get_status()
>>> water.pump_on()
```
This should print a statement about whether your sensor is wet or dry (get_status()), and also turn on the pump for 1s. If these work as expected, you're in good shape.

At this point you can also calibrate your water sensor. If your plant status is incorrect, try turning the small screw (potentiometer) on the sensor while it is in moist soil until the 2nd light comes on.

## Deployment

**Flask Webserver**

The next aspect of this project is to setup the web server. This code can be found here in a file called web_plants.py. This python script runs a web server enabling various actions from the script described above.

You will need to keep web_plants.py in the same directory as water.py described above, as well as auto_water.py. You will also need a sub-directory called "templates" containing the html file here called main.html.

You will need to install flask, and psutil as follows:
```bash
$> python3.4 -m pip install flask $> python3.4 -m pip install psutil
```
You will also need to create a sub-directory called templates, and place main.html in the templates directory.

Now run the following command command to start your web server:
```bash
$> sudo python3.4 web_plants.py
```
Now if you navigate to the ip address of your RPi, you should see a web dashboard something like this:

Try clicking the buttons to make sure everything works as expected! If so, you're off to the races.

here's another great tutorial I followed on flask + GPIO Run Website Automatically

Finally, you probably want the website to auto start when the RPi gets turned on. This can be done using a tool called cronjob, which registers your website as a startup command.

To do so, type:
```bash
$> sudo crontab -e
```
This will bring up a text editor. Add a single line that reads (and make sure to leave one empty line below):
```bash
@reboot cd <your path to web_plants>; sudo python3.4 web_plants.py
```    
Now when you reboot your pi, it should auto start the server.

## Optimizations

- Added functional Temperature/Humidity Sensor.
- Added CSS elements to the wen page to make it look a bit better.
- Added a toggle button to turn on/off the pump manually.
- Made use of thingspeak API to show live graphical visualizations of Temperature and Humidity.
- Used IFTTT to send an email whenever the temperature sensor reads more than 40°C. 

## Conclusion
- Using this system, one can save manpower, water to improve production and ultimately increase profit.
- The smart plant system is feasible and cost effective for optimizing water resources for agricultural production.
- The system would provide feedback control system which will monitor and control all the activities of irrigation system efficiently.

## Contributors

[@dalvitejs](https://www.github.com/dalvitejs)

## References

[Cyber Omelette](https://www.cyber-omelette.com/2017/09/automated-plant-watering.html)

## Feedback

If you have any feedback or queries, please reach out to us at kpatil3595@gmail.com
