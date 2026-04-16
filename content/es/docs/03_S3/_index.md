+++
title = 'S3'
date = 2024-10-15T07:04:49+02:00
draft = false
icon = "fas fa-store"
weight = 40
description = "Servicio de bukets S3"
+++
## Acceder a los servicios

Dentro de la consola de AWS accedemos a los servicios de **S3**, y seleccinamos crear un bukets

{{<line color="green" width="5px">}}
  ![img.png](img.png)
{{<line color="green" width="5px">}}

Dejamos las opciones por defecto y asignamos un nombre único al bucket, ya que los nombres en S3 son globales y no pueden repetirse en ninguna cuenta de AWS.

En nuestro caso asignamos **2048-aws**

{{<line color="green" width="5px">}}
![img_1.png](img_1.png)
{{<line color="green" width="5px">}}

{{<color>}}Acceso público{{</color>}}

Como vamos a hacer una web estática, dejamos acceso público el cual hay que confirmar

{{<line color="green" width="5px">}}
  ![img_2.png](img_2.png)
{{<line color="green" width="5px">}}
Con estas opciones seleccionamos crear el bukets
{{<line color="green" width="5px">}}
![img_3.png](img_3.png)  
{{<line color="green" width="5px">}}

## Subiendo ficheros
Ahora vamos a subir una web estática que tenemos disponbile en git, que es un sencillo juego de js llamado 2048

Primero lo podemos clonar en local

{{< highlight bash "linenos=inline, hl_lines=, style=emacs" >}}
git clone https://github.com/MAlejandroR/2048.git
{{< /highlight >}}

Ahora dentro del bucket seleccionamos **Cargar**, que es subir ficheros
{{<line color="green" width="5px">}}
  ![img_4.png](img_4.png)
{{<line color="green" width="5px">}}

Dentro de la ventana que nos muestra, tenemos botones para subir ficheros o carpetas

Para poder acceder posteriormente bien al proyecto es mejor subir el contenido no la carpeta entera, esto implica subir por un lado los ficheros, y por otro, cada una de las carpetas

Para proceder a la carga definitiva, hay que realizar la acción indicada

{{<line color="green" width="5px">}}
  ![img_6.png](img_6.png)
{{<line color="green" width="5px">}}

Al final tendremos todo subido
{{<line color="green" width="5px">}}
![img_7.png](img_7.png)
{{<line color="green" width="5px">}}

Para hacerlo una web estática, tenemos que ir a propiedades en el dasboard de este bucket

{{<line color="green" width="5px">}}
  ![img_8.png](img_8.png)
{{<line color="green" width="5px">}}

Justo en la parte inferior de la página tenemos el acceso a **Web Static**, ahí presionamos editar
{{<line color="green" width="5px">}}
![img_9.png](img_9.png)  
{{<line color="green" width="5px">}}

Simplemente habilitamos y especificamos el nombre del index.html y un fichero en el caso de errores
{{<line color="green" width="5px">}}
  ![img_10.png](img_10.png)
{{<line color="green" width="5px">}}

Guardamos cambios

{{<line color="green" width="5px">}}
  ![img_11.png](img_11.png)
{{<line color="green" width="5px">}}

Para terminar tenemos que ir a políticas y especificar unas políticas para este web site
{{<line color="green" width="5px">}}
  ![img_12.png](img_12.png)
{{<line color="green" width="5px">}}

Hay que copiar este fichero json que establece políticas de acceso a este bucket.Debes de especificar el nombre del bucket concreto.En nuestro caso es **2048-aws**, pero modifícalo según sea tu nombre

{{< highlight bash "linenos=inline, hl_lines=, style=emacs" >}}

{{< /highlight >}}


Ahora  en el dashboard del S3, copiamos la url (previo selecionamos el index) y podremos acceder a nuestro bucket en la red

{{<line color="green" width="5px">}}
  ![img_13.png](img_13.png)
{{<line color="green" width="5px">}}