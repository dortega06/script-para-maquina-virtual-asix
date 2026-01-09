---
title: "Práctica: Instalación de Nextcloud en Ubuntu Server 22.04 con VirtualBox"
author: "Práctica ASIX - Administración de Sistemas Informáticos en Xarxa"
date: "Curso 2024-2025"
geometry: margin=2.5cm
fontsize: 11pt
lang: es-ES
toc: true
toc-depth: 3
numbersections: true
header-includes:
  - \usepackage{fancyhdr}
  - \usepackage{graphicx}
  - \pagestyle{fancy}
  - \fancyhead[L]{Práctica Nextcloud}
  - \fancyhead[R]{ASIX}
  - \fancyfoot[C]{\thepage}
---

\newpage

# Introducción

## Objetivo de la práctica

El objetivo de esta práctica es aprender a instalar y configurar un servidor de almacenamiento en la nube (cloud personal) utilizando **Nextcloud** sobre **Ubuntu Server 22.04 LTS** en una máquina virtual creada con **VirtualBox**.

Al finalizar esta práctica, habrás configurado un servidor cloud completamente funcional que podrás utilizar para almacenar archivos, sincronizar datos entre dispositivos y compartir información de forma segura.

## ¿Qué es Nextcloud?

Nextcloud es una plataforma de código abierto para crear y gestionar tu propio servicio de almacenamiento en la nube. Ofrece funcionalidades similares a servicios comerciales como Google Drive o Dropbox, pero con la ventaja de que tienes control total sobre tus datos.

## Requisitos previos

- **VirtualBox** instalado en tu equipo (versión 6.0 o superior)
- **Ubuntu Server 22.04 LTS** ISO descargada (disponible en ubuntu.com)
- Al menos **4 GB de RAM** disponibles en el equipo anfitrión
- Al menos **20 GB** de espacio en disco
- Conexión a Internet

## Entregables

Al finalizar la práctica, deberás entregar un **documento PDF** que incluya:

1. **Capturas de pantalla** de cada paso indicado en esta guía
2. **Breve descripción** de lo realizado en cada paso
3. **Reflexión final** respondiendo a las siguientes preguntas:
   - ¿Qué ventajas tiene montar tu propio cloud frente a usar uno comercial?
   - ¿Qué problemas has tenido durante la práctica y cómo los has resuelto?
   - ¿Qué mejorarías si tuvieras más tiempo?

\newpage

# Parte 1: Creación de la Máquina Virtual en VirtualBox

## Paso 1.1: Crear una nueva máquina virtual

1. Abre **VirtualBox**
2. Haz clic en el botón **"Nueva"** o **"New"**
3. Configura los siguientes parámetros:
   - **Nombre**: `Nextcloud-Ubuntu-Server`
   - **Carpeta de la máquina**: Deja la ruta por defecto o elige una personalizada
   - **Tipo**: `Linux`
   - **Versión**: `Ubuntu (64-bit)`

**[CAPTURA] CAPTURA 1**: Pantalla de creación de nueva máquina virtual con los datos introducidos.

4. Haz clic en **"Siguiente"**

## Paso 1.2: Asignar memoria RAM

1. Asigna **2048 MB (2 GB)** de memoria RAM para la máquina virtual
   - Puedes asignar más si tu equipo lo permite (recomendado 4 GB)

**[CAPTURA] CAPTURA 2**: Pantalla de asignación de memoria RAM.

2. Haz clic en **"Siguiente"**

## Paso 1.3: Crear un disco duro virtual

1. Selecciona **"Crear un disco duro virtual ahora"**
2. Haz clic en **"Crear"**
3. Tipo de archivo de disco duro: **VDI (VirtualBox Disk Image)**
4. Haz clic en **"Siguiente"**
5. Almacenamiento en disco duro físico: **"Reservado dinámicamente"**
6. Haz clic en **"Siguiente"**
7. Tamaño del disco: **20 GB** (o más si dispones de espacio)

**[CAPTURA] CAPTURA 3**: Configuración del disco duro virtual mostrando el tamaño asignado.

8. Haz clic en **"Crear"**

## Paso 1.4: Configurar la red

1. Selecciona la máquina virtual creada
2. Haz clic en **"Configuración"** o **"Settings"**
3. Ve a la sección **"Red"** o **"Network"**
4. En **"Adaptador 1"**:
   - Marca la casilla **"Habilitar adaptador de red"**
   - **Conectado a**: Selecciona **"Adaptador puente"** o **"Bridged Adapter"**
   - Esto permitirá que la VM tenga su propia IP en tu red local

