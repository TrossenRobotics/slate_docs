=====================
ROS 2 Getting Started
=====================

Installing ROS 2
================

.. note::

  The ROS 2 Interbotix SLATE packages are compatible with the following distributions: Galactic, Humble, and Iron on Ubuntu 22.04, and Jazzy and Rolling on Ubuntu 24.04.

Follow the ROS 2 installation guide for your specific version on the ROS documentation site:

- `Galactic`_ (Ubuntu 22.04)
- `Humble`_ (Ubuntu 22.04)
- `Iron`_ (Ubuntu 22.04)
- `Jazzy`_ (Ubuntu 24.04)
- `Rolling`_ (Ubuntu 24.04)

.. _Galactic: https://docs.ros.org/en/galactic/Installation/Ubuntu-Install-Debians.html
.. _Humble: https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html
.. _Iron: https://docs.ros.org/en/iron/Installation/Ubuntu-Install-Debians.html
.. _Jazzy: https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debians.html
.. _Rolling: https://docs.ros.org/en/rolling/Installation/Ubuntu-Install-Debians.html

Configuring Port Permissions
============================

The SLATE uses a USB-Serial converter to communicate with the host computer.

Add your user to the dialout group:

.. code-block:: bash

  $ sudo usermod -a -G dialout $USER

Reboot your computer to apply the changes:

.. code-block:: bash

  $ sudo reboot

Installing the Interbotix ROS SLATE Packages
============================================

Clone the repository and remove the COLCON_IGNORE file:

.. code-block:: bash

  $ mkdir -p ~/interbotix_ws/src
  $ cd ~/interbotix_ws/src
  $ export ROS_DISTRO=humble  # Replace 'humble' with your desired ROS distribution
  $ git clone --recursive -b $ROS_DISTRO https://github.com/Interbotix/interbotix_ros_core.git
  $ rm ~/interbotix_ws/src/interbotix_ros_core/interbotix_ros_slate/COLCON_IGNORE

Install dependencies:

.. code-block:: bash

  $ sudo rosdep init
  $ rosdep update
  $ cd ~/interbotix_ws
  $ rosdep install --from-paths src --ignore-src -r -y

Build the workspace:

.. code-block:: bash

  $ source /opt/ros/$ROS_DISTRO/setup.bash
  $ cd ~/interbotix_ws
  $ colcon build

Running the Driver
==================

Turn on the SLATE and connect it to your computer via USB. Configure your terminal environment and run the driver:

.. code-block:: bash

  $ source /opt/ros/$ROS_DISTRO/setup.bash
  $ source ~/interbotix_ws/install/setup.bash
  $ ros2 run interbotix_slate_driver slate_base_node

If successful, you should see output similar to the following:

.. code-block:: bash

  [INFO] [1738186633.956689812] [slate_base]: Using Trossen SLATE Driver Version: 'v1.0.0'.
  Initialized base at port: '/dev/ttyUSB0'.
  Base version: 'v1.0.0'.

For more detailed usage of the driver, please refer to :doc:`../../operation/ros_interface/ros2`. See :doc:`../../troubleshooting` for common issues and solutions.