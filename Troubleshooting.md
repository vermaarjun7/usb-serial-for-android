# Introduction #

This is a collection of FAQ-style troubleshooting tips.

If your problem isn't covered here, or you'd like to suggest a new addition, please use the mailing list (linked at left).  We do not read the wiki comments.




## I am using a custom ROM or older Android build and nothing works. ##

Stop right there; this project probably isn't for you.

usb-serial-for-android only supports devices which comply with the [Android USB Host API](http://developer.android.com/guide/topics/connectivity/usb/host.html).  For a partial list of compatible devices, see CompatibleAndroidDevices.


## How do I access `/dev/ttyUSB0`? ##

You don't; see previous question.  `/dev/tty*` is the Linux kernel's driver interface to various serial devices.  Certain devices and custom ROMs **may** expose serial devices this way, but this library does not use this interface.


## I am using an Arduino Uno, Sparkfun Pro Micro, or other Arduino and "if (Serial)" doesn't work. ##

Some Arduinos use the DTR line to determine serial channel readiness.  In your Android code, call `setDTR(true);`