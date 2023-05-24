Aidan Capaldi

#### Research Items and Questions: 
- Skating project
	- Which metrics do we want to record? 
		- What hardware can measure these things in a useful way? 
	- What tech stacks are useful and applicable for the scope of our application? 
- ROS-related: 
	- How does ROS setup work? 
	- Can we leverage ROS to do any math for our application (path calculation / rendering)?
	- Do we need it at all if we have no moving parts?

##### Deciding on Metrics
I personally would like an application which can display forces and values exerted by the skater which include maximum velocity, sharpest turn, and, most critically, a semi-accurate representation of their path taken while skating. 

[![Skating Physics](https://www.real-world-physics-problems.com/images/physics_ice_skating_1.png)]

Though speed skating is a different sport than figure skating, this diagram provides a really useful look into the forces involved. 
```latex 
g: acceleration due to gravity
G: center of mass
P: point of contact with blades and ice
L: distance between P and G
F_x: horizontal contact force between the ice and the skater's blade at P
F_y: vertical contact force between the ice and the skater's blade at P
R: radius of the turn (from center of turn to center of mass)
a_c: centripetal acceleration of point G
\theta: angle between horizontal and line passing through P and G
```
We can derive the following equations:
```latex
% G has zero vertical acceleration \therefore forces in vertical direction sum to zero. M is the mass of the system
(1) F_y - mg = 0
% Applying Newton's second law
F_x = m a_c
% Centripetal acceleration
a_c = \frac{v^2}{R}
% Substitution
(2) F_x = m \frac{v^2}{R}
```
Assuming a constant `theta` (rotational equilibrium), we know there is a zero moment acting on the system about the center of mass:
```
(3) F_x \sin \theta \dot L - F_y \cos \theta \dot L = 0
\therefore \\ 
(4) tan \theta = \frac{Rg}{v^2}
```

To map out a path, we can use the mass and velocity values of the skater and these equations to trace a line. 
 
We may be interested in using an IMU to measure `\theta` and the related forces acting at the blade point. Mounting one there could prove useful. An IMU typically consists of  accelerometers,  gyroscopes, and magnetometers. IMUs provide information (raw or filtered) about the angular rate or specific force and acceleration experienced by the object tow which it is attached. 

Bear in mind that IMUs come with different dimensions; if we are interested in seeing any other things than a bird's-eye view of the skater's path on the ice we will need 3-axis IMUs. We should also beware IMU drift (accumulated error), that could impact our readings.
Here is a further guide on [Arduino integration and IMU options](https://www.seeedstudio.com/blog/2020/01/17/what-is-imu-sensor-overview-with-arduino-usage-guide/) which I was perusing.

##### ROS and Feasible Hardware
Supported list of sensors for [pose estimation](http://wiki.ros.org/Sensors/Pose%20Estimation). Sensors on this list have firmware which is regularly maintained. Pose estimation gives information about the absolute or relative position of a robot (or, in our case, the robot being the skate).

`adi_driver` provides a promising Linux-enabled interfacing with the ADIS16470 IMU and the ADXL345 accelerometer. The accelerometer provides raw data in the form of acceleration values in an array. Here is a [data sheet](https://www.analog.com/media/en/technical-documentation/data-sheets/adxl345.pdf) which walks through all the use modes and features of the accelerometer. 
The accelerometer is cheap, and the IMU is not ($300-400 range). 

###### Why bother?
ROS has the ability to record and playback the [path taken by a robot](http://wiki.ros.org/ROS/Tutorials/Recording%20and%20playing%20back%20data) a la "turtle graphics", and we could use the recorded IMU data to map out a `rosbag` recording which can be used for creating a visual path representation. 

>**[rosbag](http://wiki.ros.org/rosbag)** is a command line tool that records messages and allows you to play them back later. You can think of a rosbag as similar to a digital video file that records not only video but also other types of sensor messages. Think of it as a multi-track recording, where you can have not only a video track but also a sound track, an IMU track, and so on. There is a master time code which then allows all of the messages to synchronize when they play back.

We theoretically should be able to have an IMU track which lets us keep track of the data from the robot (skate). Using this data, we can map out the desired information and pass it to the app. 

However, we could also not use ROS should an Arduino integration be sufficient (we only need to read the IMU data and manipulate it, no robot actuation or operation). 

###### Sources 
[IMU wearables](https://www.researchgate.net/figure/The-example-of-how-the-IMUs-attached-on-the-index-finger-measure-the-rotation-a-The_fig5_336864649)
[IMU function](https://en.wikipedia.org/wiki/Inertial_measurement_unit)
[ADXL data](https://www.analog.com/en/products/adxl345.html#product-reference)
[ROS example](https://www.toptal.com/robotics/introduction-to-robot-operating-system#:~:text=ROS%20provides%20functionality%20for%20hardware,and%20visualization%2C%20and%20much%20more.)
[ROS path recording](http://wiki.ros.org/ROS/Tutorials/Recording%20and%20playing%20back%20data)
