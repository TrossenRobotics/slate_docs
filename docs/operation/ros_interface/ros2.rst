=========================
ROS 2 Interface Operation
=========================

SLATE Base Node
===============

The SLATE interfaces with ROS 2 using the **slate_base_node** from the **interbotix_slate_driver** package.

Publishers
----------

The **slate_base_node** publishes to the following topics:

* ``odom``

  * **Type**: ``nav_msgs/msg/Odometry``
  * **Description**: The odometry of the base.

* ``battery_state``

  * **Type**: ``sensor_msgs/msg/BatteryState``
  * **Description**: Battery state information including present voltage and state of charge.

Subscribers
-----------

The **slate_base_node** subscribes to the following topics:

* ``cmd_vel``

  * **Type**: ``geometry_msgs/msg/Twist``
  * **Description**: Velocity commands

Services
--------

The **slate_base_node** provides the following service servers:

* ``set_text``

  * **Type**: ``std_srvs/srv/SetString``
  * **Description**: Sets the text on the SLATE screen.

* ``set_motor_torque_status``

  * **Type**: ``std_srvs/srv/SetBool``
  * **Description**: If true, enables torque on the drive wheels.
    If false, disables torque on the drive wheels.

  .. note::

    Torque is enabled on the drive wheels by default.

* ``enable_charging``

  * **Type**: ``std_srvs/srv/SetBool``
  * **Description**: If true, enables charging via the contact charger.

Parameters
----------

The **slate_base_node** has the following parameters:

* ``update_frequency``:

  * **Type**: int
  * **Description**: The frequency in Hz of the SLATE update loop.
  This is the rate at which the SLATE updates based on the incoming data.
  * **Default**: ``10``

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
Below are some examples of how to interact with the **slate_base_node** using ROS 2 command line tools.

Setting Parameters
^^^^^^^^^^^^^^^^^^

You can set parameters for the **slate_base_node** when running it using the ``--ros-args`` flag.

.. code-block:: bash

  # Set the update frequency to 20 Hz
  $ ros2 run interbotix_slate_driver slate_base_node --ros-args -p update_frequency:=20

  # Enable publishing of the odom->base_link TF
  $ ros2 run interbotix_slate_driver slate_base_node --ros-args -p publish_tf:=true

  # Set the odometry frame name to "my_odom"
  $ ros2 run interbotix_slate_driver slate_base_node --ros-args -p odom_frame_name:="my_odom"

  # Set the base frame name to "my_base"
  $ ros2 run interbotix_slate_driver slate_base_node --ros-args -p base_frame_name:="my_base"

Calling Services
^^^^^^^^^^^^^^^^

You can call services provided by the **slate_base_node** using the ``ros2 service call`` command.

.. code-block:: bash

  # Disable charging
  $ ros2 service call /enable_charging std_srvs/srv/SetBool "{data: false}"

  # Set the lights to color BLUE
  $ ros2 service call /set_light_state interbotix_slate_msgs/srv/SetLightState "{light_state: 4}"

  # Set the text to "hello world" on the SLATE screen
  $ ros2 service call /set_text interbotix_slate_msgs/srv/SetString "{data: 'hello world'}"

  # Disable torque on the drive wheels
  $ ros2 service call /set_motor_torque_status std_srvs/srv/SetBool "{data: false}"

Publishing Velocity Commands
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can publish velocity commands to the **slate_base_node** using the ``ros2 topic pub`` command.
``-r 10`` sets the publishing rate to 10 Hz.
``-t 30`` publishes the message 30 times.
This has the effect of commanding the velocity to the base for three seconds.

.. warning::

  These commands will move the base, so make sure the SLATE is in a safe location before running them.
  Press ``Ctrl+C`` to stop the command at any time.

.. code-block:: bash

  # Publish a velocity command to move forward
  $ ros2 topic pub -r 10 -t 30 /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.1, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.0}}"

  # Publish a velocity command to rotate counter-clockwise
  $ ros2 topic pub -r 10 -t 30 /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.1}}"