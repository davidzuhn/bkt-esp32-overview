# The Blue Knobby Throttle

The Blue Knobby Throttle is designed to be an "operator's throttle" for all DCC systems.   By use of the WiThrottle protocol, this throttle is usable on all systems supported by [JMRI] and the WiThrottle protocol (this is the same mechanism used by [WiThrottle] and [Engine Driver][enginedriver]).  

This throttle is inspired by devices like the [UT-4] from [Digitrax] and the [Cab06] from [NCE].  I find them easy to use from one hand (which is good, because when I'm operating I've got one hand on a throttle, one on the switch list, and one more using the uncoupling skewer).   

There are a few things that I've thought were missing in the operator throttle experience.

 - Reliability is key.  There is no reason why wireless protocols used today should permit control events to be missed.  When you flip the direction switch, it should work.   Period.  
 - Bandwidth sharing.   There's no reason that train shows with modular layouts shouldn't be able to use wireless throttles.  By using well-known protocols like WiFi, different groups should be able to share radio frequencies without interfering with each other.
 - Easy Brake operation.   I like the braking functions that many new decoders provide.  But I find using them with current throttles to be less than fully satisfying.  The function is usually mapped to someplace that's not particularly easy to access (see discussion of one-handed operations).  Worse yet, it's hard to tell if the brakes are set.  Crank the throttle, and nothing happens.   Why not?  Try again.  Oh wait, the brake is on.  Release brake and try again.
 - Rechargable batteries.   Modern electronic devices should have built-in rechargable batteries and use standard ways to recharge them.  The battery should be able to last through an entire op session without 


##  Phone Throttles

I like the idea behind the phone-based throttle apps.  Using WiFi for communications solves the bandwidth sharing issue, and enables the use of TCP connections to ensure lossless wireless communications (which supports reliability).  BUT I find the use of a phone problematic during an op session.  I don't find it easy to operate one handedly, and when (not if) I drop the throttle (count the number of hands I use), I'd rather not it be an expensive device with a big sheet of glass.

Plus, I like a tactile feedback.  The direction switch should indicate the actual direction of travel.  I like a knob for speed.   There's little on the phone apps which provide that feedback.   To me, the UT-4 is an excellent design for physical interaction -- it's easy to hold in one hand and flip the direction switch and change the speed knob.   Wouldn't it be nice to combine the two concepts?
 
## The BKT-1

The first design used an [nRF52] chip from Nordic Semiconductor.  This chip used Bluetooth Low Energy (aka BLE) for communications and an ARM Cortex M4 processor for the code.  This throttle uses a [Serpac] [M6 case] (also used by the UT-4).  An illuminated button is close to the speed knob and is intended to serve as the brake control.   Four other buttons are provided below that.  Each button lights up when the associated function is active.   

Along with the throttle is an [iOS] app.  The throttle communicates with the app using BLE.  The app communicates upstream to JMRI using Wifi.   This lets me use the phone for things it's good at (like entering in WiFi network names & passwords) and the throttle for the things it's good at (tactile control).

You use the app to set up the WiFi information, and to select the locomotive address to use.  You can select from the roster list or enter in the address manually.   Once you've done that, you're done with the phone and you can use the throttle.  Keep the phone in your pocket, since the effective range between the phone and the throttle is probably smaller than the layout room.   WiFi from the phone will handle the longer-distance communications needed for a layout of any size.

The lithium-polymer (LiPo) battery in the throttle can be charged via the Micro-USB connection.  Using a 2000 mAH battery, the device will run for about 10 days (before using any power conservation techniques).   

This plan, however, ran into a small hitch.  After the phone sits in your pocket for a bit, the power-saving mechanisms within the phone closes the network connections and all control is lost.   This makes the throttle useless after about 5 minutes.   


## ESP32 - A New Hope

Since the phone cannot serve as an intermediate gateway, the next best choice is to use the phone to set up the throttle, and let the throttle manage the WiFi connection.  That can't work on the nRF52, since it doesn't do WiFi.  I looked at the ESP8266 chip, which does WiFi, but it doesn't have BLE.  Then along comes the ESP32 processor.  It contains radio support for both WiFi and Bluetooth Low Energy.  It's inexpensive.  It's reasonably well documented (unlike earlier ESP processors).  It's supported by the Arduino community.  

ESP32 boards are readily available for development & testing.  I've mostly been using the [Adafruit] [Huzzah32][Huzzah-32] board, which works very well on a breadboard.   

# BKT-ESP32

The next generation throttle design is in progress.  It's been built and tested on a breadboard.  


### Todos

 - Write MORE Tests
 - Add Night Mode

License
----

Creative Commons [CC-BY-SA 4.0][CCBYSA]   ![CCBYSA](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)
Open Source Hardware License

**Free Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [jmri]: <http://jmri.org/>
   [WiThrottle]: <http://www.withrottle.com/html/home.html>
   [enginedriver]: <https://enginedriver.mstevetodd.com/>
   [UT-4]: <http://www.digitrax.com/products/throttles/ut4/>
   [Digitrax]: <http://www.digitrax.com/>
   [Cab06]: <https://ncedcc.zendesk.com/hc/en-us/articles/200552679-Cab06pr>
   [NCE]: <http://www.ncedcc.com/>
   [Serpac]: <http://www.serpac.com/>
   [M6]: <http://www.serpac.com/m6.aspx>
   [iOS]: <https://www.apple.com/ios/>
   [nRF52]: <https://www.nordicsemi.com/Products/Low-power-short-range-wireless/nRF52832>
   [ESP32]: <https://www.espressif.com/en/products/hardware/esp32/overview>
   [Adafruit]: <https://www.adafruit.com/>
   [Huzzah32]: <https://www.adafruit.com/product/3405>
   
   [CCBYSA]: <http://creativecommons.org/licenses/by-sa/4.0/>
   