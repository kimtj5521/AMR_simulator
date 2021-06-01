# AMR_simulator
Autonomous Mobile Robot (AMR) ROS Gazebo simulator

This repo contains two types of AMR: 
1. Differential drive type
2. Omni-directional drive type

## How to build the simulator
- Clone the repository and catkin_make:
```
cd ~/catkin_ws/src
git clone https://github.com/kimtj5521/AMR_simulator
cd ../
catkin_make
source ~/catkin_ws/devel/setup.bash
```

## Differential drive type Example
```
roslaunch amr_simulation dd_amr_simulation.launch
```

## SLAM using google cartographer
- Occupancy grid base SLAM
```
roslaunch amr_simulation amr_slam_occ.launch
```

- TSDF base SLAM
```
roslaunch amr_simulation amr_slam_tsdf.launch
```

## Save cartographer map and convert for navigation
```
rosservice call /finish_trajectory 0
rosservice call /write_state "map_name.pbsteam" true
# example rosservie call /write_state ${HOME}/catkin_ws/src/amr_simulation/pbstream/map.pbstream true

# occupancy grid map case
rosrun map_server map_saver -f your_map.pbstream --occ 65 --free 20

# TSDF grid map case
rosrun map_server map_saver -f your_map.pbstream --occ 35 --free 15

```
If you want to get more information of usage about cartographer, 
please refer to [Cartographer_ROS](https://google-cartographer-ros.readthedocs.io/en/latest/)

You can convert the pbstream file to pgm+yaml files through using the ros map_server.

Occupied space and free space threshold values can be changed to your own threshold.

## Map based localization 

Change map path in launch file.

- Occupancy grid map
```
roslaunch amr_simulation amr_occ_localization.launch
```

- TSDF map
```
roslaunch amr_simulation amr_tsdf_localization.launch
```
