# WifiDuck 

print image.pn![g](https://github.com/meepmaster360/wifiduck/blob/main/Image/image.png)


1. Plug in your WiFi Duck
2. Connect to the WiFi network `wifiduck` with the password `wifiduck`
3. Open a browser and visit `192.168.4.1`
4. Write, save and run your first Ducky Script
5. [Recommended] Open `Settings` (top right corner) and update SSID and password

#

# WifiDuck payloads

YouTube.txt

This script essentially automates the process of opening Chrome, navigating to a specific YouTube video. 
However, it's worth noting that such automation scripts should be used responsibly and with respect to the terms of service of the services being automated.

PythonExploit.txt

This payload script aims to execute a Python HTTP server exploit by leveraging PowerShell. It's important to note that this script assumes the target system has Python 3 installed. 
However, it's worth noting that such automation scripts should be used responsibly and with respect to the terms of service of the services being automated.
#

## Scripting

### Basics

Keys are separated by a single space.  
Everything written in a single line gets pressed and released at the same time.  
To write text, use the STRING function.  
It's compatible to Ducky Script, which was developed by the wonderful people at [Hak5](https://www.hak5.org/).  

| Example | Explanation |
| ------- | ----------- |
| WINDOWS <br> r | Type the Windows key and then the r key |
| WINDOWS r | Press the Windows key and the r key simultaneously |
| STRING WINDOWS r | Write WINDOWS r |

### Functions

| Command | Example | Description |
| ------- | ------- | ----------- |
| `REM` | `REM Hello World!` |Comment |
| `DEFAULTDELAY` or `DEFAULT_DELAY` | `DEFAULTDELAY 200` | Time in ms between every command |
| `DELAY` | `DELAY 1000` | Delay in ms |
| `STRING` | `STRING Hello World!` | Types the following string |
| `REPEAT` or `REPLAY` | `REPEAT 3` | Repeats the last command n times |
| `LOCALE` | `LOCALE DE` | Sets the keyboard layout. [List](#translate-keyboard-layout) |
| `KEYCODE` | `KEYCODE 0x02 0x04` | Types a specific key code (modifier, key1[, ..., key6]) in decimal or hexadecimal |
| `LED` | `LED 40 20 10` |Changes the color of the LED in decimal RGB values (0-255) |

### Standard Keys

| Key |
| --- |
| `a` - `z` |
| `A` - `Z` |
| `0` - `9` |
| `F1` - `F12` |

### Modifier Keys

| Key |
| --- |
| `CTRL` or `CONTROL` |
| `SHIFT` |
| `ALT` |
| `WINDOWS` or `GUI` |

### Other Keys

| Key |
| --- |
| `ENTER` |
| `MENU` or `APP`|
| `DELETE` |
| `HOME` |
| `INSERT` |
| `PAGEUP` |
| `PAGEDOWN` |
| `UP` or `UPARROW` |
| `DOWN` or `DOWNARROW` |
| `LEFT` or `LEFTARROW` |
| `RIGHT` or `RIGHTARROW` |
| `TAB` |
| `END` |
| `ESC` or `ESCAPE` |
| `SPACE` |
| `PAUSE or BREAK` |
| `CAPSLOCK` |
| `NUMLOCK` |
| `PRINTSCREEN` |
| `SCROLLLOCK` |

### Numpad Keys

| Key |
| --- |
| `NUM_0` - `NUM_9` |
| `NUM_ASTERIX` |
| `NUM_ENTER` |
| `NUM_MINUS` |
| `NUM_DOT` |
| `NUM_PLUS` |

### Examples

```
REM Hello World for Windows PCs
DEFAULTDELAY 200
GUI r
STRING notepad
ENTER
STRING Hello World!
```

## CLI Commands

The command line interface or CLI is accessible using a serial connection to the ESP8266 (115200 baud, Newline ending) or via the web interface at `192.168.4.1/terminal.html`.  

### General

| Command | Description | Example |
| ------- | ----------- | ------- |
| help | Returns all available commands | `help` |
| ram | Returns available memory in bytes | `ram` |
| version | Returns version number | `version` |
| settings | Returns list of settings | `settings` |
| set -n/ame <value> -v/alue <value> | Sets value of a specific setting | `set ssid "why fight duck"` |
| reset | Resets all settings to their default values | `reset` |
| status | Returns status of i2c connection with Atmega32u4 | `status` |
| run <...> | Starts executing a Ducky script | `run example.txt` |
| stop <...> | Stops executing a Ducky script | `stop example.txt` |

### SPIFFS File Management

| Command | Description | Example |
| ------- | ----------- | ------- |
| mem | Returns available, used and free memory of SPIFFS in bytes | `mem` |
| format | Formats SPIFFS | `format` |
| ls <...> | Returns list of files | `ls /` |
| create <...> | Creates file | `create example.duck` |
| remove <...> | Deletes file | `remove example.duck` |
| cat <...> | Returns content of file | `cat example.duck` |
| rename -fileA,a <value> -fileB,b <value> | Renames file | `rename example.duck example.txt` |
| write -f/ile <value> -c/ontent <value> | Writes (appends) data to file | `write example.txt "Hello World!"` |
| stream <...> | Opens file stream | `stream example.txt` |
| close | Closes file stream | `close` |
| read | Read and return the result from file stream | `read` |

If a stream is open, everything you type (except messages containing exactly `close` or `read`) will be written to the file until you type `close`!  

## How to Debug

To properly debug, you need to have both the Atmega32u4
and the ESP8266 connected via USB to your computer.  

That can be tricky when you only have a all in one board, so it might be useful
you built one yourself. You don't need to solder it, for example you can use an
Arduino Leonardo and a NodeMCU and connect them with jumper cables.  

Now open 2 instances of Arduino (so they run as separate processes!),
select the COM port and open the serial monitor for each device.
You might need to reset the Atmega32u4 to see serial output.
If that causes problems with the i2c connection, try to reset the ESP8266 too.  
## Development

### Edit Web Files

If you would like to modify the web interface, you can!  
The `web/` folder contains all `.html`, `.css`, `.js` files.  
You can edit and test them locally as long as you're connected to the WiFi Duck
network thanks to the websocket connection handled by JavaScript in the background.  

To get the new files onto the ESP8266, run `python3 webconverter.py` in the
repository folder.  
It gzips all files inside `web/`, converts them into a hex array
and saves it in `esp_duck/webfiles.h`.  
Now you just need to [flash](#flash-software) the ESP8266 again.  

### Translate Keyboard Layout

Currently supported keyboard layouts:  
- [:de: DE](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_de.h)
- [:gb: GB](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_gb.h)
- [:us: US](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_us.h)
- [:es: ES](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_es.h)
- [:denmark: DK](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_dk.h)
- [:ru: RU](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_ru.h)
- [:fr: FR](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_fr.h)
- [:belgium: BE](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_be.h)
- [:portugal: PT](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_pt.h)
- [:it: IT](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_it.h)
- [:slovakia: SK](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_sk.h)
- [:czech_republic: CZ](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_cz.h)
- [:slovenia: SI](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_si.h)
- [:bulgaria: BG](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_bg.h)
- [:canada: CA-FR](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_cafr.h)
- [:switzerland: CH-DE](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_chde.h)
- [:switzerland: CH-FR](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_chfr.h)
- [:hungary: HU](https://github.com/spacehuhn/WiFiDuck/blob/master/atmega_duck/locale_hu.h)
