---
tags: presentation
title: Smart Citizen Webinar
---

# Smart Citizen Webinar

<a data-flickr-embed="true" href="http://smartcitizen.me" title="SCK 2.1 in context"><img src="https://live.staticflickr.com/65535/48020070592_ebad902f1d_h.jpg" alt="SCK 2.1 in context"></a>

## El kit

<a data-flickr-embed="true" href="http://docs.smartcitizen.me/Smart%20Citizen%20Kit/#sck-21" title="SCK 2.1 All parts"><img src="https://live.staticflickr.com/65535/47950912168_fcf8fa398c_h.jpg" alt="SCK 2.1 All parts"></a>

El Smart Citizen Kit (SCK) es núcleo de un sistema modular de hardware cuya intención es proporcionar herramientas de monitorización ambiental, tanto en _citizen science_ como en investigación. El sistema propuesto se compone de los siguientes elementos:

- **Data Board**: data-logger con conectividad Wi-Fi y micro SD-card, a la cual se conectan el resto de componentes.

<img src="https://live.staticflickr.com/65535/47950912298_2b132245cb_h.jpg" walt="SCK 2.1 Data Board">

- **Urban Sensor Board**: placa que contiene una selección de sensores de bajo coste, así como un conector para un sensor de partículas externo.

<img src="https://live.staticflickr.com/65535/47950912253_2919caffdb_h.jpg" alt="SCK 2.1 Urban Sensor Board">

La lista de sensores se puede ver en la siguiente tabla:

![](https://i.imgur.com/JAma2LX.png)

- **Alimentación**: caja de alimentación IP65 con entrada AC 220V y salida DC 5V con conector micro USB integrado:

<div style="text-align:center" ><img src="https://i.imgur.com/50JsH5A.jpg" width="500px">
</div>
<br>

- **Carcasa y sistema de montaje**: sistema estanco con posibilidad de montaje sobre pared o poste.

<div style="text-align:center">
<img src="https://i.imgur.com/EqFDUWj.png">
</div>
<br>
<br>

<div style="text-align:center">
<img src="https://live.staticflickr.com/65535/48992224646_bd32af64ae_k.jpg">
</div>
<br>

### Sensores

Los sensores presentes en la _Urban Sensor Board_ son un conjunto de sensores de bajo coste ([Rai et al.](https://doi.org/10.1016/j.scitotenv.2017.06.266)) que permiten monitorizar:

- Temperatura y humedad relativa del aire
- Presión barométrica
- Ruido ambiental en diferentes escalas (dBA, dBC, dBZ)
- Particulate Matter (PM) de diferentes tamaños (PM1, PM2.5, PM10)
- Medidas indicativas of TVOC y eCO2 (CO2 equivalente)

Finalmente, una descripción más completa de los sensores en la _Urban Sensor Board_ puede encontrarse en la documentación: http://docs.smartcitizen.me/Components/Urban%20Sensor%20Board/


### Modos de operación e interfaz

El kit tiene dos modos fundamentales de operación: modo configuración y modo grabación. El primero permite configurar al segundo, permitiendo seleccionar el modo de grabado de los datos (online o en micro sd-card) y proporcionar los datos necesarios para ello. En la sección de onboarding se explican los elementos necesarios en cada caso.

Estos modos se reflejan en el estado del LED, y están documentados en la siguiente página de la documentación: https://docs.smartcitizen.me/Smart%20Citizen%20Kit/#operation-modes.

El usuario también tiene la posibilidad de cambiar el modo de operación a través del botón:

![](https://i.imgur.com/BMDCmMa.png)

Las interfaces se encuentran documentadas en la siguiente página de la documentación: https://docs.smartcitizen.me/Smart%20Citizen%20Kit/#user-interfaces

## Onboarding

[![](https://i.imgur.com/v5GmJeo.png)](http://start.smartcitizen.me)

El _onboarding_ es una interfaz web que permite configurar el SCK en el modo deseado y asignar el dispositivo a un perfil de usuario en la plataforma. 

Es importante entender que un **mismo dispositivo físico puede tener ser asignado a diferentes dispositivos en la plataforma**, aunque sólo puede enviar datos a uno de ellos simultáneamente. La manera de conectar ambos se realiza a través del _token_, el cual se asigna durante el procedimiento de onboarding, y se asocia a un dispositivo en la plataforma. Este _token_ se introduce en el dispositivo físico en configuración a través de una interfaz móvil, así como las credenciales Wi-Fi (SSID y contraseña).

## La plataforma

[![](https://i.imgur.com/mo5RzkR.jpg)](https://smartcitizen.me/kits/)

La plataforma web de Smart Citizen permite realizar las siguientes funciones:

- Navegación geolocalizada y visualización de datos por dispositivo
- Gestión del perfil de usuario y edición de kits
- Subida de datos de SCKs sin conectividad con SD card
- Descarga de datos en CSV

## Análisis de datos

[![](https://i.imgur.com/nJHbu4p.png)](https://github.com/fablabbcn/smartcitizen-iscape-data)

El _Sensors analysis framework_ es un entorno de análisis de datos basado en `python` que permite:

- Generar test en función de datos en CSV o del API, descargando datos directamente de este último
- Visualización y exploración de datos en formato interactivo
- Modelado con diversas técnicas estadísticias clásicas o más avanzadas y comparación de métricas, tanto en batch como individual
- Export de modelos y datos procesados en diferentes formatos

La documentación de acceso al API se encuentra en:  https://developer.smartcitizen.me/

El repositorio del framework se encuentra en:  https://github.com/fablabbcn/smartcitizen-iscape-data

## Cuestiones prácticas


### Requerimientos para la instalación física:

* En caso de modo de grabación _online_, es necesaria una red Wi-Fi con soporte WPA/WPA2
* Toma de alimentación eléctrica (220v) a menos de dos metros del punto de instalación
* Para conseguir una buena estabilidad de los sensores, el punto de instalación debe encontrarse en una zona con poca radiación solar 


### Monitorizar kits

[![](https://i.imgur.com/sO7ZBxv.png)](https://now.smartcitizen.me/#bgg-project)

**Notificaciones por email**

![](https://i.imgur.com/Yro2QOS.png)

## Links de interés

:::info

- **Documentación**: http://docs.smartcitizen.me
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

### Soporte

💬 **Discuss**: forum.smartcitizen.me
❓ **Support**: support@smartcitizen.me


