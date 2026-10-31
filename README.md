# Teseliso y Alhambra

Dos generadores de teselaciones que funcionan en el navegador. Cada uno es una única página HTML, sin instalación ni servidor.

| Programa | Qué genera | Archivo |
|---|---|---|
| **Teseliso** | Teselaciones con **una sola forma** repetida, al estilo de Escher | `arabesco.html` |
| **Alhambra** | Lazos islámicos con **muchas formas combinadas**: estrellas, rosetas y rombos | `alhambra.html` |

Los dos generan diseños al azar y permiten elegir el tipo de teselación y la paleta de colores. También se puede desplazar el dibujo arrastrándolo y copiar la vista actual como SVG.

---

## Teseliso

### Qué es

Teseliso dibuja **teselaciones isoédricas**. En ellas todas las piezas son copias de una misma forma, y cualquier pieza puede llevarse sobre cualquier otra con una simetría del patrón completo. Son las teselaciones de los dibujos periódicos de Escher.

### Fundamento matemático

- **Grünbaum y Shephard (1977)** demostraron que existen exactamente **93 tipos** de teselaciones isoédricas, numerados IH1–IH93.
- **Heesch** había clasificado antes los **28 tipos** que admiten piezas asimétricas.
- **Escher** desarrolló por su cuenta un sistema parecido en sus cuadernos.
- Teseliso incluye los **81 tipos** que admiten una forma propia. Los 12 restantes son variantes degeneradas de otros tipos.

Cada tipo parte de un polígono base (triángulo, cuadrilátero, pentágono o hexágono). Sus lados pueden deformarse según cuatro reglas, que la ficha indica con una letra:

| Letra | Tipo de borde | Restricción |
|---|---|---|
| **J** | Libre | Cualquier curva |
| **U** | Espejo | Simétrico respecto a su punto medio por reflexión |
| **S** | Giro | Simétrico por un giro de 180° alrededor de su centro |
| **I** | Recto | Debe ser un segmento recto |

### Cómo se genera una pieza

1. Se toman los parámetros del tipo elegido y se deforman al azar. Cambian las proporciones y los ángulos del polígono base.
2. Cada borde se curva con una serie de senos. Las simetrías U y S se garantizan eligiendo solo armónicos pares o impares, según el caso.
3. Si el contorno se cruza consigo mismo, se rechaza y se vuelve a generar con menos curvatura.
4. La pieza se repite por el plano con las simetrías propias del tipo.

### Controles

- **Nueva tesela** (`Espacio`): nueva forma con el mismo tipo.
- **Tipo al azar** (`T`) y **Todo al azar**, que cambia también la paleta y el coloreado.
- **Tipo de teselación:** desplegable agrupado por polígono base, o el catálogo de miniaturas de los 81 tipos. Las flechas `←` `→` pasan al tipo anterior o siguiente.
- **Paleta:** Escher, Alhambra, Delft, Bauhaus, Arrecife, Otoño, Pizarra, Pastel, Nocturno, Tinta, Jade, o una **propia** con selectores de color.
- **Coloreado:**
  - *Teselado:* la coloración propia del tipo; dos piezas vecinas nunca comparten color.
  - *Orientación:* un color por cada orientación de la pieza.
  - *Azar:* color aleatorio por pieza.
  - *Único:* todas las piezas del mismo color.
- **Deslizadores:** curvatura de los bordes, complejidad del contorno, deformación del polígono, tamaño de pieza y grosor de línea.
- **Opciones:** mostrar el polígono base, resaltar la pieza prototipo y relieve suave.
- **Ficha técnica:** código IH, polígono, número de orientaciones, tipos de borde y semilla del diseño.

### Requisitos

Teseliso carga la biblioteca **Tactile** (Craig S. Kaplan, licencia BSD de 3 cláusulas) desde jsDelivr. Necesita conexión a internet la primera vez que se abre.

---

## Alhambra

### Qué es

Alhambra genera **lazos nazaríes e islámicos**, patrones que combinan varias formas a la vez. Se basa en el **método de Hankin** (1925), sistematizado después por Craig S. Kaplan:

1. Se parte de una **trama oculta** de polígonos.
2. Desde el punto medio de cada lado salen dos rectas con el mismo **ángulo de contacto**.
3. Las rectas se cortan dentro de cada polígono y dibujan una **estrella**. Alrededor de cada vértice de la trama forman una **roseta**.
4. Si las rectas se separan en el borde, aparecen **rombos** entre las estrellas.

Algunos ejemplos conocidos:

- Trama **4.8.8** a 67,5°: la estrella de ocho del Salón de Comares.
- Trama **3.12.12** a 60° con rosetas: el gran lazo de doce.
- Trama **16.16** con rosetas: el lazo de dieciséis de los zócalos nazaríes.

### Las 24 tramas

La notación de las tramas (por ejemplo 3.12.12) indica qué polígonos se encuentran en cada vértice.

**Arquimedianas (11).** Son todas las teselaciones con polígonos regulares y un solo tipo de vértice:
4.8.8 · 3.12.12 · 4.6.12 · 3.4.6.4 · 3.6.3.6 · 3.3.3.4.4 · 6.6.6 · 4.4.4.4 · 3.3.3.3.3.3 · 3.3.4.3.4 (cuadrado achatado) · 3.3.3.3.6 (hexágono achatado).

