# hovergames3

## Overview

Drone plans a route for the rover "to the agricultural field target" and guides it along. Drone designates the plot of land to be used by the rover. The rover organizes the plot into rows. The rover plans a route to visit each "plant". A virtual multi-tool robotic arm "attached" to the rover is used to treat each plant according to its state.

## Development plan

I. Drone plans a route for the rover to a work destination and guides it along.
   1. Rover.
      1. Set up PX4 development environment and test it with the default simulator.
      2. Set up RDDRONE vehicle programming (bootloader, J-LINK).
      3. Program the rover with FMUK66 firmware.
      4. Set up the FS-i6S radio transmitter.
      7. Update QGroundControl.
      5. Set up the rover in QGC.
      6. Figure out how to arm (possibly through GPS).
      8. Manually operate the rover. Don't exhaust the battery.
      9. Tune the steernig angle if necessary.
      10. Mount the telemetry transmitter.
      11. Drive the rover with telemetry until battery is exhausted. Have a spare (no need to charge, if new one).
      12. _(Optional) Try the NXP example application._
   2. NavQ+: rover companion computer. _Answer questions and rearange bullets._
      1. _How is NavQ+ programmed?_
      2. Inspect and inventory package.
      3. Collect online documentation and resources.
      4. Find a setup guide and follow it. _Put steps underneath this one!_
      5. Establish the development cycle for NavQ+ applications. (See NXP i.MX 8M Plus [diagram](https://www.nxp.com/products/processors-and-microcontrollers/arm-processors/i-mx-applications-processors/i-mx-8-applications-processors/i-mx-8m-plus-arm-cortex-a53-machine-learning-vision-multimedia-and-industrial-iot:IMX8MPLUS).)
         1. Applications running on the 4-core Cortex-A53.
      7. Connectivity of NavQ+ and FMUK66. _Answer questions and rearange bullets._
         1. _How does the companion computer figure in autonomous rover motion and navigation?_
      8. Mounting and powering of NavQ+ on the rover.
   3. Coral cam with NavQ+: rover computer vision. _Answer questions and rearange bullets._ 
      1. _Can the view from the Coral cam be seen on QGroundControl?_
      2. _
   5. 
