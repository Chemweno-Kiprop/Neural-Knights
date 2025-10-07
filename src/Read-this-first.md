
To Run simulation

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
p
```
 I've included m2.* maps in the workspace that correspond with world1.world. You can try it out for navigation.

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
On
```bash
ros2 launch articubot_one launch_robot.launch.py
```

Confirm its path is /dev/ttyACM0. If not, change the path in description/ros2_control.xacro


Even if you don't bother with the other parameters **make sure** you nail these:
* Robot radii for both local and global costmaps
* Inflation radii for both local and global costmaps

