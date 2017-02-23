ArduinoLog - C++ Log library for Arduino devices
====================

*An small Logging library for embedded systems.*

ArduinoLog is a minimalistic framework to help the programmer output log statements to a variety of output targets, fashioned after xtensive logging libraries such as log4cpp ,log4j and log4net. In case of problems with an application, it is helpful to enable logging so that the problem can be located. ArduinoLog is designed so that log statements can remain in the code with minimal performance cost. In order to facilitate this the loglevel can be adjusted, and if the code is completely tested all logging code can be compiled out. 

## Features

* Different log levels (Error, Info, Warn, Debug, Verbose )
* Supports multiple variables
* Supports formatted strings 
* Supports formatted strings from flash memeory
* Fixed memory allocation (zero malloc)
* MIT License

## Tested for 

* All Arduino boards (Uno, Due, Mini, Micro, Yun...)
* ESP8266

## Downloading

This package has not yet been published to the Arduino & PlatformIO package managers and can therefore only be downloaded from GitHub. 

- By directly loading fetching the Archive from GitHub: 
 1. Go to [https://github.com/thijse/Arduino-Log](https://github.com/thijse/Arduino-Log)
 2. Click the DOWNLOAD ZIP button in the panel on the
 3. Rename the uncompressed folder **Arduino-Log-master** to **Arduino-Log**.
 4. You may need to create the libraries subfolder if its your first library.  
 5. Place the **Arduino-Log** library folder in your **<arduinosketchfolder>/libraries/** folder. 
 5. Restart the IDE.
 6. For more information, [read this extended manual](http://thijs.elenbaas.net/2012/07/installing-an-arduino-library/)


##Quick start

```c++
    Serial.begin(9600);
    
    // Initialize with log level and log output. 
    Log.begin(LOG_LEVEL_VERBOSE, &Serial);
    Log.info    (  "Log as Info with integer values : %d, %d"CR                  , 34,  799870);   
```

[See JsonParserExample.ino](examples/Log/Log.ino)

## Usage

### Initialisation

The log library needs to be initialized with the log level of messages to show and the log output. The latter will often be the Serial interface.
Optionally, you can indicate whether to show the log type (error, debug, etc) for each line.

```
begin(int level, Print* logOutput, bool showLevel)
begin(int level, Print* logOutput)
```

The loglevels available are

```
* 0 - LOG_LEVEL_SILENT     no output 
* 1 - LOG_LEVEL_FATAL      fatal errors 
* 2 - LOG_LEVEL_ERROR      all errors  
* 3 - LOG_LEVEL_WARNING    errors, and warnings 
* 4 - LOG_LEVEL_NOTICE     errors, warnings and notices 
* 5 - LOG_LEVEL_VERBOSE    all 
```

example

```
    Log.begin(LOG_LEVEL_ERROR, &Serial, true);
```

if you want to fully remove all logging code, uncomment `#define DISABLE_LOGGING` in `ArduinoLog.h`, this may significantly reduce your sketch/library size.

### Log events

The library allows you to log on different levels by the following functions

```
void error  (const char *format, va_list logVariables); 
void debug  (const char *format, va_list logVariables);
void error  (const char *format, va_list logVariables);
void verbose(const char *format, va_list logVariables);

```

where the format string can be used to format the log variables

```
* %s	display as string (char*)
* %c	display as single character
* %d	display as integer value
* %l	display as long value
* %x	display as hexadecimal value
* %X	display as hexadecimal value prefixed by `0x`
* %b	display as  binary number
* %B	display as  binary number, prefixed by `0b'
* %t	display as boolean value "t" or "f"
* %T	display as boolean value "true" or "false"
```

The format string may come from flash memory.

examples

```
    Log.info    (  "Log as Info with integer values            : %d, %d"CR                  , 34,  799870);
    Log.debug   (F("Log as Debug with hex values from Flash    : %x, %X"CR                 ), 24342,  25546);
    Log.error   (F("Log as Error with string value from Flash  : %s"CR                     ), "value");
    Log.verbose (  "Log as Verbose with long value             : %l"CR                      , 7979);
```


## Credit

Based on library by 
* [/mrRobot62](https://github.com/mrRobot62)  

Bugfixes & features by
* [rahuldeo2047](https://github.com/rahuldeo2047)
* [NOX73](https://github.com/NOX73)
* [dhylands](https://github.com/dhylands)


## On using and modifying libraries

- [http://www.arduino.cc/en/Main/Libraries](http://www.arduino.cc/en/Main/Libraries)
- [http://www.arduino.cc/en/Reference/Libraries](http://www.arduino.cc/en/Reference/Libraries) 

## Copyright

ArduinoLog is provided Copyright © 2017 under MIT License.

