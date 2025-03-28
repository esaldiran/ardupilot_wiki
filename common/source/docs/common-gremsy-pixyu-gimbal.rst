.. _common-gremsy-pixyu-gimbal:

==========================================
Gremsy T3, T7, Pixy and Mio 3-Axis Gimbals
==========================================

Gremsy `T3 <https://gremsy.com/products/gremsy-t3v3>`__, `T7 <https://gremsy.com/products/gremsy-t7>`__, `Pixy WP <https://gremsy.com/products/pixy-wp>`__, `Pixy U <https://gremsy.com/products/pixy-u>`__, `Pixy F <https://gremsy.com/products/pixy-f>`__ and `Mio <https://gremsy.com/products/mio>`__ 3-axis gimbals can communicate with the flight controller using the MAVLink protocol and are compatible with a range of cameras for real-time video or mapping purposes.

.. image:: ../../../images/gremsy-pixyu-gimbal.png
    :target: https://gremsy.com/products/pixy-u

Where to Buy
============

The Pixy and Mio gimbals can be purchased from the `Gremsy store <https://gremsy.com/online-store>`__

Connecting to the Autopilot (4.2 or earlier)
============================================

.. image:: ../../../images/gremsy-pixyu-autopilot.png
    :target: ../_images/gremsy-pixyu-autopilot.png
    :width: 450px

We recommend connecting the Gimbals's COM2 port to one of the autopilot's Serial/Telemetry ports like Telem2 as shown above.

Connect with a ground station and set the following parameters:

- :ref:`MNT_TYPE <MNT_TYPE>` to "4" for "SToRM32 MavLink" and reboot the autopilot
- :ref:`SERIAL2_BAUD <SERIAL2_BAUD>` to "115" for 115200 bps.  "SERIAL2" can be replaced with another serial port (i.e. SERIAL1) depending upon the physical connection
- :ref:`SERIAL2_PROTOCOL <SERIAL2_PROTOCOL>` to 2 for "MAVLink2"
- :ref:`SR2_EXTRA1 <SR2_EXTRA1>` to 10
- :ref:`SR2_POSITION <SR2_POSITION>` to 10

The gimbal's maximum angles can be set using these parameters:

- :ref:`MNT_ANGMIN_ROL <MNT_ANGMIN_ROL>` to -3000 to allow leaning left up to 30deg
- :ref:`MNT_ANGMAX_ROL <MNT_ANGMAX_ROL>` to 3000 to allow leaning right up to 30deg
- :ref:`MNT_ANGMIN_TIL <MNT_ANGMIN_TIL>` to -9000 to allow pointing 90deg down
- :ref:`MNT_ANGMAX_TIL <MNT_ANGMAX_TIL>` to 3000 to allow pointing 30deg up
- :ref:`MNT_ANGMIN_PAN <MNT_ANGMIN_PAN>` to -18000 to allow turning around to the left
- :ref:`MNT_ANGMAX_PAN <MNT_ANGMAX_PAN>` to 18000 to allow turning around to the right

To control the gimbal's lean angles from a transmitter set:

- :ref:`MNT_RC_IN_TILT <MNT_RC_IN_TILT>` to 6 to control the gimbal's tilt (aka pitch angle) with the transmitter's Ch6 tuning knob
- :ref:`MNT_RC_IN_ROLL <MNT_RC_IN_ROLL>` to some input channel number to control the gimbal's roll angle
- :ref:`MNT_RC_IN_PAN <MNT_RC_IN_PAN>` to some input channel number to control the gimbals' heading

Gremsy's instructions can be found below:

- `How to setup Gremsy gimbal with Pixhawk Cube <https://support.gremsy.com/support/solutions/articles/36000189926-how-to-setup-gremsy-gimbal-with-pixhawk-cube>`__
- `Control Gremsy Gimbal with Herelink & Cube <https://support.gremsy.com/support/solutions/articles/36000222529-control-gremsy-gimbal-with-herelink-cube-pilot>`__

Configuring the Gimbal
----------------------

The gimbal should work without any additional configuration but to improve performance you may need to adjust the gimbal's gains to match the camera's weight

- Download, install and run the `gTune setup application <https://github.com/Gremsy/gTuneDesktop/releases>`__
- Connect the gimbal to your Desktop PC using a USB cable
- Push the "CONNECTION" button on the left side of the window, then select the COM port and press "Connect"
- Select the "CONTROLS" tab and ensure "SYNC" is selected so the gimbal communicates with the autopilot using MAVLink
- Select the "STIFFNESS" tab and adjust the Tilt, Roll and Pan gains so that the gimbal holds the camera in position without shaking

Testing Controlling the Gimbal from RC
--------------------------------------

