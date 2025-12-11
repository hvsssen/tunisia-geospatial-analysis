# Tunisia Spatial Analysis 🗺️

Comprehensive geospatial data analysis project using Python and OpenStreetMap data, conducted as part of academic coursework at ENIT (École Nationale d'Ingénieurs de Tunis).

## 📋 Project Overview

This project explores three key areas of geospatial analysis:
1. **Map Projection Comparison** - Evaluating how different projections affect Tunisia's geographic representation
2. **Urban Data Extraction** - Extracting and analyzing building data from OpenStreetMap
3. **Road Network Analysis** - Computing optimal routes using graph algorithms

## 🎯 Key Features

### 1. Map Projection Analysis
- 🗺️ Comparison of three projection systems:
  - **Mercator** (Conformal) - Preserves shapes, best for navigation
  - **Equidistant Conic** - Maintains accurate distances, ideal for route planning
  - **Albers Equal Area** - Preserves area proportions, optimal for thematic mapping
- Multiple spatial layers analyzed: administrative boundaries, waterways, highways, coastline, POIs
- CRS transformations and visual comparison in QGIS
- Decision support framework for choosing appropriate projections

### 2. Urban Structure Extraction (Ksar Hellal, Monastir)
- 🏘️ Extracted **499 buildings** from OpenStreetMap using bounding box queries
- Administrative boundary retrieval (admin_level=6)
- Spatial distribution analysis of urban features
- Foundation for urban planning and infrastructure studies

### 3. Road Network Analysis (Mahdia)
- 🛣️ Shortest path computation between Chebba and Ksour Essef using **Dijkstra's algorithm**
- Graph-based network topology analysis
- Road segment attributes: type, length, speed limits
- Route optimization for transportation planning

### 4. Satellite Image Classification (Bonus)
- 🛰️ Landsat imagery analysis with multiple classification methods:
  - **Unsupervised**: K-Means, ISODATA
  - **Supervised**: Parallelepiped, Maximum Likelihood, Minimum Distance, Mahalanobis
- Comparative analysis of classification accuracy
- Remote sensing for land cover mapping

## 🛠️ Tech Stack

### Core Libraries
- **GeoPandas** - Spatial data manipulation
- **Shapely** - Geometric operations
- **PyProj** - Coordinate reference system transformations
- **OSMnx** - OpenStreetMap data extraction and network analysis
- **NetworkX** - Graph algorithms (Dijkstra, topological analysis)

### Visualization & Analysis
- **QGIS** - Professional cartographic visualization
- **Matplotlib** - Python plotting
- **Cartopy** - Map projections and geospatial plotting
- **ENVI** - Satellite image classification

### Environment
- **Google Colab** - Cloud-based Python development
- **Jupyter Notebook** - Interactive analysis

## 📊 Results & Findings

### Projection Comparison
| Projection | Shape Fidelity | Distance Accuracy | Area Preservation | Best Use Case |
|------------|---------------|-------------------|-------------------|---------------|
| Mercator | High | Low | Low | Navigation |
| Equidistant Conic | Moderate | High | Low | Distance measurement |
| Albers Equal Area | Moderate | Moderate | High | Thematic mapping |

### Network Analysis
- Successfully computed optimal driving routes in Mahdia region
- Graph contains multiple nodes (intersections) and edges (road segments)
- Algorithm considers road type, length, and travel time

### Urban Data
- 499 buildings extracted from Ksar Hellal
- Bounding box: [10.75, 35.75, 10.85, 35.80]
- Data type: GeoDataFrame with Polygon/MultiPolygon geometries

## 🚀 Getting Started

### Prerequisites
```bash
pip install geopandas shapely pyproj osmnx networkx matplotlib cartopy
```

### Running the Analysis

**1. Map Projections:**
```python
import geopandas as gpd
import cartopy.crs as ccrs

gdf = gpd.read_file("tunisia_natural.shp")

# Define projections
proj_mercator = "EPSG:3395"
proj_equidist = "+proj=eqdc +lon_0=10 +lat_0=34 +lat_1=33 +lat_2=36"
proj_albers = "+proj=aea +lat_1=33 +lat_2=36 +lat_0=34 +lon_0=10"

# Transform
gdf_mercator = gdf.to_crs(proj_mercator)
gdf_equidist = gdf.to_crs(proj_equidist)
gdf_albers = gdf.to_crs(proj_albers)
```

**2. Building Extraction:**
```python
import osmnx as ox
from shapely.geometry import box

bounds = [10.75, 35.75, 10.85, 35.80]
bbox = box(*bounds)

buildings = ox.features_from_polygon(bbox, tags={"building": True})
print(f"Number of buildings: {len(buildings)}")
```

**3. Road Network Analysis:**
```python
import osmnx as ox
import networkx as nx

# Download road network
G = ox.graph_from_place("Mahdia, Tunisia", network_type="drive")

# Compute shortest path
orig_node = ox.distance.nearest_nodes(G, X=orig_x, Y=orig_y)
dest_node = ox.distance.nearest_nodes(G, X=dest_x, Y=dest_y)
route = nx.dijkstra_path(G, source=orig_node, target=dest_node, weight='length')
```

## 📖 Documentation

Full technical report available: [`docs/GeoSpatial_Homework_Report.pdf`](docs/GeoSpatial_Homework_Report.pdf)

Includes:
- Detailed methodology
- Visual comparisons (QGIS screenshots)
- Complete Python code
- Results analysis and discussion

## 🎓 Academic Context

- **Institution**: École Nationale d'Ingénieurs de Tunis (ENIT)
- **Department**: Information and Communication Technologies
- **Course**: Geospatial Data Analysis
- **Professor**: M. Frihida Ali
- **Date**: May 2024

## 🔍 Key Takeaways

1. **Projection selection matters**: Different projections serve different purposes - navigation vs. area analysis require different approaches
2. **OpenStreetMap is powerful**: Rich, open geospatial data accessible programmatically
3. **Graph algorithms for routing**: NetworkX + OSMnx enable sophisticated transportation analysis
4. **Spatial data pipelines**: GeoPandas + QGIS workflow enables professional cartographic analysis

## 💡 Future Improvements

- [ ] Add interactive web maps (Folium/Leaflet)
- [ ] Implement real-time routing API
- [ ] Expand to other Tunisian cities
- [ ] Add density heatmaps for building distribution
- [ ] Integrate population data for demographic analysis
- [ ] Deploy as web application with Flask/FastAPI

## 📧 Contact

**Hassen Slim**
- Email: hassen.slim@etudiant-enit.utm.tn
- LinkedIn: [linkedin.com/in/slim-hassen](https://www.linkedin.com/in/slim-hassen)
- GitHub: [github.com/hvsssen](https://github.com/hvsssen)

## 📄 License

This project is part of academic coursework and is available for educational purposes.

---

⭐ If you find this project useful, please consider giving it a star!
