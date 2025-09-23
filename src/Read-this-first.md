There wasn't time to migrate to Gazebo fortress :(
But this is tested to work in classic, both slam and navigation 

You may want to change the name of the package from articubot_one to something else. You can open the src folder in VSCode and use Ctrl+Shift+F to change every instance of 'articubot_one'

Please watch Josh's videos first. 

[Slam](https://www.youtube.com/watch?v=ZaiA3hWaRzE&list=PLunhqkrRNRhYAffV8JDiFOatQXuU-NnxT&index=17&pp=iAQB)

[Nav](https://www.youtube.com/watch?v=jkoGkAd0GYk&list=PLunhqkrRNRhYAffV8JDiFOatQXuU-NnxT&index=18&pp=iAQB)



Launch rviz:
```bash
cd Neural-Knights
rviz2 -d ./src/articubot_one/config/map_navigation.rviz
```

Launch simulation:
```bash
cd Neural-Knights
ros2 launch articubot_one launch_sim.launch.py use_sim_time:=true world:=./src/articubot_one/worlds/world1.world
```

Launch slam:
```bash
cd Neural-Knights
ros2 launch articubot_one online_async_launch.py use_sim_time:=true slam_params_file:=./src/articubot_one/config/mapper_params_online_async.yaml
```

Save your map. You can use either slam_toolbox for localization or nav2_amcl. Details in Josh's tutorial. I've included m2.* maps in the workspace that correspond with world1.world. You can try it out for navigation.

For navigation:
You may relaunch the simulation/robot but it is not absolutely necessary

Launch localization:
```bash
cd Neural-Knights
ros2 launch articubot_one localization_launch.py map:=your_map_path.yaml use_sim_time:=true
```


Launch navigation:
```bash
cd Neural-Knights
ros2 launch articubot_one navigation_launch.py map_subscribe_transient_local:=true params_file:=./src/articubot_one/config/nav2_params.yaml use_sim_time:=true
```

You can use the `2d pose estimate` button to place your robot at the correct location in the map in case it drifts off. Details in Josh's video. 


For the actual robot, replace every instance of "use_sim_time:=true" to "use_sim_time:=false", then use this instead of launch_sim:
```bash
ros2 launch articubot_one launch_robot.launch.py
```

Confirm its path is /dev/ttyACM0. If not, change the path in description/ros2_control.xacro

Slam and navigation have **a lot** of parameters. Check out these pages for guides
https://docs.nav2.org/tuning/index.html
https://docs.ros.org/en/humble/p/slam_toolbox/

Even if you don't bother with the other parameters **make sure** you nail these:
* Robot radii for both local and global costmaps
* Inflation radii for both local and global costmaps


Sources
* articubot_one https://github.com/joshnewans/articubot_one/tree/humble
* serial https://github.com/joshnewans/serial/tree/newans_ros2
* diffdrive_arduino https://github.com/RedstoneGithub/diffdrive_arduino
* Gazebo_ros2_control https://github.com/ros-controls/gazebo_ros2_control/tree/humble