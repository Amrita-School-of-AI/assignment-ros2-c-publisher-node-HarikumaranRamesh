[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/pIZu3wUF)
# Assignment: ROS2 C++ Publisher Node

**Course:** ROS2 Fundamentals  
**Build System:** ament_cmake

## Objective

The goal of this assignment is to verify your understanding of:

1. How to create a ROS2 Publisher node.
2. How to publish messages using `std_msgs/msg/String`.
3. How to configure topics and publish rates.

## Problem Statement

You must complete the provided skeleton code to create a ROS2 node that publishes a counter message to a topic.

### Requirements

1. **Source Code (`src/publisher_node.cpp`)**:
   - Implement a class `PublisherNode` that inherits from `rclcpp::Node`.
   - Initialize the node with the name `"publisher_node"`.
   - Create a publisher to the topic `"/counter"` with type `std_msgs::msg::String`.
   - Create a timer that fires every **500ms**.
   - Inside the timer callback:
     - Increment a counter (starting from 0).
     - Publish a message in the format: `"Count: X"` where X is the counter value.
     - Log the published message using `RCLCPP_INFO`.

2. **Build Configuration (`CMakeLists.txt`)**:
   - Add an executable target named `publisher_node` compiled from `src/publisher_node.cpp`.
   - Link dependencies for `rclcpp` and `std_msgs`.
   - Ensure the executable is installed to `lib/${PROJECT_NAME}`.

3. **Package Metadata (`package.xml`)**:
   - Add the missing dependency tags for `rclcpp` and `std_msgs`.

## How to Test Locally

Before pushing to GitHub, ensure your code runs locally:

```bash
# 1. Build the package
colcon build --packages-select ros2_publisher

# 2. Source the setup file
source install/setup.bash

# 3. Run the node
ros2 run ros2_publisher publisher_node
```

#### Expected Output:

```shell
[INFO] [1700000000.123456789] [publisher_node]: Publishing: 'Count: 0'
[INFO] [1700000000.623456789] [publisher_node]: Publishing: 'Count: 1'
[INFO] [1700000001.123456789] [publisher_node]: Publishing: 'Count: 2'
...
```

#### Verify with `ros2 topic echo`:

```bash
# In another terminal
ros2 topic echo /counter
```

Expected:

```
data: 'Count: 0'
---
data: 'Count: 1'
---
...
```
