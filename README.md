# ORB-SLAM2
ORB-SLAM+Realsense

1.配置realsense 

1.1安装realsense的sdk
安装地址为：http://wiki.ros.org/librealsense2
注意：貌似没有什么坑，直接安装安装步骤一步一步来就行。

１.2安装realsense和ros的接口
安装地址为：http://wiki.ros.org/realsense2_camera
注意：１．启动的launch文件是：roslaunch realsense2_camera rs_camera.launch，这样会把深度图　红外图　彩色图全部发布出来。千万不可以只launch
rs_rgbd.launch这一个文件，这样没有深度图，orb-slam跑起来的效果就会很一般。
２．有很多参数是可以设置的，可以想办法设置一下（需要调参）

１.3 升级realsense的驱动
注意：如果不升级驱动的话，可能会导致相机深度图读不出来，初始状态的固件版本是很低的，需要刷新高来。刷新固件建议再ubuntu下，方法如下。
安装链接：https://www.intel.com/content/dam/support/us/en/documents/emerging-technologies/intel-realsense-technology/Linux-RealSense-D400-DFU-Guide.pdf

２．配置orb-slam 
安装地址为：https://github.com/raulmur/ORB_SLAM2

２．１安装依赖
pangolin opencv eigen3 g2o主要是这几个。
注意：１．安装opencv: opencv3.2出现了和cuda9.0冲突的情况。解决方法是:卸载cuda9.0　
２．eigen3版本问题：３．３版本有些更新了，原有的一些函数被弃用。orb-slam使用了３．１，所以有些函数会提示找不到。所以最好的办法是安装３．１

２．２ｒｏｓ节点
注意：１. export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:PATH/ORB_SLAM2/Examples/ROS 这个要写进bashrc里面，然后还要source成功，不然没办法build

2.3 rosrun 
rosrun ORB_SLAM2 RGBD /home/qi/orbslam_ws/src/ORB_SLAM2/Vocabulary/ORBvoc.txt /home/qi/orbslam_ws/src/ORB_SLAM2/Examples/ROS/ORB_SLAM2/Asus.yaml /camera/rgb/image_raw:=/camera/color/image_raw /camera/depth_registered/image_raw:=/camera/infra1/image_rect_raw
注意:１．需要orb字典，可能是用来特征匹配的　２．需要修改相机参数：内参肯定要修改，信息再realsense的/camera/color/camera_info里面　（Ｋ是内参，Ｄ是畸变）２．畸变貌似realｓｅｎｓｅ的畸变是０（可能已经矫正过畸变了),别的相机需要矫正
３．左边是orb需要的topic 右边是realsense实际的topic 

３．还有一些报错参考oneonte 
