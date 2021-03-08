# GPS Autonomous Navigation

## An exploration into autonomous navigation with a GPS

### Background 

Our team’s project in the context of our domain is to build an autonomous GPS-based navigation system that will be robust and reliable enough to be competitive in a race. The challenge in doing so primarily comes down to understanding the shortcomings of the GPS being used so that its problems can be mitigated through supplementary methods. In addition to the differences in accuracy between GPS products at different price points, GPS’s in general tend to suffer from issues of signal interference which lead to delays in positioning updates and lack of precision as well as oscillating data even when left at a fixed position. To build a navigation system for a vehicle that will travel at high speeds, it is crucial that vehicle positioning is provided accurately and quickly. The hurdle for our project, then, is to create a reliable navigation system using GPS that can update instantaneously and precisely despite these being the characteristic issues that plague the GPS.

### GPS Comparisons: u-blox NEO-M8N vs ZED-F9P
NEO-M8N Performance:



ZED-F9P Performance:

![Sensor Fusion](Images/1_Unit_RTK_CEP.png)

- For the ZED-F9P, CEP is 0.318 feet and 2DRMS is 0.766 feet.
- For the NEO-M8N, CEP is .... and 2DRMS is ....
- Description: comparison & results

### GPS Solo Navigation

Maybe some rviz photos & explanations of solo navigation

### GPS & IMU Sensor Fusion
 
Sensor Fusion

![Sensor Fusion](Images/Sensor_Fusion.png)

The red arrows are the raw IMU and odometry data that we embedded
some noise into its y-axis. The blue arrow is EKF-filtered odometry 
and IMU data. As you can see, EKF is able to reduce the noise and 
provide a more accurate position of the vehicle.


### Waypoint Selection and Navigation

** maybe some flow charts & explanations ***

### Conclusion (video of it moving?) 
