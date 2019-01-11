---
title: nslookup
taxonomy:
    category: docs
visible: true
---

El comando **nslookup** nos mete en la utilidad de consulta de dns del sistema operativo.

Por defecto, utiliza el DNS primario configurado en la máquina. Se puede cambiar
```shell
server 8.8.8.8
```

Por defecto, las consultas devuelven al menos una dirección IP (tipo **A**) asociadas al nombre, junto con la información acerca de si la respuesta ha sido autoritativa (proviene del dns autoritativo) o no (proviene de un caché).

```shell
> iesjovellanos.org
Servidor:  google-public-dns-a.google.com
Address:  8.8.8.8

Respuesta no autoritativa:
Nombre:  iesjovellanos.org
Address:  92.48.108.120
```

Si se requiere otro tipo de respuesta, se suele especificar `set type=ANY` para devolver toda la información asociada al nombre, o bien u determinado tipo, por ejemplo `set type=MX`
```shell
> set type=ANY
> iesjovellanos.org
Servidor:  google-public-dns-a.google.com
Address:  8.8.8.8

Respuesta no autoritativa:
iesjovellanos.org       MX preference = 10, mail exchanger = ASPMX.L.GOOGLE.COM
iesjovellanos.org       MX preference = 15, mail exchanger = ALT1.ASPMX.L.GOOGLE.COM
iesjovellanos.org       MX preference = 20, mail exchanger = ALT2.ASPMX.L.GOOGLE.COM
iesjovellanos.org       MX preference = 25, mail exchanger = ASPMX2.GOOGLEMAIL.COM
iesjovellanos.org       internet address = 92.48.108.120
iesjovellanos.org
        primary name server = ns2.iesjovellanos.org
        responsible mail addr = ismael.iesjovellanos.org
        serial  = 1486374758
        refresh = 10800 (3 hours)
        retry   = 3600 (1 hour)
        expire  = 604800 (7 days)
        default TTL = 10800 (3 hours)
iesjovellanos.org       nameserver = ns1.iesjovellanos.org
iesjovellanos.org       nameserver = ns2.iesjovellanos.org
```

Para salir `exit`.
