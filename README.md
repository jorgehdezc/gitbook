---
description: Pasos para dirigir ataques
---

# 1. Ingeniería Social y DoS

Banco de pruebas: Kali linux 2023 y Metaspolitable 2

La configuración de las maquinas virtuales se establece en red NAT para permitir la comunicacion entre las maquinas imitando las condiciones de un ataque en una red local o a travez de internet con la correspondiente informacion de los puntos de ataque mediante la informacion de DNS o similar.

## Ataque de ingeniería Social

Se utiliza una herramienta llamada Setoolkit

```
// se ingresara como usuario root
sudo su
setoolkit
```

<figure><img src=".gitbook/assets/Captura de pantalla 2024-02-29 a la(s) 11.29.12 p.m..png" alt=""><figcaption></figcaption></figure>

Se seleciona el ataque de ingenieria social "1"

<figure><img src=".gitbook/assets/Captura de pantalla 2024-02-29 a la(s) 11.29.31 p.m..png" alt=""><figcaption></figcaption></figure>

Se selecciona el vector de ataque WEB "2"

<figure><img src=".gitbook/assets/Captura de pantalla 2024-02-29 a la(s) 11.29.41 p.m..png" alt=""><figcaption></figcaption></figure>

Se seleciona la opcion de recoleccion de credenciales "3"

<figure><img src=".gitbook/assets/Captura de pantalla 2024-02-29 a la(s) 11.30.04 p.m..png" alt=""><figcaption></figcaption></figure>

Selecionarmos la opacion de web template para la visualizacion del sitio "1"

<figure><img src=".gitbook/assets/Captura de pantalla 2024-02-29 a la(s) 11.30.24 p.m..png" alt=""><figcaption></figcaption></figure>

Definimos la ip de captura de informacion (puede ser nuestra misma IP)

<figure><img src=".gitbook/assets/Captura de pantalla 2024-02-29 a la(s) 11.30.54 p.m..png" alt=""><figcaption></figcaption></figure>

Seleccionamos la opcion de Google.

<figure><img src=".gitbook/assets/Captura de pantalla 2024-02-29 a la(s) 11.31.13 p.m..png" alt=""><figcaption></figcaption></figure>

Esto nos entregara un sitio web con una visualizacion muy parecida a la origina o la mas conocida por los usuarios.

<figure><img src=".gitbook/assets/Captura de pantalla 2024-02-29 a la(s) 11.33.42 p.m..png" alt=""><figcaption></figcaption></figure>

Al mismo tiempo tenemos una recolección de las credenciales introducidas por la victima.

<figure><img src=".gitbook/assets/Captura de pantalla 2024-02-29 a la(s) 11.34.59 p.m..png" alt=""><figcaption></figcaption></figure>

Con esto podemos consegir la recoleccion de contraseñas de las victimas en cuestion.

<div>

<figure><img src=".gitbook/assets/Captura de pantalla 2024-02-29 a la(s) 11.36.50 p.m..png" alt=""><figcaption></figcaption></figure>

 

<figure><img src=".gitbook/assets/Captura de pantalla 2024-02-29 a la(s) 11.36.26 p.m..png" alt=""><figcaption></figcaption></figure>

</div>

## Ataque DoS

Iniciamos por descubir cuales la ip local que tenemos en la red local.

```
ifconfig
```

<figure><img src=".gitbook/assets/Captura de pantalla 2024-02-29 a la(s) 10.53.28 p.m..png" alt=""><figcaption></figcaption></figure>

Por medio de esta ip podemos conocer los equipos en la red.

```
sudo arp -a
```

<figure><img src=".gitbook/assets/Captura de pantalla 2024-03-01 a la(s) 12.07.36 a.m..png" alt=""><figcaption></figcaption></figure>

asi mismo podemo rasterar secciones especificas de la red por medio de nmap y la ip en cuestion con la mascara de red en bit.

```
nmap 192.168.254.0/24
```

<figure><img src=".gitbook/assets/Captura de pantalla 2024-02-29 a la(s) 10.59.00 p.m..png" alt=""><figcaption></figcaption></figure>

Procedemos a utilizar la herramienta  hping3 con dirigiendo al puerto e ip de la victima.

```
hping3 -p 80 -S --flood 192.168.254.128
```

<figure><img src=".gitbook/assets/Captura de pantalla 2024-02-29 a la(s) 11.04.30 p.m..png" alt=""><figcaption><p>Esto enviara paquetes al pueto selecionado.</p></figcaption></figure>

Para visualizar los ataques de manera grafica se utilizara la herramienta etherape, para esto requeriremos intalarlo en kali mediate el sigueinte comando.

```
sudo apt-get install -y atherape
```

<figure><img src=".gitbook/assets/Captura de pantalla 2024-02-29 a la(s) 11.07.05 p.m..png" alt=""><figcaption></figcaption></figure>

Para inicializarlo puede ser desde terminal o grafico pero se deberá ejecutar como root

<figure><img src=".gitbook/assets/Captura de pantalla 2024-02-29 a la(s) 11.08.02 p.m..png" alt=""><figcaption></figcaption></figure>

Esto nos permitirá visualizar los paquetes que se enviar a la victiva asi como las comunicaciones que se realizan en la red asociada a nuestra tarjeta.

<figure><img src=".gitbook/assets/Captura de pantalla 2024-02-29 a la(s) 11.13.47 p.m..png" alt=""><figcaption></figcaption></figure>
