=====================
ROS 2 Getting Started
=====================

Installing ROS 2
================

.. note::

  The ROS 2 Interbotix SLATE packages are compatible with the following distributions: Humble on Ubuntu 22.04 and Jazzy on Ubuntu 24.04.

Follow the ROS 2 installation guide for your specific version on the ROS documentation site:

- `Humble`_ (Ubuntu 22.04)
- `Jazzy`_ (Ubuntu 24.04)

.. _Humble: https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html
.. _Jazzy: https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debians.html

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

Clone the repository and remove the COLCON_IGNORE file:

.. code-block:: bash

  $ mkdir -p ~/interbotix_ws/src
  $ cd ~/interbotix_ws/src
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

Turn on the SLATE and connect it to your computer via USB.
Configure your terminal environment and run the driver:

.. code-block:: bash

  $ source /opt/ros/$ROS_DISTRO/setup.bash
  $ source ~/interbotix_ws/install/setup.bash
  $ ros2 run interbotix_slate_driver slate_base_node

If successful, you should see output similar to the following:

.. code-block:: bash

  [INFO] [1738186633.956689812] [slate_base]: Using Trossen SLATE Driver Version: 'v1.0.0'.
  Initialized base at port: '/dev/ttyUSB0'.
  Base version: 'v1.0.0'.

For more detailed usage of the driver, please refer to :doc:`../../operation/ros_interface/ros2`.
See :doc:`../../troubleshooting` for common issues and solutions.