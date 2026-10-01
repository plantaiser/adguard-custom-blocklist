# adguard-custom-blocklist

Listas personales para AdGuard Home. Incluyen bloqueos elegidos por el autor y excepciones de compatibilidad; no todos los dominios bloqueados representan malware o telemetría.

- `CUSTOM_BLOCKLIST_FINAL_LEAN_2026-08-08.txt`: lista principal.
- `CUSTOM_GAMING_TELEMETRY_2026-08-23.txt`: complemento de juegos; utilizar junto con la principal y HaGeZi Pro.

Se conservan los nombres de archivo para mantener las suscripciones existentes.

## Fire TV / Fire Stick — revisión del 01/10/2026

La revisión de ambas listas no encontró reglas de bloqueo que coincidieran con los hosts de tienda y reproducción de Amazon implicados. Los registros de AdGuard Home atribuyeron esos bloqueos al servicio **Amazon**, con identificador de lista **-2**: `||amazon.com^`, `||amazonvideo.com^`, `||cloudfront.net^` y otros dominios de infraestructura. No es un bloqueo originado en estos dos archivos.

La lista principal conserva los dos permisos del 26/09/2026 (`softwareupdates.amazon.com` y `api.amazon.com`) y agrega **22 excepciones limitadas** a hosts observados bloqueados en las consultas del Fire Stick. Incluyen `appstore-tv-prod-na.amazon.com`, `mas-ext.amazon.com`, `mas-sdk.amazon.com`, endpoints de Amazon Video, imágenes y dos distribuciones concretas de CloudFront. La presencia de un host en el registro confirma el bloqueo, pero no prueba que cada uno sea indispensable.

No se permiten Amazon, AWS ni CloudFront completos. No se agregan excepciones para los hosts de publicidad o telemetría identificados, como `mads.amazon.com`, `unagi-na.amazon.com`, `fls-na.amazon.com` o `minerva.devices.a2z.com`. Los bloqueos preexistentes se conservan.

La lista de juegos mantiene sus siete reglas: no se encontraron bloqueos de Amazon que quitar. Solo se actualizan los comentarios de revisión; los permisos permanecen en la principal para evitar duplicaciones.

En AdGuard Home 0.107.79 el motor evalúa las listas antes de los servicios bloqueados y una coincidencia de permiso finaliza esa comprobación, siempre que el filtrado por listas esté habilitado. Las excepciones se aplican a **todos los clientes que usan la lista** y al dominio indicado y sus subdominios. No modifican la configuración de “Servicios bloqueados”.

### Aplicación y comprobación

1. Actualizar las suscripciones desde **Filtros → Listas de bloqueo DNS → Buscar actualizaciones**.
2. Limpiar la caché DNS de AdGuard Home y reiniciar el Fire Stick para descartar respuestas bloqueadas almacenadas.
3. Intentar una descarga de Appstore y reproducir Fire TV Channels / News.
4. Revisar en el registro de consultas si aparecen otros dominios bloqueados y qué regla los bloquea.

Publicar en GitHub **no confirma que el router ya haya descargado la versión nueva**. No se ha verificado todavía una descarga ni reproducción completas tras esta revisión. Las excepciones cubren los hosts observados, no garantizan todos los servicios, regiones, versiones o futuros endpoints. Si aparecen más bloqueos por el servicio Amazon, la solución más completa es excluir únicamente Amazon de los servicios bloqueados del cliente Fire Stick, conservando los demás servicios y filtros. No hace falta desactivar toda la protección de AdGuard.

## Revisión de las listas

- Se mantienen los bloqueos de contenido y las excepciones preexistentes.
- Se retiran del complemento ocho bloqueos y un permiso ya presentes en la lista principal.
- Se retira el bloqueo contradictorio de `sirius.mwbsys.com`; se conserva su permiso preexistente.
- La posición al final del archivo no determina la prioridad de una excepción.

## Fuentes técnicas

- [Motor de filtrado de AdGuard Home 0.107.79](https://github.com/AdguardTeam/AdGuardHome/blob/v0.107.79/internal/filtering/filtering.go)
- [Sintaxis de filtrado DNS](https://adguard-dns.io/kb/general/dns-filtering-syntax/)

Esta revisión no certifica individualmente la clasificación de todos los dominios de las listas.

## Consolas y redundancias — revisión del 26/09/2026

Las dos listas son ahora complementos de **HaGeZi Pro**: deben utilizarse junto con esa lista para conservar los bloqueos retirados por redundancia. Los nombres de archivo y las URLs de suscripción se mantienen.

- Juegos: se agregan cinco dominios de reportes de Nintendo Switch / Switch 2 y se conservan dos de PlayStation.
- Se eliminan 21 bloqueos ya cubiertos por HaGeZi Pro (18 de la principal y 3 de juegos).
- Se eliminan tres reglas de subdominios ya cubiertos en la principal, conservando sus reglas padre.
- Tres bloqueos preexistentes de promociones/vistas de tienda de PS3 pasan a la principal: no deben clasificarse como telemetría.
- Xbox/Windows y Steam ya tienen algunos dominios de reportes cubiertos por las fuentes comparadas; no se copian de nuevo.

Ver [auditoría, dominios y fuentes](AUDITORIA-CONSOLAS-2026-09-26.md). La revisión compara ambos archivos con HaGeZi Pro, HaGeZi DoH, Phishing Army y una copia respaldada de Native Vendors del 25/09/2026; **no representa todas las listas de Internet ni garantiza eliminar toda la telemetría**. La cobertura externa puede cambiar al actualizar las fuentes.

No se agregaron dominios generales de autenticación, tiendas, actualizaciones ni partidas. No se probaron consolas físicas y bloquear reportes puede afectar estadísticas/diagnósticos. Los servicios completos bloqueados desde AdGuard Home son una configuración independiente que esta revisión no modifica.

Después de publicar, actualizar ambas suscripciones en AdGuard Home y comprobar inicio de sesión, tienda, descargas y juego en cada consola. Publicar en GitHub no confirma que el router haya descargado la nueva versión.
