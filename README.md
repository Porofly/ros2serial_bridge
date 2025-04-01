# ROS2 Serial Communicaion Bridge

![image](https://github.com/user-attachments/assets/089d86cf-dab3-48db-b4c0-dfab6dbb34eb)

## Structure

- **jfi_comm** : ROS2 Serial Communication Library
- serial_comm_node : **Example** ROS2 Node of using a J-Fi library
```
J-Fi/
├── config/
│ ├── jfi.xml                     # Mavlink message definition.
├── include/
│ ├── jfi_comm.hpp                # Header file for the JFi Library.
│ └── serial_comm_node.hpp        # Header file for the Example ROS2 node using Library
├── launch/
│ ├── test_simulation.launch.py   # Example Launch file for simulation tests using virtual serial ports.
│ └── serial_comm_node.launch.py  # Example Launch file for running the node in a real environment.
├── mavlink/
└── src/
  ├── jfi_comm.cpp                # Implementation of the JFi Library.
  ├── serial_comm_node.cpp        # Implementation of the Example ROS2 node using Library
  └── main.cpp
```

## Features

- **MAVLink Message Handling**: Encodes ROS2 messages into MAVLink messages and decodes received MAVLink messages back into ROS2 messages.

## Prerequisites

- **ROS2**: Tested on ROS2 Humble (or specify your version).
- **socat**: (For simulation) Used to create virtual serial ports.

## Installation

### Clone repository
```
git clone https://github.com/SUV-Lab/J-Fi.git
cd J-Fi
git submodule update --init --recursive
```

### Build
```
colcon build
source install/setup.bash
```

## Run

### Parameters

- port_name: Serial port device path (default: /dev/ttyUSB0).
- baud_rate: Baud rate for serial communication (default: 115200).
- system_id: MAVLink system ID (default: 1).
- component_id: MAVLink component ID (default: 1).

### For simulation test,
Use virtual serial ports via socat:
```
ros2 launch  jfi_comm test_simulation.launch.py
```

### For real environment,
Use real serial ports:
```
ros2 launch jfi_comm serial_comm_node.launch.py
```
(Optional) Example with custom configuration:
```
ros2 launch jfi_comm serial_comm_node.launch.py port_name:=/dev/ttyUSB1 baud_rate:=115200 system_id:=2 component_id:=2
```

## TODO

- develop send buffer concept
- fix the bugs (#2)