**Derivadas (9).** Salen de dividir algunos polígonos de las arquimedianas en otros regulares. Un dodecágono se divide en un hexágono, 6 cuadrados y 6 triángulos; un hexágono, en 6 triángulos. A veces se divide solo uno de cada dos o de cada tres polígonos. Así se obtienen mezclas de vértices del tipo 2- y 3-uniforme.

**Girih y no periódicas (4):**

| Trama | Descripción |
|---|---|
| **Girih 10** | Decágonos y pajaritas. Con rosetas da el girih persa: estrella de diez rodeada de pentágonos. |
| **16.16** | Hexadecágonos y huecos en forma de estrella de 4 puntas. |
| **16 + 4** | Hexadecágonos, cuadrados y huecos en forma de estrella de 8 puntas. |
| **Penrose** | Parche de unos 7.900 rombos que no se repite nunca, con simetría local de orden 5. Da lazos cuasiperiódicos del tipo del santuario Darb-i Imam de Isfahán. |

Todas las tramas periódicas se han verificado por cálculo: el área de los polígonos llena exactamente cada celda y cada lado lo comparten dos polígonos. No hay huecos ni solapes.

### Construcciones

- **Estrellas simples:** el método de Hankin básico.
- **Rosetas:** en los polígonos de 6 o más lados, la estrella central se abre en una estrella interior rodeada de pétalos hexagonales. Su tamaño se puede ajustar.
- **Un ángulo distinto por tipo de polígono:** las estrellas de 12, de 6 o de 4 pueden tener cada una su propio ángulo de contacto.
- **Separación en el borde:** las rectas salen de dos puntos de cada lado en lugar de uno, y aparecen rombos entre las estrellas.
- **Polígonos cóncavos y rombos estrechos:** en estos casos las rectas se cruzan antes de llegar al vértice. Cada recta se une a la más cercana que encuentre dentro del polígono, y las piezas se obtienen recorriendo el dibujo resultante.

### Acabados

- **Mosaico:** piezas de color separadas por una línea fina.
- **Lacería:** cintas entrelazadas que pasan alternativamente por encima y por debajo.
- **Trazado:** solo el lazo, sin color en las piezas.
- **Trama:** los polígonos de partida.

### Color

Cada tipo de pieza forma una «familia»: estrella de 12, pétalo de 12, roseta de vértice, rombo entre un dodecágono y un triángulo, etc. Los colores de la paleta se reparten entre las familias procurando que dos familias vecinas no coincidan. La ficha del paño muestra cada forma con su color.

Paletas: Nazarí, Comares, Zellige, Iznik, Generalife, Yesería, Nocturno, Monocromo y una **propia** editable (6 colores, línea y cinta).

### Controles

- **Nuevo diseño** (`Espacio`): cambia el ángulo, la separación, las rosetas y los colores, y mantiene la trama.
- **Otros colores** (`C`): solo recolorea.
- **Todo al azar:** cambia también la trama, la paleta y el acabado.
- **Trama:** desplegable o catálogo de miniaturas. Las flechas `←` `→` pasan a la trama anterior o siguiente.
- **Deslizadores:** ángulo de contacto (30°–80°), separación en el borde, tamaño de la roseta, tamaño, anchura de cinta y grosor de línea.
- **Opciones:** rosetas, ángulo distinto por polígono y superponer la trama de polígonos.

Alhambra no necesita bibliotecas externas y funciona sin conexión, salvo las tipografías.

### Limitaciones

- **Velocidad en Penrose:** recalcular la trama tarda unos 50 ms, así que los deslizadores van algo más lentos.
- **Bordes de Penrose:** como es un parche finito, si se arrastra mucho el paño se llega a su borde.
- **Cruces en polígonos cóncavos:** en lacería, los cruces internos se dibujan como uniones, sin el efecto de «por encima y por debajo».
- **Estrellas de 10 y 16:** se obtienen con tramas concretas (girih y hexadecágonos), no con un sistema general de polígonos no regulares.

---

## Detalles comunes

- **Copiar SVG** copia al portapapeles la vista actual como gráfico vectorial, listo para pegar en un editor como Inkscape o Illustrator.
- **Centrar** devuelve el dibujo a su posición inicial tras arrastrarlo.
- Los ajustes se guardan en el navegador (`localStorage`) y se recuperan al volver a abrir la página.
- Las dos páginas se adaptan a móvil y a los temas claro y oscuro.

## Referencias

- B. Grünbaum y G. C. Shephard, *Tilings and Patterns*, 1987. La clasificación de los 93 tipos isoédricos se publicó en 1977.
- H. Heesch y O. Kienzle, *Flächenschluss*, 1963.
- E. H. Hankin, *The Drawing of Geometric Patterns in Saracenic Art*, 1925.
- C. S. Kaplan, *Islamic Star Patterns from Polygons in Contact*, 2005, y la biblioteca [Tactile](https://github.com/isohedral/tactile-js).
- P. J. Lu y P. J. Steinhardt, «Decagonal and Quasi-Crystalline Tilings in Medieval Islamic Architecture», *Science*, 2007.

