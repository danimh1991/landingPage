# danieta.com

Landing estático del dominio raíz. La aplicación **A la mesa** continúa en su repositorio y Worker propios, bajo la ruta `/alamesa*`.

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

## Añadir otra plataforma

Duplica la tarjeta `.app-card` de `public/index.html` y cambia su icono, texto y URL. La cuadrícula se adapta automáticamente al número de aplicaciones y al tamaño de la pantalla.
