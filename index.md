---
title: "GPS Based Autonomous Navigation"
image: 
  path: Images/snazzy-image-3.png
  caption: "Photo from [SnazzyMaps](https://snazzymaps.com/style/74/becomeadinosaur)"
categories:
  - Layout
tags:
  - content
  - image
  - layout

---
<p style="text-align:center">An exploration in autonomous driving built around the GPS</p>

<br>
<br>

### _Background_ 

Our team’s project in the context of our domain is to build an autonomous GPS-based navigation system. The challenge in this project primarily comes down to understanding the shortcomings of the GPS being used so that its problems can be mitigated through supplementary methods. Not mentioning the differences in accuracy between GPS products at different price points, GPS’s in general tend to suffer from issues of signal interference which lead to delays in positioning updates and lack of precision as well as oscillating data even when left at a fixed position. To build a navigation system for a vehicle that will travel at high speeds, it is crucial that vehicle positioning is provided accurately and quickly. The hurdle for our project, then, is to create a reliable navigation system using GPS that can update instantaneously and precisely despite these being the inherent issues that plague the GPS. 
<hr>

<br>
<br>

### _Part 1: GPS Selection_

Finding a GPS accurate enough was a crucial first step of our project since a navigation system built on a faulty GPS can only be so reliable. 
To do this, we needed metrics to evaluate the two GPS models that we had: u-blox's NEO-M8N and ZED-F9P. We use Circular Error Probable (CEP) and 2D Root Mean Square (2DRMS) to do so. We can interpret the metrics as follows:

1. A CEP of 5 meters lets us know that for 50% of the GPS outputs, we can expect the output to be within 5 meters of the true position. 
2. A 2DRMS of 5 meters lets us know that for 95% of the GPS outputs, we can expect the output to be within 5 meters of the true position.


The graphs below are the results that we obtained from quality testing u-blox's NEO-M8N and ZED-F9P. For more details of how we tested our GPS, please refer to
the video attached at the bottom of the page.

NEO-M8N Performance            |  ZED-F9P Performance
:-------------------------:|:-------------------------:
![neo](Images/neo_m8n_cep_2drms.png)  |  ![zed](Images/zed_f9p_park_cep_2drms.png)

- For the ZED-F9P, CEP is 0.097 meters and the 2DRMS is 0.233 meters.
- For the NEO-M8N, CEP is 1.532 meters and the 2DRMS: 3.710 meters.

From these results, we can see that the ZED-F9P performs significantly 
better then the NEO-M8N. Thus, we chose the ZED-F9P to fit onto our vehicle. 
<hr>

<br>
<br>

### _Part 2: Sensor Fusion_
 

In order to navigate with a GPS, an accurate vehicle heading is just as necessary as an accurate position. By integrating odometry, IMU, and GPS data together, we can obtain both vehicle position and orientation. To accomplish this task, we used a state estimation algorithm, Extended Kalman Filter (EKF). EKF takes in the positional information from the GPS, the acceleration and orientation data from the IMU, and the velocity measurements from both odometry and IMU to filter out noisy readings from each sensor. It provides us with an estimate of the current vehicle location more accurately than these three sensors can provide on their own and allows us to directly combine three separate data streams into a single source that contains both an accurate position and orientation. The picture below is a demonstration of EKF's accuracy. 

![Sensor Fusion](Images/Sensor_Fusion.png)

Each of the red arrows is a reading of the vehicle’s positioning and orientation as the vehicle remains in a stationary point. 
We simulated some noise in the y-axis specifically so the readings are erratic along the y-axis even though the vehicle has not moved. 
The blue arrow is the odometry and IMU data after it has been filtered by EKF. There are actually multiple blue arrows stacked 
on top of each other as EKF filters out each noisy reading to produce a consistent vehicle positioning. Compared to the raw odometry
and IMU data, you can see that filtering noisy data using EKF data is much more accurate to the vehicle’s positioning in both the x and y direction. 

![sims](Images/ground_truth_vs_estimated.png)
Over the course of a full lap around the UCSD Warren track, the EKF algorithm was able to reduce the error in vehicle localization essentially down to zero. 
<hr>

<br>
<br>

### _Part 3: Global Path Planning_
Creating an autonomous navigation system that is only reliant on GPS is essentially the same thing as driving blindfolded. To base navigation purely on GPS, the first requirement is to obtain a detailed map of the desired track to race on. This navigation map is a binary masked image where white indicates allowable driving area and black represents non-drivable areas. Using the Thunderhill Raceway track in Willows, CA we obtained high resolution satellite images that served as a basis for a navigation map. From this satellite image, a combination of both automatic and manual image processing techniques can be used to create the final binary mask. Once a mask is created, it is possible to implement navigation algorithms that will generate a feasible path for the vehicle. 

Thunderhill Satellite           |  Thunderhill Binary Mask
:-------------------------:|:-------------------------:
![thunderhill](Images/thunderhill.png)  |  ![binary](Images/binarythunderhill.png)


### _Part 4: Waypoint Selection and Navigation_

![buff](Images/BUFFER_RADIUS_DIAGRAM.png)

We set a buffer radius for each waypoint we want to go to so that we don't "miss" a waypoint & make incorrect navigation choices just because noisy data. 

![distance](Images/DISTANCE_CALUCLATION.png)

We use a lookahead point to determine if we've reached our current waypoint. 

![wpt](Images/WAYPOINT CONFIRMATION FLOWCHART-4.png)

An overview of exactly how waypoint navigation would be determined. 
<hr>

### Our Final Result & Presentation!

<iframe width="560" height="315" src="https://www.youtube.com/embed/DJktMnLdI_I" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>



