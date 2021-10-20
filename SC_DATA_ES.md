---
tags: webinar
title: Smart Citizen Data Webinar [ES]
---

# Smart Citizen Data Webinar

[TOC]

## Acceso a los datos

El acceso a los datos se puede realizar de varias maneras, de menor a mayor complejidad:

- **CSV** o datos tabulados:
    - datos de SDCARD
    - front-end en smartcitizen.me/kits y descarga de csv, siguiendo los pasos indicados en https://docs.smartcitizen.me/Guides/getting%20started/Downloading%20the%20Data/#download-data
- accediendo al **API REST**

### SDCard

Los datos en el SDCard tienen la siguiente nomenclatura: YY-MM-DD.CSV. Sin embargo, es posible encontrar otros ficheros con extensión (YY-MM-DD.01, YY-MM-DD.02...). Estos ficheros se generan cuando el SCK se reinicia. Son consecutivos a la fecha del fichero YY-MM-DD.CSV.

El SCK se reinicia diariamente a las 2am UTC para evitar pérdida de datos. En [la siguiente guía](https://docs.smartcitizen.me/Guides/data/Organise%20your%20data/#pre-process-the-sd-card-data) se explica como concatenar los ficheros.

El encabezado de los ficheros tiene la siguiente forma:

- `NOMBRE`. Ejemplo: `TEMP`
- `Unidades`. Ejemplo: `C`
- `Descripción`. Ejemplo: `Temperature`
- `ID de plataforma` (:warning:no eliminar). Ejemplo: `55`
- `Datos`

![](https://i.imgur.com/l5cPoix.png)

:::warning
Los datos inválidos se muestran como `null`
:::

En el CSV se pueden realizar comparativas sencillas de datos (ver [ejemplos](/#Ejemplos-CSV))

### CSV

Es posible obtener los datos de todo un dispositivo concatenado en formato CSV. El encabezado de los ficheros tiene la siguiente forma:

- `Nombre` in `unidades` (`sensor`). Ejemplo: `air temperature in ºC (SHT31 - Temperature)`

![](https://i.imgur.com/6HO5IW2.png)

En el CSV se pueden realizar comparativas sencillas de datos (ver [ejemplos](/#Ejemplos-CSV))

### Ejemplos CSV

:::success
EJEMPLOS
:::

### API

El API es la forma más avanzada de acceso a los datos, a la vez que más versátil y escalable. Estos son los puntos de acceso más importantes:

- Current user url: https://api.smartcitizen.me/v0/me
- Components url: https://api.smartcitizen.me/v0/components
- **Devices url: https://api.smartcitizen.me/v0/devices**
- Kits url: https://api.smartcitizen.me/v0/kits
- Measurements url: https://api.smartcitizen.me/v0/measurements
- Sensors url: https://api.smartcitizen.me/v0/sensors
- Users url: https://api.smartcitizen.me/v0/users
- Tags url: https://api.smartcitizen.me/v0/tags
- Tags sensors url: https://api.smartcitizen.me/v0/tag_sensors

:::info
- La documentación del API se encuentra en: https://developer.smartcitizen.me
- El endpoint más importante para recuperar datos de sensores es: https://api.smartcitizen.me/v0/devices/XXXXX/ donde *XXXXX* es el número de dispositivo.
:::

:::warning
El API limita el número máximo de peticiones a realizar por minuto, retornando un código de error `429`
:::

Los datos del API se pueden solicitar a través de peticiones HTTP para recuperar datos. Existen múltiples formas de acceder a los datos en el API, siempre que se disponga de un token para el acceso. Para encontrar el token, se puede encontrar en el [perfil de usuario](https://smartcitizen.me/profile/users):

![](https://i.imgur.com/qwbjnTt.png)

#### Scripts

Una manera de acceder a estos datos es utilizar el package de `python` disponible en [`scdata`](https://pypi.org/project/scdata/) y en el [repositorio git](https://github.com/fablabbcn/smartcitizen-data).

##### Instalación

Para instalar `scdata`, basta con abrir una terminal y correr:

```
pip install scdata
```

Es necesario tener un entorno de `python>3.*`. Para instalar `python` en cualquier plataforma es recomienda seguir [esta guía](https://docs.python-guide.org/starting/installation/).

Una vez instalado, existen una serie de ejemplos en [el repositorio](https://github.com/fablabbcn/smartcitizen-data/tree/master/examples) con diferentes funcionalidades. Es posible probar los ejemplos en un servidor remoto para hacer visualizaciones y probar el entorno en [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fablabbcn/smartcitizen-data-framework/master?filepath=%2Fexamples%2Fnotebooks).


:::info
**Ejemplos:**
- Getting started
- Data visualisation
- Data process
- Making HTML reports
:::

## Procesado

El procesado de datos se realiza de forma asíncrona. Todos los datos se postean en `raw` para luego procesarse apróximadamente a 500 posts a la hora. Los sensores que tienen datos en `raw` se ocultan por defecto en la plataforma:

![](https://i.imgur.com/ldhvRmd.jpg)

El procesado se puede realizar de varias maneras:

- Utilizar procesado por defecto
- Utilizar procesado customizado

### Procesado por defecto

Cada dispositivo en la plataforma tiene un procesado por defecto definido por su `blueprint`. El proposito de los blueprints es definir información de:
- Tipo de canales o métricas a calcular
- Localización de las calibraciones o modelos a aplicar

Cada dispositivo físico debe tener un, y sólo un, blueprint asociado para procesado. Existen 
[definiciones de blueprints por defecto](https://github.com/fablabbcn/smartcitizen-data/tree/master/blueprints) pero otros se pueden generar en función de las necesidades.

Para poder realizar el procesado de los datos, es necesario además disponer de una serie de parámetros en los modelos de calibración. Estos, se determinan en con un identificador único, definido [aquí](https://docs.smartcitizen.me/Guides/data/Handling%20calibration%20data/). Este identificador se encuentra en una pegatina en la carcasa y en el interior de los dispositivos:

```
{
  "blueprint_url": "https://raw.githubusercontent.com/fablabbcn/smartcitizen-data/master/blueprints/sc_21_station_module.json",
  "description": "2PMS5003-4ELEC-GPS",
  "versions": [
    {
      "ids": {
        "AS_48_01": "162893650",
        "AS_48_23": "202702016",
        "AS_4A_01": "164200207",
        "AS_4A_23": "204702953"
      },
      "from": "2020-11-30",
      "to": null
    }
  ]
}
```

Para realizar el procesado por defecto, es necesario introducir el código de identificación del dispositivo (el de la pegatina) en la página de edición del kit: https://smartcitizen.me/kits/XXXXX/edit

![](https://i.imgur.com/h4Np5ht.png)

Una vez introducido, los datos definidos en el blueprint, se procesarán con los modelos y parámetros definidos por dispositivo de acuerdo al `HARDWARE-ID`.

### Procesado customizado

Es posible realizar un procesado de los datos "customizado" al descargarlos en local a través de los métodos vistos anteriormente. Se recomienda usar `scdata` para ello, siguiendo los ejemplos en:

- Processing data: https://github.com/fablabbcn/smartcitizen-data/tree/master/examples/notebooks/04_processing_data.ipynb
- Sensor calibration: https://github.com/fablabbcn/smartcitizen-data/tree/master/examples/notebooks/05_sensor_calibration_workflows.ipynb

#### Automatización

Para evitar analizar los datos manualmente, se puede definir un procesado automático una vez definidas las funciones y modelos de procesado.

Es procedimiento sería:

- Añadir la funcionalidad necesaria en `scdata` mediante PR al repositorio de [smartcitizen-data](https://github.com/fablabbcn/smartcitizen-data)
- Generar `blueprint` asociado y `hardware_id` y añadirlo al repositorio de [smartcitizen-data](https://github.com/fablabbcn/smartcitizen-data) mediante PR
- Añadir el `hardware_id` al dispositivo para que sea procesado periódicamente

## Visualización



## Análisis

