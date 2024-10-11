# MRes-project-code

Introduction
This project includes the necessary code and simulation environment for bimanual haptic feedback control, RL-based autonomous control, and shared control navigation. To demonstrate the visual rendering demo, you can refer to the previously generated visual rendering video. The "Rendered Images Raw Data.zip" contains robot images with different poses and depths. Following the tutorial, you can replicate the cell sorting demo.

Usage
1. Preparation
Prepare two computers with ROS1 (ROS2 is not supported) for bimanual haptic feedback control. Only one of the computers (main computer) needs Isaac Sim installed to run the RL navigation code.

2. Bimanual Haptic Feedback Control
Download the Bimanual_haptic_feedback_control_code package.
Deploy the Left_hand_geomagic_touch_control and Right_hand_geomagic_touch_control workspaces on the two computers configured with Geomagic Touch devices.
Compile the code and complete the basic setup.
3. RL Navigation Setup
Download the RL_navigation_code and 3DModel packages.
Extract the files and place them in paths without Chinese characters.
Place the RL code in the same directory where Isaac Sim's built-in example standalone code is located. This ensures it has access to the necessary compilation environment for running the code.
Update the file paths in the code where necessary:
DQN_env: Drives the robot for shared control.
deploy_best_model: Drives the robot for full autonomous control.
best_model_750.pth: RL-trained network parameters.
smoothed_path.csv: Stores the optimal path calculated by the A* algorithm.
4. Simulation Environment
Download all files starting with Sim_env and extract them.
Start ROS (roscore) on the laptop.
Open the USD files in Omniverse via ROS1 bridge, and update all referenced USD file paths to avoid errors.
5. Running the Demo
Run the Geomagic Touch code.
Launch the Isaac Sim simulation environment.
Finally, run the RL code.
