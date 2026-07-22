# Catálogo Mandi Chips - Project Documentation

Este documento sirve como memoria y guía de arquitectura para optimizar el análisis del proyecto en futuros cambios. Describe la estructura, los datos y las características clave implementadas en el catálogo.

## 🛠 Stack Tecnológico
- **Core:** HTML5, CSS3 (Vanilla) y JavaScript (ES6+ sin frameworks).
- **Estilos:** Variables CSS, animaciones personalizadas (keyframes), Flexbox/Grid y diseño responsivo adaptado primariamente a móvil (Mobile First).
- **Tipografía y Recursos:** Google Fonts (`Outfit` para títulos, `Inter` para cuerpo), FontAwesome para iconos.

## 📁 Estructura del Archivo `index.html`
Toda la aplicación es un "Single Page" que vive en `index.html`. Se divide en las siguientes secciones principales:

1. **Variables y CSS (`<style>`)**: Define la paleta de colores (Rojo, Dorado, fondos oscuros `#0a0a0a`), animaciones globales, tarjetas de producto y estado del modal.
2. **Navegación (`<nav>`)**: Barra superior fija con buscador y botón de carrito ("Mi Orden").
3. **Hero Section (`.hero`)**: Encabezado principal con el logo, título y animación de partículas de fondo.
4. **Catálogo (`.catalog`)**: Inyección dinámica de categorías (`maxis`, `mandis`, `especialidades`, `patacones`, `arepas`).
5. **Secciones Inyectadas Promocionales**: Banners dinámicos (Ej: "Mandi Martes") renderizados en medio del catálogo (después de la categoría `mandis`).
6. **Zoom Modal (`#zoom-ov`)**: Modal para ver el detalle de los productos, ingredientes y galería multimedia.
7. **Popup de Recomendación (`#recommend-popup`)**: Pop-up flotante que reacciona al scroll al pasar por las promociones.
8. **Drawer del Carrito (`#order-drawer`)**: Menú lateral deslizable donde se gestiona el pedido.
9. **Lógica JS (`<script>`)**: Maneja todo el estado del carrito, renderizado del DOM, observadores de scroll (IntersectionObserver) y generación del enlace a WhatsApp.

## 💾 Estructura de Datos (JavaScript)

El inventario está definido en la constante `products`. Un producto típico tiene este formato:
```javascript
{
    id: 18, 
    name: "DORI CHIPS GRANDE", 
    cat: "especialidades", 
    desc: "Papa • Carne desmechada • Pollo desmechado...", 
    price: 30000, 
    image: "IMAGENS/DORICHIPS GRANDE.jpg", 
    // Opcional: Para categorías como "especialidades"
    gallery: [
        { type: 'image', src: 'IMAGENS/DORICHIPS GRANDE.jpg' },
        { type: 'video', src: 'hero-video.mp4', thumb: 'IMAGENS/DORICHIPS GRANDE.jpg' }
    ]
}
```

El estado del carrito vive en la variable global `order` (arreglo de objetos).
```javascript
{
    product: { /* Objeto Producto */ },
    qty: 1,
    sauces: ["Rosada", "BBQ"],
    note: "Sin cebolla"
}
```

## ✨ Características y Funcionalidades Clave Añadidas Recientemente

- **Animación "Fly to Cart":** Al agregar un producto, una esfera roja vuela desde el botón "Quiero Este" hacia el icono del carrito en el navbar.
- **Galería Multimedia "Salsa Rosada":** Los productos de *Especialidades* tienen una galería horizontal interactiva (imágenes/videos) dentro del modal de Zoom. Su diseño visual (scroll y bordes activos) utiliza tonos rosados, sombras rojas e imágenes inactivas en escala de grises.
- **Notas de Orden:** Dentro del carrito ("Mi Orden"), debajo del selector de salsas, el usuario puede añadir notas específicas (ej. exclusión de ingredientes) que se anexan automáticamente al mensaje de WhatsApp.
- **Pop-up Inteligente (Recomendación):** Un pop-up flotante recomendando la "Mandi Burger" aparece cuando el usuario hace scroll y la sección del banner `promo-grid` entra en la pantalla. Este popup incluye un botón con ancla que dirige al cliente y resalta el producto específico (ID 22).

## 🚀 Flujo de Orden y WhatsApp
El sistema calcula los totales dinámicamente y genera un string amigable con emojis. Luego codifica este string y lo envía a través del protocolo `https://wa.me/{numero}?text={msg}` al finalizar el pedido.

---
*Nota para Inteligencias Artificiales / Desarrolladores:*
Lee este documento antes de hacer modificaciones estructurales para mantener el diseño visual premium y las convenciones actuales (ej. NO crear múltiples archivos JS o CSS; mantener la lógica modular dentro del IIFE actual).
