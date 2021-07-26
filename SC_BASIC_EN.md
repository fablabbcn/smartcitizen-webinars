---
tags: presentation
---

# Smart Citizen Webinar [EN]

[TOC]

<a data-flickr-embed="true" href="http://smartcitizen.me" title="SCK 2.1 in context"><img src="https://live.staticflickr.com/65535/48020070592_ebad902f1d_h.jpg" alt="SCK 2.1 in context"></a>

## The kit

<a data-flickr-embed="true" href="http://docs.smartcitizen.me/Smart%20Citizen%20Kit/#sck-21" title="SCK 2.1 All parts"><img src="https://live.staticflickr.com/65535/47950912168_fcf8fa398c_h.jpg" alt="SCK 2.1 All parts"></a>

The Smart Citizen Kit (SCK) is the core of a modular hardware system which aims to provide tools for environmental monitoring, ranging from citizen science activities to more advanced research. The system is comprised of the following elements:

- **Data Board**: data-logger with Wi-Fi connectivity and micro SD-card, to which the other components are branched to

<img src="https://live.staticflickr.com/65535/47950912298_2b132245cb_h.jpg" alt="SCK 2.1 Data Board">

- **Urban Sensor Board**: board contiening a selection of low cost sensors, as well as a connector for an external PM Sensor

<img src="https://live.staticflickr.com/65535/47950912253_2919caffdb_h.jpg" alt="SCK 2.1 Urban Sensor Board">

The sensor list is shown in the table below:


| Measurement | Units | Sensor |
| -------- | -------- | -------- |
| Air temperature     | degC     | Sensirion SHT-31     |
| Relative Humidity     | %REL     | Sensirion SHT-31     |
| Noise level     | dBA     | Invensense ICS43432     |
| Ambient Light     | Lux     | Rohm BH1721FVC     |
| Barometric pressure     | kPa     | NXP MPL3115A26     |
| Equivalent Carbon Dioxide     | ppm     | AMS CCS811     |
| Volatile Organic Compounds     | ppb     | AMS CCS811     |
| Particle Matter PM1 / 2.5  / 10     |  ug/m3     | Plantower PMS5003     |

:::success
The most relevant sensors for outdoor exposure are noise (Noise dBA) and PM1-PM2.5
:::

### Sensors

