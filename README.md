# hovergames3

## Overview

Drone plans a route for the rover "to the agricultural field target" and guides it along. Drone designates the plot of land to be used by the rover. The rover organizes the plot into rows. The rover plans a route to visit each "plant". A virtual multi-tool robotic arm "attached" to the rover is used to treat each plant according to its state.

## Development plan: hardware and software stacks

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
   5. Establish the development cycle for NavQ+ applications. (See NXP i.MX 8M Plus [block diagram](https://www.nxp.com/products/processors-and-microcontrollers/arm-processors/i-mx-applications-processors/i-mx-8-applications-processors/i-mx-8m-plus-arm-cortex-a53-machine-learning-vision-multimedia-and-industrial-iot:IMX8MPLUS).)
      1. Applications running on the 4-core Cortex-A53.
      2. Applications running on the single-core Cortex-M7. _Real time?_
      3. Applications requiring machine learning acceleration. 
   7. Connectivity of NavQ+ and FMUK66. _Answer questions and rearrange bullets._
      1. _How does the companion computer figure in autonomous rover motion and navigation?_
      2. This seems overly complicated. The only documentation from NXP so far is the [NavQPlus_MR-Buggy3 Tradeshow Demo Guide](https://nxp.gitbook.io/8mpnavq/mr-buggy3-demo/mr-buggy3-demo-guide) and that includes ROS2 and a number of additional CAN devices.) __Problems:__
         1. The hovergames3 forum has information about ROS2 not working (no bridge, though old bridge seems to work).
         2. The PX4 development stack does not support ROS2 under macOS.
   8. Mounting and powering of NavQ+ on the rover.
3. Coral cam with NavQ+: rover computer vision. _Answer questions and rearange bullets._ 
   1. _Can the view from the Coral cam be seen on QGroundControl?_
   2. _How to do dynamic video object segmentation on the rover and how to see it live?_
4. Bosch BME688: rover environmental sensor.
   1. Connect to FMUK66 (and read through telemetry?) or to NavQ+ and integrate in application (e.g. overlay on video stream)?
5. Drone.
   1. Exchange the FMUK66 and GPS with the new kit.
   2. Set up in QGroundControl.
   3. Get to _very conservative_ manual flight.
6. NavQ: drone companion computer.
   1. Connectivity with FMUK66.
   2. Mounting on side plate.
   3. Mounting of Coral cam on front plate (possibly on the bottom for downward vision).
8. Coral cam with NavQ: drone computer vision.
9. Communication between rover and drone?
   1. Set up a WiFi link between the two vehicles.
   2. _How can the two vehicles get on the same PX4 uORB network?_
   3. _Is this where ROS2 becomes inevitable?_

## Development plan: applications

1. Drone plans a route for the rover to a work destination and guides it along.
   1. Autonomously fly from start to destination and land. If enough battery, return. 
      1. _Where can one fly drones?_
      2. _What about houses, trees, and power lines?_
      3. _Flying above all obstacles or flying at 7-10 feet to avoid them?_
   2. Fly above a ground path.
      1. _How to define it manually?_
      2. _How can the drone, given a destination, use vision and terrain understanding to plan the path for the rover?_
   3. Get in the air and find the rover on the ground.
      1. _Should there be a beacon on the rover for the drone to home in on? Are there other ways for give the drone a heuristic for locating the rover, based on the rover's normal radio activity?_
      2. Segment the view from the drone camera and label the rover.
   4. Follow the rover.
      1. Borrow from the Follow-Me application.
   5. Create a common 3D AR virtual space for the two camera views.
      1. This should be a moving box strictly corresponing to the environment, and be used for high-resolution planning.
      2. The two cameras should show it overlayed on their video streams and should continously update and fine-tune to ensure maximum correspondence of the virtual space to the physical space, including the locations of the two vehicles.
   7. Guide the rover along a path.
      1. Regardless of how the path is generated, drone-planned or geo-labeled, guide the rover along it.
      2. Display the path overlayed in the drone camera view in QGroundControl.
      3. Create AR markers "in front of" the rover's camera view to follow the path. _How will the virtual space overlays be communicated and shared between the vehicles? This may need to be borrowed from multi-player game development and AR applications._
   8. Dynamic path replanning to avoid obstacles.
      1. Cars when crossing the street.
      2. Puddles and ice patches.
      3. Fallen branches and other debris.
      4. Other obstacles defined by the criterion that the rover cannot go through (e.g. a space between two slats of a bridge that may trap one of the wheels).
      5. Avoid people. _Need to add a forward-looking camera to the drone and train the drone to pick its flight path based on what it "sees". **This is a an application in itself!**_
   9. Define the plot of land in the common virtual space.
      1. The drone should define the boundaries, while the rover should organize it into rows and "plant" position with sufficient spacing for rover navigation.
   10. Virtual (partial digital-twin) multi-tool (multi-applicator) robotic arm for the rover.
       1. Possible tools/applicators are: liquids (water, pesticide, fertilizer), tools (high-zoom camera, sampler), physical (environmental sensors, particulate sensors).
   12. Work the "plants" in the plot.
       1. Plan a trajectory including all the "plants" (objects in the shared virtual space) and "work" on each one.
