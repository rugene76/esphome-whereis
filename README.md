# esphome-whereis
Presence detection implemented using esphome and leveraging the
home assistant ibeacon feature in the android app

I'll get around to more completely documenting this project.
Note, the coding is brute force but it works good enough. Improvements to make the code more generic are encouraged.

For now, 
This code provides presence detection using the home assistant app
as a ble beacon. I intend that the code be inserted into other esphome projects. The project is similar in function to the 
excellent espresence project but allows esphome compatibility.

To install: 
1) In the homeassistant android app go to "Companion App"
          
     -select "Manage Sensors"

     -scroll to and select "BLE Traansmitter"

     -select "enabled" and "enable transmitter"

     -set "Transmitter power" to high

     -note the UUID for the beacon at the bottom of the page
     
2) In the home assistant configuration.yaml, paste in the configuration yaml snippet from this project. You will need to adjust the names and nodes to suit your needs.
3) Drop the esphome-whereis.yaml code into your esphome project 
    
    -adjust the wifi parameters for your environment 
    
    -adjust the substitution values as needed, i.e., replace the ibeacon uuid, names, etc
    
4) Validate and install the esphome project into your ESP32 device
5) In home assistant, be sure to configure the newly found esphome device in the integration page
6) Create a lovelace card to observe and adjust the input_number entities

You should see your ibeacon device (Where is John) in one of three possible states:
1) not_home; this means the device is not detected at all
2) home; this means the device is detected but the signal has not reached the capture threshold
3) $roomname; e.g., "familyroom", this means the device has surpassed the rssi capture threhold

In home assistant, use the input_number entities to get acceptable device detection by adjusting the rssi thresholds.

The configuration.yaml snippet has a template sensor that attempts to combine all states from all nodes into a global state for the whole environment. Once several nodes are installed, you should be able to walk around your home and see the global state update as you move from node to node. At least that's what I'm going for. Seems to work well in my house with 5 nodes.

Of course the code can be improved, so suggestions are encouraged.
enjoy
