# winclap-dashboards

Repo general para dashboards de clientes de Winclap, servidos vía GitHub Pages.

A diferencia de `rappi-dashboards` (repo dedicado exclusivamente a Rappi, con un subfolder por sub-unidad de Rappi), este repo tiene una granularidad más general: **un folder de primer nivel por cliente**, y dentro de cada uno, un folder por dashboard específico.

## Estructura

```
winclap-dashboards/
├── README.md
├── {cliente}/
│   ├── {nombre-dashboard}/
│   │   ├── index.html      ← password gate
│   │   └── dashboard.html  ← contenido real del dashboard
│   └── {otro-dashboard}/
│       ├── index.html
│       └── dashboard.html
├── {otro-cliente}/
│   └── {nombre-dashboard}/
│       ├── index.html
│       └── dashboard.html
```

## Convenciones

- **Nombres de folder**: minúsculas, guiones (`-`), sin espacios. Ej: `shellbox/biweekly-report/`, `lulobank/wow-analysis/`.
- **Password gate**: cada dashboard tiene su propio `index.html` con un prompt de contraseña en JS (no es seguridad fuerte, pero evita acceso casual). La contraseña se define por dashboard.
- **Deploy**: GitHub Pages sirve desde `main` / root. URL resultante: `https://winclap.github.io/winclap-dashboards/{cliente}/{dashboard}/`.
- **Repo público**: el código HTML es visible en el repo, pero el acceso al dashboard publicado queda atrás del password gate. Igual que el patrón usado en `rappi-dashboards`.

## Cómo se generan los dashboards

Los dashboards se generan con la skill `client-dashboard-builder`, que:
1. Recibe el contenido/datos a mostrar y el nombre de cliente + dashboard.
2. Genera el HTML con password gate + dashboard.
3. Hace commit y push a este repo, respetando la estructura `{cliente}/{dashboard}/`.
4. Puede re-ejecutarse para actualizar datos o cambiar estilos de un dashboard existente, una vez que tiene el token del repo.

## Credenciales

El token de GitHub para pushear a este repo se pide una vez (al team member que ejecuta la skill) y no se hardcodea en el repo.
