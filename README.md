# RoadScan

RoadScan es una herramienta diseñada para evaluar la transitabilidad en vías, incluyendo la detección de vehículos y de anomalías en el pavimento. Este repositorio contiene la metodología y los notebooks desarrollados para evaluar el estado de las vías usando imágenes satelitales tipo TMS, modelos de segmentación como SAM, y algoritmos de detección de anomalías. Se puede usar para otros tipos de lugares especificando las áreas de descarga desde un archivo KML.

El enfoque de este proyecto combina técnicas de procesamiento de imágenes, machine learning y algoritmos de detección avanzada para lograr una segmentación precisa de las vías, identificar vehículos en movimiento y evaluar anomalías en la infraestructura vial. La automatización de estos procesos reduce la necesidad de inspecciones manuales y proporciona una herramienta eficiente para el monitoreo en tiempo real.

---

## 🗂 Estructura del Proyecto

<img src="Road_Scan_flujo_modelo.png" width="1000" />

| Archivo / Notebook              | Descripción breve |
|-------------------------------|-------------------|
| `2_CreacionBB_DescargaDataset.ipynb` | Genera los bounding boxes a partir del KML y descarga imágenes TMS (Terrain / Satellite). |
| `3_SegmentacionVias.ipynb`           | Segmenta la infraestructura vial desde imágenes Terrain usando umbralización y morfología. |
| `4_RecorteImagenesVias.ipynb`        | Recorta imágenes satelitales para conservar solo la vía (intersección espacial con shapefiles). |
| `5_SAM_Vehiculos.ipynb`              | Usa LangSAM con prompt `cars, buses and trucks` para segmentar vehículos en las vías. |
| `6_SAM_Pavement.ipynb`               | Usa LangSAM para segmentar únicamente el pavimento y eliminar ruido visual lateral. |
| `7_Anomalias.ipynb`                  | Detecta anomalías visuales (como manchas o baches) usando filtrado cromático en HSV. |
| `8_GeocodificacionInversa.ipynb`     | Aplica geocodificación inversa a los segmentos de vía para extraer ubicación detallada. |
| `8_Consolidacion.ipynb`              | Consolida todos los resultados (vía, autos, anomalías, ubicación) en una tabla unificada. |

---

## 📦 Requisitos

Para correr los notebooks necesitas un entorno Python 3.8+ con las siguientes librerías:

```bash
pip install geopandas rasterio matplotlib opencv-python shapely tqdm segment-anything samgeo pandas numpy leafmap pyproj scikit-image geopy requests
```

> **Nota**: El proyecto utiliza el modelo SAM (Segment Anything Model). El checkpoint necesario se descarga automáticamente en los notebooks correspondientes.

---

## 🚀 Cómo usar

### Orden de ejecución recomendado

El diagrama "Flujo del modelo" (arriba) muestra visualmente el pipeline completo. Los notebooks deben ejecutarse en el siguiente orden:

1. **`2_CreacionBB_DescargaDataset.ipynb`** - Genera bounding boxes desde KML y descarga imágenes satelitales + terrain
2. **`3_SegmentacionVias.ipynb`** - Segmenta las vías desde imágenes terrain
3. **`4_RecorteImagenesVias.ipynb`** - Recorta imágenes satelitales para aislar solo las vías
4. **`5_SAM_Vehiculos.ipynb`** - Detecta vehículos usando LangSAM (genera vectores de autos)
5. **`6_SAM_Pavement.ipynb`** - Segmenta pavimento limpio (genera imágenes "only pavement")
6. **`7_Anomalias.ipynb`** - Detecta anomalías visuales en pavimento (genera vectores clasificados)
7. **`8_GeocodificacionInversa.ipynb`** - Añade información de ubicación geográfica
8. **`8_Consolidacion.ipynb`** - Consolida todos los resultados en vectores unificados

### Requisitos previos

- Archivo KML con las áreas de interés a analizar
- Acceso a imágenes satelitales tipo TMS (Terrain/Satellite)
- Espacio en disco para almacenar imágenes descargadas y resultados procesados

### Configuración básica

Cada notebook contiene variables configurables al inicio. Las principales son:

- `troncal`: Identificador de la vía o ruta a analizar
- `BB`: Parámetro de bounding box extendido
- `z`: Nivel de zoom para las imágenes satelitales

> **⚠️ Documentación en desarrollo**: Estamos trabajando en ampliar la documentación de parámetros específicos y casos de uso. Para contribuir o reportar problemas, por favor abre un issue.

---

## 📊 Salidas del Pipeline

El pipeline genera los siguientes tipos de archivos:

- **Imágenes `.tif`**: Resultados de segmentación en formato raster
- **Archivos `.shp`**: Vectores geoespaciales de vías, vehículos y anomalías
- **Archivos `.geojson`**: Versión web-friendly de los vectores
- **Archivos `.txt`**: Reportes de análisis cromático y anomalías
- **Imágenes `.jpg`**: Visualizaciones comparativas

---

## 🤝 Contribuciones

Este proyecto está en desarrollo activo. Las contribuciones son bienvenidas, especialmente en:

- Mejoras de documentación
- Optimización de algoritmos
- Nuevos casos de uso
- Corrección de bugs

Para contribuir, por favor abre un Pull Request o un Issue describiendo tu propuesta.

---
