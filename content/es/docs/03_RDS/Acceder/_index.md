+++
title = 'Acceso a RDS'
date = 2024-10-15T07:04:49+02:00
draft = false
icon = "fas fa-server"
weight = 40
description = "Acceder a la bd"
+++
## Acceder a los servicios

Lo primero que necesitamos el el punto de acceso

Para ello vamos a la opción **Conectividad y seguridad** y seleccionamo **puntos de conexion** 

{{<line color="green" width="5px">}}
  ![img.png](img.png)
{{<line color="green" width="5px">}}

En esa ventana buscamos el punto de enlace
{{<line color="green" width="5px">}}
  ![img_1.png](img_1.png)
{{<line color="green" width="5px">}}
Ese es nuestro punto de enlace

{{<color>}}Un docker para conectar{{</color>}}

Creamos un docker asignando directamente esas credenciales

{{< highlight bash "linenos=inline, hl_lines=, style=emacs" >}}
services:
phpmyadmin:
image: phpmyadmin
ports:
- 8100:80
environment:
- PMA_HOST=database-2.cpq8yuuka3jr.us-east-1.rds.amazonaws.com
- PMA_USER=admin
- PMA_PASSWORD=12345678
{{< /highlight >}}

 Ahora lanzamos el docker 
{{< highlight bash "linenos=inline, hl_lines=, style=emacs" >}}
docker compose up -d
{{< /highlight >}}

Podemos abrir el navegador y vemos nuestra base de datos en AWS
{{<line color="green" width="5px">}}
  ![img_2.png](img_2.png)
{{<line color="green" width="5px">}}