**[CAPTURA] CAPTURA 4**: Configuración de red mostrando el adaptador puente.

5. Haz clic en **"Aceptar"**

## Paso 1.5: Montar la ISO de Ubuntu Server

1. Con la máquina virtual seleccionada, haz clic en **"Configuración"**
2. Ve a la sección **"Almacenamiento"** o **"Storage"**
3. En **"Dispositivos de almacenamiento"**, selecciona el icono del CD (disco vacío)
4. En el lado derecho, haz clic en el icono del CD junto a **"Unidad óptica"**
5. Selecciona **"Elegir/Crear disco virtual"**
6. Busca y selecciona el archivo ISO de **Ubuntu Server 22.04 LTS**

**[CAPTURA] CAPTURA 5**: Configuración de almacenamiento con la ISO montada.

7. Haz clic en **"Aceptar"**

\newpage

# Parte 2: Instalación de Ubuntu Server 22.04

## Paso 2.1: Iniciar la instalación

1. Selecciona la máquina virtual **"Nextcloud-Ubuntu-Server"**
2. Haz clic en **"Iniciar"** o **"Start"**
3. La máquina virtual arrancará desde la ISO de Ubuntu Server

**[CAPTURA] CAPTURA 6**: Pantalla de arranque inicial de Ubuntu Server.

4. Selecciona el idioma: **English** (recomendado para evitar problemas de compatibilidad)
5. Presiona **Enter**

## Paso 2.2: Seleccionar distribución de teclado

1. En la pantalla de configuración de teclado:
   - **Layout**: Selecciona **Spanish** o el idioma de tu teclado
   - **Variant**: Selecciona la variante apropiada

**[CAPTURA] CAPTURA 7**: Configuración de distribución del teclado.

2. Navega hasta **"Done"** y presiona **Enter**

## Paso 2.3: Tipo de instalación

1. En **"Choose type of install"**, selecciona:
   - **Ubuntu Server** (opción por defecto)

**[CAPTURA] CAPTURA 8**: Selección del tipo de instalación.

2. Navega hasta **"Done"** y presiona **Enter**

## Paso 2.4: Configuración de red

1. El instalador detectará automáticamente la interfaz de red
2. Debería mostrar una dirección IP asignada por DHCP
3. **Anota esta dirección IP**, la necesitarás más adelante

**[CAPTURA] CAPTURA 9**: Configuración de red mostrando la IP asignada.

4. Navega hasta **"Done"** y presiona **Enter**

## Paso 2.5: Configurar proxy

1. Si no usas proxy, deja el campo vacío
2. Navega hasta **"Done"** y presiona **Enter**

**[CAPTURA] CAPTURA 10**: Pantalla de configuración de proxy (puede dejarse vacío).

## Paso 2.6: Configurar mirror de Ubuntu

1. Deja la URL por defecto del mirror de Ubuntu
2. Navega hasta **"Done"** y presiona **Enter**

## Paso 2.7: Configuración del disco

1. En **"Storage configuration"**, selecciona:
   - **Use an entire disk** (usar todo el disco)
   - Selecciona el disco virtual que creaste (debería aparecer uno solo)

**[CAPTURA] CAPTURA 11**: Configuración del almacenamiento mostrando el disco seleccionado.

2. Navega hasta **"Done"** y presiona **Enter**
3. En la pantalla de confirmación del esquema de particiones:
   - Revisa que todo esté correcto

**[CAPTURA] CAPTURA 12**: Resumen del esquema de particiones antes de confirmar.

4. Navega hasta **"Done"** y presiona **Enter**
5. Confirma la acción destructiva escribiendo **"Continue"** y presionando **Enter**

## Paso 2.8: Configuración de perfil de usuario

1. Completa la información del perfil:
   - **Your name**: Tu nombre (ej: `Alumno ASIX`)
   - **Your server's name**: `nextcloud-server`
   - **Pick a username**: `admin` o tu nombre de usuario preferido
   - **Choose a password**: Una contraseña segura (¡anótala!)
   - **Confirm your password**: Repite la contraseña

**[CAPTURA] CAPTURA 13**: Configuración del perfil de usuario con todos los campos completados.

