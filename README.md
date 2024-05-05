# CDF
road to the best robot

# Create a robot using onshape

The name of the link should be : dof_nameofthelink
The only link accepted in the following simulation are :fixed, revolute and prismatic

To create a caster wheel I chose to use a fixed link and in the simulation give it a friction of 0 then it is allow to move in any direction.

# Step to follow to use it 

On a linux environment

### Install onSHape to Urdf python module
sudo pip install onshape-to-robot

###  Or you can install it in a virtual environment of python
python -m venv onshape_venv
source onshape_venv/bin/activate

###  You should see now in your linux promt the (onshape_venv)
pip install onshape-to-robot
​
### Install Dependencies
sudo add-apt-repository ppa:openscad/releases
sudo apt-get update
sudo apt-get install openscad -y 
sudo apt-get install meshlab -y 
​
### Add the OnShapeKeys to the `keys.sh` file
cd ~/ros2_ws
touch keys.sh
chmod +x keys.sh
​
### Source the keys and check
cd ~/ros2_ws
source keys.sh
echo $ONSHAPE_API
echo $ONSHAPE_ACCESS_KEY
echo $ONSHAPE_SECRET_KEY
​
### Create the ROS2 package and some folders
cd ~/ros2_ws/src
ros2 pkg create --build-type ament_cmake quadruped_description --dependencies urdf xacro
cd quadruped_description
mkdir quadruped
touch quadruped/config.json
​
mkdir launch
mkdir rviz
​
### Export form OnShape to URDF file
cd ~/ros2_ws/src/quadruped_description
Execute th export
onshape-to-robot quadruped
​
### Create launch files
cd ~/ros2_ws/src/quadruped_description
touch launch/quadruped.launch.py
touch launch/start_rviz.launch.py
touch rviz/quadruped.rviz
​
### Build
cd ~/ros2_ws/
source install/setup.bash
colcon build --packages-select quadruped_description
source install/setup.bash
​
### Launch Generated system
cd ~/ros2_ws/
source install/setup.bash
ros2 launch quadruped_description quadruped.launch.py
​
Dans un autre terminal

cd ~/ros2_ws/
source install/setup.bash
ros2 launch quadruped_description start_rviz.launch.py

dans un autre terminal​

cd ~/ros2_ws/
source install/setup.bash
ros2 run joint_state_publisher_gui joint_state_publisher_gui
--



### Following work 
Look at those video 
https://www.youtube.com/watch?v=IyvU03j-37I
https://www.youtube.com/watch?v=IjFcr5r0nMs
