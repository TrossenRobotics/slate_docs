=====================
ROS 1 Getting Started
=====================

Installing ROS 1
================

.. note::

  The ROS 1 Interbotix SLATE packages are only compatible with Noetic on Ubuntu 20.04.

Follow the `Ubuntu install of ROS Noetic guide on the ROS Wiki`_.

.. _`Ubuntu install of ROS Noetic guide on the ROS Wiki`: https://wiki.ros.org/noetic/Installation/Ubuntu

Configuring Port Permissions
============================

The SLATE uses a USB-Serial converter to communicate with the host computer.

Remove ``brltty`` to prevent it from claiming the device:

.. code-block:: bash

  $ sudo apt-get remove brltty

Add your user to the dialout group:

.. code-block:: bash

  $ sudo usermod -a -G dialout $USER

Reboot your computer to apply the changes:

.. code-block:: bash

  $ sudo reboot

Installing the Interbotix ROS SLATE Packages
============================================

Clone the repository and remove the CATKIN_IGNORE file:

.. code-block:: bash

  $ mkdir -p ~/interbotix_ws/src
  $ cd ~/interbotix_ws/src
  $ git clone -b noetic https://github.com/Interbotix/interbotix_ros_core.git
  $ rm ~/interbotix_ws/src/interbotix_ros_core/interbotix_ros_slate/CATKIN_IGNORE

Install dependencies:

.. code-block:: bash

  $ sudo rosdep init
  $ rosdep update
  $ cd ~/interbotix_ws
  $ rosdep install --from-paths src --ignore-src -r -y

Build the workspace:

.. code-block:: bash

  $ source /opt/ros/noetic/setup.bash
  $ cd ~/interbotix_ws
  $ catkin_make

Running the Driver
==================

Turn on the SLATE and connect it to your computer via USB.
Configure your terminal environment and run the ROS master node:

.. code-block:: bash

  $ source /opt/ros/noetic/setup.bash
  $ source ~/interbotix_ws/devel/setup.bash
  $ roscore

Open another terminal and run the driver:

.. code-block:: bash

  $ source /opt/ros/noetic/setup.bash
  $ source ~/interbotix_ws/devel/setup.bash
  $ rosrun interbotix_slate_driver slate_base_node

If successful, you should see output similar to the following:

.. code-block:: bash

  INFO console [uart.cpp:77 uart_open_no_block]; Open Serial Port!
  INFO console [uart.cpp:79 uart_open_no_block]; fd->open=; 10
  INFO console [serial_driver.cpp:31 init]; open the uart port success; /dev/ttyUSB0
  [ INFO] [1738191485.305142044]: Initialized base at port '/dev/ttyUSB0'.
  [ INFO] [1738191485.310998047]: Base version: 1.0.0

For more detailed usage of the driver, please refer to :doc:`../../operation/ros_interface/ros1`.
See :doc:`../../troubleshooting` for common issues and solutions.