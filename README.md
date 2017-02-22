# Code & Dataset for mesh-based scene estimation 
This work is described in the paper "Real-Time Mesh-based Scene Estimation for Aerial Inspection", by Lucas Teixeira and Margarita Chli, published in the Proceedings of the IEEE/RSJ Conference on Intelligent Robots and Systems (IROS) 2016 [[paper](http://ieeexplore.ieee.org/document/7759714/)].

#### Video:
<a href="https://www.youtube.com/embed/LvmBjMvmZKA" target="_blank"><img src="http://img.youtube.com/vi/LvmBjMvmZKA/0.jpg" 
alt="Mesh" width="240" height="180" border="10" /></a>

If you use this Code or Dataset, please cite the following publication:
 
```
 @inproceedings{Teixeira:etal:IROS2016,
title	= {{Real-Time Mesh-based Scene Estimation for Aerial Inspection}},
author	= {Lucas Teixeira and Margarita Chli},
booktitle	= {Proceedings of the {IEEE/RSJ} Conference on Intelligent Robots and Systems({IROS})},
year	= {2016}
}
```

## Code

The code that we developed is an extension of [OKVIS](https://github.com/ethz-asl/okvis). On this repository you can find the part of the code that implement the algorithm described in the our paper. You have to adapt in order to with your code, but it is a fairly simple implementation. There are small improvements and adaptation, mainly in the rasterization part. We recommend instead of use this code, you should run the code already integrate on OKVIS. We will give the instructions below. 

### Working Example
This example embedded our code inside OKVIS. We also have added a new topic to publish a point cloud that is sampled over the mesh. 

If you use the example code, please acknowledge our paper, OKVIS papers and the Fade2d library.

### License
The original [OKVIS](https://github.com/ethz-asl/okvis) is BSD, but we use two libraries that are not. Fade2D is a commercial software that can be used for research proposes for free. Please check their website http://www.geom.at/ . The new rasterization code is inspired by the [Scratchapixel.com's Tutorial](http://www.scratchapixel.com/lessons/3d-basic-rendering/rasterization-practical-implementation) and they request GPLv3 license. We will be working to remove this dependence in the future, but, in summary, this code only can be used for research and under GPLv3 license. 


#### Dependences
This code was tested on the Ubuntu 14.04 and using ROS Indigo. Our code should work on the same environment that OKVIS works, but we have a extra dependency that is the Fade2D. We added the Fade2D binaries on the example code. If you wanna run in another distribution you have to change the Fade2D library on the main CMakeLists. 

```bash
sudo apt-get install cmake ros-indigo-pcl-ros libgoogle-glog-dev libatlas-base-dev libeigen3-dev libsuitesparse-dev libboost-dev libboost-filesystem-dev libopencv-dev
```

#### Building
The best way to try this example is creating a new catkin workspace. In case of you use an old workspace, you cannot have okvis_ros inside, given we did not change the name of the package. The installation instruction from the [okvis_ros github repository](https://github.com/ethz-asl/okvis_ros) is also a good source of information.


```bash
cd ~/catkin_ws/src
git clone --recursive https://github.com/weblucas/okvis_ros_mesh_mapping.git
cd ..
catkin build
```

#### Running

You can see our algorithm running using the provided launch file and one of the bagfiles from our ETHZ_V4RL-CAB Dataset. The links are in the next section. The configuration file *config_fpga_v4r4.yaml* already contains the calibration data for this dataset, but only using one camera.

In one terminal you should run the line below just changing the location of the bagfile that you download.
```bash
roslaunch okvis_ros okvis_node_synchronous_mesh_mapping.launch \
           bagfile:=/home/lucas/data/iros16/ethz_v4rl_ground.bag
```

In another terminal you should run rviz with our configuration file
```bash
rviz -d /home/lucas/catkin_ws/src/okvis_ros_mesh_mapping/config/rviz.rviz
```




## ETHZ_V4RL-CAB Dataset

### Examples
<a href="https://www.youtube.com/embed/SA4KoRjvx04" target="_blank"><img src="http://img.youtube.com/vi/SA4KoRjvx04/0.jpg" 
alt="Aerial 1" width="200"  border="10" /></a>
<a href="https://www.youtube.com/embed/FEQiClIlLZI" target="_blank"><img src="http://img.youtube.com/vi/FEQiClIlLZI/0.jpg" 
alt="Aerial 2" width="200"  border="10" /></a>
<a href="https://www.youtube.com/embed/HLIJ59BRaBo" target="_blank"><img src="http://img.youtube.com/vi/HLIJ59BRaBo/0.jpg" 
alt="Aerial 3" width="200"  border="10" /></a> 
<a href="https://www.youtube.com/embed/a-ITwYMPzZs" target="_blank"><img src="http://img.youtube.com/vi/a-ITwYMPzZs/0.jpg" 
alt="Ground" width="200"  border="10" /></a> 


### Data
**Aerial 1** - [Bagfile](https://drive.google.com/open?id=0B82ekrhU9sDmTTdIeFJXTlBBLVE) - [Youtube](http:/ /www.youtube.com/embed/SA4KoRjvx04)

**Aerial 2** - [Bagfile](https://drive.google.com/open?id=0B82ekrhU9sDmNjZiMTUxUWlHcnc) - [Youtube](http:  //www.youtube.com/embed/FEQiClIlLZI)
 
**Aerial 3** - [Bagfile](https://drive.google.com/open?id=0B82ekrhU9sDmOUkzX2xrMWRSMEE) - [Youtube](http://www.youtube.com/embed/HLIJ59BRaBo)

**Ground** - [Bagfile](https://drive.google.com/open?id=0B82ekrhU9sDmTjVweklrNGdJTjA) - [Youtube](http://www.youtube.com/embed/a-ITwYMPzZs)


### Calibration
The images where captured using a [VI-Sensor](http://wiki.ros.org/vi_sensor) and calibrated using [ETHZ ASL Kalibr](https://github.com/ethz-asl/kalibr). We show below the calibration result. Most values are straightforward. T_SC is the transformation from the Camera to the Sensor(IMU). There is two sets of values, camera0's intrinsics and camera1's intrinsics, respectively.

```python

cameras:
    - {T_SC:     
        [ 0.9999921569165363, 0.003945890103835121, 0.0003406709575200133, -0.030976405894694664,        
         -0.003948017768440125, 0.9999711543561547, 0.0064887295612456805, 0.003944069243840622,         
         -0.00031505731688472255, -0.0064900236445916415, 0.9999788899431723, -0.016723945219020563,
         0.0, 0.0, 0.0, 1.0],
        image_dimension: [752, 480],
        distortion_coefficients: [0.0038403216668672986, 0.025065957244781098, -0.05227986912373674, 0.03635919730588422],
        distortion_type: equidistant,
        focal_length: [464.2604856754006, 463.0164764480498],
        principal_point: [372.2582270417875, 235.05442086962864]}
    - {T_SC:
        [ 0.9999722760516375, 0.007329193771005421, 0.0013153124248847282, 0.0790982900835488,
          -0.007335059837348439, 0.9999629194070246, 0.004511840884063492, 0.003549628903031918,
          -0.0012821954962168199, -0.00452136369336114, 0.9999889565615523, -0.01713313929463862,
          0.0, 0.0, 0.0, 1.0],
        image_dimension: [752, 480],
        distortion_coefficients: [0.00823121215582322, -0.015270152487108836, 0.03085334360639285, -0.017760720995454376],
        distortion_type: equidistant,
        focal_length: [456.3683366282091, 455.03924786357857],
        principal_point: [375.1783411236692, 238.22971133267725]}
```
## Qualitative Results
You can reproduce the qualitative results of our [paper](http://ieeexplore.ieee.org/document/7759714/) using this [bagfile](https://drive.google.com/open?id=0B82ekrhU9sDmT3hiV3pPakdrTXc) and this ground-truth [laser scan](https://drive.google.com/open?id=0B82ekrhU9sDmN2QyOFlFNHA5c2c). You can also visualize the point-cloud inside the RViz software together with the laser scan of the facade. You only need to use *rosbag play* to run the bagfile. You can use the ros node *read* from the package [ethz-asl:point_cloud_io](
https://github.com/ethz-asl/point_cloud_io).

#Contact
Please create an issue if you have questions or bug reports. Alternatively, you can also contact me at lteixeira@mavt.ethz.ch.
 
 
 
 
