# GPS Autonomous Navigation

## An exploration into autonomous navigation with a GPS

### Background 

Our team’s project in the context of our domain is to build an autonomous GPS-based navigation system that will be robust and reliable enough to be competitive in a race. The challenge in doing so primarily comes down to understanding the shortcomings of the GPS being used so that its problems can be mitigated through supplementary methods. In addition to the differences in accuracy between GPS products at different price points, GPS’s in general tend to suffer from issues of signal interference which lead to delays in positioning updates and lack of precision as well as oscillating data even when left at a fixed position. To build a navigation system for a vehicle that will travel at high speeds, it is crucial that vehicle positioning is provided accurately and quickly. The hurdle for our project, then, is to create a reliable navigation system using GPS that can update instantaneously and precisely despite these being the characteristic issues that plague the GPS.

### GPS Comparisons: u-blox NEO-M8N vs ZED-F9P
NEO-M8N Performance:
![Sensor Fusion](Images/neo_m8n_cep_2drms.png)

- For the NEO-M8N, CEP is 1.532 meters and the 2DRMS: 3.710 meters.

ZED-F9P Performance:

![Sensor Fusion](Images/1_Unit_RTK_CEP.png)

- For the ZED-F9P, CEP is 0.097 meters and the 2DRMS is 0.233 meters.

From these results, we can see that the ZED-F9P performs significantly better then the NEO-M8N. Thus we chose this GPS for the purposes of developing an autonomously navigating vehicle! 

### GPS & IMU Sensor Fusion
 
We fused together our GPS with an IMU using an Extended Kalman Filter (EKF). 

![Sensor Fusion](Images/Sensor_Fusion.png)

The red arrows are the raw IMU and odometry data that we embedded
some noise into its y-axis. The blue arrow is EKF-filtered odometry 
and IMU data. As you can see, the EKF is able to reduce the noise and 
provide a more accurate position of the vehicle.


### Waypoint Selection and Navigation

** maybe some flow charts & explanations ***

### Conclusion (video of it moving?) 
