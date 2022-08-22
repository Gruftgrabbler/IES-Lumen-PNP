# IES-Lumen-PNP

Repository with files and descriptions about the IES lumenPnP.

You can find the official documentation [here](https://docs.opulo.io).

The official repository can be found [here](https://github.com/opulo-inc/lumenpnp.git)

# Build
The build is mostly done after the documentation, but uses some modifications here and there. I've tried to insert all custom STLs into this repository.

## Staging Plate

Eventually we'll need at least one other stating plate as an actual workplace to put the PCB on and do the pick and placing stuff..
This repository contains gerbers for the staging plate as well as .dxf version.
You can order an aluminum version of the staging plate at [PCBWay](https://www.pcbway.com) using the gerbers. Unfortunately JLCPCB does not offer manufacturing with this dimensions.

Or if you want to order at [cutworks](https://www.cutworks.com/en/) just use the .dxf file.

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


[OpenPNP YouTube Tutorial](https://www.youtube.com/watch?v=vuFalyzcCZA)


# Next Steps

- [x] Setup all Axis in OpenPNP
- [ ] Lens Calibration
- [ ] Maybe add an additional stepper driver for the second Y-Axis motor to the auxillary driver
- [ ] Finish the OpenPNP settings
- [ ] Setup a Job
- [ ] Run the PNP on the Test PCBs