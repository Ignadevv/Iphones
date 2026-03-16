# 📱 iStore Demo — Web de Venta de iPhones

Web de demostración moderna para tiendas que venden iPhones.
Lee el catálogo automáticamente desde **Google Sheets** y facilita
el contacto por **WhatsApp** para cerrar ventas.

---

## 🚀 Cómo configurar en 5 minutos

### 1. Crear el Google Sheets

Crea una nueva hoja de cálculo en Google Sheets con estas columnas
**exactamente en este orden** (fila 1 = encabezados, datos desde fila 2):

| A | B | C | D | E | F | G |
|---|---|---|---|---|---|---|
| Modelo | Precio | Almacenamiento | Color | Stock | URL_imagen | Descripción |
| iPhone 15 Pro | 999 | 128GB | Titanio Negro | 5 | https://… | Chip A17 Pro… |
| iPhone 14 | 699 | 256GB | Medianoche | 0 | https://… | Chip A15… |

> ⚠️ **Importante:** El precio debe ser solo el número (ej: `999`, no `$999`).
> Si Stock = 0, el producto se muestra como **Agotado** automáticamente.

---

### 2. Publicar la hoja

1. En el Sheet, ve a **Archivo → Compartir → Publicar en la web**
2. Selecciona **Hoja 1** y formato **Valores separados por comas (.csv)**
3. Haz clic en **Publicar**
4. Copia el **ID** de la URL de tu hoja. Es el string largo entre `/d/` y `/edit`:
   ```
   https://docs.google.com/spreadsheets/d/[ESTE_ES_EL_ID]/edit
   ```

---

### 3. Configurar la web

Abre `index.html` y busca el bloque `CONFIG` al final del archivo:

```javascript
const CONFIG = {
  SHEET_ID: "1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgVE2upms", // 👈 Reemplaza con tu ID
  WHATSAPP_NUMBER: "51987654321",   // 👈 Número con código de país, sin + ni espacios
  STORE_NAME: "iStore",            // 👈 Nombre de la tienda
  CURRENCY_SYMBOL: "$",            // 👈 Símbolo de moneda (S/ para Perú, $ para USD, etc.)
};
```

---

### 4. Publicar la web

La web es un solo archivo `index.html` — no necesita servidor.
Puedes publicarla en:

- **GitHub Pages** (gratis): Sube `index.html` a un repo y activa Pages en Settings.
- **Netlify** (gratis): Arrastra `index.html` a netlify.com/drop.
- **Cualquier hosting estático**.

---

## 🖼️ Cómo agregar imágenes de productos

### Opción A — Google Drive (recomendado)
1. Sube la imagen a Google Drive
2. Comparte el archivo como "Cualquiera con el enlace puede ver"
3. Obtén el ID del archivo de la URL: `drive.google.com/file/d/[ID]/view`
4. Convierte el enlace a formato directo:
   ```
   https://drive.google.com/uc?export=view&id=[ID]
   ```
5. Pega esa URL en la columna **URL_imagen** del Sheet

### Opción B — Imágenes de Apple Store
Puedes usar directamente las URLs de imágenes de apple.com/shop, por ejemplo:
```
https://store.storeimages.cdn-apple.com/4982/as-images.apple.com/is/iphone-15-pro-finish-select-202309-6-1inch-blacktitanium?wid=800&hei=800&fmt=p-jpg&qlt=80
```

---

## 📁 Estructura del proyecto

```
istore-demo/
└── index.html      ← Todo en un solo archivo (HTML + CSS + JS)
└── README.md       ← Este archivo
```

---

## ✨ Funciones incluidas

| Función | Estado |
|---|---|
| Carga desde Google Sheets | ✅ |
| Skeletons de carga | ✅ |
| Datos de ejemplo (si el Sheet falla) | ✅ |
| Filtro por modelo | ✅ |
| Filtro por almacenamiento | ✅ |
| Tarjetas con imagen / precio / specs | ✅ |
| Badge "Agotado" si stock = 0 | ✅ |
| Carrito lateral (drawer) | ✅ |
| Eliminar productos del carrito | ✅ |
| Mensaje automático a WhatsApp | ✅ |
| Diseño responsive (móvil + escritorio) | ✅ |
| Animaciones suaves | ✅ |
| Sin dependencias externas | ✅ |

---

## 🎨 Personalización del diseño

Puedes cambiar colores editando las variables CSS al inicio del `<style>`:

```css
:root {
  --accent:  #0071e3;  /* Color principal (botones, chips activos) */
  --bg:      #f5f5f7;  /* Fondo de la página */
  --surface: #ffffff;  /* Fondo de tarjetas y drawer */
  --text:    #1d1d1f;  /* Texto principal */
}
```

Para cambiar el nombre y logo de la tienda, edita el `<header>` en el HTML.

---

## ❓ Preguntas frecuentes

**¿Se actualiza automáticamente cuando edito el Sheet?**
Sí. Cada vez que alguien abre la web, se cargan los datos más recientes del Sheet.

**¿Necesito saber programar para adaptarlo?**
Solo necesitas cambiar 2-3 valores en el bloque CONFIG. El resto es automático.

**¿Funciona en móvil?**
Sí, el diseño es completamente responsive.

**¿Puedo tener más de una tienda con este código?**
Sí. Cada tienda tiene su propio Sheet (con su SHEET_ID) y su número de WhatsApp.
Solo cambia esos dos valores para cada cliente.

---

*Demo creada con HTML + CSS + JavaScript puro. Sin frameworks, sin backend.*
