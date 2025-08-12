All you need is a serial terminal emulator that supports Xmodem file transfer protocol. I downloaded ExtraPuTTY from SourceForge for free. I used Windows but there are builds for most common operating systems.

You will need a Philips Head #00 screwdriver to remove the dongle from the case.

With the dongle popped out of the case and plugged into your USB extension cable start ExtraPuTTY and make these changes to the default settings:

1 - On the first screen (Session) click Serial first to set up for serial communications.
* Find the COM port from Windows Device Manager (have this open when you before installing the Dongle and beside ExtraPuTTY on your screen. For me it comes up as COM12
* Set the speed to 115200
* From the Serial Side Menu, select Flow Control NONE (Disable DTS/RTS)
* Back to the sessions, save this if you want to reuse it as ZDongle
  
Click Open to start the serial session with your ZDongle-E
* Boot the ZDongle into configure mode:
** Instead of trying to press the tiny buttons with two fingers, just roll your thumbnail across the two buttons, outside in. All-in-one-motion you’ll press and hold Reset, press and hold Boot, release Reset, and release Boot. You should get the menu

Press return and you should be presented with a short 3 option menu

Option 1 - Load, the ZDongle-E goes into a loading state, awaiting you to send the firmware.
* File Transfer Menu at top of Screen, and then XMODEM Send. Select Router Firmware.

Once that is done, the menu returns

Option 2 - Run
* This restarts the ZDongle-E and puts it into pairing mode. The LED should be Green.
* Put it back into it's case and it's ready to be discovered in Home-Assistant.

