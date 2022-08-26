# IES-Lumen-PNP

Repository with files and descriptions about the IES lumenPnP.
This readme contains all of the sub repositories you should checkout to have all files together.

- You can find the official documentation [here](https://docs.opulo.io). You can skip the assembly part and start at [Testing](https://docs.opulo.io/docs/testing/).

- Official [releases](https://github.com/opulo-inc/lumenpnp/releases). Don't use the firmware directly. Always compile it yourself.

- The official repository can be found [here](https://github.com/opulo-inc/lumenpnp.git)

- STLs I think are quite interesting on [printables](https://www.printables.com/social/127530-gruftgrabbler/collections/229786)

**IMPORTANT: This repository contains a `machine.xml`file with all previously done calibration. You have to copy them into your openpnp installation folder:

```
Configuration files are located in your home directory, under a subdirectory called .openpnp2.

On Mac this will typically be /Users/[username]/.openpnp2.

On Windows 2000, XP and 2003 it will be C:\Documents and Settings[username].openpnp2.

On Windows Vista and above it’s C:\Users[username].openpnp2.
```
**
# Build
The build of the machine is almost done. Only missing an additional staging plate and feeders. There are some custom modifications implemented. The associated STLs should be in this repository.

## Staging Plate

Eventually we'll need at least one other stating plate as an actual workplace to put the PCB on and do the pick and placing stuff..
This repository contains gerbers for the staging plate as well as .dxf version.
You can order an aluminum version of the staging plate at [PCBWay](https://www.pcbway.com) using the gerbers. Unfortunately JLCPCB does not offer manufacturing with this dimensions.

Or if you want to order at [cutworks](https://www.cutworks.com/en/) just use the .dxf file.

**IMPORTANT:** The first stating plate which is mounted on the machine was ordered with too small holes. You need to drill larger holes with 3.3mm drills. Be very careful and drill very slowly: Use 800RPM and cutting oil.

## Custom STLs
- assembly-belt-clamp003 v3.stl : Small extrusion to ensure that the Y-Axis Limit switch is actually triggered.
- assembly-umbilical-swivel v3.stl : Longer Extrusion and hole to insert a screw to hold the part in position.
- StagingPlateValveAdapter v5.stl : Adapter for the Valve used on the IES-LumenPNP.
- LumenPnPStagingPlateSpacer.stl : A little spacer to prevent the staging plate from scratching the V-Frame.

# Motherboard
The IES lumenPnP uses an old motherboard beta version which does not have the same pin layout as newer versions. This means that you can't simply flash the official firmware releases. Therefore you need to compile the firmware yourself and replace the corresponding pin header file.

Sometimes you need to have the original KiCAD files.
You can find a repository where you can checkout the old motherboard version [here](https://github.com/Gruftgrabbler/ies-index-files). Just clone the repository and checkout the given version:

```sh
git clone https://github.com/Gruftgrabbler/ies-index-files
git checkout 9a7900cbae88ed8e339672445f84904c968a0e6b
``` 

You can find the KiCAD project under `pnp/pcb/mobo/mobo.kicad_pro`.

# Firmware

Since the pins with newer versions are mixed up you need to compile the firmware yourself, if you wish to update it.
Open VSC, install **Auto Build Marlin** Extension and copy the 
You can do this with 

```sh
git clone https://github.com/MarlinFirmware/Marlin.git
wget -nv https://raw.githubusercontent.com/MarlinFirmware/Configurations/bugfix-2.1.x/config/examples/Opulo/Lumen_REV3/Configuration.h
wget -nv https://raw.githubusercontent.com/MarlinFirmware/Configurations/bugfix-2.1.x/config/examples/Opulo/Lumen_REV3/Configuration_adv.h

cp pins_OPULO_LUMEN_REV3.h Marlin/Marlin/src/pins/stm32f4/
cp Configuration.h Marlin/Marlin/
cp Configuration_adv.h Marlin/Marlin/
```

Then use the build button in **Auto Build Marlin**

I wasn't able to upload the firmware the upload Button so I used a [J-Link EDU Mini](https://www.segger.com/products/debug-probes/j-link/models/j-link-edu-mini/) and flashed the firmware with [J-Flash Lite](https://wiki.segger.com/J-Flash_Lite).
In J-Flash Lite you have to choose the STM32F407VE as device. 


[Docs](https://docs.opulo.io/docs/motherboard/update-firmware/)


Instead you have to `pins_OPULO_LUMEN_REV3.h` to `Marlin/src/pins/stm32f4/`


# OpenPNP
For a successful connection first connect the machine to your computer then open openPNP.

In order to use the existing OpenPNP configuration copy the `machine.xml` file from this repository into **TODO**

[OpenPNP YouTube Tutorial](https://www.youtube.com/watch?v=vuFalyzcCZA)

## Cameras

**Done:** ~~First of all there is a small screw on the side of the camera which you can adjust the focus of the lense. Unfortunately it is impossible to reach the screw while the camera is mounted. So you need to unmount the camera from the machine. Unscrew the screw, mount the camera again and then rotate the camera until the picture gets sharp enough, then unmount the camera and save the screw in position.. And that has to be done for both cameras.~~

**Note:** 
Unexpectedly the camera does have a pretty high focal length, and therefore a "high zoom". That makes it impossible for the machine to completely see large objects. This could be a problem for placing big components, but should be fine for small ones. **BUT that means that the camera can not be calibrated accordingly to the [docs](https://docs.opulo.io/openpnp/calibration/camera-fisheye-cal/). Logically the camera has such a high focal length, that a fisheye effect does not occur anyway...**

## How to setup a Job

[YouTube Tutorial](https://www.youtube.com/watch?v=75hHtclelN4)

## Demo Board

The Gerbers for the OpenPNP Demo board can be found in the openPNP repository. You have to follow the instructions from the []() or watch this [youtube video](https://www.youtube.com/watch?v=75hHtclelN4)

```
git clone https://github.com/openpnp/openpnp.git
cd openpnp/samples/demoboard
```

# Next Steps

- [x] The arm holding the right cable-tube is really shitty. Another solution should be found. --> I think the new arm is sufficient enough.
- [x] Setup all Axis in OpenPNP
- [ ] Mount Datum Board on staging plate 
- [ ] **IMPORTANT:** [Homing Fiducial](https://docs.opulo.io/openpnp/calibration/homing-fiducial/) 
- [?] Lens Calibration -> Since the focal length is so high, it might be impossible to do.
- [ ] Optional: Maybe add an additional stepper driver for the second Y-Axis motor to the auxillary driver
- [ ] Finish the OpenPNP settings
- [ ] Setup a Job
- [ ] Run the PNP on the Test PCBs
- [ ] Build the [drag feeders](https://www.youtube.com/watch?v=Gm1oQjoRitc). STLs can be found [here](https://www.printables.com/model/221378-lumen-pnp-passive-drag-feeder)