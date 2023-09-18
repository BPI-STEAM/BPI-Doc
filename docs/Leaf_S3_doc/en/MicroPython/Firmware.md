# Micropython firmware download and burning

The firmware supporting ESP32S3 chip can be found on [MicroPython official website](https://micropython.org/) https://micropython.org/download/ESP32_GENERIC_S3/

After clicking the link to enter the page, you can see several firmware download addresses below, select a file with a .bin suffix and download it locally.

![](../assets/images/Micropython_operating_env_6.jpg)

Pay attention to the date marked in the firmware name, the closer to the current time, the newer the function.

You can use two tools to burn the firmware, Espressif's official FLASH download tool or esptool, you can choose one of the two.

## Set firmware download mode

There are two methods of operation:

1. Connect to the computer via USB, press and hold the BOOT button, then press the RESET button and release it, and finally release the BOOT button.

2. Press and hold the BOOT button when the power supply is disconnected, then connect to the computer via USB, and finally release the BOOT button.

It can be seen from this that the chip selects the startup mode when reset or re-powered through the GPIO0 controlled by the BOOT key.

Confirm the COM interface in the device manager. The serial number of the COM interface in the firmware download mode and the normal mode is usually different.

## Windows FLASH download tool

Download and unzip: [FLASH download tool download address](https://www.espressif.com/zh-hans/support/download/other-tools)

Open the software and select the chip model as ESP32S3, and set the download mode to usb:

![](../assets/images/Micropython_operating_env_7.png)

At this point, you need to set the development board to firmware download mode.

Under the condition that the chip is in the firmware download mode, modify the COM interface to the corresponding interface in the FLASH download tool window, here is COM22.

Add MicroPython firmware, set the flash start address to `0x0` for ESP32-S3 chip.

![](../assets/images/Micropython_operating_env_8.png)

First click the ERASE button to clear the data on the flash, and then click START to burn the firmware to the flash.

After the programming is completed, press the RESET button once to make the development board enter the normal use mode.

## esptool

Take the specific operation steps of Windows PowerShell as an example.

Install esptool with the following command:

```shell
pip install esptool
```

If needed in the future, you can upgrade esptool with the following command:

```shell
pip install -U esptool
```

Go into the directory where the firmware is located in PowerShell via a command or other method.

A PowerShell window can be opened in this folder by holding down the shift key and right-clicking in the Windows folder window.

At this time, you need to set the development board to firmware download mode, see above for details.

To clear the flash through the following commands, you need to modify the COM interface to the corresponding interface, here is COM1.

```shell
python -m esptool --chip esp32s3 --port COM1 erase_flash
```

To burn the firmware through the following commands, you need to modify the firmware file name corresponding to the current file name to be burned.

```shell
python -m esptool --chip esp32s3 --port COM1 --baud 460800 --before=usb_reset --after=no_reset write_flash 0x0 GENERIC_S3_SPIRAM-20220618-v1.19.1.bin
```

If it is burned through USB, press the RESET button once to reset after completion, so that the development board enters the normal use mode.

If programming via UART, it will reset automatically after completion.