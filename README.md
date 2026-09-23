# danieta.com

Landing estático del dominio raíz y aplicación Android privada. La aplicación **A la mesa** continúa en su repositorio y Worker propios, bajo la ruta `/alamesa*`.

## Preparar el proyecto

```powershell
npm install
```

## Probar en local

```powershell
npm run dev
```

## Publicar

```powershell
npm run deploy
```

El comando crea o actualiza el Worker `danieta-home`. Después, en Cloudflare:

1. Abre **Workers & Pages → danieta-home → Settings → Domains & Routes**.
2. Añade `danieta.com` como **Custom Domain**.
3. Conserva en el Worker `alamesa` la ruta `danieta.com/alamesa*`.

La ruta específica de `alamesa` tiene prioridad sobre el Worker asociado al dominio completo.

## Aplicación Android

La carpeta `android/` contiene una aplicación nativa mínima que muestra `https://danieta.com` dentro de una WebView. El contenido se actualiza al publicar la web, sin volver a instalar la APK.

Para compilar una APK instalable de desarrollo:

```powershell
cd android
.\gradlew.bat assembleDebug
```

La APK se genera en `android/app/build/outputs/apk/debug/app-debug.apk`.

El workflow **Build Android APK** ejecuta la misma compilación cuando cambia la carpeta `android/` y deja la APK como artefacto descargable en GitHub Actions. El workflow también se puede ejecutar manualmente.

### Firmado privado estable

La APK de desarrollo está firmada con una clave de depuración. Antes de distribuir una versión definitiva, crea una clave privada fuera del repositorio y guarda sus datos como secretos de GitHub. Nunca subas archivos `.jks`, `.keystore` ni contraseñas al repositorio.

### Despliegue automático de la web

El workflow **Deploy web** publica la landing después de cada push a `main`. Requiere estos secretos del repositorio:

- `CLOUDFLARE_API_TOKEN`
- `CLOUDFLARE_ACCOUNT_ID`

Mientras no estén configurados, el workflow omite la publicación sin hacer fallar el resto de comprobaciones.

## Añadir otra plataforma

Duplica la tarjeta `.app-card` de `public/index.html` y cambia su icono, texto y URL. La cuadrícula se adapta automáticamente al número de aplicaciones y al tamaño de la pantalla.
