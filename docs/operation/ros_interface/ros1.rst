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

Examples
--------

The **slate_base_node** is designed to be controlled by other user-written nodes that publish to the ``cmd_vel`` topic or call the services provided by the **slate_base_node**.
Below are some examples of how to interact with the **slate_base_node** using ROS 1 command line tools.

Setting Parameters
^^^^^^^^^^^^^^^^^^

You can set parameters for the **slate_base_node** when running it using the ``_param`` flag.

.. code-block:: bash

  # Enable publishing of the odom->base_link TF
  $ rosrun interbotix_slate_driver slate_base_node _publish_tf:=true

  # Set the odometry frame name to "my_odom"
  $ rosrun interbotix_slate_driver slate_base_node _odom_frame_name:="my_odom"

  # Set the base frame name to "my_base"
  $ rosrun interbotix_slate_driver slate_base_node _base_frame_name:="my_base"

Calling Services
^^^^^^^^^^^^^^^^

You can call services provided by the **slate_base_node** using the ``rosservice call`` command.

.. code-block:: bash

  # Disable charging
  $ rosservice call /enable_charging std_srvs/SetBool "{data: false}"

  # Set the lights to color BLUE
  $ rosservice call /set_light_state interbotix_slate_msgs/SetLightState "{light_state: 4}"

  # Set the text to "hello world" on the SLATE screen
  $ rosservice call /set_text interbotix_slate_msgs/SetString "{data: 'hello world'}"

  # Disable torque on the drive wheels
  $ rosservice call /set_motor_torque_status std_srvs/SetBool "{data: false}"

Publishing Velocity Commands
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can publish velocity commands to the **slate_base_node** using the ``rostopic pub`` command.
``-r 10`` sets the publishing rate to 10 Hz.

.. warning::

  These commands will move the base, so make sure the SLATE is in a safe location before running them.
  Press ``Ctrl+C`` to stop the command at any time.

.. code-block:: bash

  # Publish a velocity command to move forward
  $ rostopic pub -r 10 /cmd_vel geometry_msgs/Twist "{linear: {x: 0.1, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.0}}"

  # Publish a velocity command to rotate counter-clockwise
  $ rostopic pub -r 10 /cmd_vel geometry_msgs/Twist "{linear: {x: 0.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.1}}"