# ha-meural
**Integration for Meural Canvas digital art frame in Home Assistant**  

The Netgear Meural Canvas is a digital art frame with both a local interface and a cloud API.  
Home Assistant is an open source home automation package that puts local control and privacy first.  
This integration leverages Meural's API and local interface to control the Meural Canvas as a media player in Home Assistant.  
# Installation
Copy this integration into your Home Assistant's custom_components folder and restart Home Assistant. Log in with your Netgear account when setting up the integration. The integration will detect all Canvas devices registered to your account. Each Canvas will become a Media Player entity and can be added to your Lovelace UI using any component that supports it, for example the default Media Control card.  

The integration supports built-in media player service calls to pause, play, go to next/previous track (artwork), select source (art playlist), set shuffle, turn on and turn off. Additional services built into this integration are:  
*meural.load_gallery*  
*meural.set_device_option*  
*meural.set_device_orientation*  
*meural.set_brightness*  
*meural.reset_brightness*  
These services are fully documented in services.yaml.

The current image displayed in the Media Control card is polled from the Meural API. The Canvas normally only syncs to the Meural API once every few hours, so the current displayed art is often out-of-sync with the Meural API. The integration forces a sync when a mismatch between the local current artwork and the remote current artwork is detected. Because of this the image displayed in Home Assistant will only have about 10 seconds of lag compared to local changes on your device.

# Meural API
Meural has an undocumented REST API that their mobile app and web-interface run on. This API has been reverse-engineered and crowdsourced documentation can be found here:  
https://documenter.getpostman.com/view/1657302/RVnWjKUL?version=latest

# Local Web Server
While Meural positions the mobile app as the main method to control the Canvas, they do refer to a 'remote controller' in their support documentation:  
https://kb.netgear.com/000060746/Can-I-control-the-Canvas-without-a-mobile-app-or-gesture-control-and-if-so-how  
This 'remote controller' is a local web server available at: http://LOCALIP/remote/  
It runs on a javascript available at: http://LOCALIP/static/remote.js

The available calls in this javascript are:  
*/remote/identify/*  
*/remote/get_galleries_json/*  
*/remote/get_gallery_status_json/*  
*/remote/get_frame_items_by_gallery_json/*  
*/remote/get_wifi_connections_json/*  
*/remote/get_backlight/*  
*/remote/control_check/sleep/*  
*/remote/control_check/video/*  
*/remote/control_check/als/*  
*/remote/control_check/system/*  
*/remote/control_command/boot_status/image/*  
*/remote/control_command/set_key/*  
*/remote/control_command/set_backlight/*  
*/remote/control_command/suspend*  
*/remote/control_command/resume*  
*/remote/control_command/set_orientation/*  
*/remote/control_command/change_gallery/*  
*/remote/control_command/change_item/*  
*/remote/control_command/rtc/*  
*/remote/control_command/language/*  
*/remote/control_command/country/*  
*/remote/control_command/als_calibrate/off/*  
*/remote/control_command_post/connect_to_new_wifi/*  
*/remote/control_command_post/connect_to_exist_wifi/*  
*/remote/control_command_post/connect_to_hidden_wifi/*  
*/remote/control_command_post/delete_wifi_connection/*  
*/remote/postcard/*  

First version of this integration built by [@balloob](https://github.com/balloob). All jury-rigged code added afterwards by [@guysie](https://github.com/guysie). I'm not a dev, so I apologize in advance for code quality.  