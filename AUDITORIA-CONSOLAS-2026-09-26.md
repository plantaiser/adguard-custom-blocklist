# Auditoría de telemetría de consolas — 26/09/2026

Consulta de las fuentes: 2026-09-26T22:47:25.846155+00:00.

## Alcance

Dominios de consolas y plataformas de juego utilizables desde Argentina. Los dominios no tienen una restricción geográfica argentina. No existe un inventario verificable de todas las consolas, sus juegos y todas las listas publicadas. La cobertura es la de los endpoints documentados abajo; no una garantía de anonimato o de ausencia de telemetría.

## Resultado de las reglas

- 5 bloqueos nuevos de Nintendo.
- 2 bloqueos de telemetría PlayStation conservados.
- 21 bloqueos redundantes con HaGeZi Pro eliminados.
- 3 reglas redundantes con sus padres en la principal eliminadas.
- 3 bloqueos preexistentes de promociones PS3 trasladados a la principal.
- 0 bloqueos restantes coincidentes con las fuentes externas comparadas, considerando dominio y ancestros.
- 0 duplicados exactos o subdominios redundantes del mismo tipo entre ambos archivos.
- Excepciones Fire TV y demás permisos conservan su cobertura.

## Cobertura de consolas y plataformas

| Plataforma | Resultado |
| --- | --- |
| PlayStation | Se conservan `telemetry-console.api.playstation.com` y `telemetry-cii.api.playstation.com`. No se afirma cobertura completa de cada generación. |
| PS3 | `mercury.dl.playstation.net`, `nsx.np.dl.playstation.net` y `nsx-e.np.dl.playstation.net` son bloqueos preexistentes de promociones/vistas de tienda; pasan a la principal. |
| Nintendo Switch | Se agregan `receive-lp1.dg.srv.nintendo.net`, `receive-lp1.er.srv.nintendo.net` y `realtime-receive-lp1.dg.srv.nintendo.net`. |
| Nintendo Switch 2 | Se agregan `receive.p01.lp1.dg.srv.nintendo.net` y `receive.p01.lp1.er.srv.nintendo.net`. |
| Xbox / Windows | `vortex.data.microsoft.com` y `vortex-win.data.microsoft.com` ya cubiertos por Pro; `v10.events.data.microsoft.com` cubierto por `events.data.microsoft.com` en el respaldo de Native Vendors. |
| Steam / Steam Deck | `crash.steampowered.com` ya cubierto por Pro. No implica bloquear toda la telemetría de SteamOS ni de cada juego. |
| Juegos con GameAnalytics / Unity | Los dos endpoints GameAnalytics y el de Unity retirados ya están cubiertos por dominios padre en Pro. |
| Portátiles Windows (ROG Ally, Legion Go, etc.) | La cobertura Windows anterior es parcial; no se agregan endpoints del fabricante sin evidencia suficiente. |
| PSP/Vita, DS/3DS, Wii/Wii U, Sega, Atari y otras retro | No se validaron nuevos endpoints de telemetría para agregar. Esto no demuestra que no exista recopilación; depende de conectividad, firmware y juegos. |

No se agregan `sprofile-lp1.cdn.nintendo.net` (función incierta en la fuente), pruebas de conexión, autenticación, eShop, CDN de actualizaciones ni servidores de partidas. Tampoco se copian listas que bloquean servicios completos de Xbox Live.

## Fuentes de clasificación

