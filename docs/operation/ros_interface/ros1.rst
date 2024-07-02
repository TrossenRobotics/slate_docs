=========================
ROS 1 Interface Operation
=========================

SLATE Base Node
===============

The SLATE interfaces with ROS using the **slate_base_node** from the **interbotix_slate_driver** package.

Publishers
----------

The **slate_base_node** publishes to the following topics:

* ``odom``

  * **Type**: ``nav_msgs/Odometry``
  * **Description**: The odometry of the base.

* ``battery_state``

  * **Type**: ``sensor_msgs/BatteryState``
  * **Description**: Battery state information including present voltage and state of charge.

Subscribers
-----------

The **slate_base_node** subscribes to the following topics:

* ``cmd_vel``

  * **Type**: ``geometry_msgs/Twist``
  * **Description**: Velocity commands

Services
--------

The **slate_base_node** provides the following service servers:

* ``set_text``

  * **Type**: ``std_srvs/SetString``
  * **Description**: Sets the text on the SLATE screen.

* ``set_motor_torque_status``

  * **Type**: ``std_srvs/SetBool``
  * **Description**: If true, enables torque on the drive wheels.
    If false, disables torque on the drive wheels.

  .. note::

    Torque is enabled on the drive wheels by default.

* ``enable_charging``

  * **Type**: ``std_srvs/SetBool``
  * **Description**: If true, enables charging via the contact charger.

Parameters
----------

The **slate_base_node** has the following parameters:

* ``publish_tf``:

  * **Type**: bool
  * **Description**: Setting this to true publishes the odom->base_link TF following REP 105.
  * **Default**: ``false``

* ``odom_frame_name``:

  * **Type**: string
  * **Description**: The name of the odometry frame when publishing the odom->base_link TF.
  * **Default**: ``"odom"``

* ``base_frame_name``:

  * **Type**: string
  * **Description**: The name of the base_link frame when publishing the odom->base_link TF.
  * **Default**: ``"base_link"``

Usage
-----

Using rosrun
^^^^^^^^^^^^

.. code-block:: bash

  $ rosrun interbotix_slate_driver slate_base_node
