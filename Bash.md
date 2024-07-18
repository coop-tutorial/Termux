El problema que estás enfrentando se debe a los caracteres de retorno de carro (`\r`) en tu script `coop-adb.sh`. Esto generalmente ocurre cuando el archivo se crea o edita en un sistema Windows y luego se ejecuta en un entorno Unix, como Termux, donde estos caracteres no son necesarios y causan errores.

Para solucionar esto, puedes convertir los finales de línea de formato DOS (CRLF) a formato Unix (LF). Aquí tienes dos formas de hacerlo:

### Método 1: Usando `dos2unix`
1. Instala `dos2unix` en Termux:
   ```sh
   pkg install dos2unix
   ```
2. Convierte tu archivo:
   ```sh
   dos2unix coop-adb.sh
   ```
3. Ejecuta el script nuevamente:
   ```sh
   bash coop-adb.sh
   ```

### Método 2: Usando `sed`
1. Usa `sed` para eliminar los caracteres `\r`:
   ```sh
   sed -i 's/\r$//' coop-adb.sh
   ```
2. Ejecuta el script nuevamente:
   ```sh
   bash coop-adb.sh
   ```

### Recomendación
Si vuelves a copiar el contenido del script desde una fuente en línea, asegúrate de copiarlo en un editor que no agregue caracteres de retorno de carro. Aquí tienes el script limpio y sin los caracteres `\r` para que lo puedas usar directamente:

```sh
#!/data/data/com.termux/files/usr/bin/bash

# Definición de colores
YELLOW='\033[1;33m'
NC='\033[0m' # Sin color

# Función para imprimir mensajes en color amarillo
function print_yellow {
    echo -e "${YELLOW}$1${NC}"
}

# Actualización de paquetes en Termux
print_yellow "Actualizando paquetes en Termux..."
print_yellow "Créditos: Retired64 on YouTube..."
pkg update -y &>/dev/null && pkg upgrade -y &>/dev/null
print_yellow "Paquetes actualizados."

# Instalación de android-tools
print_yellow "Instalando android-tools..."
pkg install android-tools -y &>/dev/null
print_yellow "android-tools instalado."

# Instrucciones para la depuración inalámbrica
print_yellow "Configurando la depuración inalámbrica..."

# Ingresar la IP y el puerto para emparejar
read -p "Ingrese la IP y el puerto para emparejar (formato: ip:puerto): " IP_PORT
print_yellow "Emparejando con $IP_PORT..."
adb pair $IP_PORT

# Conectar el dispositivo
read -p "Ingrese la IP y el puerto para conectar (formato: ip:puerto): " CONNECT_IP_PORT
print_yellow "Conectando con $CONNECT_IP_PORT..."
adb connect $CONNECT_IP_PORT

# Verificar la conexión
print_yellow "Verificando la conexión..."
adb devices | grep 'device$' &>/dev/null

if [ $? -eq 0 ]; then
    print_yellow "Conexión exitosa. Dispositivos conectados:"
    adb devices

    # Ejecutar comandos adb shell
    print_yellow "Ejecutando comandos adb shell..."
    adb shell "/system/bin/device_config set_sync_disabled_for_tests persistent"
    adb shell "/system/bin/device_config put activity_manager max_phantom_processes 2147483647"
    adb shell "settings put global settings_enable_monitor_phantom_procs false"
    adb shell "setprop persist.sys.fflag.override.settings_enable_monitor_phantom_procs false"
    print_yellow "Comandos ejecutados exitosamente."
else
    print_yellow "Error en la conexión. No se encontraron dispositivos conectados."
fi
```

Intenta ejecutar este script limpio y debería funcionar sin problemas
