# multi_map_merge
机器人1
 ssh ubuntu@192.168.1.100
[TurtleBot] 
ROS_NAMESPACE=tb3_0 roslaunch turtlebot3_bringup turtlebot3_robot.launch multi_robot_name:="tb3_0" set_lidar_frame_id:="tb3_0/base_scan"
[Remote PC]启动第一台小车模型 
ROS_NAMESPACE=tb3_0 roslaunch turtlebot3_bringup turtlebot3_remote.launch multi_robot_name:=tb3_0
启动第一台slam建图
ROS_NAMESPACE=tb3_0 roslaunch turtlebot3_slam turtlebot3_gmapping.launch set_base_frame:=tb3_0/base_footprint set_odom_frame:=tb3_0/odom set_map_frame:=tb3_0/map

机器人2
ssh ubuntu@192.168.1.107
[TurtleBot]
 ROS_NAMESPACE=tb3_1 roslaunch turtlebot3_bringup turtlebot3_robot.launch multi_robot_name:="tb3_1" set_lidar_frame_id:="tb3_1/base_scan"
[Remote PC] 启动第二台小车模型
ROS_NAMESPACE=tb3_1 roslaunch turtlebot3_bringup turtlebot3_remote.launch multi_robot_name:=tb3_1
启动第二台slam建图
ROS_NAMESPACE=tb3_1 roslaunch turtlebot3_slam turtlebot3_gmapping.launch set_base_frame:=tb3_1/base_footprint set_odom_frame:=tb3_1/odom set_map_frame:=tb3_1/map
启动地图合并
roslaunch turtlebot3_bringup  turtlebot3_multi_map_merge.launch
[Remote PC] 启动rviz
rosrun rviz rviz -d `rospack find turtlebot3_bringup`/launch/multi_turtlebot3_slam.rviz
[Remote PC]启动第一台机器人键盘控制
ROS_NAMESPACE=tb3_0 rosrun turtlebot3_teleop turtlebot3_teleop_key
 启动第二台机器人键盘控制
 ROS_NAMESPACE=tb3_1 rosrun turtlebot3_teleop turtlebot3_teleop_key
 启动第二台机器人键盘控制
 ROS_NAMESPACE=tb3_2 rosrun turtlebot3_teleop turtlebot3_teleop_key


注意建图效果与初始位置有关（机器人正面为X轴的负方向，且实物距离（单位为米）：参数=1：20。）
