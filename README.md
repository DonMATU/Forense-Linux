# Metodologías forenses en Linux 🐧

Matu-Fuzzer es un script de Bash para fuzzing web, diseñado para descubrir directorios y ficheros en servidores web.

## Adquisisción de evidencias
<br>
<br>
<br>

### Volcado de memoria 🚀
Hay distinas formas y herramientas para realizar el volcado de memoria en un sistema Linux. Las más populares y comunes dentro del mundo del forense digital serían las siguientes: 

#### 🔷 AVML 

1. Descarga el script `AVML`
   ```bash
   wget https://github.com/microsoft/avml/releases/download/v0.13.0/avml
   ```

2. Dale permisos de ejecución al scirpt:
   ```bash
   chmod +x avml
   ```

3. (OPCIONAL) Crea el directorio donde almacenar el directorio donde almacenar el volcado de memoria
   ```bash
   mkdir evidencias
   ```
   
4. Ahora lanza el volcado de memoria. (No te asustes si se cuelga un poco el sistema)
   ```bash
   sudo ./avml ./evidencias/memory_avml.dmp
   ```

Recuerda hascer las comprobaciones de integridad pertinentes :)
<br>
<br>
<br>

#### 🔷 LIME 
Esta herramienta se debe compilar, siendo necesaria la instalación de varios paquetes para poder realizar este procedimiento. <br>
<br>
Para un correcto volcado de memoria, se debería montar un host gemelo (misma distribución con la misma versión de kernel) y compilar en él el driver .ko, ya que si descargamos esta herramienta y compilamos en la máquina objetivo, vamos a modificar la memoria y por lo tanto las evidencias digitales
<br>

1. Descarga los paquetes `git` y `gcc` en el sistema.
   ```bash
   sudo apt install -y git make gcc
   ```
   
2. Descarga la herramienta `LIME` desde Github.
   ```bash
   git clone https://github.com/504ensicsLabs/LiME.git
   ```
      
3. Se compila el software descargado.
   ```bash
   cd LiME/src && make
   ```

4. Carga un módulo del kernel (lime-*.ko) especificando la ubicación del archivo de imagen de memoria, el formato (lime), y un tiempo de espera de 0 segundos.
   ```bash
   sudo insmod ./lime-*.ko "path=/tmp/limeImage.mem format=lime timeout=0"
   ```  

5. Crea el directorio donde almacenarás el volcado de memoria
   ```bash
   mkdir ~/Descargas/evidencias/
   ```
   
6. Mueve el volcado de memoria al directorio de salida
   ```bash
   sudo mv /tmp/limeImage.mem ~/Descargas/evidencias/
   ```  

<br>
<br>
<br>


### Triaje
#### 🔷 CyLR 
1. Descarga la herramienta CylR
   ```bash
   sudo apt install -y git make gcc && unzip CyLR_linux-x64.zip
   ```
   
2. Dale permisos de ejecución al scirpt:
   ```bash
   sudo chmod +x CyLR
   ```

3. (OPCIONAL) Crea el directorio donde almacenar el directorio donde almacenar el volcado de memoria
   ```bash
   mkdir evidencias
   ```

4. Se genera el volcado de :
   ```bash
   sudo ./CyLR -od ./evidencias
   ```
<br>
<br>
<br>

## Generación del profile



