# uc3mICS
uc3mICS está pensado para ser un CGI que sirva un horario de la UC3M.
Elimina el acceso a través del portal adAS para permitir la sincronizción
con sólo la URL. Así se puede, por ejemplo, sincronizar el calendario de Android
con la aplicación [ICSx⁵](https://icsx5.bitfire.at/).

Tengo el CGI operativo en (https://danoloan.es/cgi/uc3mics);
puedo asegurar que ningunas credenciales se quedarán guardadas,
pero eso es cuestión de confianza...

## Uso como CGI
Los horarios de la UC3M se pueden obtener en formato ICS en
https://aplicaciones.uc3m.es/horarios-web/alumno/alumno.page.

Las URL de los ficheros ICS son de la forma:
```
https://aplicaciones.uc3m.es/horarios-web/alumno/verHorario.page?exp=EXP&per=PER&fmt=ics
```
donde `EXP` y `PER` son números.

Si `<cgi-uri>` es la ruta de este CGI, basta con acceder a la siguiente URL,
sustituyendo `EXP` y `PER` con los valores anteriores:
```
<cgi-uri>?exp=EXP&per=PER
```
La petición HTTP debe tener **la cabezera 'Authorization' conteniendo el NIA y la contraseña codificados en base64** (esto lo hacen algunas aplicaciones, ver [Sincronización en Android](#sincronización-en-android)),
y devolverá entonces el fichero ICS.

No se puede recomendar lo suficiente el uso de HTTPS en un servicio como este,
que las credenciales van sin cifrar.

### Sincronización en Android
La aplicación [ICSx⁵](https://icsx5.bitfire.at/) se puede usar para sincronizar el calendario generado por este script con Android. Al suscribirlo, hay que marcar la opción **Requiere autenticación** e introducir ahí las credenciales.

## Uso interactivo
El script también se puede usar de forma interactiva, y sirve para obtener un recurso cualquiera que esté tras el portal adAS. Se preguntará por la ruta del recurso, que debe ser su URL completa.

## Dependencias
Las dependencias están en el fichero `requirements.txt`.
Este es el comando para instalarlas usando `pip3`:
```
$> pip3 install -r requirements.txt
```

Las dependencias son:
- BeautifulSoup ([pypi](https://pypi.org/project/beautifulsoup4/))
- Mechanize ([pypi](https://pypi.org/project/mechanize/))

## Créditos
La mitad del script este es copia-pega del gran script [`aulaglobal.py`](https://github.com/tairosonloa/Aula_Global_UC3M) de [tairosonloa](https://github.com/tairosonloa).
