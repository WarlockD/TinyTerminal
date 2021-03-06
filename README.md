Tiny Terminal - TT
==================

This is a tiny console based terminal program for Microsoft Windows. Suitable for debugging console of embedded projects.
It has low memory and low cpu consumtion, is extremly fast, easy to use and has nice of features. 

The title of the commandline-window shows the the current port configuration and other information.

![TinyTerminal](https://madex.github.io/tt.png)

This is a fork from http://elm-chan.org/fsw_e.html. ElmChan makes really nice soft- and firmware.

I added some extra features like ALT+G and ALT+Z. And reduced the binary size.

OPTIONS
=======

Options can be defined in as command line arguments and in an option file. 
For example in a shortcut property.

`tt.ini` is the option file for tt.exe. The options must be listed from the first line
in this file and the options are terminated by end of file or a blanked line.
This file is searched in order of current dir, system dir and pathed dir.
If it is found, it is imported prior to command line options, so that options
specified in this file will be overridden by command line options.

```
port=<port>,<format>,<bps>

 Specifies port number (1 to 99), data format (n|o|e)(7|8)(1|2) and bit rate.
 The default setting is: port=1,n81,9600

 Example:
  port=10         (Set port number. Format and bit rate are left unchanged)
  port=5,,115200  (Set port number and bit rate. Format is left unchanged)


bps=<bps>

  Same as port=,,<bps>


flow=<flag>

  Specifies if RTS/CTS flow control is enabled (1) or disabled (0). 
  The default setting is: flow=0


pol=<flags>

  Specifies polarity of DTR and RTS signals. The value can be 0 to 7.
  The bit0 specifies to invert DTR signal, bit1 specifies to invert
  RTS signal and bit2 specifies to invert TXD signal. When bit1 is set,
  RTS/CTS flow control is disabled regardless of flow option. When bit2
  is set, no data is transmitted. The default setting is: pol=0


help=<flag>

  Shows keyboard command list on start up.
  The default setting is: help=1
```


KEYBOARD COMMAND
================
```
[Alt]+[X]          - Exit program.
[Alt]+[V]          - Switch view mode, TTY and HEX.
[Alt]+[L]          - Start/Stop logging to a file.
[Alt]+[G]          - Start/Stop with predefined Filename
[Alt]+[T]          - Transmit a file as byte stream.
[Alt]+[Z]          - Timestamp for every Line.
[Alt]+[Y]          - Transmit a file in XMODEM.
[Alt]+[H]          - Hang-up. (Invert DTR for 300ms)
[Alt]+[B]          - Break. (Set TXD '0' for 300ms)
[Alt]+[P]          - Change parity (cycle beetween NONE, ODD, EVEN)
[Alt]+<nums>       - Transmit a byte by number. (e.g. 0 transmits a '\0', 122 transmits a 'z')
[Alt]+[Up/Down]    - Change bit rate.
[Alt]+[Left/Right] - Change port number.
```

Install
=======

[Download](https://github.com/madex/TinyTerminal/archive/master.zip) and extract `tt.exe` and `tt.ini` into a folder and run `tt.exe`.

Compile
=======

For the small Filesize I use my fork of TinyCC http://github.com/madex/tcc, it is a fork from http://bellard.org/tcc/ with advanced win32api Headers. You need it because the original version has no comdlg32 support.
```
 tcc -lcomdlg32 -luser32 -o tt.exe tt.c
``` 
It also compiles with mingw32, this is usefull for debugging. There is also a Code::Blocks project file.
``` 
 mingw32-gcc -Os -s -mconsole -mwindows -o tt.exe tt.c
``` 
