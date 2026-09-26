# adguard-custom-blocklist

Listas personales para AdGuard Home. Incluyen bloqueos elegidos por el autor y excepciones de compatibilidad; no todos los dominios bloqueados representan malware o telemetría.

- `CUSTOM_BLOCKLIST_FINAL_LEAN_2026-08-08.txt`: lista principal.
- `CUSTOM_GAMING_TELEMETRY_2026-08-23.txt`: complemento de juegos; utilizar junto con la principal.

Se conservan los nombres de archivo para mantener las suscripciones existentes.

## Fire TV / Fire Stick

La revisión del 26/09/2026 encontró consultas bloqueadas a `softwareupdates.amazon.com` y `api.amazon.com` por el servicio **Amazon** de AdGuard Home (regla `||amazon.com^`, identificador de lista -2), no por una regla de bloqueo de estos archivos.

La lista principal incorpora excepciones limitadas a esos dos dominios y sus subdominios. No permite Amazon, AWS o CloudFront completos. Las excepciones se aplican a todos los clientes que usan la lista; no son exclusivas de un Fire Stick.

En AdGuard Home 0.107.79 las reglas de permiso se evalúan antes de los servicios bloqueados, siempre que el filtrado por listas esté habilitado. Después de actualizar la suscripción, verificar las consultas del dispositivo y volver a intentar la actualización. Otros dominios o reglas pueden requerir revisión: no se ha confirmado una actualización completa del Fire Stick.

Si se prefiere una excepción exclusiva del dispositivo, se debe configurar por cliente en AdGuard Home.

## Revisión de las listas

- Se mantienen los bloqueos de contenido y las excepciones preexistentes.
- Se retiran del complemento ocho bloqueos y un permiso ya presentes en la lista principal.
- Se retira el bloqueo contradictorio de `sirius.mwbsys.com`; se conserva su permiso preexistente.
- La posición al final del archivo no determina la prioridad de una excepción.

## Fuentes técnicas

- [Motor de filtrado de AdGuard Home 0.107.79](https://github.com/AdguardTeam/AdGuardHome/blob/v0.107.79/internal/filtering/filtering.go)
- [Sintaxis de filtrado DNS](https://adguard-dns.io/kb/general/dns-filtering-syntax/)

Esta revisión no certifica individualmente la clasificación de todos los dominios de las listas.
