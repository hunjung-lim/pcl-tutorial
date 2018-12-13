ROS파일에서 PCD파일 추출 하기


http://wiki.ros.org/pcl_ros

rosrun pcl_ros bag_to_pcd <input_file.bag> /<topic> <output_directory>
rosrun pcl_ros bag_to_pcd lobby_velodyne.bag /velodyne_points ./lobby_pcd
