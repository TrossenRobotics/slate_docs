===============
Troubleshooting
===============

SLATE Base Error Codes
======================

The following table lists common errors that can be indicated on the base's screen, their cause, and their solution.

.. table::
  :align: center

  ============================== ============ =============================================== ===========================================================
    Error Name                     Code        Cause                                           Solution
  ============================== ============ =============================================== ===========================================================
    Emergency Stop                 E-Stop       Emergency stop button is pressed                Release E-Stop button
    Communication Error            Err18        CAN bus communication is offline                Contact support
    Collision Error                Collision    Collision sensor triggered                      Remove SLATE base from its collision
    Battery Undervoltage           U-Vol        Battery voltage too low                         Charge the SLATE base
    Battery Overvoltage            O-Vol        Battery voltage too high                        If using the original battery, overvoltage can be ignored
    Driver Error                   Err25        Malfunctioning driver                           Contact support
    Drive Overvoltage              Err26        Drive voltage is too high                       If using the original battery, this should not occur
    Drive Undervoltage             Err27        Drive voltage is too low                        If using the original battery, this should not occur
    Drive Overtemperature          Err28        High drive temperature                          Contact support
    Drive Overcurrent              Err29        Drive motor current is too high                 Contact support
    Drive servo out of tolerance   Err30        Drive motor is out of tolerance                 Contact support
    Drive Overload                 Err31        Drive current has exceeded 200% of rated load   Check if the wheels are blocked. Contact support
    Encoder Error                  Err32        Drive encoder signal is malformed               Contact support
    Hall Error                     Err33        The Hall sensor signal is malformed             Contact support
  ============================== ============ =============================================== ===========================================================

SLATE driver can't connect to base
==================================

The USB-Serial converter device shares the same vendor and product ID with some braille readers.
Because of this, the ``brltty`` program may claim the device, preventing its use by other drivers.
Solving this issue is as simple as removing the package using apt.

.. code-block:: bash

  $ sudo apt-get remove brltty
