---
tags: webinar
title: Smart Citizen Data Webinar [ES]
---

# Smart Citizen Data Webinar

[![hackmd-github-sync-badge](https://hackmd.io/OtkFE3TIRruBNS5L4BbTpw/badge)](https://hackmd.io/OtkFE3TIRruBNS5L4BbTpw)


[TOC]

## Acceso a los datos

![](https://i.imgur.com/loUgFJv.png)

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

En el CSV se pueden realizar comparativas sencillas de datos (ver [ejemplos](#Visualización-CSV))

### CSV

Es posible obtener los datos de todo un dispositivo concatenado en formato CSV. El encabezado de los ficheros tiene la siguiente forma:

- `Nombre` in `unidades` (`sensor`). Ejemplo: `air temperature in ºC (SHT31 - Temperature)`

![](https://i.imgur.com/6HO5IW2.png)

En el CSV se pueden realizar comparativas sencillas de datos (ver [ejemplos](#Visualización-CSV))

### API

![](https://i.imgur.com/qiDKL0r.jpg)

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

![](https://upload.wikimedia.org/wikipedia/commons/thumb/a/aa/FAIR_data_principles.jpg/1200px-FAIR_data_principles.jpg)

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

Es procedimiento a seguir para la integración:

- Añadir la funcionalidad necesaria en `scdata` mediante PR al repositorio de [smartcitizen-data](https://github.com/fablabbcn/smartcitizen-data)
- Generar `blueprint` asociado y `hardware_id` y añadirlo al repositorio de [smartcitizen-data](https://github.com/fablabbcn/smartcitizen-data) mediante PR
- Añadir el `hardware_id` al dispositivo para que sea procesado periódicamente

## Visualización

Es posible visualizar los datos de varias formas:

- Datos CSV
- Scripts (`scdata`)
- Otros

### Visualización CSV

- Timeseries
- Scatter plot

:::info
**Pasos:**

- Hacer copia del CSV a documento .xls o .ods
- Eliminar filas 2 a 4
- Hacer filtro automático
- En caso de querer graficar PM, eliminar `null`
:::

![](https://i.imgur.com/SVYayDF.png =400x)

- Generar gráficos con herramientas por defecto (mejor utilizar Line o XY (Scatter como Chart type para timeseries o scatter plots))

![](https://i.imgur.com/yJkbrf4.png)

- Ejemplo timeseries con Line Chart Type:

![](https://i.imgur.com/aTdcb2t.png)

- Ejemplo Scatter plot (con línea de tendencia y R2) - baja correlación

![](https://i.imgur.com/8m47ogk.png)

- Ejemplo Scatter plot (con línea de tendencia y R2) - alta correlación

![](https://i.imgur.com/YkjR2S6.png)

:::warning
Este método tiene el limitante del número de datos a graficar.
:::

:::success
**Comentarios**

- La correlación de dos variables implica únicamente cuánto de relacionadas están entre ellas en una expresión lineal, es decir, cuánto de predecible es una variable cuando tenemos la otra. Sin embargo, no implica causalidad. Un valor de correlación alto (cercano a 1), es indicador de alta relación entre ambas variables. Es importante además tener en cuenta que las variables deben tener grados similares de ruido (o no) para evitar falsas conclusiones
- Cuando representemos datos, especialmente intendando compararlos, es importante establecer escalas "justas (_justicia_)", no tratando de ampliar o reducir los ejes para forzar conclusiones sobre los datos en lugar de extraerlas de los mismos: más ejemplos en esta [referencia](https://infogram.com/blog/dataviz-chart-guide-101-dos-and-donts/)

:::

### Scripts

- Gráficos interactivos
- Varios formatos de gráfico: timeseries, scatter-plot, scatter-plot matrix, dendogram, target plot, violin, box plot...

**Ejemplos**

- Timeseries de ruido
![](https://i.imgur.com/u1WyxSf.png)

- Máximos de temperatura cada 24h
![](https://i.imgur.com/LXxzgPk.png)

- Distribución diaria de ruido
![](https://i.imgur.com/sKtz3m9.png)

- Promedio de particulas respecto a eventos
![](https://i.imgur.com/bPJ3FeE.png)

:::success
**Ventajas**

- Manejo de altas cantidades de datos con herramientas adaptadas a ello
- Versatilidad en el análisis y la visualización
- Muchos ejemplos avanzados en github.com, stackoverflow.com, etc...

:::

### Otros

Adicionalmente, existen otros métodos de visualización y conectores en [toolkit](https://github.com/fablabbcn/smartcitizen-toolkit):

- Nodered
- Processing
- ...

## Análisis

Antes de proceder al análisis, se recomienda seguir los siguientes pasos:

- Definir el objetivo del análisis
- Preprocesar y validar los datos: filtrado, limpieza, etc.
- Calcular métricas: promedios, máximos, mínimos, desviaciones
- Realizar visualizaciones
- Derivar conclusiones (datos vs. standards)
- Generar report

### Preprocesado

En sensores en general, y más incluso en el caso de los sensores de bajo coste para medidas ambientales, se recomienda aplicar filtrado (entendido como smoothing) en las lecturas.

**Ejemplos**

- Moving average, rolling average, etc

![](https://i.imgur.com/DYc7pXV.png)

:::danger
Es peligroso hacer un smoothing muy alto de los datos al poder perder información importante de los mismos
:::

Adicionalmente, se recomienda hacer limpieza de `outliers`, por ejemplo derivados de lecturas erróneas de lectores. El origen de estos `outliers` puede proceder de:

- Periodos de adaptación de sensores
- Errores en la cadena de lectura
- Sucesos aleatorios (golpes, salpicadura o condensación en los sensores que provoquen fallas)

**Ejemplos**

![](https://i.imgur.com/IB67TdY.png)

:::info
Normalmente, una gran cantidad de `outliers` se eliminan simplemente haciendo un filtrado de los datos. 

Otros métodos alternativos:

- Peak detection
- Stadistical Outlier removal
:::

### Cálculo de métricas

**Métricas comunes:**

1. Promedio, máximos, mínimos de la lecturas a distintos intervalos: periodo completo, horario, diario, etc:

```python=
for device in test.devices:
    print (f"{device} PM1 avg: {test.devices[device].readings['PM_1'].mean()}")
    print (f"{device} PM1 max: {test.devices[device].readings['PM_1'].max()}")
    print (f"{device} PM1 min: {test.devices[device].readings['PM_1'].min()}")
```

Resultado:

```
14129 PM1 avg: 5.776936723832052
14129 PM1 max: 73.0
14129 PM1 min: 0.0
```

2. Desviaciones en distintos intervalos (no sólo valores puntuales, sino cuánto varían)

### Derivar conclusiones

Tratar de incluir otros datos en el _mix_: bien otras redes de monitorización (sirven además para validar la nuestra), así como standards:

:::info
**Ejemplos**
- Redes locales: http://www.aire.cdmx.gob.mx
- Standards WHO: https://www.who.int/news/item/22-09-2021-new-who-global-air-quality-guidelines-aim-to-save-millions-of-lives-from-air-pollution
:::

### Generación de reports

Documentos explicativos de análisis que contengan información sobre:

- Qué datos se usaron para el análisis, de qué sensores
- Qué procesado sufrieron
- Cómo se acceden
- ...

:::info
**TL;DR**
No es suficiente tener sensores de código abierto, ni datos abiertos, sino explicar cómo esos datos se han usado, dónde están, cómo se han procesado y qué conclusiones se han extraído
:::

Es posible generar directamente análisis y reports `html` y `pdf` con estas referencias en `scdata`:

![](https://i.imgur.com/2fMdu1t.png)

![](https://i.imgur.com/3doY810.png)

:::info
**Ejemplos**

https://github.com/fablabbcn/smartcitizen-data/blob/master/examples/notebooks/11_making_html-pdf_reports.ipynb
:::