The sensors in the _Urban Sensor Board_ are a selection of low-cost sensors ([Rai et al.](https://doi.org/10.1016/j.scitotenv.2017.06.266)) that allow monitoring:

- Temperature and relative humidity
- Barometric pressure
- **Ambient noise** in different scales (**dBA**, dBC, dBZ)
- **Particulate Matter** (PM) in different sizes (PM1, **PM2.5**, PM10)
- Indicative measurements TVOC & eCO2 (CO2 equivalent)

:::info
Additionally, a more **complete description** of the sensors in the Urban Board can be found at: https://docs.smartcitizen.me/Components/boards/Urban%20Board/. All the **performance** of the sensors can be found in: https://docs.smartcitizen.me/Components/sensors/performance/. Some other sensors can be found:
- **PM Sensor**: https://docs.smartcitizen.me/Components/sensors/air/PM%20Sensors/
- **AMS CCS811**: https://docs.smartcitizen.me/Components/sensors/air/CCS811/
- **Noise**: https://docs.smartcitizen.me/Components/sensors/air/Noise/
:::



### Operation modes and interface

The kit has two main operation modes: _setup_ mode, and *recording* mode. The first configures the second, allowing to select the recording mode for the data (online or SD-card). The [onboarding section](#Onboarding) explains the differences between them.

:::info
These modes are reflected in the status of the LED, and are documented in the following page of the documentation: https://docs.smartcitizen.me/Smart%20Citizen%20Kit/#operation-modes
:::

The user also has the option to change the operation mode by pressing the button:

<img src="https://live.staticflickr.com/65535/48439505516_d210ce2c8a_h.jpg" alt="SCK 2.1 Outdoor enclosure"><br>

:::info
The interfaces are documented in the following page: https://docs.smartcitizen.me/Smart%20Citizen%20Kit/#user-interfaces
:::


### Power

Some recommendations are listed below:

- The Kit needs to be charged **before the first installation**
- When the Kit is connected on online mode it will report to the platform, and even an email notification can be set. However, on SD card mode we will need to check the LED. You can see some feedback from the LED to know if it's charging (more information [here](https://docs.smartcitizen.me/SCK_Station/#operation-modes))

<div style="text-align:center">
<img src="https://i.imgur.com/ABSXX4w.jpg" width="400px">
</div>

- A **full charge can take up to 9 hours**, and this charge will last for at least 3-4 weeks. You can check this battery calculator to get a more accurate estimation: https://docs.smartcitizen.me/Smart%20Citizen%20Kit/#battery-calculator

#### Saving power

Battery can be saved by reducing the reading and publication intervals of the kit. Make sure to follow this guide: https://docs.smartcitizen.me/Guides/getting%20started/Using%20the%20Shell/#set-recording-and-publication-intervals

:::info
**When to charge it?**
The LED will start flashing in orange when the SCK has low battery. After connecting the kit to a power source you will see orange blinks during the charging process until and green blinks when the battery is fully charged.

One option for powering the Kit is to leave it on battery and bring a power extention to it every 3 weeks to charge it. For instance, you can do so through a window and just during some hours.
:::

### Power Supply

The Smart Citizen Power Supply is a simple power supply to power the SCK and the Smart Citizen Station with 110-230 AC mains power, including a 1.6A input fuse protection and a 5VDC regulated output.

:::info
More information on the unit: https://docs.smartcitizen.me/Components/boards/Power%20Supply/ and how to check it's **operation**: https://docs.smartcitizen.me/Guides/deployments/Using%20the%20power%20supply/
:::

## Onboarding

[![](https://i.imgur.com/v5GmJeo.png)](http://start.smartcitizen.me)

The _onboarding_ is a web interface that allows configuring the SCK in the desired mode, and to link the device with an user profile in the platform.

:::success
Check this guide to not miss a step: https://docs.smartcitizen.me/Guides/getting%20started/Onboarding%20Sensors/
:::

It is important to understand that the **same physical device can be linked with several devices in the platform**, although it can only send data to one of them at a time. The link between them is done through a _token_, which is assigned during the _onboarding_ procedure. This is then associated with an user profile and it's copied into the physical device through a mobile interface. This interface also serves as a method to tell the device the Wi-Fi credentials (SSID and password).

## Enclosure and mounting system

The mounting system provided has the possibility to mount on wall or post. It is a rain-proof enclosure that can be opened by hand:

![](https://i.imgur.com/dhMbs7d.png)

<div style="text-align:center">
<img src="https://live.staticflickr.com/65535/48991677568_9b41b36cce_k.jpg">
</div>
<br>

## Data

### The platform

[![](https://i.imgur.com/mo5RzkR.jpg)](https://smartcitizen.me/kits/)

The web platform has the following functions:

- Geolocalized browsing and basic data visualization per device
- Kits edition and user profile management
- SD card data upload
- CSV data download

:::info
Generally, the data is sent to the platform in real-time, and we use the sd-card as a back-up in case of loss of connectivity. In this case, you will be using the kit in sd-card mode, so the analysis can be done with common spreadsheets. More advance data analysis is provided in the section below.
:::

### Advanced data analysis

[![](https://i.imgur.com/nJHbu4p.png)](https://github.com/fablabbcn/smartcitizen-iscape-data)

The _Sensors analysis framework_ is an environment developed in `python` that allows:

- Manage data from different sources (API or sd card)
- Explore data in an interactive way
- Model and calibrate sensor data
- Model managament and data export

:::info
The API developer documentation can be found in:
https://developer.smartcitizen.me/
:::

:::info
The framework repository can be found in: https://github.com/fablabbcn/smartcitizen-iscape-data
:::

## Practical questions

### Physical installation tips

* If in _online_ mode, a Wi-Fi WPA/WPA2 Personal network is needed. We are not able to support more complex networks (with captive portals, as in airports, eduroam, etc)
* In order to charge the device periodically (every 3 weeks in this case), it would be desirable to have a power supply nearby
* For a proper sensor stability, the sensor should be installed away from direct sun radiation

### Monitor your kits

[![](https://i.imgur.com/sO7ZBxv.png)](https://now.smartcitizen.me/#bgg-project)

### Troubleshooting :scream:

1. :radio_button: **The magical reset button**

![](https://i.imgur.com/lnFrnwS.png)

2. 👷 **Troubleshooting page** https://docs.smartcitizen.me/Troubleshooting/

3. :nut_and_bolt: **Debugging the sensors** https://docs.smartcitizen.me/Guides/getting%20started/Debugging%20your%20sensors/

4. 💬 **Forum**: https://forum.smartcitizen.me

5. ❓ **Support**: [support@smartcitizen.me](mailto:support@smartcitizen.me)

## Interesting links

:::info
- **Documentation**: http://docs.smartcitizen.me
- **Onboarding**: http://start.smartcitizen.me
- **#Now tracking**: https://now.smartcitizen.me/#bgg-project
- **Enclosures (3D printing parts)**: https://github.com/fablabbcn/smartcitizen-enclosures/tree/master/SmartCitizen%20Outdoor%20Cases%20V2.0-2.1
- **Using the Shell**: https://docs.smartcitizen.me/Guides/getting%20started/Using%20the%20Shell/
- **Debugging your sensors**: https://docs.smartcitizen.me/Guides/getting%20started/Debugging%20your%20sensors/
:::

:::info
**Publications**
- **General**: https://docs.smartcitizen.me/Use%20Cases/
- **Hardware X Publication**: https://doi.org/10.1016/j.ohx.2019.e00070
- **Particle Characterisation**: https://www.atmos-meas-tech-discuss.net/amt-2019-422/amt-2019-422.pdf
- **iSCAPE Results**: https://cordis.europa.eu/project/id/689954/results
:::
