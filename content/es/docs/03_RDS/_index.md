+++
title = 'RDS Bases de datos'
date = 2024-10-15T07:04:49+02:00
draft = false
icon = "fas fa-database"
weight = 40
description = "Crear servicios de BD"
+++
## Acceder a los servicios

Dentro de la consola de AWS accedemos a los servicios de **bases de datos** y seleccionamos **Amazon RDS**.

{{< line color="green" width="5px" >}}
![Acceso a RDS](img.png)
{{< line color="green" width="5px" >}}

Accederemos al **panel de control (dashboard)** del servicio.

---



## Crear una base de datos

Tenemos diferentes tipos de bases de datos.

Vamos a trabajar con bases de datos relacionales que son las que manejamos habitualmente

En el menú lateral, seleccionamos **Bases de datos** y pulsamos el botón **Crear base de datos**.

{{< line color="green" width="5px" >}}
![Crear base de datos](img_1.png)
{{< line color="green" width="5px" >}}

Seleccionamos la opción Base de datos y apretamos el botón **crear base de datos** seleccinando **configuración completa**
{{<line color="green" width="5px">}}
![img_2.png](img_2.png)  
{{<line color="green" width="5px">}}


### Configuración del servicio
Ahora vamos a ir viendo y entendiendo las diferentes opciones que se presentas


A diferencia de las instancias EC2 dónde selecinamos un AMI, aquí seleccionamos el motor de la base de datos que vamos a utilizar.
Lo primero seleccionamos lo que se llama el **sabor** o el motor de la base de datos que queremos utilizar

En nuestro caso seleccionaremos **MySQL**
{{<line color="green" width="5px">}}
![img_3.png](img_3.png)
{{<line color="green" width="5px">}}



{{<color>}}Opciones de configuración {{</color>}}

Seleccionamos en la siguiente opción una configuracion completa y en modo de pruebas y así veremos diferentes opciones.
Seleccionamos modo de de pruebas, que implica que no habrá replicacion y por lo tanto será mucho más económico (se puede ver gráficamente en la imagen que le acompaña)
{{<line color="green" width="5px">}}
![img_4.png](img_4.png)
{{<line color="green" width="5px">}}

{{<color>}}Usario y contraseña{{</color>}}

Las siguientes opciones son muy importantes, ya que van a permitir acceder a la base de datos.

En ella especificaremos el usuario, que por defecto indican **admin** y la password, dándonos diferentes opciones para generarla

En nuestro caso vamos a poner **12345678** por comodidad y ya que la base de datos no se va a quedar en ejecución mucho tiempo (es una práctica de laboratorio)
{{<line color="green" width="5px">}}
![img_5.png](img_5.png)  
{{<line color="green" width="5px">}}

No es lo más habitual, pero ahora vamos a dar acceso públic a esta base de datos para poder acceder a ella

{{<line color="green" width="5px">}}
  ![img_9.png](img_9.png)
{{<line color="green" width="5px">}}
El resto de opciones las dejamos por defecto y vamos a **Configuración adicional**  donde podemos seleccionar el nombre de la base de datos
{{<line color="green" width="5px">}}
![img_6.png](img_6.png)  
{{<line color="green" width="5px">}}

Ya podemos dar a crear **la base de datos**, acción que puede tardar entre 2 y 4 minutos
{{<line color="green" width="5px">}}
  ![img_7.png](img_7.png)
{{<line color="green" width="5px">}}

Vemos que la instancia se está creando
{{<line color="green" width="5px">}}
  ![img_8.png](img_8.png)
{{<line color="green" width="5px">}}