# Módulo 8 - Cloud: Azure con Docker y GitHub Actions

App Vite + React + TypeScript empaquetada con Docker y desplegada en Azure App Service con GitHub Actions.

## Enlaces

- **App desplegada:** modulo08-cloud-azure-danivegi-dvazasekh8eje8hm.spaincentral-01.azurewebsites.net
- **Imagen en GitHub Container Registry:** https://github.com/danivegi/modulo08-cloud-azure/pkgs/container/modulo08-cloud-azure

> La primera carga puede tardar un poco si el contenedor estaba detenido.

## Cómo se despliega

Cada merge a `main` ejecuta el workflow `.github/workflows/deploy.yml`, que tiene dos jobs:

1. **build:** construye la imagen con el `Dockerfile` (multi-stage: build con Node y servido con Nginx) y la publica en GitHub Container Registry (GHCR) con los tags `latest` y el hash del commit.
2. **deploy:** con `azure/webapps-deploy`, indica a la Web App que despliegue la imagen del commit actual.

## Infraestructura en Azure

- Azure App Service (Web App para contenedores Linux), plan gratuito F1.
- Imagen pública en GHCR, sin credenciales de registro.

## Credenciales del workflow

- `GITHUB_TOKEN`: lo genera GitHub automáticamente y se usa para publicar en GHCR.
- `AZURE_WEBAPP_PUBLISH_PROFILE`: secret del repositorio con el perfil de publicación de la Web App.