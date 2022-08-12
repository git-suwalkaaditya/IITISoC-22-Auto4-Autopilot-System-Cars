# Demo of Prius in ROS/GAZEBO

This is a simulation of a Prius in [gazebo 9](http://gazebosim.org) with sensor data being published.
The car's throttle, brake, steering, and gear shifting are controlled by publishing a ROS message.
A ROS node allows driving with a gamepad or joystick.

# Video + Pictures

A video and screenshots of the demo can be seen in this blog post: https://www.osrfoundation.org/simulated-car-demo/

![Prius Image](https://www.osrfoundation.org/wordpress2/wp-content/uploads/2017/06/prius_roundabout_exit.png)






# Running

First you need to build the ```car_demo``` package:
```
$ mkdir -p osrf_car/src
$ cd osrf_car/src
$ git clone https://github.com/git-suwalkaaditya/car_demo.git
$ cd ..
$ catkin_make
$ source devel/setup.bash
```
Now to run the simulation:

```
$ roslaunch car_demo demo.launch
```

To move the car, run the following sample code:
```
$ rosrun car_demo move.py
```
