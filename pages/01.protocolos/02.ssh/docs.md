---
title: SSH
taxonomy:
    category: docs
visible: true
---

[TOC] 
Protocolo de terminal remoto seguro con **cifrado** en la comunicación entre cliente y servidor
y autentificación mediante claves criptofráficas asimétricas opcional.

Se desarrolló como reemplazo de _telnet_, el protocolo de terminal remoto tradicional de unix, sin cifrado y muy vulnerable.

* Significado: Secure SHell
* Nivel: aplicación
* Puerto: **22 TCP**
* Versión actual: 2. Año 2006. Estándar IETF [RFC4253](https://tools.ietf.org/html/rfc4253). 
* Primera versión de 1995 por _Tatu Ylönen_, Universidad Politécnica de Helsinki.
![Tatu Ylönen](https://www.ssh.com/s/tatu-ylonen-300x300-JMhKzl5L.jpg) (Tatu Ylönen, Finlandia, 1968) 

## software
### servidores
El servidor más común es **OpenSSH**, un fork del original de Tatu Ylönen, que forma parte del sistema operativo BSD.

* Instalar e iniciar servicio SSH con OpenSSH server: `apt-get install openssh-server` 
* El fichero de configuración del servidor se encuentra en: `/etc/ssh/sshd_config`, y cada usuario puede tener configuración adicional sólo para él dentro de una carpeta `.ssh` en su home
#### Manejar el servicio
```
service sshd OPTION
```
> Donde OPTION es:
> * **status** comprueba el estado del servicio
> * **restart** lo reinicia
> * **reload** carga de nuevo la configuración sin parar el servicio
> * **stop** para el servicio
> * **start** arranca el servicio

Esta misma sintaxis puede usarse para otros servicios, de tipo _Unix System V init_ (Como apache2 y proftpd), que instalan scripts en /etc/init.d

#### usar root en ubuntu
Por defecto, el accesso por ssh al usuario root está desactivado. Se maneja todo a través del usuario que especificamos
durante la instalación, que podrá hacer **sudo**. Vamos a habilitar root, al estilo de como lo hacen los VPS.  

Primero cambiamos el usuario a root.
```
sudo su
```

Ahora somos root, y asignamos una contraseña.
```
passwd
```

Ahora ya se puede acceder localmente, pero quizá no por SSH. Edita el fichero de configuración de ssh `/etc/ssh/sshd_config`.
Busca una línea con la directiva `PermitRootLogin` y cambiala por `Yes`. Si la línea no existe, añadela al fichero.
```
PermitRootLogin yes
```

Reinicia el servicio SSH
```
service sshd restart
```

### clientes
En linux, disponemos de un cliente de texto desarrollado para OpenSSH, que se instala con `apt install openssh-client`  
En windows, podemos obtener el cliente de OpenSSH de terceros. Por ejemplo, con la instalación del gestor de versiones [git](https://git-scm.com/)  
También para windows es muy popular el entorno de [putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html), un cliente con entorno gráfico muy compacto y portable.