2. Navega hasta **"Done"** y presiona **Enter**

## Paso 2.9: Configuración de SSH

1. En **"SSH Setup"**:
   - Marca la opción **"Install OpenSSH server"** usando la barra espaciadora
   - Esto te permitirá conectarte remotamente al servidor

**[CAPTURA] CAPTURA 14**: Pantalla de instalación de OpenSSH server marcada.

2. No importes ninguna identidad SSH (deja vacío)
3. Navega hasta **"Done"** y presiona **Enter**

## Paso 2.10: Server Snaps (opcional)

1. En esta pantalla puedes seleccionar snaps predefinidos
2. **No selecciones ninguno** por ahora, instalaremos todo manualmente

**[CAPTURA] CAPTURA 15**: Pantalla de Server Snaps (sin seleccionar ninguno).

3. Navega hasta **"Done"** y presiona **Enter**

## Paso 2.11: Completar la instalación

1. El sistema comenzará a instalar Ubuntu Server
2. Este proceso puede tardar entre 5 y 15 minutos

**[CAPTURA] CAPTURA 16**: Pantalla mostrando el progreso de la instalación.

3. Cuando aparezca el mensaje **"Install complete!"**:

**[CAPTURA] CAPTURA 17**: Pantalla indicando que la instalación se ha completado.

4. Navega hasta **"Reboot Now"** y presiona **Enter**
5. Si aparece el mensaje "Please remove the installation medium", presiona **Enter**
   - VirtualBox debería desmontar automáticamente la ISO

## Paso 2.12: Primer inicio de sesión

1. Después del reinicio, verás la pantalla de login
2. Introduce tu **nombre de usuario** y presiona **Enter**
3. Introduce tu **contraseña** y presiona **Enter**

**[CAPTURA] CAPTURA 18**: Terminal después del primer inicio de sesión exitoso.

\newpage

# Parte 3: Preparación del Sistema

## Paso 3.1: Actualizar el sistema

Es fundamental mantener el sistema actualizado para tener los últimos parches de seguridad.

1. Ejecuta los siguientes comandos:

```bash
sudo apt update
```

**[CAPTURA] CAPTURA 19**: Salida del comando `apt update`.

```bash
sudo apt upgrade -y
```

Este comando actualizará todos los paquetes instalados. Puede tardar varios minutos.

**[CAPTURA] CAPTURA 20**: Proceso de actualización de paquetes en ejecución.

2. Una vez finalizado, reinicia el sistema:

```bash
sudo reboot
```

3. Vuelve a iniciar sesión después del reinicio

## Paso 3.2: Verificar la dirección IP

1. Verifica la dirección IP del servidor:

```bash
ip addr show
```

o alternativamente:

```bash
hostname -I
```

**[CAPTURA] CAPTURA 21**: Salida mostrando la dirección IP del servidor.

**Anota esta IP**, la necesitarás para acceder a Nextcloud desde tu navegador.

\newpage

# Parte 4: Instalación de Apache, MySQL y PHP (LAMP Stack)

## Paso 4.1: Instalar Apache

Apache es el servidor web que alojará Nextcloud.

1. Instala Apache:

```bash
sudo apt install apache2 -y
```

**[CAPTURA] CAPTURA 22**: Instalación de Apache en proceso.

2. Verifica que Apache esté funcionando:

```bash
sudo systemctl status apache2
```

**[CAPTURA] CAPTURA 23**: Estado de Apache mostrando "active (running)".

3. Puedes probar Apache desde tu navegador:
   - Abre un navegador en tu equipo anfitrión
   - Accede a `http://[IP_DE_TU_SERVIDOR]`
   - Deberías ver la página por defecto de Apache

**[CAPTURA] CAPTURA 24**: Página de bienvenida de Apache desde el navegador del anfitrión.

## Paso 4.2: Instalar MySQL/MariaDB

MariaDB es el sistema de gestión de bases de datos que usará Nextcloud.

1. Instala MariaDB:

```bash
sudo apt install mariadb-server -y
```

**[CAPTURA] CAPTURA 25**: Instalación de MariaDB.

2. Verifica que MariaDB esté funcionando:

```bash
sudo systemctl status mariadb
```

**[CAPTURA] CAPTURA 26**: Estado de MariaDB mostrando "active (running)".

3. Ejecuta el script de seguridad:

```bash
sudo mysql_secure_installation
```

Responde a las preguntas como sigue:

