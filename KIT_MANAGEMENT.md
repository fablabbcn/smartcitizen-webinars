# Kit management

## Setup

- [x] Download and [install git](https://fablabbcn-projects.gitlab.io/learning/fabacademy-local-docs/guides/code/gitsetup/)
- [x] Download firmware repository: https://github.com/fablabbcn/smartcitizen-kit-21
- [x] Download platformio
- [x] Alternatively install `jupyter notebook` from [here](https://jupyter.org/) or `jupyter lab` from [here](https://jupyterlab.readthedocs.io/en/stable/)
- [x] Download python following [this guide](https://docs.python-guide.org/starting/installation/)
- [x] Install `scdata`

## The hardware

![](https://i.imgur.com/4310NdR.png)

![](https://i.imgur.com/xPSlJ6I.jpg)

![](https://i.imgur.com/PEv8OXk.jpg)

Operation modes: https://docs.smartcitizen.me/Smart%20Citizen%20Kit/#operation-modes

## Configure one kit

Start here https://start.smartcitizen.me/wizard/landing?lang=eng

## Getting firmware information

This guide: https://docs.smartcitizen.me/Guides/getting%20started/Getting%20firmware%20information/

## Connecting to the SCK via SHELL

This guide: https://docs.smartcitizen.me/Guides/getting%20started/Using%20the%20Shell/

- Set the recording configuration
- Set recording and publication intervals
- Get version data
- List/modify the active sensors
- Read/monitor some sensors

Battery calculator: https://docs.smartcitizen.me/Smart%20Citizen%20Kit/#battery-calculator

## Update the firmware

### Without compilation

Request a firmware bin from us or download the latest release from github: https://github.com/fablabbcn/smartcitizen-kit-21. Then follow this guide: https://docs.smartcitizen.me/Guides/firmware/Update%20the%20firmware/

### Compiling the firmware

For this you need to compile the firmware with platformio. Clone the firmware repository and launch this in the terminal from the firmware main folder:

* For both microcontrollers:

```
python make.py build sam esp -v
```

* For the main microcontroller (more frequent updates):

```
python make.py build sam -v
```

* For the WiFi (less frequent):

```
python make.py build esp -v
```

If you see <span style="color: green">**[SUCCESS]**</span>, then we recommend to make a copy of the device's information. For this, connect it to your computer and in the SHELL of the kit:

```
SCK> config
...
```

And copy the output. After that, you can flash the microcontrollers:


* For both microcontrollers (not recommended at the same time):

```
python make.py flash sam esp -v -k
```

* For the main microcontroller (fast):

```
python make.py flash sam -v -k
```

* For the WiFi (slow):
```
python make.py flash esp -v -k
```


## Debug the sensors

Follow this guide: https://docs.smartcitizen.me/Guides/getting%20started/Debugging%20your%20sensors/

## Data analysis

In jupyter lab or other, follow the examples in the examples folder:
https://github.com/fablabbcn/smartcitizen-data/tree/master/examples/notebooks

## Inventory

Clone the firmware repository and launch this in the terminal from the firmware main folder:

```
➜  smartcitizen-kit-21 git:(master) ✗ python tools/register.py --help
USAGE:

resgister.py [options] action[s]

options: -v: verbose; -t: test device
actions: register, inventory
register options: -n platform_name -i kit_blueprint_id (default: 26)
inventory -d "description" --with-test [y/n] (default: n)
```

:::warning
Kits registration is not possible if you are not an admin, but we'll look into making a `researcher` role.
:::

However, it's possible to keep track of the kits in a local inventory if needed using this command:

```
python tools/register.py inventory -d "TEST_SCHOOL_1"
```

## Links of interest

:::info

- **Documentation**: http://docs.smartcitizen.me
- **Onboarding**: http://start.smartcitizen.me
- **#Now tracking**: https://now.smartcitizen.me/#bgg-project
:::

:::info
**Publications**:
- **General**: https://docs.smartcitizen.me/Use%20Cases/
- **Hardware X Publication**: https://doi.org/10.1016/j.ohx.2019.e00070
- **Particle Characterisation**: https://www.atmos-meas-tech-discuss.net/amt-2019-422/amt-2019-422.pdf
- **iSCAPE Results**: https://cordis.europa.eu/project/id/689954/results
:::

### Support

💬 **Discuss**: forum.smartcitizen.me
❓ **Support**: support@smartcitizen.me
