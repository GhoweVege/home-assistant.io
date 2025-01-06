---
title: Vegetronix VegeHub
description: Instructions on how to integrate a VegeHub device with Home Assistant.
ha_category:
  - Sensor
  - Switch
ha_config_flow: true
ha_release: 2024.11
ha_iot_class: Local Push
ha_codeowners:
  - '@ghowevege'
ha_domain: vegehub
ha_platforms:
  - sensor
  - switch
ha_integration_type: integration
---

The **Vegetronix VegeHub** {% term integration %} allows you to control your [VegeHub](https://www.vegetronix.com/Products/VG-HUB-RELAY/) and gather data from its attached sensors.

There is currently support for the following platforms within Home Assistant:

- Sensor - Gathers data from sensor channels on a VegeHub and stores the values in Home Assistant
- Switch - Allows you to view the status of relays on a VegeHub, and control them.

{% include integrations/config_flow.md %}

## Supported devices

- [Vegetronix VegeHub](https://www.vegetronix.com/Products/VG-HUB-RELAY/) - Firmware **4.0 or later** - All variants

## Setup

### WiFi

The VegeHub can be connected to WiFi *without* the need of additional apps or cloud accounts. When powered on, the VegeHub creates a WiFi access point called "Vege_XX_XX" where the XX are different for each device. Simply connect to this network from a phone, tablet, or other similar device. The default passphrase to connect to the access point is ```vegetronix```. This can (and should) be changed in the WiFi settings.

Once connected to the network, you should automatically be directed by your device to log in to the network. Follow the prompt to be directed to the VegeHub's WiFi setup page, where you can scan for available networks, put in your WiFi network's credentials, change the device's name, and change the access point password. Ensure that you change the access point password. If you don't it will be very easy for someone to access your VegeHub, where they will have access to all your WiFi credentials.

Press "Apply" and your VegeHub will reset the network connection and try to connect to the credentials you put in.

### Integration

The VegeHub integration will automatically detect VegeHub devices that are connected to the same network as your Home Assistant, and will present them in ```Settings->Devices and Services```.

Alternatively, a VegeHub can be added manually by going to ```Settings->Devices and Services```, then click the "Add Integration" button, search for the VegeHub integration, and click on it. If your VegeHub is not already listed here, click "Setup another instance of Vegetronix VegeHub" where you will be prompted for the device's IP address in order to continue setup.

There is currently no way to set up a VegeHub using {% term YAML %} in the 'configuration.yaml' file.

### Device Configuration

Once set up, you can click on the VegeHub integration in ```Settings->Devices and Services```. Here you can click "Configure" next to your VegeHub's listing in "Integration entries", where you will be able to set the sensor data type for any sensor channels on your VegeHub, and also change the "Default actuator duration", which is the maximum number of seconds that a command from Home Assistant will maintain control of a relay before releasing control back to the VegeHub's internal schedule. It defaults to 5 minutes (300 seconds).

The options for sensor data types are:

- Raw Voltage (Default) - Display and store the sensor value as the raw voltage measured by the VegeHub on this channel.
- VH400 - This sensor channel is connected to a [VH400](https://www.vegetronix.com/Products/VH400/) soil moisture sensor. Data will be converted from raw voltage into soil moisture percentage before displaying or storing it in Home Assistant.
- THERM200 - This sensor channel is connected to a [THERM200](https://www.vegetronix.com/Products/THERM200/) soil temperature sensor. Data will be converted from raw voltage into temperature before displaying or storing it in Home Assistant.

### Device Settings

In the VegeHub integration page, if you click "1 device" under your VegeHub's listing, you will be taken to your Device Info page. Here you will see all the entities available from this VegeHub, and you can click the "Visit" link to be taken directly to the VegeHub's device settings interface. Here you can directly change setting on the VegeHub.

## Power Management

The VegeHub has two power modes:

- Battery mode (default): Device sleeps after five minutes of inactivity
- Power adapter mode: Device remains always active

When in Power Adapter mode, the device will use significantly more power, so this mode should not be used when powering from batteries, as they will quickly be drained.

To change the power mode, visit the [Hub's settings interface](#device-settings), go to the "Settings" page, and change the "Power source" to "Power adapter".

## Device Removal

To remove a VegeHub from Home Assistant, find and click on the VegeHub integration on the "Devices and Services" page, click the menu dots next to the device you want to remove, and select "Delete"

## Troubleshooting

- Setup is failing
  - Ensure that the VegeHub is awake by pressing the button on the board, or by disconnecting, and reconnecting power.
- [Hub's settings interface](#device-settings) is not accessible
  - Ensure that the VegeHub is awake by pressing the button on the board, or by disconnecting, and reconnecting power.
- Actuators are not responding
  - Ensure that the VegeHub is awake by pressing the button on the board, or by disconnecting, and reconnecting power.
  - Consider switching to [power adapter mode](#power-management) for consistent response

## Further Information

- [VegeHub Product Page](https://www.vegetronix.com/Products/VG-HUB-RELAY/)
- [VegeHub Quick Start Guide](https://www.vegetronix.com/Products/VG-HUB-GEN2/QuickStart)
- [VegeHub Manual](https://vegetronix.com/Products/VG-HUB-GEN2/Manual)