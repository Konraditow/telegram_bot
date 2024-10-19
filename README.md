# Guión MikroTik: Bot de Telegram

Este _script_ se utiliza para controlar tu MikroTik simplemente usando las redes sociales Telegram. Hay muchos comandos para monitorear, cambiar puntos de acceso, eliminar usuarios de puntos de acceso, agregar nuevas cuentas de puntos de acceso, cambiar contraseñas de usuarios de puntos de acceso, etc.

# Lista de contenidos
- [Descargo de responsabilidad](#descargo de responsabilidad)
- [Historial de versiones](#version-history)
- [Instalación](#instalación)
- [Comandos, Parámetros y Funciones](#comandos-parámetros-y-funciones)
- [Fuente](#fuente)

# Descargo de responsabilidad
Este _script_ es _de código abierto_. Puede modificar, agregar o reducir el contenido de este _script_ siempre que no viole las disposiciones aplicables de la licencia _MIT_. Este _script_ **NO TIENE GARANTÍA** mientras lo utilices. Si tiene problemas durante la instalación o el uso de este _script_, analice y explique cómo ocurrió el problema a través de la función [**Problemas**] (https://github.com/dwichan0905/telegram_bot/issues).

# Contribución
Las contribuciones a este _repositorio_ se limitan únicamente a los scripts y la documentación de MikroTik. Puede contribuir _bifurcando este repositorio_, creando una nueva _sucursal_, realizando cambios y realizando una _pull request_ a este _repositorio_. Describe lo que agregaste y lo que cambiaste en este _repositorio_. No olvide escribir un script de ayuda en ```tg_cmd_help``` para ayudar si el usuario de este script olvida el comando que tiene que escribir.

# Historial de versiones
#### 1.3.1 (27 de octubre de 2020)
- Se agregó el comando ``/monitoring`` que funciona para observar la tasa de transferencia y la tasa de recepción desde la interfaz, y también puede observar el uso de CPU y RAM.
- se agregó el comando ``/stop`` para detener el proceso de monitoreo que se ejecuta actualmente en Telegram
vídeo: [YouTube](https://www.youtube.com/watch?v=0HEuqgMZVp4)

#### 1.3 (8 de octubre de 2020)
- Genere cada script en una versión de texto para que pueda leerse directamente sin tener que importarlo a Mikrotik.
- Se agregó la función de minúsculas `func_lowercase`
- modificó el comando de hotspot, agregó una función de minúsculas para que si hay parámetros que usan letras mayúsculas aún se puedan leer (por ejemplo, un usuario escribe `/hotspot SesSion CoUnT`, entonces se leerá y el bot enviará una respuesta )
- eliminados `tg_cmd_start` y `tg_cmd_hi` (explicación a continuación)
- Se agregaron comandos alternativos a tg_getUpdates, si el usuario escribe: `/hi`, `/start`, `/hi`, `/halo`, `/hello`, `/help`. Luego, ejecutará el script `tg_cmd_help`. En otras palabras, `tg_cmd_help` también maneja esos comandos.
- también se aplica a `/hotspot`. Si el usuario escribe `/hs`, se redireccionará a `tg_cmd_hotspot`
- tg_cmd_dhcp modificado para usar funciones en minúsculas y eliminado parámetros innecesarios
- se agregó el comando de arrendamiento /dhcp
- añadido el comando /interfaz mostrar todo

#### 1.2 (11 de agosto de 2019)
 1. Se corrigió un _error_ al _importar un script_ (error ``argumento predeterminado no válido``)
 2. Actualización de comandos en el punto de acceso:
   - Se cambió el comando ``/usuarios de hotspot`` a ``/recuento de sesiones de hotspot``
   - Se cambió el comando ``/hotspot showall`` a ``/hotspot session showall``
   - Se agregaron nuevos comandos: ``/hotspot session deauth-by-mac``, ``/hotspot session deauth-by-ip`` y ``/hotspot session deauth-by-user``
 3. Mejoras en los comandos:
   - ``/reboot`` ahora se puede usar para reiniciar el _router_ (_retraso_ 30 segundos)
 4. Se agregaron nuevas condiciones:
   - Después de _reiniciar_, _Router_ enviará un informe a través de Telegram de que se ha _reiniciado_ y registrará todos los casos por los que lo hizo en el "Registro crítico" (una pausa de 30 segundos después de que el enrutador haya terminado de _reiniciarse_).

#### 1.1 (8 de agosto de 2019)
 1. Primera versión

## Instalación
Antes de iniciar la instalación, debes tener un _Access Token_ para el Telegram Bot y su ChatID. Siga [este enlace (labkom.co.id)](https://labkom.co.id/mikrotik/mikrotik-netwach-monitoring-status-access-point-hotspot-dengan-using-telegram) para obtener una guía sobre cómo para crear un telegrama bot
Para instalarlo, _clone_ o _descargue este repositorio_ y luego:

 1. Extraiga el archivo ZIP que _descarga_ (omita si _clona este repositorio_)
 2. _Cargue_ el archivo ``telegram_bot.rsc`` en su MikroTik (puede ser a través de FileZilla FTP, también puede ser a través de WinBox) y guárdelo en la carpeta principal (raíz o /) de su MikroTik.
 3. Después de eso, abra MikroTik _Terminal_ y escriba el siguiente comando:
 ``importar nombre-archivo=telegram_bot.rsc``
 4. Configure los ajustes del _bot_ en ``Sistema > Scripts > tg_config`` cambiando el siguiente comando:
 > Complete su token de acceso al bot de Telegram:
   ``"botAPI"="xxxxxx:xxxxxxxx-xxxxxxx"`` 

 > Complete su ID de chat de Telegram:
    ``defaultChatID"="xxxxxxxxxx"``
    
> Complete algunos de sus ChatID, pueden ser personales o grupales. Separar con comas:
  ``"de confianza"="xxxxxxxxxx, xxxxxxxxx, -xxxxxxxxx"``
  
  Luego guarde la configuración.
  
  5. ¡Listo!

## Comandos, parámetros y sus funciones
Escribe el siguiente comando en tu columna _chat_ con tu _bot_ de Telegram. Cada _parámetro_ ingresado está separado mediante espacios, por ejemplo ``/interface show``.

| Comando | Parámetros | Función | Ejemplo |
|-----------|--------|-------|-----|
| ``/ayuda`` | | Muestra una lista de funciones ejecutables | |
| ``/inicio`` | | Muestra una lista de funciones ejecutables | |
| ``/cpu`` | | Muestra la ID del enrutador, la carga de la CPU, el tiempo de actividad y la RAM total utilizada | |
| ``/dhcp`` | ``arrendamiento`` | muestra todos los detalles sobre el arrendamiento de DHCP| ``/arrendamiento dhcp`` |
| ``/dhcp`` | ``versión del cliente <interfaz>`` | Liberando cliente dhcp en ciertas interfaces| ``/versión del cliente dhcp ether1`` |
| ``/interfaz`` | ``mostrar`` | Muestra el estado de la conexión entre los puertos Ethernet en MikroTik | ``/mostrar interfaz`` |
| ``/interfaz`` | ``mostrar todo`` | Muestra el estado de conexión de todas las interfaces en MikroTik | ``/interfaz mostrar todo`` |
| ``/punto de acceso`` | ``ayuda`` | Muestra detalles de ayuda para el comando `/hotspot` | ``/ayuda de punto de acceso`` |
| ``/punto de acceso`` | ``recuento de sesiones`` | Muestra el número de usuarios actualmente activos | ``/recuento de sesiones de hotspot`` |
| ``/punto de acceso`` | ``showhall de sesiones`` | Muestra todos los detalles del usuario activo desde el nombre de usuario hasta el tiempo de actividad (excepto la contraseña) | ``/sesión hotspot showall`` |
| ``/punto de acceso`` | ``desautorización de sesión por usuario <nombre de usuario>`` | Revocar la _sesión_ del dispositivo según el nombre de usuario | ``/desautorización de sesión de hotspot por usuario administrador de telecomunicaciones`` |
| ``/punto de acceso`` | ``desautorización de sesión por ip <ip>`` | Revocar la _sesión_ del dispositivo según la dirección IP | ``/desautorización de sesión de punto de acceso por ip 192.168.1.2`` |
| ``/punto de acceso`` | ``sesión deauth-by-mac <dirección mac>`` | Revocar la _sesión_ del dispositivo según la dirección MAC | ``/desautorización de sesión de punto de acceso por mac AB:CD:EF:01:23:45`` |
| ``/punto de acceso`` | ``agregar <nombre de usuario> <contraseña>`` | Agregar un nuevo usuario de punto de acceso | ``/hotspot agregar telecomadmin admintelecom`` |
| ``/punto de acceso`` | ``eliminar <nombre de usuario>`` | Eliminar permanentemente usuarios de hotspot | ``/hotspot eliminar telecomadmin`` |
| ``/punto de acceso`` | ``deshabilitar <nombre de usuario>`` | Apagar o desactivar usuarios de hotspot | ``/hotspot desactivar telecomadmin`` |
| ``/punto de acceso`` | ``habilitar <nombre de usuario>`` | Habilitar usuarios de hotspot deshabilitados | ``/hotspot habilitar telecomadmin`` |
| ``/punto de acceso`` | ``cambiar-contraseña <nombre de usuario> <nueva contraseña>`` | Cambiar la contraseña del usuario del hotspot | ``/hotspot cambio-contraseña telecomadmin p4ssw0rdny4`` |
| ``/ping`` | | Hacer ping al DNS de Google | ``/ping`` |
| ``/monitoreo`` | ``interfaz <interfaz>`` | Supervisión de la interfaz | ``/interfaz de monitoreo wlan1`` |
| ``/monitoreo`` | ``procesador`` | Monitoreo del uso de CPU en el enrutador | ``/monitoreo de CPU`` |
| ``/monitoreo`` | ``carnero`` | Monitoreo del uso de RAM/memoria en el enrutador | ``/ram de monitoreo`` |
| ``/monitoreo`` | ``memoria`` | Monitoreo del uso de RAM/memoria en el enrutador | ``/memoria de monitoreo`` |
| ``/ping`` | ``a <dirección IP>`` | Haga ping a una dirección IP específica | ``/ping a 127.0.0.1`` |
| ``/público`` | | Mostrando DNS dinámico e IP pública en su MikroTik | ``/público`` |
| ``/enablehotspot`` | | Activar todas las funciones del hotspot | ``/enablehotspot`` |
| ``/disablehotspot`` | | Deshabilitar todas las funciones del hotspot | ``/disablehotspot`` |
| ``/forceupdateddns`` | | Actualización forzada de DNS dinámico | ``/forceupdateddns`` |
| ``/reiniciar`` | | Reiniciando MikroTik (pausa 30 segundos antes de reiniciar) | ``/reiniciar`` |
> **Nota**: para poder ejecutar los comandos ``/disablehotspot``, ``/enablehotspot`` y ``/interface show``, configure usted mismo qué hotspot aparecerá "automáticamente" en el script. ``tg_cmd_disablehotspot``, ``tg_cmd_enablehotspot`` y cualquier conexión Ethernet se mostrarán en ``tg_cmd_interface``.

# Fuente

 - [Labkom](https://labkom.co.id)
 - [Foro Mikrotik (ES)](https://forum.mikrotik.com)
 - [API de Telegram (ES)](https://api.telegram.org)