- [Game Console Adblock List — DandelionSprout](https://github.com/DandelionSprout/adfilt/blob/master/GameConsoleAdblockList.txt): endpoints de PlayStation, reportes Nintendo y distinción entre promociones y telemetría.
- [NintendoClients — Telemetry Servers](https://github.com/kinnay/NintendoClients/wiki/Telemetry-Servers): documentación comunitaria de investigación de protocolos; diferencia Switch y Switch 2. No es documentación oficial de Nintendo.
- [Nintendo Wiki — Telemetry](https://nintendo-wiki.pretendo.network/docs/switch/telemetry.html): reportes de uso y de errores.
- [Microsoft — eventos de juegos](https://learn.microsoft.com/en-us/gaming/gdk/docs/services/player-data/stats-leaderboards/event-based/events/live-game-events): eventos enviados al endpoint Vortex.
- [Microsoft — datos de Xbox](https://www.microsoft.com/en-us/privacy/data-collection-xbox): datos requeridos y opcionales.
- [Valve — reporte con registro del emisor de fallos](https://github.com/ValveSoftware/steam-for-linux/issues/6459): endpoint de crash reporting.
- [HaGeZi FAQ](https://github.com/hagezi/dns-blocklists/blob/main/FAQ.md): bloquear telemetría de Windows/Xbox puede afectar funciones como historial de logros.

Estas fuentes permiten clasificar candidatos, pero no sustituyen pruebas de funcionamiento en las consolas del usuario.

## Fuentes comparadas

Se descargaron las tres fuentes públicas en memoria desde Zorin. Native Vendors se leyó del respaldo del 25/09/2026; no se comprobó su archivo actual en el router.

| Fuente | Reglas parseadas | SHA-256 del texto comparado |
| --- | ---: | --- |
| HaGeZi Pro | 228668 | `97dfee3ed05ec34d5167a01b2944cad77182a6f953996d7317e5d06dd0ddaf05` |
| HaGeZi DoH | 3334 | `8b43f8aa8296990d53f1bfce873b3d4623efcc213bcfcae69e2c6f956c202dc3` |
| Phishing Army | 149528 | `30d750f5be0c3643ed3ab73712e1ca90ab6004dfcb5ed8a6bcf01979fec9a1b0` |
| Native Vendors respaldo 2026-09-25 | 209 | `c1fd542355a1cac855803d7f0cc5d8316a3f6428441cb1006bf59c7f7c8249b8` |

URLs públicas:

- https://cdn.jsdelivr.net/gh/hagezi/dns-blocklists@latest/adblock/pro.txt
- https://cdn.jsdelivr.net/gh/hagezi/dns-blocklists@latest/adblock/doh.txt
- https://adguardteam.github.io/HostlistsRegistry/assets/filter_18.txt

## Método y límites

Se compararon reglas simples `||dominio^` y dominios de Phishing Army; se comprobaron coincidencias exactas y cobertura por dominios padre. Todas las líneas activas de las cuatro fuentes entraron en esos formatos. La revisión interna separó permisos, bloqueos y `$badfilter`; no trató una excepción como un bloqueo. No se ejecutó el motor de AdGuard ni se auditaron todas las opciones globales, reglas por cliente o servicios bloqueados del router.

La cobertura por un padre elimina redundancias como `api.gameanalytics.com` bajo `gameanalytics.com`. Los dominios de Phishing Army también se compararon por ancestros de forma conservadora; no hubo coincidencias con los bloqueos conservados.

Las eliminaciones cubiertas por Pro crean una dependencia explícita de esa lista. Si se desactiva Pro, sus bloqueos dejan de estar garantizados por estos archivos. Las fuentes cambian: el resultado corresponde a los hashes anteriores.

## Reglas eliminadas por redundancia

HaGeZi Pro cubre los siguientes bloqueos retirados de ambos archivos:

- `||beacons3.gvt2.com^`
- `||beacons4.gvt2.com^`
- `||beacons5.gvt2.com^`
- `||beacons.gcp.gvt2.com^`
- `||beacons.gvt2.com^`
- `||beacons2.gvt2.com^`
- `||beacons5.gvt3.com^`
- `||analytics.mercadolibre.com^`
- `||events.mercadolibre.com^`
- `||analytics.mercadopago.com^`
- `||events.mercadopago.com^`
- `||analytics.mercadopago.com.ar^`
- `||statistical-report.djiservice.org^`
- `||copilot-telemetry.githubusercontent.com^`
- `||sentry-webapp.quillbot.com^`
- `||collector.quillbot.com^`
- `||telemetry.desktopcommander.app^`
- `||improving.duckduckgo.com^`
- `||api.gameanalytics.com^`
- `||sandbox-api.gameanalytics.com^`
- `||collect.analytics.unity3d.com^`

Redundancias internas eliminadas:

| Regla retirada | Regla que conserva la cobertura |
| --- | --- |
| `||events.stats.openai.com^` | `||stats.openai.com^` |
| `@@||player.twitch.tv^` | `@@||twitch.tv^` |
| `@@||dns.adguard-dns.com^` | `@@||adguard-dns.com^` |

No se modificó la configuración del router ni se forzó una actualización de suscripciones. No se generaron archivos temporales en el router o Zorin durante esta revisión.
