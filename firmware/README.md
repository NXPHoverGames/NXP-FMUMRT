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

### with PX4 developer toolchain based on own compiled code
1) Install PX4 developer toolchain according https://docs.px4.io/main/en/dev_setup/dev_env.html
2) Download PX4 Autopilot sourcecode - https://docs.px4.io/main/en/dev_setup/building_px4.html#download-the-px4-source-code
3) Move into PX4-Autopilot code directory
4) do **git checkout pr-px4_fmu-v6xrt**
5) do **git pull --recurse-submodules**
6) do **make px4_fmu-v6xrt_default upload** to build the PX4 FW image and flash via USB
7) connect Pixhawk v6X-RT via USB to flash the PX4 FW image

### updating the bootloader
For this a **SEGGER debug probe** HW is needed - https://www.segger.com/products/debug-trace-probes/
As well as the **SEGGER J-Link** SW - https://www.segger.com/downloads/jlink/
And the **Pixhawk Debug Adapter** - https://holybro.com/collections/flight-controller-accessories/products/pixhawk-debug-adapter

1) Move into PX4-Autopilot code directory with checked out pr-px4_fmu-v6xrt (see instruction above)
2) do **git pull --recurse-submodules**
3) do **make distclean**
4) do **make px4_fmu-v6xrt_default** to build the PX4 FW image and flash via USB
5) Connect the holybro pixhawk debug adapter, with SEGGER debug probe connected, to Pixhawk 6X-RT
6) Power the Pixhawk 6X-RT either via USB or POWERx connector.
7) Launch JlinkExe
8) Type connect
9) Select SWD and target is MIMXRT1176XXXA_M7
10) type reset and halt
11) Type loadbin /path/to/firmware/px4_fmu-v6xrt_bootloader.bin 0x30000000              # needed only in case of bootloader to be flashed
12) Type loadbin /path/to/firmware/px4_fmu-v6xrt_default.bin 0x30020000
13) type reset and go

## Precompiled PX4 FW images

### 20231114 - based on [84766c4](https://github.com/PX4/PX4-Autopilot/commit/84766c4cb89ebdabfa7f2230e88a272f4c677ce3)
* [px4_fmu-v6xrt_default_20231114.zip](px4_fmu-v6xrt_default_20231114.zip) - contains both bootloader and default FW. Please update
  
### 20231111 - based on [f2227e8](https://github.com/PX4/PX4-Autopilot/commit/076cf41cff5bca695950768ccb3597df22703e11)
* [px4_fmu-v6xrt_f2227e8.zip](px4_fmu-v6xrt_f2227e8.zip) - contains both bootloader and default FW. Please update both!
