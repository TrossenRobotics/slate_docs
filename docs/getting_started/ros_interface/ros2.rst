=====================
ROS 2 Getting Started
=====================

Install ROS 2
=============

.. note::

  The ROS 2 Interbotix SLATE packages are only compatible with Humble on Ubuntu 22.04.

Follow the `Ubuntu (Debian packages)`_ ROS 2 installation guide on the ROS documentation site.
Once installed, make sure to follow the `How do I use the rosdep tool?`_ guide to to set up and install the development and dependency toolchains.

.. _`Ubuntu (Debian packages)`: https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html
.. _`How do I use the rosdep tool?`: https://docs.ros.org/en/humble/Tutorials/Intermediate/Rosdep.html#how-do-i-use-the-rosdep-tool

Install the Interbotix ROS Slate Packages
=========================================

#.  Clone the humble branch of the interbotix_ros_core repository into your colcon workspace.

  .. code-block:: bash

    $ mkdir -p ~/interbotix_ws/src
    $ cd ~/interbotix_ws/src
    $ git clone -b humble https://github.com/Interbotix/interbotix_ros_core.git

#.  Remove the COLCON_IGNORE file preventing the interbotix_ros_slate metapackage from being built.

  .. code-block:: bash

    $ rm ~/interbotix_ws/src/interbotix_ros_core/interbotix_ros_slate/COLCON_IGNORE

#.  Run rosdep in the root of the workspace to install all required dependencies.

  .. code-block:: bash

    $ cd ~/interbotix_ws
    $ rosdep install --from-paths src --ignore-src -r -y

#.  Build the workspace, making sure that you have sourced your ROS system installation first.

  .. code-block:: bash

    $ source /opt/ros/$ROS_DISTRO/setup.bash
    $ cd ~/interbotix_ws
    $ colcon build

Post-Install
============

The USB-Serial converter device shares the same vendor and product ID with some brail readers.
Because of this, the ``brltty`` program may claim the device, preventing its use by other drivers.
Solving this issue is as simple as removing the package using apt.

.. code-block:: bash

  $ sudo apt-get remove brltty

Verification
============

Configure your terminal environment, run the driver using ros2run, and check that the driver successfully connects to the base.

.. code-block:: bash

  $ source /opt/ros/$ROS_DISTRO/setup.bash
  $ source ~/interbotix_ws/install/setup.bash
  $ ros2 run interbotix_slate_driver slate_base_node
