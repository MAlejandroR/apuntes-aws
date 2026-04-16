+++
title = 'Instalaciones en  EC2'
date = 2024-10-15T07:04:49+02:00
draft = false
weight = 20
icon= "fas fa-cogs"
description = "Trabajar con la EC2"
+++


{{< objetivos >}}
Conectarse
Configurar nuestro sistema
Desplegar un proyecto laravel
Compartir ficheros entre la EC2 y nuestro equipo (fillezilla, phptorm o viusal code)
{{</objetivos>}}
---
## Accedemos a la máquina

Verificamos en la consola de AWS que nuestra instancia está disponible.

Para ello, volvemos al servicio EC2 y accedemos al listado de instancias (la página **dashboard** de instancias:

{{<line color="green" width="5px">}}
![img_16.png](../img_16.png)
{{<line color="green" width="5px">}}

---

En el panel de instancias podemos ver **todas las instancias creadas** y **su estado** actual.

{{<line color="green" width="5px">}}
![img.png](img.png)
{{<line color="green" width="5px">}}

---

Seleccionamos la instancia para ver su información detallada:

{{<line color="green" width="5px">}}
![img_1.png](images/img_1.png)
{{<line color="green" width="5px">}}

---

Desde aquí podemos consultar datos importantes como:

- Dirección IP pública
- Dirección IP privada
- Estado de la instancia
- Tipo de instancia
- Zona de disponibilidad

También podemos acceder a todos los detalles haciendo clic sobre la instancia.

{{<line color="green" width="5px">}}
![img_1.png](img_1.png)
{{<line color="green" width="5px">}}

---

{{<color>}}Estados de una instancia{{</color>}}

Una instancia EC2 puede estar en diferentes estados:

- **pending** → iniciándose
- **running** → en ejecución
- **stopping / stopped** → detenida
- **shutting-down / terminated** → eliminándose / eliminada

 Importante:

- Una instancia **stopped** se puede volver a iniciar
- Una instancia **terminated** no se puede recuperar

Cuando eliminamos una instancia, puede seguir apareciendo durante un tiempo en el listado hasta que AWS la elimina completamente.
## Conexión por ssh

Para conectar a la instancia lo vamos a hacer por **SSH**. Podremos conectar desde _una máquina Linux o una máquina Windows._

Vamos a conectar de varias formas:
* Consola
* Desde un IDE (PhpStorm o Visual Studio Code)
* Desde un cliente FTP (FileZilla)

---

Necesitamos para conectar disponer de la **clave privada** de la pareja de claves con los permisos correctos.

Descargamos el fichero de clave privada desde la plataforma (botón **AWS Details**) y lo guardamos en un directorio local.

{{<line color="green" width="5px">}}
![AWS_Details_select.png](images/AWS_Details_select.png)
{{<line color="green" width="5px">}}

{{<line color="green" width="5px">}}
![ventana_PPK_PEM.png](images/ventana_PPK_PEM.png)
{{<line color="green" width="5px">}}

---

Vemos dos tipos de claves privadas, nosotros utilizaremos **PEM**:

- **PEM (Privacy-Enhanced Mail)**  
  Formato estándar de clave privada usado en Linux/Mac para conectarse por SSH (ej. EC2).

- **PPK (PuTTY Private Key)**  
  Formato de clave privada específico de PuTTY (Windows), equivalente al PEM.

---

Descargamos el fichero y cambiamos los permisos.

> * {{<color>}}En Linux{{</color>}}

{{< highlight bash "linenos=inline, hl_lines=, style=emacs" >}}
    chmod 400 labsuser.pem

{{< /highlight >}}

---

> * {{<color>}}En Windows{{</color>}}

Para que la clave funcione correctamente en Windows, debemos restringir los permisos del fichero:

- Clic derecho sobre el fichero `.pem`
- **Propiedades**
- Pestaña **Seguridad**
- Pulsar en **Opciones avanzadas**
- Pulsar en **Deshabilitar herencia**
- Elegir **Quitar todos los permisos heredados**
- Pulsar en **Agregar**
- Seleccionar tu usuario
- Dar permisos de **Lectura**
- Eliminar cualquier otro usuario/grupo si aparece

---

{{<color>}}Establecemos la conexión{{</color>}}

Localizamos la IP pública para poder conectar:

{{<line color="green" width="5px">}}
![img_2.png](images/img_2.png)
{{<line color="green" width="5px">}}

---

Tanto en Windows como en Linux vamos a conectar por SSH (en Windows también se puede usar PuTTY).

En Windows abrimos una **PowerShell**.

El usuario que se crea en este tipo de instancias (Ubuntu) es **ubuntu**, y lo especificaremos en la conexión.

Si tenemos dudas, podemos verlo en el botón **Connect** de la instancia.

En general, los usuarios por defecto son:

| AMI            | Usuario   |
|----------------|----------|
| Ubuntu         | ubuntu   |
| Amazon Linux   | ec2-user |
| Debian         | admin    |
| CentOS         | centos   |
| RHEL           | ec2-user |
| SUSE           | ec2-user |

---
{{< highlight bash "linenos=inline, hl_lines=, style=emacs" >}}
ssh -i labsuser.pem ubuntu@100.48.89.140

{{< /highlight >}}

---

Nos preguntará si queremos continuar con la conexión:

{{<line color="green" width="5px">}}
![img_2.png](images/fingerprint_question.png)
{{<line color="green" width="5px">}}

---

Escribimos **yes** y se establecerá la conexión:

{{<line color="green" width="5px">}}
![Mensaje conexión ssh ok](images/conexion_ssh_ok.png)
{{<line color="green" width="5px">}}

## Instalación de todo el sistema

Ahora vamos a proceder a la instalación de las librerías necesarias para nuestro objetivo.

Primero actualizamos los repositorios de paquetes:

{{< highlight bash "style=emacs" >}}
sudo apt update
{{< /highlight >}}

---

* {{<color>}}php y apache2{{</color>}}

{{< highlight bash "style=emacs" >}}
sudo apt install -y php apache2 libapache2-mod-php
{{< /highlight >}}

---

* {{<color>}}Librerías necesarias para nuestro proyecto de laravel{{</color>}}

{{< highlight bash "style=emacs" >}}
sudo apt install -y php-mbstring php-xml php-zip php-sqlite3 php-curl php-mysql
{{< /highlight >}}

---

* {{<color>}}composer{{</color>}}

Para instalar composer tenemos diferentes opciones. En este caso vamos a descargar el instalador, ejecutarlo con PHP y copiar el ejecutable generado a una carpeta que está en el PATH del sistema con el nombre **composer**.

{{< highlight bash "style=emacs" >}}
curl "https://getcomposer.org/installer" -o composer.phar
sudo php composer.phar --install-dir=/usr/local/bin --filename=composer
{{< /highlight >}}

Tras la instalación podemos verificar la versión (se instalará la última disponible):

{{< highlight bash "style=emacs" >}}
composer --version
{{< /highlight >}}

{{<line color="green" width="5px">}}
![Ver versión de composer](images/composer_version.png)
{{<line color="green" width="5px">}}

---

* {{<color>}}node y npm{{</color>}}

En este caso procederemos de forma similar, descargando el script de configuración e instalando Node.js.

{{< highlight bash "style=emacs" >}}
curl "https://deb.nodesource.com/setup_22.x" -o node.sh
sudo -E bash ./node.sh
sudo apt install -y nodejs
{{< /highlight >}}

Igualmente que en el caso anterior, tras la instalación deberemos verificarlo:

{{< highlight bash "style=emacs" >}}
node -v
npm -v
{{< /highlight >}}

{{<line color="green" width="5px">}}
![Ver versión de node y de npm](images/node_npm_version.png)
{{<line color="green" width="5px">}}

---

{{<color>}}Preparar el document root para copiar el proyecto de laravel{{</color>}}

Ahora queremos copiar el proyecto de Laravel en la carpeta **/var/www/html**, para lo cual necesitamos permisos de escritura en esa carpeta.

Actualmente esta carpeta es propiedad de **root**, ya que se ha creado durante la instalación de Apache (que hemos hecho con **sudo**).

{{< highlight bash "style=emacs" >}}
sudo chown -R ubuntu:www-data /var/www/html
{{< /highlight >}}

Podemos ver la evolución de propietarios en la siguiente imagen:

{{<line color="green" width="5px">}}
![propietario carpetas /var/www](images/permisos_var_www.png)  
{{<line color="green" width="5px">}}

---

{{<color>}}Clonamos el proyecto de laravel{{</color>}}<br />

{{< highlight bash "style=emacs" >}}
cd /var/www/html
git clone https://github.com/MAlejandroR/laravel_aws.git
{{< /highlight >}}

Esto nos descargará el proyecto en la carpeta **laravel_aws**, teniendo el directorio:

```text
/var/www/html/laravel_aws



