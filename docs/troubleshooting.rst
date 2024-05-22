===============
Troubleshooting
===============

SLATE driver can't connect to base
==================================

The USB-Serial converter device shares the same vendor and product ID with a brail readers.
Because of this, the ``brltty`` program will claim the device, preventing its use by other drivers.
Solving this issue is as simple as removing the package using apt.

.. code-block:: bash

  $ sudo apt-get remove brltty