- **Enter current password for root**: Presiona **Enter** (no hay contraseña por defecto)
- **Switch to unix_socket authentication**: **n** (No)
- **Change the root password?**: **Y** (Sí)
  - Introduce una contraseña segura (¡anótala!)
  - Confirma la contraseña
- **Remove anonymous users?**: **Y** (Sí)
- **Disallow root login remotely?**: **Y** (Sí)
- **Remove test database?**: **Y** (Sí)
- **Reload privilege tables now?**: **Y** (Sí)

**[CAPTURA] CAPTURA 27**: Ejecución del script mysql_secure_installation.

## Paso 4.3: Crear base de datos para Nextcloud

1. Accede a la consola de MySQL:

```bash
sudo mysql -u root -p
```

Introduce la contraseña de root de MySQL que configuraste.

2. Ejecuta los siguientes comandos SQL (uno por uno):

```sql
CREATE DATABASE nextcloud;
```

```sql
CREATE USER 'nextclouduser'@'localhost' IDENTIFIED BY 'Nextcl0ud2024!';
```

**Nota**: Cambia `'Nextcl0ud2024!'` por una contraseña fuerte de tu elección que incluya mayúsculas, minúsculas, números y símbolos (¡anótala!).

```sql
GRANT ALL PRIVILEGES ON nextcloud.* TO 'nextclouduser'@'localhost';
```

```sql
FLUSH PRIVILEGES;
```

```sql
EXIT;
```

**[CAPTURA] CAPTURA 28**: Comandos SQL ejecutados para crear la base de datos de Nextcloud.

## Paso 4.4: Instalar PHP y módulos necesarios

Nextcloud requiere PHP y varios módulos específicos.

1. Instala PHP y los módulos necesarios:

```bash
sudo apt install php php-mysql php-gd php-curl php-mbstring \
php-intl php-gmp php-bcmath php-xml php-imagick php-zip \
php-bz2 php-apcu libapache2-mod-php -y
```

Este comando puede tardar un poco.

**[CAPTURA] CAPTURA 29**: Instalación de PHP y módulos en proceso.

2. Verifica la versión de PHP instalada:

```bash
php -v
```

**[CAPTURA] CAPTURA 30**: Versión de PHP instalada.

3. Configura PHP para Nextcloud:

Edita el archivo de configuración de PHP. Primero, verifica la versión instalada:

```bash
ls /etc/php/
```

Luego edita el archivo usando la versión correcta (ejemplo con 8.1):

```bash
sudo nano /etc/php/8.1/apache2/php.ini
```

**Nota**: Reemplaza `8.1` con la versión que aparece en tu sistema (puede ser 8.1, 8.2, 8.3, etc.).

4. Busca y modifica las siguientes líneas (usa `Ctrl+W` para buscar):

```ini
memory_limit = 512M           ; Permite operaciones con archivos grandes
upload_max_filesize = 500M    ; Tamaño máximo de archivos individuales
post_max_size = 500M          ; Tamaño máximo de datos POST
max_execution_time = 300      ; Evita timeouts en subidas grandes
```

**[CAPTURA] CAPTURA 31**: Archivo php.ini abierto con los parámetros modificados.

5. Guarda los cambios:
   - Presiona `Ctrl+O` para guardar
   - Presiona `Enter` para confirmar
   - Presiona `Ctrl+X` para salir

6. Reinicia Apache para aplicar los cambios:

```bash
sudo systemctl restart apache2
```

\newpage

# Parte 5: Descarga e Instalación de Nextcloud

## Paso 5.1: Descargar Nextcloud

1. Ve al directorio temporal:

```bash
cd /tmp
```

2. Descarga la última versión de Nextcloud:

```bash
wget https://download.nextcloud.com/server/releases/latest.zip
```

**[CAPTURA] CAPTURA 32**: Descarga de Nextcloud en progreso.

3. Instala unzip si no está instalado:

```bash
sudo apt install unzip -y
```

4. Descomprime el archivo:

```bash
unzip latest.zip
```

**[CAPTURA] CAPTURA 33**: Descompresión del archivo de Nextcloud.

## Paso 5.2: Mover Nextcloud al directorio web

1. Mueve la carpeta de Nextcloud al directorio de Apache:

```bash
sudo mv nextcloud /var/www/html/
```

2. Cambia el propietario de los archivos:

