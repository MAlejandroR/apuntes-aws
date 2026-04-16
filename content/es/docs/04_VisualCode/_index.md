---
title: "Conexión SSH Visual"
date: 2024-10-15
draft: false
weight: 40
icon: "fas fa-terminal"
description: "Conectar a una instancia EC2 de AWS mediante SSH usando Visual Studio Code"
---

## Conexión por SSH a una instancia EC2 usando Visual Studio Code

### 1. Requisitos previos

- Tener una instancia EC2 creada en AWS
- Disponer del archivo `.pem` (clave privada)
- Conocer la IP pública o DNS de la instancia
- Tener instalado:
    - Visual Studio Code
    - Extensión **Remote - SSH**

---

### 2. Instalar extensión en VS Code

1. Abrir Visual Studio Code
2. Ir a **Extensiones** (Ctrl + Shift + X)
3. Buscar: `Remote - SSH`
4. Instalar la extensión de Microsoft

---

### 3. Preparar la clave `.pem`


{{< highlight "style=emacs">}}
    chmod 400 mi-clave.pem
{{< /highlight >}}

---

### 4. Configurar el fichero SSH

Ruta del fichero:

{{< highlight "style=emacs">}}
    ~/.ssh/config
{{< /highlight >}}

Configuración:

{{< highlight "style=emacs">}}
    Host mi-ec2
        HostName IP_PUBLICA_O_DNS
        User ubuntu
        IdentityFile /ruta/a/mi-clave.pem
{{< /highlight >}}

Ejemplo:

{{< highlight "style=emacs">}}
Host mi-ec2
    HostName ec2-54-210-124-155.compute-1.amazonaws.com
    User ubuntu
    IdentityFile ~/.ssh/mi-clave.pem
{{< /highlight >}}

---

### 5. Conectarse desde VS Code

1. Abrir la paleta de comandos (`Ctrl + Shift + P`)
2. Ejecutar:
    - `Remote-SSH: Connect to Host`
3. Seleccionar:
    - `mi-ec2`

---

### 6. Primera conexión

- VS Code instalará el servidor remoto automáticamente
- Aceptar el fingerprint si lo solicita
- Esperar unos segundos

---

### 7. Trabajar en la instancia

- Abrir carpeta remota:

{{< highlight "style=emacs">}}
    /var/www/html/laravel_aws
{{< /highlight >}}

- Editar archivos directamente
- Usar terminal integrada

---

### 8. Problemas comunes

#### Permisos de la clave

{{< highlight bash >}}
chmod 400 mi-clave.pem
{{< /highlight >}}

#### Error de conexión

- Verificar IP pública
- Verificar Security Group (puerto 22 abierto)

#### Usuario incorrecto

- Ubuntu → `ubuntu`
- Amazon Linux → `ec2-user`

---

### 9. Comprobación manual

{{< highlight "style=emacs">}}
    ssh -i mi-clave.pem ubuntu@IP_PUBLICA
{{< /highlight >}}

---

### 10. Recomendación

Guardar la configuración en `~/.ssh/config` permite reutilizar conexiones fácilmente y simplifica el acceso desde Visual Studio Code.