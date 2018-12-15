Edit: Add two timers:
- One 15 min timer so that the away is not immediately active.
- One "stop timer" to interrupt the 15 min waste timer.


# home aware with home assistant, nmap and node-red

<pre>

I used this great video as a guide: https://www.youtube.com/watch?v=SuoSXVqjyfc and changed it to work with nmap.



How to check if someone is at home

required:
- Home Assistant
- Node red with home assistant pallet (node-red-contrib-home-assistant-websocket)
- Wifi
- Reserved dhcp on mobiles (or static)
- 3 iphones (or less)


Edit configuration.yaml:
------------------------
# *************************************************************
# Start Device tracker scans devices en put them in know_devices.yaml
# *************************************************************
device_tracker:
#  - platform: ping
#    hosts:
#      iphjan: 192.168.10.20
  - platform: nmap_tracker
    hosts:
      - 192.168.10.20
      - 192.168.10.21
      - 192.168.10.23
    new_device_defaults:
      hide_if_away: false
#      track_new_devices: false
# interval_seconds: xx set the seconds to scan interval
    interval_seconds: 30
# home_interval: xx sets the minutes duration that a device
# is marked “Home” after it is found during a scan
#     home_interval: 10
# consider_home: xx Seconds to wait till marking someone as
# not home after not being seen. 3 minutes: 180, 0:03, 0:03:00
#    consider_home: 15
# *************************************************************
# End Device tracker scans devices en put them in know_devices.yaml
# *************************************************************

    
After restarting hass it will create a known_devices.yaml file
with MAC numbers in it.
If not, generate a empty file and restart hass.
After a while the MAC numbers will appear.

known_devices.yaml will looks like:
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
change the device_tracker.000000000000 to your own MAC numbers or click in de node settings
and get the device from Home Assistant.






<pre>

 
    
    
    
