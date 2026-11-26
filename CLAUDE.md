# Portafolio ARISTI — guía del proyecto

Portafolio de **Santiago Aristizábal Márquez (ARISTI)**, filmmaker, fotógrafo y comunicador en Cali, Colombia.
Publicado con GitHub Pages en **https://aristipsd.github.io** (repo `aristipsd/aristipsd.github.io`, rama `main`, raíz).
El dueño habla español: responde siempre en español.

## Estructura
- `index.html` — toda la página (HTML + CSS + JS en un solo archivo, sin dependencias ni build).
- `assets/img/` — portada, retrato, logo (`logo-blanco.png`, `logo-negro.png`), favicon, imagen para redes (`og.jpg`).
- `assets/fotos/NN.jpg` (2000 px) y `NN-sm.jpg` (900 px) — galería.
- `assets/video/<slug>.mp4` (720p), `<slug>-poster.jpg`, `<slug>-prev.mp4` (clip de 6 s sin audio), `teaser.mp4`.
- `assets/personaje/cara-1..10.png` — caras del personaje (1 frente, 2 tres cuartos, 3 perfil, 4 espalda, 5 serio, 6 feliz, 7 bravo, 8 sorpresa, 9 triste, 10 presumido) y `sticker.png`.
- `assets/logos/` — logos de clientes en blanco sobre transparente.
- `.server.js` — servidor local solo para previsualizar (`node .server.js`, puerto 8771). No se sube.

## Dónde se edita el contenido
Al final de `index.html`, en el bloque "TU CONTENIDO":
- `REEL_YOUTUBE` — link embed del reel (vacío = muestra `teaser.mp4`).
- `PROYECTOS` — cada proyecto con `videos: [[slug, título], ...]`; la portada es el primer video.
- `FOTOS` — `[número, título, categoría]`; categorías: Cabaret, Danza, Retrato, Gastronomía.
- `CARAS` y `FRASES` — personaje acompañante.
Textos de secciones (sobre mí, experiencia, servicios, contacto) están directamente en el HTML.

## Material original
Los archivos sin procesar están en la carpeta de arriba (`..\FOTOGRAFIA`, `..\PROYECTOS`, `..\LOGO`, `..\PERSONAJE`, `..\PORTADA`, `..\EXPERIENCIA`). No se suben a GitHub.

## Cómo agregar videos o fotos nuevos
Usar ffmpeg (instalado vía winget; la PC tiene GPU NVIDIA → `h264_nvenc`):
- Video completo: `-vf "scale=trunc(iw*sar/2)*2:ih,setsar=1,scale='if(gt(iw,ih),-2,720)':'if(gt(iw,ih),720,-2)',fps=30" -c:v h264_nvenc -preset p6 -rc vbr -cq 30 -b:v 0 -maxrate 2.5M -bufsize 5M -pix_fmt yuv420p -c:a aac -b:a 96k -movflags +faststart`
- Póster: un fotograma al 35 % de la duración, 960 px lado largo, `-q:v 4`.
- Preview: 6 s desde el 30 %, lado corto 480 px, `-cq 33 -maxrate 1M -an`.
- Fotos: 2000 px (`-q:v 4`) y 900 px (`-q:v 5`) lado largo.
GitHub rechaza archivos de más de 100 MB; mantener cada video muy por debajo.
En PowerShell 5.1, los scripts .ps1 con tildes/ñ deben guardarse con BOM o buscar archivos con comodines.

## Publicar cambios
Desde esta carpeta: `git add -A`, `git commit -m "..."`, `git push`. GitHub Pages se actualiza en 1–2 minutos.
Si `git`/`gh` no se encuentran en PowerShell, refrescar PATH:
`$env:Path = [Environment]::GetEnvironmentVariable('Path','Machine') + ';' + [Environment]::GetEnvironmentVariable('Path','User')`
Probar en escritorio y en celular (375 px) antes de subir: no debe haber scroll horizontal.
