.. _installation:

Installation
============

**Apio** is written in `Python <https://www.python.org/downloads/>`_ and
works on Linux (+ARM), Mac OS X, Windows.

.. contents::

System requirements
-------------------

:Operating System: Linux (+ARM), Mac OS X or Windows
:Python Interpreter: Python 2.7, Python 3.5+

  .. attention::
      **Windows Users**: Please `Download the latest Python
      <https://www.python.org/downloads/>`_ and install it.
      **DON'T FORGET** to select ``Add python.exe to Path`` feature on the
      "Customize" stage, otherwise Python Package Manager ``pip`` command
      will not be available.

      .. image:: _static/python-installer-add-path.png

:Terminal Application:

    All commands below should be executed in
    `Command-line <http://en.wikipedia.org/wiki/Command-line_interface>`_
    application (Terminal). For Mac OS X and Linux OS - *Terminal* application,
    for Windows OS – ``cmd.exe`` application.

Install Apio
------------

The latest stable version of Apio may be installed or upgraded via
Python Package Manager (`pip <https://pip.pypa.io>`_) as follows:

.. code::

    $ pip install -U apio

If ``pip`` command is not available run ``easy_install pip``.

Note that you may run into permissions issues running these commands. You have
a few options here:

* Run with ``sudo`` to install Apio and dependencies globally
* Specify the `pip install --user <https://pip.pypa.io/en/stable/user_guide.html#user-installs>`_
  option to install local to your user
* Run the command in a `virtualenv <https://virtualenv.pypa.io>`_ local to a
  specific project working set.

.. note::

    Debian users can also install the application and its packages by executing:

    .. code::

        $ curl -sSL http://fpgalibre.sf.net/debian/go | sudo sh
        $ sudo apt-get install apio
        $ sudo apt-get install apio-scons apio-icestorm apio-iverilog apio-examples apio-system

.. _install_drivers:

Install FPGA FTDI drivers
-------------------------

Using apio
~~~~~~~~~~

.. code::

    $ apio drivers --ftdi-enable

To revert the FTDI drivers configuration

.. code::

    $ apio drivers --ftdi-disable

Manually
~~~~~~~~

**Linux**

Download `80-icestick.rules <https://github.com/FPGAwars/apio/blob/develop/apio/resources/80-icestick.rules>`_ and execute

.. code::

    $ sudo cp 80-icestick.rules /etc/udev/rules.d/
    $ sudo service udev restart


**Mac OS X**

Install `homebrew <http://brew.sh/>`_ and libftdi

.. code::

    $ brew update
    $ brew install libftdi
    $ brew install libffi

Configure the drivers

If **com.FTDI.driver.FTDIUSBSerialDriver** is loaded (``kextstat | grep FTDIUSBSerialDriver``), unload it:

.. code::

  $ sudo kextunload -b com.FTDI.driver.FTDIUSBSerialDriver

If **com.apple.driver.AppleUSBFTDI** is loaded (``kextstat | grep AppleUSBFTDI``), unload it:

.. code::

  $ sudo kextunload -b com.apple.driver.AppleUSBFTDI

Then upload the bitstream. And finally revert the drivers configuration:

.. code::

  $ sudo kextload -b com.FTDI.driver.FTDIUSBSerialDriver -q

or

.. code::

  $ sudo kextload -b com.apple.driver.AppleUSBFTDI -q

`More information <https://github.com/FPGAwars/apio/wiki/FTDI-Drivers-flowchart-Mac-OS>`_.

**Windows**

Go to this `tutorial <https://github.com/FPGAwars/libftdi-cross-builder/wiki#driver-installation>`_.
