Sistema Inteligente de Rutas en TransMilenio

Notebook de Jupyter que implementa un sistema inteligente basado en una base de conocimiento de reglas lógicas y búsqueda heurística (A*) para encontrar la mejor ruta entre dos puntos de la red real de TransMilenio (Bogotá, Colombia).

Proyecto desarrollado para la asignatura de Inteligencia Artificial Avanzada, aplicando los conceptos de lógica y representación del conocimiento, sistemas basados en reglas y técnicas de búsqueda heurística a un problema de transporte real.

Contenido
transmilenio_sistema_inteligente.ipynb — el notebook completo, listo para ejecutar.
Qué hace el sistema
Base de conocimiento (hechos): cada estación, la línea (troncal) a la que pertenece y las conexiones entre estaciones consecutivas se representan como hechos declarativos (estacion, pertenece, conecta), usando datos oficiales y actuales de TransMilenio.
Motor de reglas (encadenamiento hacia adelante):
R1 / R2 — moverse entre estaciones consecutivas de una misma línea, en ambos sentidos.
R3 — transbordar de línea en una misma estación.
R4 — transbordar caminando entre estaciones cercanas de líneas distintas (proximidad geográfica).
Búsqueda heurística A*: explora el grafo de estados (estación, línea) guiado por una heurística admisible (distancia en línea recta al destino, convertida a tiempo), y devuelve la ruta de menor tiempo estimado.
Interfaz interactiva: dos cajas de texto (Origen / Destino) con autocompletado aproximado, un botón que ejecuta todo el proceso y muestra el resultado en texto y sobre un mapa real de Bogotá (folium / OpenStreetMap).
Datos reales utilizados

La red de estaciones y troncales se tomó del geoportal oficial de TransMilenio S.A. (capas de estaciones y trazados troncales, servidas como ArcGIS FeatureServer), reproyectada de coordenadas planas (EPSG:3116, MAGNA-SIRGAS Bogotá) a coordenadas geográficas WGS84.

152 estaciones reales
13 troncales reales: Autopista Norte, Caracas, Caracas Sur, Eje Ambiental, NQS Central, NQS Sur, Américas, Calle 26, Calle 80, Suba, Avenida Ciudad de Cali, Carrera 10, Carrera 7.
Requisitos
Python 3.9 o superior
Jupyter Notebook o JupyterLab (o la extensión de Jupyter en VS Code)

El notebook instala automáticamente las librerías que falten (networkx, matplotlib, folium, ipywidgets, pyproj) en el kernel activo la primera vez que se ejecuta la celda de imports, así que no es necesario instalarlas a mano de antemano. Si se prefiere hacerlo manualmente:

bash
pip install networkx matplotlib folium ipywidgets pyproj

Si usas VS Code: asegúrate de tener seleccionado el mismo kernel/entorno de Python con el que vas a ejecutar el notebook antes de correr la primera celda.

Cómo ejecutar
Abre transmilenio_sistema_inteligente.ipynb en Jupyter o VS Code.
Ejecuta las celdas en orden (Run All o celda por celda).
En la sección de interfaz interactiva, escribe el nombre de una estación de origen y una de destino (hay autocompletado aproximado, no es necesario escribir el nombre exacto) y pulsa el botón de calcular ruta.
El notebook mostrará la secuencia de pasos, el tiempo estimado, los transbordos y un mapa interactivo de Bogotá con la ruta resaltada.

También incluye ejemplos ya resueltos (p. ej. Portal Norte – Unicervantes → Portal Sur – JFK, Portal 80 → Portal Américas) y una comparación de rendimiento entre la búsqueda A* y una búsqueda no informada (equivalente a Dijkstra).

Limitaciones conocidas
El orden de las estaciones dentro de cada troncal se reconstruye con un heurístico de vecino más cercano, porque los datos oficiales no vienen ordenados por recorrido.
Los tiempos de viaje son estimados, calculados con una velocidad comercial promedio, no con datos de operación en tiempo real.
Los transbordos entre líneas cercanas (regla R4) se infieren por proximidad geográfica, no a partir de un dato oficial de conexión física entre estaciones.
Algunos nombres de estación incluyen la palabra "Temporal", reflejando reubicaciones reales por las obras del Metro de Bogotá, tal como constan en la fuente oficial.
La troncal Avenida Ciudad de Cali queda aislada del resto del grafo: en la realidad se conecta mediante rutas alimentadoras que no están incluidas en los datos troncales usados. El sistema responde honestamente "no se encontró ruta" en vez de inventar una conexión.
Material adicional

Créditos
Datos de estaciones y troncales: TransMilenio S.A. (geoportal / datos abiertos oficiales).
Mapa base: © colaboradores de OpenStreetMap.
