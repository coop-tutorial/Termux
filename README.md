## Solucion al problema de Signal -9 Kill Process
![image](https://cdn.discordapp.com/attachments/1120450661050499083/1192235969429127288/remix-982452fa-c8fc-4fb6-bde3-4ddab23dface.png?ex=65a85745&is=6595e245&hm=9b1c5d6a02a82b276c3e8b37e946e582ea1e6f2d119576e1c433609181568187&)
* Primero tener en cuenta que debemos tener termux instalado y actualizado en nuestro dispositivo 
necesitaremos la herramienta de `android-tools` en nuestro termux para conectarnos mediante adb shell localmente y eliminar esos porcesos.
### Esto soluciona posibles errores si no se instala tu herramienta
* No es necesario si no tienes problemas al instalar `android-tools`✓
```bash
termux-change-repo
```
### Instalamos la herramienta

```bash
pkg install android-tools
```
__________________________________________________________________________________________
* ahora procederemos a activar opciones de desarrollador en nuestro sistema android en ajustes 
para ello tocamos el numero de compilacion 7 veces de forma progresiva constante una tras otra.
para cualquier duda visita `Youtube` Busca: Como activar las opciones de desarrollador en mi dispositivo `(Pones el nombre de tu dispositivo)`
teniendo esa opcion desbloqueada ahora procedemos a activar Depuracion inalambrica.
__________________________________________________________________________________________
![image](https://cdn.discordapp.com/attachments/1120450661050499083/1192237511016185966/Picsart_24-01-03_14-45-58-685.jpg?ex=65a858b5&is=6595e3b5&hm=5efd8ef1b1b3ac869d42b44411f353bffa15b4a8833289fe45f9713d3eaf38c3&)

__________________________________________________________________________________________________
### Activar Depuracion inalambrica 
* Deberemos dividir la pantalla en 2 para tener ajustes y termux en la misma pantalla para realizar
la conexion local...
lo comectaremos mediante codigo de vinculación
con el sigiente comando

```bash
adb pair
```
`adb pair ip:puerto`
* donde `ip` es la.que saldra en tu opción de depuracion inalambrica y `puerto` es lo que sigue despues de los dos puntos
![image](https://cdn.discordapp.com/attachments/1120450661050499083/1192240916614877255/Picsart_24-01-03_14-57-56-761.jpg?ex=65a85be1&is=6595e6e1&hm=ec1a4f53d28d5553852ec63e0ca1142d85b5a45bb3631482bdd3e98eecabd95b&)
____________________________________________________________________________________________________________

* Despues de ingresar tu `ip:port` Te solicitara un `code` que sera el que estara en la parte superior

## Code 
* en tu caso sera distinto a este pero esta en la misma ubicación

![image](https://cdn.discordapp.com/attachments/1120450661050499083/1192240936957259826/Picsart_24-01-03_14-59-30-188.jpg?ex=65a85be6&is=6595e6e6&hm=e396eecb04be1deffbe401497bd995dbee67b30ba1ce2f28f06e25aadc66cdf6&)
________________________________________________________________________________________________________

una vez inresado esto ahora deberemos poner

```
adb connect
```
donde:
`adb connect ip:port`
sera el ip y puerto que te salga a continuación

![image](https://cdn.discordapp.com/attachments/1120450661050499083/1192243872626118826/Picsart_24-01-03_15-11-11-514.jpg?ex=65a85ea2&is=6595e9a2&hm=a29c855132b018073c0b98ae8a4a5e7e33343b9b7e1c8835eb624d107e0bbec5&)

una vez realizado para verificar que ya estas conectado, ingresa este comando en termux:

```bash
adb devices
```
si en tu pantalla sale esto a continuación, significa que realizaste los pasos con exito ✓

![image](https://cdn.discordapp.com/attachments/1120450661050499083/1192244746719084554/Picsart_24-01-03_15-14-37-573.jpg?ex=65a85f72&is=6595ea72&hm=1d2d6d01db2fd839cc2f4e14368308613a29ab0ca54cf41acd04e0af8accecc0&)
________________________________________________________________________________________________________

## Ahora queda imgresar estos comandos

![image](https://cdn.discordapp.com/attachments/1120450661050499083/1192245352946995260/Picsart_24-01-03_15-17-12-105.jpg?ex=65a86002&is=6595eb02&hm=fa177bd1fda735523454212b56dce01bf6cb2ce01aee9bed9a34b176bfbd554e&)

### PRIMER COMANDO 

```
adb shell "/system/bin/device_config set_sync_disabled_for_tests persistent"
```
### SEGUNDO COMANDO
```
adb shell "/system/bin/device_config put activity_manager max_phantom_processes 2147483647"
```
### TERCER COMANDO
```
adb shell settings put global settings_enable_monitor_phantom_procs false
```

## Ahora puedes ejecutar tu PC sin problemas
* Ya puedes desactivar la depuración inalámbrica

