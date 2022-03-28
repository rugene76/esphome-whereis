# esphome-whereis
Presence detection implemented using esphome and leveraging the
home assistant ibeacon feature in the android app

I'll get around to more completely documenting this project.

For now, 
This code provides presence detection using the home assistant app
as a ble beacon. I intend that the code be inserted into other esphome projects. The project is similar in function to the 
excellent esppresence project but allows esphome compatibility.

To install: 
1) In the homeassistant android app go to "Companion App"
          
     -select "Manage Sensors"

     -scroll to and select "BLE Traansmitter"

     -select "enabled" and "enable transmitter"

     -set "Transmitter power" to high

     -note the UUID for the beacon at the bottom of the page
     
2) in the home assistant configuration.yaml, paste in the configuration yaml snippet from this project. You may need to adjust it to your needs.
3) Drop the esphome-whereis.yaml code into your esphome project 
    
    -adjust the wifi parameters for your environment 
    
    -adjust the substitution values as needed, i.e., replace the ibeacon uuid, names, etc
    
4) Validate and install the esphome project into your ESP32 device
5) Back in Home assistant, be sure to configure the newly found esphome device in the integration page
6) create a lovelace card to observe the new entities

You should see your ibeacon device in one of three possible states:
1) not_home; this means the device is not detected at all
2) home; the device is detected by the signal has not reached the capture threshold
3) $roomname; e.g., "familyroom", the device has surpassed the rssi capture threhold

In home assistant, use the input_number entities to play with the proper values to get acceptable device detection.

The configuration.yaml snippet has a template sensor that attempts to combine all states from all nodes into a global state for the whole environment. Once several nodes are installed, you should be able to walk around your home and see the global state update as you move from node to node. At least that's what I'm going for. Seems to work well in my house with 5 nodes.

Of course the code can be improved, so suggestions are encouraged.
enjoy
