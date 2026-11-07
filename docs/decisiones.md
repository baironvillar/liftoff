# Decisiones

Cada decisión con su porqué. Si una cambia, no se borra: se marca como
reemplazada y se agrega la nueva abajo.

## 1. Oxc (`vp check`) y no Biome

Vite+ hace formato, lint y tipos en una pasada con Oxfmt, Oxlint y tsgolint, y
flotas ya lo usa así. Mezclar Biome en el mismo repo deja `vp check` casi vacío
y dos configuraciones que discuten. En las apps, la puerta del kit es
configurable: Starless, que usa Biome, la apunta a `biome check` + `bun test`.

## 2. Repo propio, no un paquete dentro de flotas

El kit es para varias apps, y su versión y su historia no tienen que ver con
las de flotas. flotas lo consume por pull request, como cualquier otra app.

## 3. Bun y TypeScript sin build mientras sea privado

Bun ejecuta TypeScript directo, así que instalar desde git funciona sin
compilar. `vp pack` agrega un paso que hoy no resuelve nada; entra cuando se
publique en npm.

## 4. El CLI en la raíz del repo

Bun no instala un subdirectorio de un repo git. Si el CLI viviera en
`packages/cli`, no se podría instalar con `github:baironvillar/liftoff`.

## 5. No se reinventa `tauri-action` ni el updater

`tauri-action` v1 ya compila, firma, crea la release, sube instaladores y firmas,
renombra los assets (`releaseAssetNamePattern`) y genera `latest.json`. El kit
valida antes y verifica después.

## 6. La lógica en el CLI, no en el YAML

Starless tiene la lógica en PowerShell dentro del workflow, y varias fallas
vinieron de ahí (un `exit` con el código de git, CRLF en las notas). En
TypeScript se prueba con tests, corre igual en local y en la CI, y en Windows y
Linux.

## 7. Windows y Linux primero; macOS después

Firmar y notarizar en macOS exige una cuenta de Apple Developer y un flujo
propio. Se hace cuando Windows y Linux estén bien hechos.

## 8. Primeros consumidores: flotas (web) y Starless (escritorio)

flotas no va a tener cliente de escritorio. Usa el núcleo y el target `web`. El
target `tauri` lo estrena Starless cuando migre.
