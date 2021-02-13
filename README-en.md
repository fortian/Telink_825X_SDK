# Telink TLSR825X Software Development Kit

Telink TLSR825X Bluetooth chip software development kit, for
use with the Anxinke development board.

# Set up Development Environment

- [Window Development Environment Setup](https://github.com/Ai-Thinker-Open/Telink_825X_SDK/blob/master/start_windows.md)

- [Linux 64-bit Development Environment Setup](https://github.com/Ai-Thinker-Open/Telink_825X_SDK/blob/master/start_linux.md)

- [Mac OS Development Environment Setup](https://github.com/Ai-Thinker-Open/Telink_825X_SDK/blob/master/start_macos.md)


# Get SDK

    git clone https://github.com/Ai-Thinker-Open/Telink_825X_SDK.git

# Compile Demo Program

    cd Telink_825X_SDK/example/blink
    make

You should see output similar to the following:

    Invoking: Print Size
    tc32-elf-size -t /home/aithinker/ESP/Telink_SDK/example/blink/out/blink.elf
    text data bss dec hex filename
    3712 8 593 4313 10d9 /home/aithinker/ESP/Telink_SDK/example/blink/out/blink.elf
    3712 8 593 4313 10d9 (TOTALS)
    Finished building: sizedummy

# Burn Program to Chip

The chip itself does not support serial programming.  Only the programmer
provided by the chip manufacturer can be used for programming.  Anxinke
independently developed a serial port programming tool, which can be used
without an official programmer.  The Anxinke bootloader must be burned into the
module first.  Generally, the Anxinke factory modules and development boards are
support serial programming.

- If you use Anxinke TB series development board for development, you can
  directly connect the development board to the computer via USB.
- If you use Anxinke TB series modules for development, you need to prepare a
  USB-to-serial module that supports hardware flow control, and connect the
  Bluetooth module with the USB-to-serial port according to the following table,
  and then insert the USB-to-serial port into the computer.

# Serial Port Wiring

|Serial Port|Module|
|----|---|
|VCC|3V3|
|GND|GND|
|TX|RX|
|RX|TX|
|RTS|RST|
|DTR|SWS|

SWS is the boot selection pin.  Hold low to enter download mode, and hold high
to enter operating mode.

# Set Serial Port

After connecting the development board or module to the computer via USB, find
its corresponding serial port:

- Windows systems can view the serial port in the Device Manager.  Windows
  serial port IDs start with `COM`.
- In Linux systems, check the detected serial ports with `ls /dev/ttyUSB*`.
- In Mac OS systems, check the detected serial ports with `ls /dev/cu*`.

Check the serial port number, modify the `DOWNLOAD_PORT` line in `makefile` in
the `blink` directory, and change the value to the serial port number of the
development board.  For example, if you're using Windows and the port number
corresponding to the development board is `COM3`, the line should read:
`DOWNLOAD_PORT := com3`

# Burn Firmware

After successfully setting the serial port number, you can use the following
commands to burn the firmware to the chip:
Burning instructions:

    make flash

## Common Programming Errors

    Telink_Tools.py v0.3 dev
    Open /dev/ttyUSB0 ... ... Fail!

If the above error occurs, please check whether the serial port number is set
correctly and whether the serial port is in use by another program.

# Run Firmware

Press the RST button on the development board to reset the development board and
start running the firmware that has just been burned.

If you use a single module for development or want to open the serial port, you
can use the `make monitor` command.

# Other Instructions

To erase the firmware:

    make erase_fw

To erase the entire flash, except the bootloader:

    make erase_all

# Other Information

[API Reference
Manual](https://shyboy.oss-cn-shenzhen.aliyuncs.com/readonly/tb/Telink%20Kite%20BLE%20SDK%20Developer%20Handbook.pdf)
