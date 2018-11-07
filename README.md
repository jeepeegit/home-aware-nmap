# home assistant-aware-nmap


(Click on raw for readability)


I used this video as a guide: https://www.youtube.com/watch?v=SuoSXVqjyfc and changed it to work with nmap



How to check if someone is at home

Need:
- Home Assistant
- Node red with home assistant pallet (node-red-contrib-home-assistant-websocket)
- Wifi
- Reserved dhcp on mobiles (or static)
- 3 iphones (or less)


Edit configuration.yaml:
------------------------
device_tracker:
  - platform: nmap_tracker
    hosts:
      - 192.168.1.20
      - 192.168.1.21
      - 192.168.1.23

input_boolean:
  home_occupied:
    name: Home occupied
    initial: off
    icon: mdi:home
    
After restarting hass it will create a known_devices.yaml file
with MAC numbers.
If not generate a empty the file and restart hass
After a while the MAC numbers will appear.

known_devices.yaml:
-------------------

# Jan Iphone 6
000000000000:
  hide_if_away: false
  icon:
  mac: 00:00:00:00:00:00
  name: j6-000000000000
  picture:
  track: true
  
# more iphones ....
  
  
the rest goes with node-red:
----------------------------
copy / paste the content (in home-aware-nmap-nodered.txt) in node-red.
change the device_tracker.000000000000 to your own MAC numbers or click in de node settings and get the device form Home Assistant.



 
    
    
    
