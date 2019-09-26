# Janus : Testing Dive Day (9/13/2019)
## Plan
2 Hours of testing at CU Boulder divewell alongside Leviathan

Goals:
* Test and Tune Depth/Pitch/Roll PID Loops
* Drive out to divewell window, look through, and drive back using joystick/video feed
* Determine runtime on 3Ah battery
* Measure top forward speed
## Successes:
1. Depth control worked.  Initially PID gains where backwards but after fixes held depth.
2. Reached divewell window, had video lag issues
3. 3Ah battery runtime to 14v was about 10 minutes, maybe 30 minutes to completely dead
4. Foward speed was comprimised by burt out ESC, felt quite slow/hard to control (Video Lag)

## Issues:
1. Motor Mounts Broken In Transport
    * Acetone weld repair
    * Carbon Fiber Overwrap
    * Hard Carry Case
      * Sub Dimensions: 17" x 12" x 7" (L x W x H)
      * Nanuk 950 Waterproof Hard Case
2. Laggy video
    * Theories
      * CPU bottleneck due to thermal throttling?
      * Network issues due to water?
      * Could not reproduce either issue on bench
      * User error: Raw/Compress stream instead of Theora?
    * Can we detection condition by looking at image timestamps?
    * Respond by lowering stream quality 
      * /theora/quality
      * /theora/target_bitrate (default 800kBit)
      * These appear to have no effect
    * Reduce resolution to 320x240
    * Use NVIDIA streaming pipeline
      * Reduces CPU usage from 100% to 8% for 640x480 10fps
        * gst-launch-1.0 -e nvarguscamerasrc ! 'video/x-raw(memory:NVMM), width=640, height=480, format=NV12, framerate=10/1' ! nvv4l2h265enc bitrate=160000 ! rtph265pay mtu=1400 ! udpsink host=192.168.0.156 port=5000 sync=false async=false
         * gst-launch-1.0 udpsrc port=5000 ! application/x-rtp,encoding-name=H265,payload=96 ! rtph265depay ! h265parse ! queue ! avdec_h265 ! xvimagesink sync=false async=false -e
      * CPU usage only 28% for 1920x1080 30fps
      * Possible dual sink for deep learning and teleview?
3. Bad situation awarness (Killed Battery)
    * Dedicated Status UI
      * Pitch/Roll/Yaw indicators
      * Battery indicator
      * Control Axis Effort/State/Setpoint bar
     * Audible Alarm/UI Flashing below 12.5V
     * Motor Auto-Kill below 12V

4. Back Cap Pop due to thermal expansion of internal air
     * Short-Term: Pre-vaccum air a bit, higher efficency ESC?
     * Long-Term: ESC thermal coupling to rear plate/heatsink

5. Short Battery Life
   * 5Ah without battery formfactor change possible
     * Turnigy High Capacity 5200mAh 4S 12C Lipo Pack w/XT60
   * Consider 18650
     * 12 cells (Comfortable Fit) 9Ah
     * 20 cells (Nano Interference Fit) 15Ah
     * 24-36 cells (Bottom All Battery, Smaller ESCs, Single Sensor Board) 18-27 Ah

6. Tether Disconnected
   * Tether thimble and anchor point
7. ESC Carrier broke off
    *  Permanent Acetone Weld
    * Screw mount
8. Dead ESC
     * Keep spare ESCs on hand
9. Pitching when driving forwards
    * Lower center of mass by moving balast weights along bottom of tube   
## Next Test Plan
1. Verify bandwidth in pool.  640x480 10FPS stream only uses 160kbit/s so given 90mbit/s iperf result out of water hard to belive we would degrade below that level and see lag
2. Watch thermals thorughout test
3. Try nvidia streaming pipline for teleop
4. Check PID gain directions and tune pitch/roll/depth