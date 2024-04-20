# Metodología forense básica en Linux 🐧



## Adquisisción de evidencias
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


### Triaje 📂
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

## Generación del profile 💻
(En una máquina clonada)
<br>

1. Descarga los paquetes necesarios para nuestro sistema (cloado) `bison` `flex` `dwarfdump` `linux-headers-$(uname -r)`:
   ```bash
   sudo apt-get install -y bison flex dwarfdump linux-headers-$(uname -r)
   ```
   
2. Descarga la herramienta `volatility`:
   ```bash
   git clone https://github.com/volatilityfoundation/volatility.git
   ```

3. Se compila el software `volatility`:
   ```bash
   cd volatility/tools/linux/ && make
   ```

4. Vuelve el directorio padre:
   ```bash
   cd ../../../
   ```

5. Genera el profile del sistema a tratar:
   ```bash
   sudo zip $(lsb_release -i -s)_$(uname -r)_profile.zip ./volatility/tools/linux/module.dwarf /boot/System.map-$(uname -r)
   ```

6. Revisa revisar la integridad de la información:
   ```bash
   md5sum Ubuntu_4.15.0-213-generic_profile.zip
   ```
