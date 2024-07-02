=====================
ROS 1 Getting Started
=====================

Install ROS
===========

.. note::

  The ROS 1 Interbotix SLATE packages are only compatible with Noetic on Ubuntu 20.04.

Follow the `Ubuntu install of ROS Noetic guide on the ROS Wiki`_.
Once installed, make sure to follow steps 1.6 and 1.6.1 to set up and install the development and dependency toolchains.

.. _`Ubuntu install of ROS Noetic guide on the ROS Wiki`: https://wiki.ros.org/noetic/Installation/Ubuntu

Install the Interbotix ROS Slate Packages
=========================================

#.  Clone the noetic branch of the interbotix_ros_core repository into your catkin workspace.

  .. code-block:: bash

    $ mkdir -p ~/interbotix_ws/src
    $ cd ~/interbotix_ws/src
    $ git clone -b noetic https://github.com/Interbotix/interbotix_ros_core.git

#.  Remove the CATKIN_IGNORE file preventing the interbotix_ros_slate metapackage from being built.

  .. code-block:: bash

    $ rm ~/interbotix_ws/src/interbotix_ros_core/interbotix_ros_slate/CATKIN_IGNORE

#.  Run rosdep in the root of the workspace to install all required dependencies.

  .. code-block:: bash

    $ cd ~/interbotix_ws
    $ rosdep install --from-paths src --ignore-src -r -y

#.  Build the workspace.

  .. code-block:: bash

    $ cd ~/interbotix_ws
    $ catkin_make

Post-Install
============

The USB-Serial converter device shares the same vendor and product ID with some brail readers.
Because of this, the ``brltty`` program may claim the device, preventing its use by other drivers.
Solving this issue is as simple as removing the package using apt.

.. code-block:: bash

  $ sudo apt-get remove brltty

Verification
============

Run the driver using rosrun and check that the driver successfully connects to the base.

.. code-block:: bash

  $ rosrun interbotix_slate_driver slate_base_node
