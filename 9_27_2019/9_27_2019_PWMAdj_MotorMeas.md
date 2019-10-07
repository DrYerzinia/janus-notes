# Janus : Motor Measurments & PWM Adjustments (9/27/2019)

## PWM Adjustments

During inital motor testing it appeared there was a bias between reversed motors in terms of thrust.  This was belived to be due to the adjustment that was done to the PWM range for the PCA9685.  It was set to (1085, 2000) so that a thrust command of 0.5 was a center PWM value of 1500uS.

An oscilicope was attached to one of the signal lines and the PWM range was set to (1100, 1900) to match the programmed values of the ESCs.  The neutral PWM value was measured to be 1440uS.  The range was adjusted to (1160, 2060) to compensate and then the PWM values where measured at 100uS intervals.


| In PWM | Out PWM |
|--------|---------|
|   1000 |    1116 |
|   1100 |    1196 |
|   1200 |    1272 |
|   1300 |    1348 |
|   1400 |    1424 |
|   1500 |    1500 |
|   1600 |    1576 |
|   1700 |    1656 |
|   1800 |    1732 |
|   1900 |    1812 |
|   2000 |    1888 |

We can see that the 1000-2000 uS range used by the cusub system is correctly mapped to the 1100-1900 setup for the ESCs.

## Motor Measurments

The forward thrust of the motors was measured in 50uS intervals by measuring the downforce from the motors.  The sub was placed in a bucket with duct tape around the body.  A hanging scale was hooked onto the duct tape and the hanging scale was attached to a shower curtain rod that was installed above the bucket.  The height of the current rod was set to keep the scale out of the water while allowing the sub to be submered several inches below the water.  This setup has considerable issues when trying to measure higher thrusts as the boundary conditions of the surface of the water and the small container size have a large effect.  The higher thrusts are likley inaccurate and a better method will have to be devised to measure them accuratly.

|Relative PWM|Downforce (lb)|Thrust (N)|
|------------|--------------|----------|
|          0 |          0   |   0      |
|         50 |          0   |   0      |
|        100 |          0.2 |   0.2224 |
|        150 |          0.6 |   0.6672 |
|        200 |          1.0 |   1.112  |
|        250 |          1.7 |   1.89   |
|        300 |          2.4 |   2.669  |
|        350 |          2.8 |   3.114  |
|        400 |          3.0 |   3.336  |
|        450 |          3.1 |   3.447  |
|        500 |          3.2 |   3.559  |

We can see a small deadzone from 0 to 50uS.  These values should be used in the motor driver to linearize the force applied given a control effort.