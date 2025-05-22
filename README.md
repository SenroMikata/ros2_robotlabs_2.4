This repository is a backup for the 2.4 tutorial of ROS2 Jazzy by RobotLabs. Follow the steps below to set it up on a new machine.

---
## Prerequisites
- **Ubuntu 24.04** (required for ROS2 Jazzy Jalisco).
- **ROS2 Jazzy Jalisco installed**:  
  Follow the [official installation guide](https://docs.ros.org/en/jazzy/Installation.html).
- **Github with SSH configured on your local machine**:
  Check RobotLabs tutorial on [how to](https://www.youtube.com/watch?v=asKyDmM_TBY&t=671s).
---

## Installation & Setup

### 1. Clone the Repository
```bash
git clone https://github.com/SenroMikata/ros2_robotlabs_2.4.git
or
git clone git@github.com:SenroMikata/ros2_robotlabs_2.4.git

cd ros2_robotlabs_2.4
```

### 2. Install Dependencies
Update rosdep and install workspace dependencies:
```bash
sudo apt update && sudo rosdep init
rosdep update
rosdep install --from-paths src --ignore-src -y
```
### 3. Build the Workspace
Build all packages using colcon:
```bash
colcon build
```
### 4. Source the Workspace
Load the environment variables into your terminal:
```bash
source install/setup.bash
```
### (Optional) Add this to your .bashrc to auto-source on startup:
```bash
echo "source $(pwd)/install/setup.bash" >> ~/.bashrc
```
### Running the Workspace
After building and sourcing, the nodes and launch files should be usable:
```bash
ros2 launch mec_mobile_description robot_state_publisher.launch.py
ros2 launch mec_mobile_gazebo world.launch.py
ros2 launch mec_mobile_gazebo spawn_robot.launch.py
```
### Workspace Structure
```bash
your-repo-name/
  ├── src/               # ROS2 packages (custom or cloned)
  ├── .gitignore         # Ignores build/install/log
  └── README.md          # This documentation
```
### Troubleshooting
Dependency Issues

    If rosdep install fails, manually install missing packages listed in the error.

    Ensure all package dependencies are declared in package.xml.

Build Errors

    Clean the workspace and rebuild:
    bash

    rm -rf build/ install/ log/
    colcon build

Environment Not Sourced

    If ROS2 commands aren’t recognized, re-source the workspace:
    bash

    source install/setup.bash

Optional: Reconstruct Workspace with vcstool

If this workspace uses packages from multiple repositories (via a .repos file):
bash

# Install vcstool (if not already installed)
```bash
sudo apt install python3-vcstool
```
# Import repositories into src/
```bash
vcs import src < your-repos-file.repos
```
