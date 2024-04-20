# :shipit: Metodologías forenses en Linux 🐧

Matu-Fuzzer es un script de Bash para fuzzing web, diseñado para descubrir directorios y ficheros en servidores web.

## Adquisisción de evidencias

### Volcado de memoria 🚀
Hay distinas formas y herramientas para realizar el volcado de memoria en un sistema Linux. Las más populares y comunes dentro del mundo del forense digital serían las siguientes: 

#### AVML


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

