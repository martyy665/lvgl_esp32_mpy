# LVGL on ESP32 with MicroPython (as a USER_C_MODULE)

This repository is an attempt to create an out-of-the-box LVGL experience on ESP32 files using MicroPython.

## Rationale

While there are a lot of libraries, examples and information available on getting LVGL working on MicroPython there is a
huge amount of fragmented, outdated and non-working code out there.

After spending several days getting increasingly frustrated about the state of things I decided to fragment a bit more
and create my own module with the following requirements:

- Must compile as a USER_C_MODULE
- Works with latest release of LVGL
- Works with latest release of MicroPython
- Works with latest (supported by MicroPython) release of ESP-IDF 
- Uses the `esp_lcd` driver of ESP-IDF with an SPI bus
- Allows sharing SPI for example with SD card

There are currently no plans to support 
- non-ESP32 devices 
- other than the standard `esp_lcd` displays
- other buses than SPI
- other displays than ST7789 as I do not possess any to test

The final objective of this project is to support the camp badges for [Fri3d Camp](https://www.fri3d.be) and as such
certain functionality you'd expect from a display driver might be missing as they are not necessary for that project.

Don't hesitate to create a pull request to add the required functionality. 

## Building

First follow the MicroPython documentation to create a build for your device without this module and verify it is
working.

Once you are sure it does, clone the repository with recursive submodules, this makes sure 

```shell
git clone --recurse-submodules <repository-url>
```

Compile adding the `USER_C_MODULES` parameter to the `make` command.

```shell
make USER_C_MODULES=/path/to/lvgl_esp32_mpy/micropython.cmake <other options>
```

## Missing things

Things I'll probably still implement at some point:

- There is no deinit functionality, once it's loaded, it's there to stay
- Rotation of displays

## Supported versions

- LVGL: 9.1
- MicroPython: 1.22.2
- ESP-IDF: 5.1.2

## Acknowledgements

A lot of ideas and/or work were borrowed from

- [kdschlosser](https://github.com/kdschlosser/lvgl_micropython)'s LVGL binding
- [russhughes](https://github.com/russhughes/s3lcd)'s s3lcd
- The original [lv_binding_micropython](https://github.com/lvgl/lv_binding_micropython)
