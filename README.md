# Bie — Taller de Prendas 3D

Herramienta en el navegador para diseñar mockups de ropa en 3D (`index.html`, sin instalación).

- **Prendas y cortes**: polos (clásico, cuello V, oversize, slim, crop, manga larga, sin mangas), poleras (con capucha, hoodie oversize, cuello redondo, crop hoodie), pantalones (recto, skinny, ancho, jogger, cargo, acampanado) y shorts (clásico, deportivo, bermuda, cargo). Se puede combinar una parte superior y una inferior.
- **Ajuste**: holgura, largo, manga, escote, hombro caído, ancho de pierna, basta, tiro, talla S–XL y contextura del maniquí. La prenda se recalcula sobre el cuerpo.
- **Color y tela**: color principal y de detalles (cuello, puños, pretina), telas algodón, felpa, denim y nylon.
- **Estampados**: sube imágenes, dibuja o escribe texto; el estampado se proyecta sobre la superficie 3D y sigue sus curvas. Se arrastra sobre la prenda, se escala, rota, refleja y duplica.
- Deshacer/rehacer, vistas de cámara, giro automático y captura del mockup. El diseño se guarda en el navegador.

Hecho con three.js (r128) y `DecalGeometry`. Para usarlo localmente basta abrir `index.html` dentro de una página HTML o servirlo con cualquier servidor estático.

## Camiseta 360 (`camiseta.html`)

Mockup de camiseta en blanco sobre fondo blanco de estudio, que gira 360°, con costuras, dobladillo doble, cuello en rib y etiqueta interior. Permite cambiar el corte (regular, oversize, slim, boxy crop, cuello V, longline, manga larga, sin mangas) y sus proporciones, color, tela e hilo; agregar diseños en capas (imagen, dibujo, texto) con recorte y quitado de fondo, y ubicaciones estándar de estampado. Exporta una ficha para la diseñadora (4 vistas, medidas, colores y posición de cada diseño) y las vistas sueltas en PNG.
