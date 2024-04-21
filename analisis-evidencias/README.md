# Analizar el volcado de memoria 🚀
Ahora debes compartirte a tí mismo las evidencias recopiladas.
1. Crea el directorio `profile`:
   ```bash
   mkdir profiles
   ```

2. Mueve el profile generado anteriormente al directorio `profile` creado:
   ```bash
   cp Descargas/Ubuntu_5.4.0-84-generic_profile.zip profiles/
   ```

3. Revisa que el profile haya sido agregado correctamente:
   ```bash
   vol.py --plugins=/path/to/profiles --info | grep "Linux"
   ```

4. Revisa los comandos que puedes ejecutar:
   ```bash
   vol.py --info | grep linux_
   ```

5. Por probar, intenta ejecutar el comando pstree:
   ```bash
   vol.py --plugins=profiles --profile=<Linux_profile> -f /path/to/mfile.dmp linux_pstree
   ```
   

