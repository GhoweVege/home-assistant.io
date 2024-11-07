---
title: Vegetronix VegeHub
description: Instructions on how to integrate a VegeHub device with Home Assistant.
ha_category:
  - Sensor
  - Switch
ha_config_flow: true
ha_release: 2024.12
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

- [Vegetronix VegeHub](https://www.vegetronix.com/Products/) - Firmware **4.0 or later** - All variants

## Setup

### WiFi

The VegeHub can be connected to WiFi *without* the need of additional apps or cloud accounts. When powered on, the VegeHub creates a WiFi access point called "Vege_XX_XX" where the XX are different for each device. Simply connect to this network from a phone, tablet, or other similar device. The default passphrase to connect to the access point is ```vegetronix```. This can (and should) be changed in the WiFi settings.

Once connected to the the network, you should automatically be directed by your device to log in to the network. Follow the prompt to be directed to the VegeHub's WiFi setup page, where you can scan for available networks, put in your WiFi network's credentials, change the device's name, and change the access point password. Press "Apply" and your VegeHub will reset the network connection and try to connect to the credentials you put in.

### Integration

The VegeHub integration will automatically detect VegeHub devices that are connected to the same network as your Home Assistant, and will present them in ```Settings->Devices and Services```.

Alternatively, a VegeHub can be added manually by going to ```Settings->Devices and Services```, then click the "Add Integration" button, search for the VegeHub integration, and click on it. If your VegeHub is not already listed here, click "Setup another instance of Vegetronix VegeHub" where you will be prompted for the device's IP address in order to continue setup.

There is currently no way to set up a VegeHub using {% term YAML %} in the 'configuration.yaml' file.

### Device Configuration

Once set up, you can click on the VegeHub integration in ```Settings->Devices and Services```. Here you can click "Configure" next to your VegeHub's listing in "Integration entries", where you will be able to set the sensor data type for any sensor channels on your VegeHub, and also change the "Default actuator duration", which is the maximum amount of time that a command from Home Assistant will maintain control of a relay before releasing control back to the VegeHub's internal schedule.

### Device Settings

In the VegeHub integration page, if you click "1 device" under your VegeHub's listing, you will be taken to your Device Info page. Here you will see all the entities available from this VegeHub, and you can click the "Visit" link to be taken directly to the VegeHub's device settings interface. Here you can directly change setting on the VegeHub.

## Troubleshooting

- Setup is failing
  - Ensure that the VegeHub is on. In its default configuration the VegeHub goes to sleep after five minutes of inactivity, and only wakes up when it has sensor readings to send, or internally scheduled relays to flip. Simply press the button on your VegeHub to wake it up.
- [Hub's settings interface](#device-settings) is not accessible
  - Ensure that the VegeHub is on. In its default configuration the VegeHub goes to sleep after five minutes of inactivity, and only wakes up when it has sensor readings to send, or internally scheduled relays to flip. Simply press the button on your VegeHub to wake it up.
- Actuators are not flipping when told to do so
  - Ensure that the VegeHub is on. In its default configuration the VegeHub goes to sleep after five minutes of inactivity, and only wakes up when it has sensor readings to send, or internally scheduled relays to flip. Simply press the button on your VegeHub to wake it up. If you would like the VegeHub to always be available, visit the [Hub's settings interface](#device-settings), go to the "Settings" page, and change the "Power source" to "Power adapter". This means that your VegeHub will always be active, but should be powered from a power adapter rather than by batteries.
