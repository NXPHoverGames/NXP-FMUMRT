# NXP-FMUMRT, MR-FMURT6, MR-VMU-RT117x
This is an open reference design for a PX4 V5X flight controller. 

Note1: For MR-FMURT6 based on NXP i.MX RT1062: This design is NOT being produced in volume, and we will produce MR-VMU-RT1176 using i.MX RT1176 MCU instead.
The RT1176 offers higher processing speed (Ghz) and additional UARTS as well as a dual core processor.
MR-FMURT6 It is still a valuable reference point for cost-optimzed design usign i.MX RT1062
Alternative software could also be used on this design such as Zephyr + Cognipilot.

Note2: MR-VMU-RT117x is being called a "VMU" or "Vehicle Management Unit" rather than "FMU" or "Flight Management Unit" since this is more inclusive 
of the many types of vehicles that can use a real time controller. 

Note3: The i.MX RT117x is currently contstrained on MR-VMU-RT117x by the Pixhawk Autopilot Bus (PAB) connector standard. 
The PAB standard was already revised to allow for extra PWM from the RT1176 and allows potential elimination of the IO co-processor that is on 
the VxX carrier board. Additionally there is a 3rd CAN port available.
(July/2023) - In the future look for a revised VxX7 carrier board which makes use of these new signals on the PAB.

Note4: Given the i.MX RT117x is currently contstrained on MR-VMU-RT117x, we will look in the future collaboration on a "chip down" design that takes advantage
of all the extra IP an peripherals such as the camera and vision pipeline that are currently unused on this chip.
