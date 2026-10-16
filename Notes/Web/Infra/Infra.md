---
graph-size: 200
---
#module #web

Orchestration et terminaison TLS.

## Fichiers

- <a href="#vault://../web/compose.yaml" class="LinkRelativeTo">compose.yaml</a> — orchestration : service web + service `certs` (génère un cert self-signed au premier boot) + nginx
- <a href="#vault://../web/nginx/nginx.conf" class="LinkRelativeTo">nginx/nginx.conf</a> — reverse proxy, redirect HTTP→HTTPS, terminaison TLS

## Connexions

- Orchestre [[Server]]
