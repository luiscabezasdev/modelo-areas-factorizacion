# Modelo de Áreas para Factorización

Simulador educativo interactivo para visualizar la factorización de polinomios cuadráticos (a² + pa + q) usando el modelo geométrico de áreas.

Página en vivo: _(agrega aquí tu URL una vez publicada)_

## Tecnologías
- HTML + JavaScript puro
- Tailwind CSS (vía CDN)
- Font Awesome (vía CDN)

## Cómo correrlo localmente
Abre `index.html` directamente en tu navegador, o sirve la carpeta con cualquier servidor estático.

## Changelog

### 2026-08-21 — Corrección de bugs en el modo "Rompecabezas"
- **Fix:** las fichas del rompecabezas se reiniciaban por completo (perdiendo lo agregado/armado) cada vez que se cambiaba de modo de visualización (Auto ↔ Rompecabezas), aunque el polinomio no hubiera cambiado. Ahora solo se reinician cuando `p` o `q` realmente cambian.
- **Fix:** al arrastrar una ficha desde el "Banco de Fichas" hasta el tablero, el cálculo de su posición mezclaba dos sistemas de coordenadas distintos (uno relativo al banco, otro relativo al tablero), lo que hacía que la ficha "saltara" a una posición incorrecta o quedara fuera del tablero y regresara silenciosamente al banco. Corregido para usar siempre el mismo sistema de referencia.
- **Fix:** el "doble clic/toque para girar" una ficha nunca funcionaba, porque el temporizador que detecta el doble toque se reiniciaba en cada redibujado de la ficha. Ahora el estado persiste en el objeto de la ficha.
- **Fix:** los campos numéricos de p y q permitían valores mayores a los que soportaban sus sliders (30 y 50 vs. 15 y 24), desincronizando el número mostrado con la posición del control deslizante. Ahora los rangos coinciden.
- Se unificó la generación de IDs de fichas en una sola función auxiliar (`nextTileId()`) para mayor claridad del código.
