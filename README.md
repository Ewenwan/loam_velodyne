![Screenshot](/capture.bmp)
Sample map built from [nsh_indoor_outdoor.bag](http://www.frc.ri.cmu.edu/~jizhang03/Datasets/nsh_indoor_outdoor.bag) (opened with [ccViewer](http://www.danielgm.net/cc/))

:white_check_mark: Tested with ROS Indigo and Velodyne VLP16. [(Screencast)](https://youtu.be/o1cLXY-Es54)

All sources were taken from [ROS documentation](http://docs.ros.org/indigo/api/loam_velodyne/html/files.html)

Ask questions [here](https://github.com/laboshinl/loam_velodyne/issues/3).


    利用2D Lidar解决SLAM问题已非常成熟，但2D只能得到二维地图，不能表达三维场景。
    于是很多学者就想能不能利用3D激光得到场景的三维点云，解决SLAM问题？
    LOAM就是其中的一个代表性方法，它分为三个版本，对应不同的硬件设备，
    分别为：back_and_forth，continous以及velodyne，分别针对前后摆动的二维扫描仪、
    连续旋转的二维扫描仪及Velodyne16线程激光扫描仪。各版本都有相应的数据集，
    且目前较为流行的KITTI数据集也包含Velodyne16线程的激光数据，都可以用来对程序进行测试。
    论文作者Zhang Ji写论文一直都很详细，通过仔细阅读论文，基本可将其算法复现。
    本文以velodyne的版本为主，但实际上三种方法大同小异（
    毕竟Lidar直接出来的三维激光可比旋转的2DLidar方便多了，
    如果你非要自己拿2D Lidar集成个微控、电机、编码器啥的我只能劝你别钻坑）。
    LOAM的整体思想就是将复杂的SLAM问题分为：
    1. 高频的运动估计； 
    2. 低频（低一个数量级）的环境建图。




How to build with catkin:

```
$ cd ~/catkin_ws/src/
$ git clone https://github.com/laboshinl/loam_velodyne.git
$ cd ~/catkin_ws
$ catkin_make -DCMAKE_BUILD_TYPE=Release 
$ source ~/catkin_ws/devel/setup.bash
```

Running:
```
roslaunch loam_velodyne loam_velodyne.launch
```

In second terminal play sample velodyne data from [VLP16 rosbag](https://db.tt/t2r39mjZ):
```
rosbag play ~/Downloads/velodyne.bag 
```

Or read from velodyne [VLP16 sample pcap](https://midas3.kitware.com/midas/folder/12979):
```
roslaunch velodyne_pointcloud VLP16_points.launch pcap:="/home/laboshinl/Downloads/velodyne.pcap"
```

---
[Quantifying Aerial LiDAR Accuracy of LOAM for Civil Engineering Applications.](https://ceen.et.byu.edu/sites/default/files/snrprojects/wolfe_derek.pdf) Derek Anthony Wolfe

[ROS & Loam_velodyne](https://ishiguro440.wordpress.com/2016/04/05/%E5%82%99%E5%BF%98%E9%8C%B2%E3%80%80ros-loam_velodyne/) 
