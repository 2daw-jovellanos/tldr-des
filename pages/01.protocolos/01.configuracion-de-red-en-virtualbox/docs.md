---
title: 'Configuración de red en VirtualBox'
taxonomy:
    category: docs
visible: true
---

[TOC]
Los [hypervisores](https://es.wikipedia.org/wiki/Hipervisor) como **VirtualBox** o **VMWare** no solo virtualizan sistemas, sino también redes.

## Conceptos previos
### DHCP
__Dynamic Host Configuration Protocol__ es un sistema por el cual se puede proporcionar la configuración IP a una máquina durante su arranque. Ideal para máquinas de consumo , no tanto para máquinas de servicio.

Las máquinas sin configuración lanzan una señal de difusión indicando que necesitan configuración. Esta señal llega a todas las máquinas de la red, pero será atendida por el servidor de DHCP, que tiene la configuración básica de una máquina de la red:
* Un rango de IPs para asignar
* La máscara de subred
* Un par de servidores de resolución de nombres (DNS)
* Una puerta de enlace (el router que permite dar acceso a ordenadores de otras redes, como los de Internet)

### Puerta de enlace
En una red local, las máquinas suelen estar configuradas para dirigir todo el tráfico que no es interno (a otras máquinas de la misma red) hacia un router conectado dentro de la red, al que se suele llamar **puerta de enlace**, porque es el primero que interconecta con el exterior (habitualmente internet).

## Configuraciones de red en hypervisores
### NAT
El anfitrion actúa de servidor __DHCP__ y de __puerta de enlace__ hacia internet para una máquina huesped. Adecuado para una sola máquina virtual en la que se requiera conexión a internet. Se crea una red virtual sencilla en la que solo está el sistema huesped.

### Red NAT
Es una red virtual con todo un rango de direcciones IP privadas, una puerta de enlace virtual y un servidor DHCP.
Las redes NAT deben crearse explícitamente.

### Modo bridge
La máquina virtual utiliza la tarjeta de red física para conectarse a la red del anfitrion, y no a una red virtual. 
>>>> En entornos con un número de IPs limitado en el servidor DHCP (como el instituto), poner muchas máquinas en modo bridge
>>>> podría agotar las IP   
>>>> Por algún motivo que desconozco, el modo bridge no siempre funciona adecuadamete con wifi

### Red Sólo anfitrion
Se crea una red que contiene al anfitrión y a la máquina virtual nada más. No hay puerta de acceso, aunque puede haber servicio DHCP

## Recomendación VirtualBox y Ubuntu 18

Para simular un VPS y dotarlo de estabilidad:

> Poner dos adaptadores de red a la máquina virtual:
> * Uno conectado a una red NAT, que nos dará acceso a Internet.
> * Otro, conectado a una red sólo anfitrion, que permitirá la comunicación con el anfitrion,
> que es desde donde utilizaremos los clientes.

La red NAT tiene un DCHP que asignará una IP a la máquina y configurará DNS y puerta de enlace a Internet. Está bien la configuración dinámica porque es la que utilizaremos para que la máquina se conecte a internet, pero los clientes de prueba estarán en el anfitrión, no en internet.

En la red del anfitrion, habrá que configurar una IP estática dentro del rango. No hay DHCP ni DNS aquí. Por ejemplo, si nuestra red anfitrion es la 192.168.56.0/24, y el anfitrión se queda con la IP 192.168.56.1/24, entronces al huesped le podemos asignar la 192.168.56.2/24

Ubuntu 18 guarda la configuración permanente de red en un fichero `.yaml` en la carpet `/etc/netplan/`

Configuraremos el adaptador sólo anfitrion, que suele llamarse **enp0s8** con una ip fija del rango. Puedes comprobar los nombres de los adaptadores con el comando `ifconfig -a`, que muestra la información de todos los adaptadores, incluso los que no están activos.

### Edita el fichero de configuración de red:
```
sudo nano /etc/netplan/50-cloud-init.yaml
#ojo: el nombre del fichero podría variar
```

Especifica una configuración fija para el segundo adaptador:
```
network:
    ethernets:
        enp0s3:
            addresses: []
            dhcp4: true
            optional: true
        enp0s8:
            addresses: [192.168.56.2/24]
            dhcp4: no
    version: 2
```

>>> El fichero está en el lenguaje de marcas YAML, en el que la indentación indica el anidamiento.
>>> Debe hacerse con espacios, no tabuladores.

Para aplicar los cambios:
```
sudo netplan apply
```

Asegúrate de que todo está correcto con `ifconfig`

Ahora, probamos la conectividad:
* En el host haz un ping al anfitrion `ping 192.168.56.1`
* En el anfitrion haz un ping al host `ping 192.168.56.2`
