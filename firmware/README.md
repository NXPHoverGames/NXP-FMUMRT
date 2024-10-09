# Firmware for px4_fmu-v6xrt (i.MX RT117x)

**This info is aimed to be used for testers of the Pixhawk 6X-RT (Developer Edition)**

Hardware desccription on Manufacturers webpage - https://holybro.com/products/fmuv6x-rt-developer-edition
Documentation on PX4.io - https://docs.px4.io/main/en/flight_controller/pixhawk6x-rt.html

**IMPORTANT** if you are using the v6xrt FMUM on a development baseboard from NXP and like to use the T1 ethernet: 
Please make sure that you enable the T1 ethernet PHY - **TJA1103** - via **make px4_fmu-v6xrt menuconfig**. 
Ethernet PHY is in **Device Drivers** --> **Network Device/PHY Support** --> **Board PHY Selection (ETH0)** 

## Firmware sources
PX4 firmware for px4_fmu-v6xrt has been merged to PX4 main - https://github.com/PX4/PX4-Autopilot on Nov 15th 2023.
Please build from there.

## Issue reporting
Please report all issues found via https://github.com/PX4/PX4-Autopilot/issues/new/choose

## flashing the code
### with QGC
For flashing code with QGC stable release version v4.4.0 or later is needed  - https://docs.qgroundcontrol.com/master/en/qgc-user-guide/getting_started/download_and_install.html

### with PX4 developer toolchain based on own compiled code
1) Install PX4 developer toolchain according https://docs.px4.io/main/en/dev_setup/dev_env.html
2) Download PX4 Autopilot sourcecode - https://docs.px4.io/main/en/dev_setup/building_px4.html#download-the-px4-source-code
3) Move into PX4-Autopilot code directory
4) do **git pull --recurse-submodules**
5) optional: do **make distclean** if you had build already from this code directory before.
6) do **make px4_fmu-v6xrt_default upload** to build the PX4 FW image and flash via USB
7) connect Pixhawk v6X-RT via USB to flash the PX4 FW image

### updating the bootloader
For this a **SEGGER debug probe** HW is needed - https://www.segger.com/products/debug-trace-probes/
As well as the **SEGGER J-Link** SW - https://www.segger.com/downloads/jlink/
And the **Pixhawk Debug Adapter** - https://holybro.com/collections/flight-controller-accessories/products/pixhawk-debug-adapter

1) Move into PX4-Autopilot code directory with checked out pr-px4_fmu-v6xrt (see instruction above)
2) do **git pull --recurse-submodules**
3) do **make distclean**
4) do **make px4_fmu-v6xrt_bootloader** to build the PX4 bootloader
5) Connect the holybro pixhawk debug adapter, with SEGGER debug probe connected, to Pixhawk 6X-RT
6) Power the Pixhawk 6X-RT either via USB or POWERx connector.
7) Launch JlinkExe
8) Type connect
9) Select SWD and target is MIMXRT1176XXXA_M7
10) type reset and halt
11) Type loadbin /path/to/firmware/px4_fmu-v6xrt_bootloader.bin 0x30000000              # needed only in case of bootloader to be flashed
12) type reset and go

## Precompiled PX4 FW images

**IMPORTANT:** Support for px4_fmu-v6xrt has been merged to PX4 main on 15th of Nov 2023. Therefore we no longer provide precompiled images.
Please build the bootloader and PX4 FW according instruction above.
