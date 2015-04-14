# PROJECT MOVED! #

**9/13/2013: MOVED TO GITHUB:** https://github.com/mik3y/usb-serial-for-android

Please adjust your links; **no further updates are being made here**.

## . ##
## . ##
## . ##
## . ##
## . ##
## . ##

# Archive Below #

This is a driver library for communication with Arduinos and other USB serial hardware on Android, using the [Android USB Host API](http://developer.android.com/guide/topics/connectivity/usb/host.html) available on Android 3.1+.

No root access, ADK, or special kernel drivers are required; all drivers are implemented in Java.  You get a raw serial port with `read()`, `write()`, and other basic functions for use with your own protocols.

  * **Homepage**: http://code.google.com/p/usb-serial-for-android
  * **Google group**: http://groups.google.com/group/usb-serial-for-android
  * **Latest release**: v0.1.0 (November 13, 2012, see [CHANGELOG](http://usb-serial-for-android.googlecode.com/git/CHANGELOG.txt))

## Quick Start ##

**1.** Download [usb-serial-for-android-v010.jar](http://usb-serial-for-android.googlecode.com/files/usb-serial-for-android-v010.jar)

**2.** Copy the jar to your Android project's `libs/` directory. (See [Android's FAQ](http://developer.android.com/guide/faq/commontasks.html#addexternallibrary) for help).

**3.** Copy [device\_filter.xml](http://usb-serial-for-android.googlecode.com/git/UsbSerialExamples/res/xml/device_filter.xml) to your project's `res/xml/` directory.

**4.** Configure your `AndroidManifest.xml` to notify your app when a device is attached (see [Android USB Host documentation](http://developer.android.com/guide/topics/connectivity/usb/host.html#discovering-d) for help).

```
<activity
    android:name="..."
    ...>
  <intent-filter>
    <action android:name="android.hardware.usb.action.USB_DEVICE_ATTACHED" />
  </intent-filter>
  <meta-data
      android:name="android.hardware.usb.action.USB_DEVICE_ATTACHED" 
      android:resource="@xml/device_filter" />
</activity>
```

**5.** Use it! Example code snippet:

```
// Get UsbManager from Android.
UsbManager manager = (UsbManager) getSystemService(Context.USB_SERVICE);

// Find the first available driver.
UsbSerialDriver driver = UsbSerialProber.acquire(manager);

if (driver != null) {
  driver.open();
  try {
    driver.setBaudRate(115200);
    
    byte buffer[] = new byte[16];
    int numBytesRead = driver.read(buffer, 1000);
    Log.d(TAG, "Read " + numBytesRead + " bytes.");
  } catch (IOException e) {
    // Deal with error.
  } finally {
    driver.close();
  } 
}
```

For a more complete example, see the [UsbSerialExamples code](http://code.google.com/p/usb-serial-for-android/source/browse/#git%2FUsbSerialExamples) in git, which is a simple application for reading and showing serial data.

A [simple Arduino application](http://code.google.com/p/usb-serial-for-android/source/browse/#git%2Farduino) is also available which can be used for testing.

## Compatible Devices ##

  * **Serial chips:** FT232R, CDC/ACM (eg Arduino Uno) and possibly others.  See CompatibleSerialDevices
  * **Android phones and tablets:** Nexus 7, Motorola Xoom, and many others. See CompatibleAndroidDevices.


## Author, License, and Copyright ##

usb-serial-for-android is written and maintained by **mike wakerly**.

This library is licensed under **LGPL Version 2.1**.  Please see LICENSE.txt for the
complete license.

Copyright 2011-2012, Google Inc. All Rights Reserved.

Portions of this library are based on libftdi
(http://www.intra2net.com/en/developer/libftdi).  Please see
FtdiSerialDriver.java for more information.

## Help & Discussion ##

Please join our Google Group, [usb-serial-for-android](https://groups.google.com/forum/?fromgroups#!forum/usb-serial-for-android) (also linked at left).

Are you using this library? Let us know and we'll add your project to ProjectsUsingUsbSerialForAndroid.


## Contributing ##

Patches are welcome.  We're especially interested in supporting more devices.
Please see ContributingToUsbSerialForAndroid for more information.