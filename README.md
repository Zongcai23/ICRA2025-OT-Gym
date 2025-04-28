# 📝 Interactive OT Gym: A Reinforcement Learning-Based Interactive Optical tweezer (OT)-Driven Microrobotics Simulation Platform

## ✍️ Authors & Affiliations  
**Zongcai Tan**, Imperial College London  
**Dandan Zhang**, Imperial College London  

## 🔗 Project Links  
[Paper](https://your-paper-link.example.com) | [Website](https://sites.google.com/view/otgym) | [Short Video](https://youtu.be/your-short-video) | [Long Video](https://youtu.be/your-long-video)

## 🛠️ Status & Requirements  
![IsaacSim 3.10.0](https://img.shields.io/badge/IsaacSim-4.1.0-lightgrey) ![Python 3.10](https://img.shields.io/badge/Python-3.10-blue) ![Platform Linux-64](https://img.shields.io/badge/Platform-Linux--64-brightgreen) ![pre-commit enabled](https://img.shields.io/badge/pre--commit-enabled-green)


## 📖 Overview  
![Overview Diagram](overview.jpg)  
OT-Gym is a physics-based optical micro-robot simulation framework built on NVIDIA Isaac Sim to train reinforcement-learning algorithms for micro-manipulation tasks. This repo provides code and simulation environments for:  
- **Bimanual haptic-feedback control**  
- **RL-based autonomous control**  
- **Shared-control navigation for cell sorting**  
using optical-tweezer-actuated microrobots.  

## ✨ Features  

### 🤖 Shared OT Micromanipulation Process  
![Shared OT Micromanipulation GIF](gifs/shared_ot_process.gif)  
Users first indirectly grasp target cells using optical robots, then transport the cells to designated locations before releasing them.  

### 📈 Effectiveness Validation Experiment  
![Shared Control Validation GIF](gifs/shared_control_validation.gif)  
Manual control is safe yet inefficient, autonomous control is efficient but collision-prone, and shared control balances efficiency with safety.  

## 📋 Requirements  

### 🖥️ Hardware  
- Two **Geomagic Touch** haptic devices for teleoperation  
- Two computers with **ROS 1** (ROS 2 _not_ supported)  
- One “main” computer with NVIDIA Isaac Sim installed  

### 💾 Software  
- **ROS 1** on both machines  
- **Isaac Sim** (latest) on the main machine  
- Extraction paths must contain only ASCII characters  
- All devices on the same LAN  

## 📚 User Guide  

### 1. Basic Setup  
OT-Gym builds on NVIDIA Isaac Sim. See the [Isaac Sim docs](https://developer.nvidia.com/isaac/sim). 

### 2. Bimanual Haptic-Feedback Teleoperation 
Download the Bimanual_haptic_feedback_control_code.zip package. Deploy the Left_hand_geomagic_touch_control and Right_hand_geomagic_touch_control workspaces on the two computers configured with Geomagic Touch devices. Compile the code and complete the basic setup.
```bash
# Download & unzip
unzip Bimanual_haptic_feedback_control_code.zip

# Configuring the device
./Touch_Setup
sudo chmod 777 /dev/ttyACM2

# Compile the code
# Machine 1 (Left hand)
cd Left_hand_geomagic_touch_control
source ./devel/setup.bash
catkin_make
# Machine 2 (Right hand)
cd Right_hand_geomagic_touch_control
source ./devel/setup.bash
catkin_make

# On each machine
roscore                # if not already running
roslaunch geomagic_control geomagic.launch
```

### 3. RL Navigation Setup  
```bash
# Download & unzip RL navigation
unzip RL_navigation_code.zip

# Ensure ASCII-only paths
# Place RL code alongside Isaac Sim examples
mv RL_navigation_code path/to/IsaacSim/examples/

# Update paths in code if needed:
# - DQN_env.py → Drives the robot for shared control.
# - deploy_best_model.py → Drives the robot for full autonomous control (RL).
# - best_model_750.pth → RL-trained network parameters
# - smoothed_path.csv → Stores the optimal path calculated by the A* algorithm.
```

### 4. Simulation Environment  
```bash
# Download & unzip Sim environment & 3D models
unzip SimEnv_*.zip
unzip 3DModel.zip

# On main computer:
roscore

Download all files starting with Sim_env and extract them. Start ROS (roscore) on the laptop.
Open the USD files in Omniverse via ROS1 bridge, and update all referenced USD file paths to avoid errors.
```  
- Load USD files via the ROS1 bridge in Omniverse  
- Update USD file paths to avoid errors  

### 5. Running the Demo  
```bash
# Start Geomagic Touch on both machines
roslaunch left_touch_control geomagic_touch.launch
roslaunch right_touch_control geomagic_touch.launch

# Launch Isaac Sim on main machine
./launchIsaacSim.sh

# Run RL demo
rosrun rl_navigation deploy_best_model.py
```

## 📂 File Structure  
```plaintext
.
├── docs/
│   ├── badges/                     # badge SVGs
│   └── overview.png                # overview diagram
├── gifs/
│   ├── shared_ot_process.gif
│   └── shared_control_validation.gif
├── Bimanual_haptic_feedback_control_code.zip
├── RL_navigation_code.zip
├── 3DModel.zip
├── Rendered_Images_Raw_Data.zip
└── Sim_env_*.zip
```