```bash
sudo chown -R www-data:www-data /var/www/html/nextcloud
```

3. Establece los permisos correctos:

```bash
sudo chmod -R 755 /var/www/html/nextcloud
```

**[CAPTURA] CAPTURA 34**: Comandos de movimiento y cambio de permisos ejecutados.

## Paso 5.3: Configurar Apache para Nextcloud

1. Crea un archivo de configuración para Nextcloud:

```bash
sudo nano /etc/apache2/sites-available/nextcloud.conf
```

2. Añade el siguiente contenido:

```apache
<VirtualHost *:80>
    DocumentRoot /var/www/html/nextcloud
    ServerName nextcloud.local

    <Directory /var/www/html/nextcloud/>
        Options +FollowSymlinks
        AllowOverride All
        Require all granted
        
        <IfModule mod_dav.c>
            Dav off
        </IfModule>
        
        SetEnv HOME /var/www/html/nextcloud
        SetEnv HTTP_HOME /var/www/html/nextcloud
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/nextcloud-error.log
    CustomLog ${APACHE_LOG_DIR}/nextcloud-access.log combined
</VirtualHost>
```

**[CAPTURA] CAPTURA 35**: Archivo de configuración de Apache para Nextcloud.

3. Guarda y cierra el archivo (`Ctrl+O`, `Enter`, `Ctrl+X`)

4. Habilita el sitio y los módulos necesarios de Apache:

```bash
sudo a2ensite nextcloud.conf
```

```bash
sudo a2enmod rewrite headers env dir mime
```

**[CAPTURA] CAPTURA 36**: Habilitación del sitio y módulos de Apache.

5. Deshabilita el sitio por defecto de Apache (opcional pero recomendado):

```bash
sudo a2dissite 000-default.conf
```

6. Verifica la configuración de Apache:

```bash
sudo apache2ctl configtest
```

Debería mostrar "Syntax OK".

**[CAPTURA] CAPTURA 37**: Verificación de la configuración de Apache.

7. Reinicia Apache:

```bash
sudo systemctl restart apache2
```

\newpage

# Parte 6: Configuración Web de Nextcloud

## Paso 6.1: Acceder al asistente de instalación

1. Desde tu navegador en el equipo anfitrión, accede a:

```
http://[IP_DE_TU_SERVIDOR]/nextcloud
```

o simplemente:

```
http://[IP_DE_TU_SERVIDOR]
```

2. Verás la página de bienvenida de Nextcloud

**[CAPTURA] CAPTURA 38**: Página de bienvenida y configuración inicial de Nextcloud.

## Paso 6.2: Completar el asistente de configuración

1. En la página de configuración inicial, completa los siguientes campos:

**Crear una cuenta de administrador:**
- **Usuario**: `admin` (o el nombre que prefieras)
- **Contraseña**: Una contraseña segura (¡anótala!)

**Carpeta de datos:**
- Deja la ruta por defecto: `/var/www/html/nextcloud/data`

**Configurar la base de datos:**
- Haz clic en **"Almacenamiento y base de datos"** para expandir opciones
- Selecciona **MySQL/MariaDB**
- **Usuario de base de datos**: `nextclouduser`
- **Contraseña de base de datos**: La contraseña que configuraste en el Paso 4.3
- **Nombre de la base de datos**: `nextcloud`
- **Servidor de la base de datos**: `localhost`

**[CAPTURA] CAPTURA 39**: Formulario de configuración completado antes de hacer clic en "Instalar".

2. Desmarca las aplicaciones recomendadas por ahora (opcional)

3. Haz clic en **"Instalar"** o **"Install"**

4. La instalación puede tardar unos minutos

**[CAPTURA] CAPTURA 40**: Pantalla de progreso durante la instalación de Nextcloud.

## Paso 6.3: Primer acceso a Nextcloud

1. Una vez completada la instalación, serás redirigido a la página principal de Nextcloud

**[CAPTURA] CAPTURA 41**: Panel principal de Nextcloud después de la instalación exitosa.

2. Nextcloud puede mostrar algunas recomendaciones o tutoriales iniciales
   - Puedes explorarlos o cerrarlos

**[CAPTURA] CAPTURA 42**: Vista del tutorial de bienvenida de Nextcloud (si aparece).

\newpage

# Parte 7: Configuración Adicional y Optimización

## Paso 7.1: Configurar tareas programadas (cron)