- Disconnect the USB cable connecting your PC to the gimbal
- Powerup the vehicle and gimbal
- Move the transmitter's channel 6 tuning knob to its minimum position, the camera should point straight down
- Move the ch6 knob to maximum and the gimbal should point upwards

.. note::

   The RC's channel 6 input can be checked from Mission Planner's Radio calibration page

Testing ROI
-----------

The ROI feature points the vehicle and/or camera to point at a target.  This can be tested by doing the following:

- Ensure the vehicle has GPS lock
- If using the Mission Planner, go to the Flight Data screen and right-mouse-button-click on a point about 50m ahead of the vehicle (the orange and red lines show the vehicle's current heading), select **Point Camera Here** and input an altitude of -50 (meters).  The camera should point forward and then tilt down at about 45 degrees

.. image:: ../../../images/Tarot_BenchTestROI.jpg
    :target: ../_images/Tarot_BenchTestROI.jpg

Pilot control of the gimbal can be restored by setting up an :ref:`auxiliary function switch <common-auxiliary-functions>` to "Retract Mount" (i.e. RCx_OPTION = 27) and then move the switch to the lower position

Connecting to the Autopilot (4.3 or higher)
===========================================

If using ArduPilot 4.3 (or higher) please follow these setup instructions

.. image:: ../../../images/gremsy-pixyu-autopilot.png
    :target: ../_images/gremsy-pixyu-autopilot.png
    :width: 450px

Connecting the Gimbals's COM2 port to one of the autopilot's Serial/Telemetry ports like Telem2 as shown above.

Connect with a ground station and set the following parameters:

- :ref:`MNT_TYPE <MNT_TYPE>` to "6" for "Gremsy" and reboot the autopilot
- :ref:`SERIAL2_BAUD <SERIAL2_BAUD>` to "115" for 115200 bps.  "SERIAL2" can be replaced with another serial port (i.e. SERIAL1) depending upon the physical connection
- :ref:`SERIAL2_PROTOCOL <SERIAL2_PROTOCOL>` to 2 for "MAVLink2"
- :ref:`SERIAL2_OPTIONS <SERIAL2_OPTIONS>` to 1024 for "Don't forward mavlink to/from"
- Optionally set :ref:`RC9_OPTION <RC9_OPTION>` to 163 for "Mount Lock" to allow the pilot to switch between "lock" and "follow" modes during "RC Targetting".  Note "RC9" can be replaced with any RC input channel

When the autopilot has successfully connected to the gimbal, "Mount: GREMSY PixyU fw:7.7.1.0" (or similar) will be sent to the ground station.  Looking for this message may be useful in determining if the autopilot and gimbal are communicating successfully.

Configuring the Gimbal
----------------------

- Download and install `gTune Desktop <https://github.com/Gremsy/gTuneDesktop/releases>`__
- Connect the gimbal to your Desktop PC using a USB cable and power on the gimbal
- Use gTune Desktop to check the gimbal firmware version

  - Open gTune Desktop application, "Found your device" should be displayed
  - Select "CONNECT"
  - Select "INFO" and confirm the gimbal is running Firmware "7.7.1" or higher

  .. image:: ../../../images/gremsy-firmware-version-check.png
      :target: ../_images/gremsy-firmware-version-check.png
      :width: 450px

  - If the gimbal firmware is older than 7.7.1 download the latest .hex for `T3 <https://github.com/Gremsy/T3V3-Firmware/releases>`__, `T7 <https://github.com/Gremsy/T7-Firmware/releases>`__, `Pixy W <https://github.com/Gremsy/PixyW-Firmware/releases>`__, `Pixy U <https://github.com/Gremsy/PixyU-Firmware/releases>`__, `Pixy F <https://github.com/Gremsy/PixyF-Firmware/releases>`__ or `Mio <https://github.com/Gremsy/Mio-Firmware/releases>`__
  - Select "UPGRADE", "BROWSE" and select the file downloaded above
  - Press the other "UPGRADE" button and the upgrade should complete within 30 seconds

  .. image:: ../../../images/gremsy-settings-upgrade.png
      :target: ../_images/gremsy-settings-upgrade.png
      :width: 450px

- Use gTune Desktop to configure the gimbal

  - Select "SETTINGS", "CONTROLS" and ensure "SYNC" is selected so the gimbal communicates with the autopilot using MAVLink

  .. image:: ../../../images/gremsy-settings-sync.png
      :target: ../_images/gremsy-settings-sync.png
      :width: 450px

  - Select "Settings", "REDUCE DIRFT by DRONE"

  .. image:: ../../../images/gremsy-settings-reduce-drift-by-drone.png
      :target: ../_images/gremsy-settings-reduce-drift-by-drone.png
      :width: 450px

- Select the "STIFFNESS" tab and adjust the Tilt, Roll and Pan gains so that the gimbal holds the camera in position without shaking
