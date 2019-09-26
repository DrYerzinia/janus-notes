# Janus : Simulation (9/22/2019)

## Changes to cusub code
* Enabled roll control on joystick.  This has sideffect of roll actually being controlled so should make sure PID loop doesn't mess with Leviathans functionality.
* Removed the Thruster Allocation Matrix from the PID_pololu_matrix and moved it to a yaml config file.  This allows submarines with different thruster configurations to work.
* Removed feed-forward from PID_pololu_matrix for down motors.  This should be done as an explicit configuration if we want it.  Idealy we would know weight/bouyancy as config parameters and change to sending thrust commands rather than PWMs.  Then we can calculate required downforce and need less pid tuneing.  This has the problem that the subs mass may change sigificantly as we add/remove parts.
* Reordered motor commands to be from 0-7.  Unclear why we have this mapping as it is redundant with the mapping in the pololu driver.  Will need to fix Leviathan motor mapping when this change goes to develop.
* Removed unneeded bgsegm include that prevented building.  Is this perhaps needed for unit test thats currently not being built?
* Changed gazebo driver to use ordered motor mapping (0-7).  Removed thrust tuning constants.  Added flip motor array to match real sub.  Removed feedforward offset removal.  Really could use desired thrusts as input instead of PWMs.

## Thoughts on PID Pololu Matrix
The user of the TAM is inflexible as it limits the number of motors to 8.  This is maybe resonalbe as it will still allow for lower count motor combinations.  It also restrics us to a control axis mapping of drive/strafe/depth/roll/pitch/yaw.  When we do interesting manuvers, say tilting downwards how these remap is an interesting question.  A Dynamic thruster allocation matrix would be useful especialy in combination with feed-forward for depth.  Interesting question, with our 8 motors is it possible to always end up with zero torque and zero translation?

## TODOs
* Add Leviathan TAM
* Fix Leviathan motor mapping
* Integrate motor mapping into gazebo motor driver