Para un mejor rendimiento, es recomendable configurar cron en lugar de AJAX.

1. Vuelve al terminal del servidor

2. Edita el crontab del usuario www-data:

```bash
sudo crontab -u www-data -e
```

Si es la primera vez, selecciona un editor (recomendado: nano, opción 1).

3. Añade la siguiente línea al final del archivo:

```
*/5 * * * * php -f /var/www/html/nextcloud/cron.php
```

**[CAPTURA] CAPTURA 43**: Archivo crontab editado con la tarea de Nextcloud.

4. Guarda y cierra (`Ctrl+O`, `Enter`, `Ctrl+X`)

5. Desde la interfaz web de Nextcloud:
   - Haz clic en tu avatar (esquina superior derecha)
   - Selecciona **"Configuración de administración"** o **"Administration settings"**
   - En el menú lateral, ve a **"Configuración básica"** o **"Basic settings"**
   - En **"Tareas en segundo plano"**, selecciona **"Cron"**

**[CAPTURA] CAPTURA 44**: Configuración de tareas en segundo plano establecida en "Cron".

## Paso 7.2: Ajustar configuración de PHP para CLI

1. Edita el archivo php.ini para CLI:

```bash
sudo nano /etc/php/8.1/cli/php.ini
```

2. Busca y modifica:

```ini
memory_limit = 512M
```

3. Guarda y cierra el archivo

## Paso 7.3: Configurar advertencias de seguridad

1. En la interfaz web, ve a **"Configuración"** → **"Información general"** o **"Overview"**

**[CAPTURA] CAPTURA 45**: Página de información general de Nextcloud.

2. Revisa si hay advertencias de seguridad o configuración
   - Si aparecen advertencias sobre "default phone region", continúa con el siguiente paso

3. Edita el archivo de configuración de Nextcloud:

```bash
sudo nano /var/www/html/nextcloud/config/config.php
```

4. Añade la siguiente línea antes del último `);`:

```php
  'default_phone_region' => 'ES',
```

**[CAPTURA] CAPTURA 46**: Archivo config.php con la configuración de región añadida.

5. Guarda y cierra el archivo

6. También añade el dominio confiable. En el mismo archivo `config.php`, localiza la sección `trusted_domains` y añade tu IP:

```php
  'trusted_domains' =>
  array (
    0 => 'localhost',
    1 => '[TU_IP_DEL_SERVIDOR]',
  ),
```

**Nota**: Reemplaza `[TU_IP_DEL_SERVIDOR]` con tu IP real sin corchetes, por ejemplo: `'192.168.1.100'` (mantén las comillas simples).

**[CAPTURA] CAPTURA 47**: Configuración de dominios confiables actualizada.

7. Guarda y cierra

\newpage

# Parte 8: Instalación de HTTPS (SSL) con Certificado Autofirmado

## Paso 8.1: Habilitar el módulo SSL de Apache

1. Habilita el módulo SSL:

```bash
sudo a2enmod ssl
```

**[CAPTURA] CAPTURA 48**: Habilitación del módulo SSL de Apache.

## Paso 8.2: Crear un certificado autofirmado

1. Crea el certificado SSL:

```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout /etc/ssl/private/nextcloud-selfsigned.key \
-out /etc/ssl/certs/nextcloud-selfsigned.crt
```

2. Completa la información solicitada:
   - **Country Name**: `ES` (o tu país)
   - **State**: Tu provincia
   - **Locality**: Tu ciudad
   - **Organization Name**: `ASIX` o tu centro educativo
   - **Organizational Unit**: `Practica`
   - **Common Name**: La IP o dominio de tu servidor
   - **Email Address**: Tu email (opcional)

**[CAPTURA] CAPTURA 49**: Generación del certificado SSL autofirmado.

## Paso 8.3: Configurar Apache para usar SSL

1. Crea un nuevo archivo de configuración SSL:

```bash
sudo nano /etc/apache2/sites-available/nextcloud-ssl.conf
```

2. Añade el siguiente contenido:

