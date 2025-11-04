## Exact usage (from the included scripts)
This repository includes two runnable Python examples:
- `MujocoSim.py` — provides the `FR3Sim` class which launches a MuJoCo simulation of the FR3 model. The constructor signature is:
```python
from MujocoSim import FR3Sim
# programmatic options
sim = FR3Sim(interface_type="torque", render=True, dt=0.001, xml_path=None)
# interface_type: currently only "torque" is supported
Run the default simulation (launches the viewer):
```bash
python MujocoSim.py
- `admittance.py` — an example admittance controller that uses `FR3Sim` to read state and send joint torques. Run it directly:
```bash
python admittance.py
Notes: these example scripts are simple runners and currently do not implement a full command-line parser. For custom runs, import `FR3Sim` in your own script and pass the desired options programmatically (see example above).
## Requirements (auto-generated)
The main Python packages used by the code are listed below. Some components (MuJoCo, ROS 2, Pinocchio) require system-level installation; see notes after the pip packages.
Pip-installable (add to `requirements.txt`):
- numpy
- scipy
- matplotlib
- mujoco
- pinocchio
System / environment requirements:
- MuJoCo and its Python bindings (the `mujoco` wheel). Install MuJoCo from https://mujoco.org and follow binding installation instructions for your OS.
- Pinocchio: often installed via conda-forge (`conda install -c conda-forge pin`) or built from source.
- ROS 2 and rclpy: if you plan to use the ROS 2 publishers/subscribers in `MujocoSim.py`, install ROS 2 (Humble/Foxy or your distro) and ensure `rclpy` and message packages (`std_msgs`, `sensor_msgs`) are available.
If you want I can generate a `requirements.txt` with the pip packages above and a short `install-README` with system installation steps for MuJoCo, Pinocchio and ROS 2.
# Admittance_Control_FR3
Short, editable README for the Admittance Control project targeting the FR3 platform.
## Overview
Admittance_Control_FR3 implements an admittance-style force/impedance controller for the FR3 robot platform. This repository contains the controller implementation, configuration files, example launch scripts, and tests to validate behavior in simulation and on hardware.
Replace placeholders below with concrete project details, hardware refs, and usage examples.
## Features
- Admittance controller core (C++ / Python) — modular and real-time friendly
- Configurable mass-damper-spring parameters
- Logging and replay utilities
- Simulation support (Gazebo / other) and hardware interface stubs
- Unit and integration tests
## Requirements
- Linux (Ubuntu recommended)
- C++17 toolchain (g++, clang) or Python 3.8+
- CMake >= 3.10 (if C++)
- Optional: ROS2 (Humble/Foxy/your distro) for middleware/launch
- Optional: Gazebo (for simulation)
## Quick start (example)
1. Clone the repo:
    git clone https://github.com/your-org/Admittance_Control_FR3.git
    cd Admittance_Control_FR3
2. Configure:
    - Edit config/params.yaml (or config/*.json/.xml) to set admittance gains and hardware topics.
    - Provide robot-specific URDF and joint mappings in config/.
3a. Build (CMake/C++):
    mkdir -p build && cd build
    cmake ..
    make -j$(nproc)
3b. Install (Python):
    pip install -r requirements.txt
    python -m pip install -e .
4. Run (examples):
    - Simulation: ./bin/admittance_node --config ../config/params.yaml --sim
    - Hardware: ./bin/admittance_node --config ../config/params.yaml --hw
(Replace commands with actual executable names in this repo.)
## Usage
- Set admittance parameters: mass, damping, stiffness via configuration file or runtime parameter server.
- Start data logging for analysis of force, position, and admittance outputs.
- Use provided scripts in tools/ to replay logs and visualize results.
## Configuration
- config/params.yaml — main controller parameters
- config/robot_mapping.yaml — joint and frame mappings for FR3
- env/*.sh — environment setup scripts (sourcing workspace, ROS)
## Testing
- Unit tests: run with your test runner (e.g., ctest or pytest)
- Integration: launch simulation and run example scenarios under tests/integration/
## Repository layout (suggested)
- src/          — controller implementation
- include/      — headers (C++)
- scripts/      — helper and launch scripts
- config/       — parameter files
- tools/        — visualization, logging, replay tools
- tests/        — unit and integration tests
- docs/         — design notes, math derivations
- examples/     — example configs and launch files
## Troubleshooting
- If controller is unstable: verify sign conventions for forces and joint directions, reduce admittance gains, enable logging and replay a short scenario.
- For real-time issues: ensure real-time kernel / proper thread priorities and small control loop jitter.
## Contributing
- Fork the repository, create a feature branch, and open a pull request.
- Add tests for new features and update documentation.
- Follow the coding style used in src/ and include brief commit messages.
## License
Specify a license (e.g., MIT, Apache-2.0) in LICENSE file. Replace this line with the chosen license summary.
## Contact
Project owner: replace-with-your-name or maintainers list in MAINTAINERS.md
Notes: Edit this README to add project-specific instructions (exact build commands, ROS launch examples, hardware safety checks) before sharing or deploying on real hardware.
