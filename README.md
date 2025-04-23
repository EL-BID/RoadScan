# RoadScan


Este repositorio contiene la metodología y los notebooks desarrollados para evaluar el estado de las troncales principales de Venezuela usando imágenes satelitales tipo TMS, modelos de segmentación como SAM, y algoritmos de detección de anomalías, se puede usar para otro tipo de lugares especificando las areas de descarga desde un kml.


---

## 🗂 Estructura del Proyecto

| Archivo / Notebook              | Descripción breve |
|-------------------------------|-------------------|
| `2_CreacionBB_DescargaDataset.ipynb` | Genera los bounding boxes a partir del KML y descarga imágenes TMS (Terrain / Satellite). |
| `3_SegmentacionVias.ipynb`           | Segmenta la infraestructura vial desde imágenes Terrain usando umbralización y morfología. |
| `4_RecorteImagenesVias.ipynb`        | Recorta imágenes satelitales para conservar solo la vía (intersección espacial con shapefiles). |
| `5_SAM_Vehiculos.ipynb`              | Usa LangSAM con prompt `cars, buses and trucks` para segmentar vehículos en las vías. |
| `6_SAM_Pavement.ipynb`               | Usa LangSAM para segmentar únicamente el pavimento y eliminar ruido visual lateral. |
| `7_DeteccionAnomalias.ipynb`         | Detecta anomalías visuales (como manchas o baches) usando filtrado cromático en HSV. |
| `8_ubicaciones.ipynb`                | Aplica geocodificación inversa a los segmentos de vía para extraer ubicación detallada. |
| `8_UnionResultados.ipynb`            | Consolida todos los resultados (vía, autos, anomalías, ubicación) en una tabla unificada. |

---

## 📦 Requisitos

Para correr los notebooks necesitas un entorno Python 3.8+ con las siguientes librerías:

```bash
pip install geopandas rasterio matplotlib opencv-python shapely tqdm segment-anything samgeo