```apache
<VirtualHost *:443>
    DocumentRoot /var/www/html/nextcloud
    ServerName nextcloud.local

    SSLEngine on
    SSLCertificateFile /etc/ssl/certs/nextcloud-selfsigned.crt
    SSLCertificateKeyFile /etc/ssl/private/nextcloud-selfsigned.key

    <Directory /var/www/html/nextcloud/>
        Options +FollowSymlinks
        AllowOverride All
        Require all granted
        
        <IfModule mod_dav.c>
            Dav off
        </IfModule>
        
        SetEnv HOME /var/www/html/nextcloud
        SetEnv HTTP_HOME /var/www/html/nextcloud
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/nextcloud-ssl-error.log
    CustomLog ${APACHE_LOG_DIR}/nextcloud-ssl-access.log combined
</VirtualHost>
```

**[CAPTURA] CAPTURA 50**: Archivo de configuración SSL para Nextcloud.

3. Guarda y cierra el archivo

4. Actualiza la configuración HTTP para redirigir a HTTPS:

```bash
sudo nano /etc/apache2/sites-available/nextcloud.conf
```

5. Añade estas líneas dentro del bloque `<VirtualHost *:80>` después de `ServerName`:

```apache
    Redirect permanent / https://[TU_IP_DEL_SERVIDOR]/
```

**Importante**: Reemplaza `[TU_IP_DEL_SERVIDOR]` con tu dirección IP real, eliminando los corchetes. Por ejemplo: `https://192.168.1.100/`

**[CAPTURA] CAPTURA 51**: Configuración HTTP con redirección a HTTPS.

6. Guarda y cierra

7. Habilita el nuevo sitio SSL:

```bash
sudo a2ensite nextcloud-ssl.conf
```

8. Verifica la configuración:

```bash
sudo apache2ctl configtest
```

9. Reinicia Apache:

```bash
sudo systemctl restart apache2
```

**[CAPTURA] CAPTURA 52**: Habilitación del sitio SSL y reinicio de Apache.

## Paso 8.4: Actualizar configuración de Nextcloud

1. Edita el archivo config.php:

```bash
sudo nano /var/www/html/nextcloud/config/config.php
```

2. Añade o modifica la línea:

```php
  'overwrite.cli.url' => 'https://[TU_IP_DEL_SERVIDOR]',
```

**Nota**: Reemplaza `[TU_IP_DEL_SERVIDOR]` con tu IP real sin corchetes, manteniendo las comillas. Ejemplo: `'https://192.168.1.100'`

3. Guarda y cierra

\newpage

# Parte 9: Pruebas Finales

## Paso 9.1: Acceder por HTTPS

1. Desde tu navegador, accede a:

```
https://[IP_DE_TU_SERVIDOR]
```

2. El navegador mostrará una advertencia de seguridad (porque el certificado es autofirmado)
   - Haz clic en **"Avanzado"** o **"Advanced"**
   - Haz clic en **"Continuar al sitio"** o **"Proceed to site"**

**[CAPTURA] CAPTURA 53**: Advertencia de seguridad del navegador y cómo continuar.

3. Deberías ver la página de login de Nextcloud con el candado de HTTPS

**[CAPTURA] CAPTURA 54**: Página de login de Nextcloud con conexión HTTPS activa.

4. Inicia sesión con tus credenciales de administrador

## Paso 9.2: Subir un archivo de prueba

1. Una vez dentro de Nextcloud, haz clic en el icono **"+"** o **"Nuevo"**
2. Selecciona **"Cargar archivo"** o **"Upload file"**
3. Selecciona un archivo de prueba desde tu equipo (imagen, documento, etc.)

**[CAPTURA] CAPTURA 55**: Proceso de subida de archivo en Nextcloud.

4. Verifica que el archivo se haya subido correctamente

**[CAPTURA] CAPTURA 56**: Archivo subido correctamente y visible en Nextcloud.

## Paso 9.3: Crear una carpeta

1. Haz clic en el icono **"+"** o **"Nuevo"**
2. Selecciona **"Nueva carpeta"** o **"New folder"**
3. Nombra la carpeta (ej: "Documentos Practica")
4. Haz clic en **"Crear"** o **"Create"**

**[CAPTURA] CAPTURA 57**: Carpeta creada en Nextcloud.

## Paso 9.4: Compartir un archivo o carpeta

1. Haz clic en el icono de **compartir** (tres puntos o icono de compartir) junto a un archivo o carpeta
2. Crea un enlace de compartición público:
   - Haz clic en **"Compartir enlace"** o **"Share link"**
   - Se generará un enlace público

**[CAPTURA] CAPTURA 58**: Diálogo de compartir mostrando el enlace generado.

3. Copia el enlace y pruébalo en una ventana de incógnito o en otro navegador

