# Development firmware for px4_fmu-v6xrt (i.MX RT117x)

This firmware is aimed to be used for testers of the Pixhawk 6X-RT (Developer Edition) 

Hardware desccription on Manufacturers webpage - https://holybro.com/products/fmuv6x-rt-developer-edition

Documentation on PX4.io - https://docs.px4.io/main/en/flight_controller/pixhawk6x-rt.html

**Precompiled PX4 firmware files can be found at the end of the page!**

## Firmware sources
PX4 firmware is still under development on PX4 branch pr-px4_fmu-v6xrt - https://github.com/PX4/PX4-Autopilot/tree/pr-px4_fmu-v6xrt

## Issue reporting
Please report all issues found on PR 22263 - https://github.com/PX4/PX4-Autopilot/pull/22263

**IMPORTANT:** For bug reports please include the output from ver all and the hardfault log file. Not Pictures; Also removed all OLD logged hard fault logs from the FMU's SD card.
See message from David Sidrane - https://github.com/PX4/PX4-Autopilot/pull/22263#issuecomment-1785403997

## flashing the code
### with QGC
For flashing code with QGC a daily build of QGC needs to be used - https://docs.qgroundcontrol.com/master/en/releases/daily_builds.html

### with SEGGER debug probe
For this a **SEGGER debug probe** HW is needed - https://www.segger.com/products/debug-trace-probes/
As well as the **SEGGER J-Link** SW - https://www.segger.com/downloads/jlink/
And the **Pixhawk Debug Adapter** - https://holybro.com/collections/flight-controller-accessories/products/pixhawk-debug-adapter

1) Connect the holybro pixhawk debug adapter, with SEGGER debug probe connected, to Pixhawk 6X-RT
2) Power the Pixhawk 6X-RT either via USB or POWERx connector.
3) Launch JlinkExe
4) Type connect
5) Select SWD and target is MIMXRT1176XXXA_M7
6) type reset and halt
7) Type loadbin /path/to/firmware/px4_fmu-v6xrt_bootloader.bin 0x30000000              # needed only in case of bootloader to be flashed
8) Type loadbin /path/to/firmware/px4_fmu-v6xrt_default.bin 0x30020000
9) type reset and go

### with PX4 developer toolchain based on own compiled code
1) Install PX4 developer toolchain according https://docs.px4.io/main/en/dev_setup/dev_env.html
2) Download PX4 Autopilot sourcecode - https://docs.px4.io/main/en/dev_setup/building_px4.html#download-the-px4-source-code
3) Move into PX4-Autopilot code directory
4) do **git checkout pr-px4_fmu-v6xrt**
5) do **git pull --recurse-submodules**
6) do **find boards/px4/fmu-v6xrt/nuttx-config/nsh -type f -iname "*defconfig*" -print0 | xargs -0 sed -i '/CONFIG_DEBUG_ASSERTIONS/s/y/n/g'** to switch off ASSERTION
7) do **make px4_fmu-v6xrt_bootloader upload** to build the bootloader image and flash via USB **IF needed**
8) connect Pixhawk v6X-RT via USB to flash the bootloader image and disconnect again when done
9) do **make px4_fmu-v6xrt_default upload** to build the PX4 FW image and flash via USB
10) connect Pixhawk v6X-RT via USB to flash the PX4 FW image

## Precompiled PX4 FW images

### 20231111 - based on [f2227e8](https://github.com/PX4/PX4-Autopilot/commit/076cf41cff5bca695950768ccb3597df22703e11)
* [px4_fmu-v6xrt_f2227e8.zip](px4_fmu-v6xrt_f2227e8.zip) - contains both bootloader and default FW. Please update both!

### 20231101 - based on [d745fe2](https://github.com/PX4/PX4-Autopilot/commit/d745fe25d05a89b94a56b63d69e54e10577bcb92)
* [px4_fmu-v6xrt_default_20231101.zip](px4_fmu-v6xrt_default_20231101.zip)
* [px4_fmu-v6xrt_bootloader_20231101.zip](px4_fmu-v6xrt_bootloader_20231101.zip)

### 20231031 - based on [3f42a0f](https://github.com/PX4/PX4-Autopilot/commit/3f42a0f943a996f44fc49276fbf68d03b917bb56)
* [px4_fmu-v6xrt_default_20231031.zip](px4_fmu-v6xrt_default_20231031.zip)
* [px4_fmu-v6xrt_bootloader_20231031.zip](px4_fmu-v6xrt_bootloader_20231031.zip)
