# Arduino BLE Support
As part of this Github project, we provide libraries for Bluetooth Low Energy (BLE) for the ESP32 Arduino environment.  Support for this capability is still in the process of being cooked (as of September 2017).  As such you should not build product based on these functions as changes to the API and implementation are extremely likely over the next couple of months.

That said, we now have the ability to produce a driver you can use for testing.  This will give you early access to the function while give those who choose to build and maintain the code early feedback on what works, what doesn't and what can be improved from a usage perspective.

When complete, the BLE support for ESP32 Arduino will be available as a single ZIP file.  The file will be called **ESP32_BLE.zip**.  It is this file that will be able to be imported into the Arduino IDE from the `Sketch -> Include Library -> Add .ZIP library`.  When initial development of the library has been completed, this ZIP will be placed under some form of release control so that an ordinary Arduino IDE user can simply download this as a unit and install.

A build of the BLE support for Arduino can be found through the Arduino IDE.  Visit Sketch -> Include Library -> Manage Libraries.  In the library filter, enter "esp32 ble arduino".  The search will narrow and you should see "ESP32 BLE Arduino" available for installation or upgrade.



Should you wish to build your own instance of the ZIP from the source, here is the recipe.

1. Create a new directory called `build`
2. Enter that directory and run `git clone https://github.com/nkolban/esp32-snippets.git`
3. Change into the directory called  `./esp32_snippets/cpp_utils`
4. Run `make -f Makefile.arduino build_ble`
5. Change into the directory called `./Arduino`

And here you will find the `ESP32_BLE.zip` that is build from the latest source.  You can then install this into your Arduino IDE environment are you are ready to go.


## Installing a new version
If you have previously installed a version of the Arduino BLE Support and need to install a new one, follow the steps above to build yourself a new instance of the `ESP32_BLE.zip` that is ready for installation.  I recommend removing the old one before installing the new one.  To remove the old one, find the directory where the Arduino IDE stores your libraries (on Linux this is commonly `$HOME/Arduino`).  In there you will find a directory called `libraries` and, if you have previously installed the BLE support, you will find a directory called `ESP32_BLE`.  Remove that directory.

## Switching on debugging
The BLE support contains extensive internal diagnostics which can be switched on by editing the file called `sdkconfig.h` and finding the lines which read:

```
#define CONFIG_LOG_DEFAULT_LEVEL 1
```

Change this to:

```
#define CONFIG_LOG_DEFAULT_LEVEL 5
```

and rebuild/deploy your project.

This file can be found in your Arduino IDE installation directories at:

```
<ArduinoIDE>/hardware/espressif/esp32/tools/sdk/include/config
```

## Decoding an exception stack trace
While using the BLE C++ classes there is always the unfortunate possibility that something will go wrong and your application crash.  Fortunately, this results in some debug information being logged to the console.  This is known as a *stack trace*.   Included in the stack trace are a sequence of hexadecimal numbers known as the *back trace* which are the list of addresses of functions that were executed just before the crash was detected.  If we could decode these we would have a lot of great information that could be used to aid in the resolution.   Fortunately there is a fantastic project that makes decoding this information very easy indeed.

This project can be found here:

https://github.com/me-no-dev/EspExceptionDecoder

If you start to encounter crashes in your BLE C++ applications and wish to report these through Github issues, please help us to help you by installing this tool int your Arduino IDE and including the decoded information in the issue report.