**[CAPTURA] CAPTURA 59**: Vista del archivo compartido desde el enlace público (sin autenticación).

## Paso 9.5: Explorar aplicaciones adicionales

1. Haz clic en tu avatar (esquina superior derecha)
2. Selecciona **"Aplicaciones"** o **"Apps"**
3. Explora las aplicaciones disponibles:
   - **Calendar**: Para gestionar calendarios
   - **Contacts**: Para gestionar contactos
   - **Notes**: Para tomar notas
   - **Talk**: Para videoconferencias
   - etc.

**[CAPTURA] CAPTURA 60**: Página de aplicaciones de Nextcloud mostrando opciones disponibles.

## Paso 9.6: Verificar el estado del sistema

1. Ve a **"Configuración"** → **"Información general"**
2. Revisa que no haya advertencias críticas
3. Verifica el estado de seguridad y rendimiento

**[CAPTURA] CAPTURA 61**: Página de información general sin advertencias críticas.

\newpage

# Parte 10: Conclusión y Reflexión

¡Felicidades! Has completado la instalación y configuración de tu propio servidor cloud con Nextcloud sobre Ubuntu Server 22.04.

## Resumen de lo realizado

En esta práctica has:

1. [OK] Creado una máquina virtual en VirtualBox
2. [OK] Instalado Ubuntu Server 22.04 LTS
3. [OK] Configurado un stack LAMP (Linux, Apache, MySQL, PHP)
4. [OK] Instalado y configurado Nextcloud
5. [OK] Implementado SSL/HTTPS con certificado autofirmado
6. [OK] Realizado pruebas de funcionalidad (subir archivos, compartir, etc.)

## Comandos de mantenimiento útiles

### Ver logs de Apache
```bash
sudo tail -f /var/log/apache2/nextcloud-error.log
```

### Ver logs de Nextcloud
```bash
sudo tail -f /var/www/html/nextcloud/data/nextcloud.log
```

### Reiniciar servicios
```bash
sudo systemctl restart apache2
sudo systemctl restart mariadb
```

### Actualizar Nextcloud
```bash
cd /var/www/html/nextcloud
sudo -u www-data php occ upgrade
```

### Verificar estado de Nextcloud
```bash
cd /var/www/html/nextcloud
sudo -u www-data php occ status
```

## Tareas de reflexión

Para completar tu entrega, debes responder de forma detallada (mínimo 100 palabras por pregunta) a las siguientes cuestiones:

### 1. ¿Qué ventajas tiene montar tu propio cloud frente a usar uno comercial?

**Escribe tu reflexión aquí:**

_[Ejemplo de aspectos a considerar: privacidad y control de datos, costes a largo plazo, personalización, independencia de terceros, aprendizaje técnico, limitaciones de ancho de banda y escalabilidad, etc.]_

---

### 2. ¿Qué problemas has tenido durante la práctica y cómo los has resuelto?

**Escribe tu reflexión aquí:**

_[Describe los problemas específicos que encontraste, qué errores aparecieron, cómo buscaste soluciones, qué comandos o configuraciones tuviste que ajustar, etc.]_

---

### 3. ¿Qué mejorarías si tuvieras más tiempo?

**Escribe tu reflexión aquí:**

_[Ejemplo de aspectos a considerar: configurar un dominio real, implementar certificado SSL válido, configurar backups automáticos, añadir más aplicaciones, mejorar la seguridad con firewall, implementar 2FA, etc.]_

---

## Recursos adicionales

- **Documentación oficial de Nextcloud**: https://docs.nextcloud.com/
- **Foro de la comunidad Nextcloud**: https://help.nextcloud.com/
- **Ubuntu Server Guide**: https://ubuntu.com/server/docs
- **Apache Documentation**: https://httpd.apache.org/docs/

## Criterios de evaluación

Tu práctica será evaluada según:

- **Completitud (40%)**: Todas las capturas requeridas están presentes y son correctas
- **Documentación (30%)**: Cada captura incluye una breve descripción de lo que muestra
- **Reflexión (20%)**: Las respuestas a las preguntas son completas, reflexivas y demuestran comprensión
- **Presentación (10%)**: El documento está bien organizado, es legible y profesional

---

**¡Buen trabajo!**

Guarda este documento junto con todas las capturas en un único archivo PDF y entrégalo según las instrucciones de tu profesor/a.
