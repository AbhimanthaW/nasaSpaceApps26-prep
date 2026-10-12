# P0

**Planetary GIS Fundamentals**

- [x] Raster vs vector data  
- [x] Latitude/longitude grids  
- [x] Map projections  
- [x] Coordinate reference systems  
- [x] Spatial resolution  
- [x] Pixel resolution vs geographic resolution  
- [x] Bounding boxes  
- [ ] Resampl
      - [ ] nearest  
      - [ ] bilinear  
      - [ ] cubic, conceptually  
- [ ] NoData / missing pixels  
- [ ] Reprojection  
- [ ] DEMs / digital elevation models  
- [ ] Elevation → gradient → slope  
- [ ] Spatial interpolation basics  
- [ ] Great-circle/spherical distance

Mars-specific coordinate knowledge

- [ ] planetocentric vs planetographic latitude
- [ ] positive-east vs positive-west longitude
- [ ] `0–360°` vs `-180–180°`
- [ ] Mars radius / ellipsoid assumptions
- [ ] why two datasets with identical-looking coordinates may not line up

#### **Practice**

Take **one actual Mars DEM** and:

- [ ] inspect its metadata  
- [ ] determine coordinate convention  
- [ ] determine units  
- [ ] crop a region  
- [ ] visualize elevation  
- [ ] calculate slope  
- [ ] query elevation at a coordinate  
- [ ] convert pixel ↔ geographic coordinates

**NASA/PDS data literacy**

- [ ] NASA PDS structure  
- [ ] PDS3 vs PDS4 conceptually  
- [ ] dataset/product/collection distinction  
- [ ] metadata labels  
- [ ] observation vs derived product  
- [ ] units  
- [ ] spatial coverage  
- [ ] temporal coverage  
- [ ] instrument provenance  
- [ ] resolution  
- [ ] uncertainty/limitations  
- [ ] science product vs browse image

### **Practice**

For MOLA, create a tiny notebook/script that prints something like:

| Dataset: Instrument: Mission: Target: Latitude convention: Longitude convention: Resolution: Units: NoData: Projection: Coverage: Processing level: Derived fields we create: |
| :---- |

Then generate:

| MOLA    ↓ metadata validation    ↓ crop / normalize    ↓ elevation grid    ↓ derived slope grid    ↓ algorithm-ready terrain layer |
| :---- |

**Terrain-derived calculations**

- [ ] Elevation  
- [ ] Local elevation difference  
- [ ] Gradient  
- [ ] Slope  
- [ ] Basic roughness  
- [ ] Distance from point/feature  
- [ ] Neighborhood/window operations  
- [ ] Boolean exclusion masks  
- [ ] Normalized continuous scores

### **Practice**

Given a DEM:

- [ ] compute slope  
- [ ] identify cells exceeding an arbitrary test threshold  
- [ ] create a binary hazard mask  
- [ ] create a continuous terrain-difficulty score  
- [ ] visualize the layers independently

**Cost surfaces and multi-factor scoring**

Understand the difference between:

- [ ] **Hard constraints :** valid \= slope \< threshold  
- [ ] **Soft preferences :** cost \= w1 \* slope\_cost \+ w2 \* roughness\_cost \+ w3 \* distance\_cost

- [ ] min-max normalization  
- [ ] clipping  
- [ ] weighted sums  
- [ ] thresholds  
- [ ] masks  
- [ ] penalty functions  
- [ ] categorical vs continuous layers  
- [ ] sensitivity to weights  
- [ ] avoiding double-counting correlated features

### **Practice**

Build a deliberately generic:

| score \= (     w\_slope \* slope\_score     \+ w\_elevation \* elevation\_score     \+ w\_distance \* distance\_score ) |
| :---- |

Then change weights and observe the result.

**Pathfinding**

- [ ] Dijkstra's algorithm  
- [ ] A*  
- [ ] heuristic concept  
- [ ] admissible heuristic concept  
- [ ] 4-neighbour vs 8-neighbour grids  
- [ ] traversal cost  
- [ ] blocked cells  
- [ ] start/end snapping  
- [ ] reconstructing paths  
- [ ] path cost vs geometric distance

**Practice**

| DEM  ↓ Slope  ↓ Terrain cost  ↓ Cost grid  ↓ A\*  ↓ Route |
| :---- |

Compare  
**Route A:** pure shortest-distance path  
against:  
**Route B:** terrain-aware path.

**Algorithm validation**

- [ ] obvious synthetic cases  
- [ ] edge cases  
- [ ] known expected outputs  
- [ ] parameter sensitivity  
- [ ] resolution sensitivity  
- [ ] missing data  
- [ ] impossible routes  
- [ ] coordinates outside the raster  
- [ ] start=end  
- [ ] disconnected regions

**Practice**

| Start ───── steep ridge ───── End         \\                 /          \\ safe valley   / |
| :---- |

**Scientific uncertainty and provenance**

- [ ] Every derived layer should have

| {   "name": "terrain\_slope",   "source": "MOLA DEM",   "type": "derived",   "units": "degrees",   "method": "...",   "resolution": "...",   "assumptions": \[\],   "limitations": \[\] } |
| :---- |

Learn to distinguish:

- [ ] **Observed**: *MOLA elevation*  
- [ ] **Derived**: *slope calculated from MOLA elevation*  
- [ ] **Modelled**/**scored**: *terrain suitability \= 0.74*  
- [ ] **Predicted**: *Something estimated about future conditions.*

**Python geospatial/data stack**

#### **Very strong**

- [ ] NumPy  
- [ ] Rasterio  
- [ ] FastAPI  
- [ ] Pydantic

#### **Functional**

- [ ] PyProj  
- [ ] SciPy  
- [ ] Shapely

#### **Familiar**

- [ ] GeoPandas  
- [ ] GDAL concepts  
- [ ] xarray

**Performance engineering**

- [ ] array vectorization  
- [ ] raster window reads  
- [ ] cropping before processing  
- [ ] downsampling  
- [ ] precomputation  
- [ ] caching  
- [ ] serialization  
- [ ] profiling  
- [ ] avoiding unnecessary data copies

example:

| raw DEM    ↓ precompute slope      ← offline    ↓ cache terrain layers    ↓ user selects A/B    ↓ route computation     ← interactive |
| :---- |

**API/interface design**

- [ ] GET /layers  
- [ ] GET /region  
- [ ] POST /route  
- [ ] POST /evaluate  
- [ ] GET /metadata/{layer}

example:

| POST /route {   "start": {     "lat": \-4.5,     "lon": 137.4   },   "end": {     "lat": \-4.6,     "lon": 137.6   },   "weights": {     "slope": 0.7,     "distance": 0.3   } } |
| :---- |

output:

| {   "path": \[\],   "distance\_m": 4210,   "cost": 0.42,   "warnings": \[\],   "provenance": {} } |
| :---- |

### **Practice**

- [ ] Pydantic models  
- [ ] validation  
- [ ] versionable contracts  
- [ ] clear error responses  
- [ ] OpenAPI  
- [ ] deterministic outputs

**Architecture under hackathon constraints**

NASA / Partner Data > Data ingestion > Metadata validation > Preprocessing > DEM, Slope, Other layers > Scientific / spatial engine > FastAPI > Frontend map / workflow

### **Frontend mapping literacy**

- [ ] raster overlays

- [ ] GeoJSON

- [ ] coordinate arrays

- [ ] polylines

- [ ] markers

- [ ] tiles

- [ ] image overlays

- [ ] viewport/bounds

- [ ] click coordinate - backend query

- [ ] layer toggling

### 

# P1

**Basic Mars Science**

- [ ] Martian topography  
- [ ] major terrain types  
- [ ] craters  
- [ ] plains  
- [ ] volcanoes  
- [ ] canyons  
- [ ] polar regions  
- [ ] regolith  
- [ ] dust  
- [ ] temperature extremes  
- [ ] atmospheric pressure  
- [ ] radiation as a surface hazard  
- [ ] water-ice evidence  
- [ ] rover mobility constraints

**Sensitivity Analysis**

- [ ] Weights

**Graceful Failure**

- [ ] dataset unavailable  
- [ ] API timeout  
- [ ] corrupted input  
- [ ] missing metadata  
- [ ] NoData region  
- [ ] impossible path  
- [ ] unsupported coordinate convention  
- [ ] huge request  
- [ ] frontend/backend schema mismatch

**Git/integration speed**

- [ ] branching  
- [ ] PRs  
- [ ] merge conflicts  
- [ ] reverting  
- [ ] rebasing enough to survive  
- [ ] environment variables  
- [ ] `.env.example`  
- [ ] dependency pinning  
- [ ] shared types/contracts  
- [ ] clean repository structure  
- [ ] reproducible setup

**Technical explanation**

- [ ] LVL 1: 15 seconds  
- [ ] LVL 2: 60 seconds  
- [ ] LVL 3: Deep Judge Questioning

# P2

- [ ] Docker basics  
- [ ] basic deployment  
- [ ] tile servers  
- [ ] spatial databases/PostGIS concepts  
- [ ] more advanced interpolation  
- [ ] spatial indexing  
- [ ] 3D terrain visualization  
- [ ] GPU raster processing

**By END:**

- [ ] I can inspect an unfamiliar planetary dataset without help.  
- [ ] I understand Mars coordinate/projection traps.  
- [ ] I can manipulate raster data confidently.  
- [ ] I can derive slope/terrain metrics correctly.  
- [ ] I understand cost surfaces and weighted scoring.  
- [ ] *I can implement/debug A or similar routing.*\*  
- [ ] I can validate an algorithm with synthetic and real data.  
- [ ] I can design clean frontend/backend/data contracts.  
- [ ] I can explain every transformation from NASA input → user output.  
- [ ] I can integrate the team's components quickly when everyone else's beautiful independent code inevitably meets reality.

# Drills

### **Drill 1 \- Mars Raster** 

Load MOLA → inspect metadata → crop → visualize → query

**Target:** GIS competence

| mola/ ├── inspect.py ├── preprocess.py ├── visualize.py ├── metadata.json └── README.md |
| :---- |

### **Drill 2 \- Terrain Engine** 

DEM → slope → masks → cost surface

**Target:** Scientific processing

| terrain/ ├── slope.py ├── normalize.py ├── masks.py ├── cost.py └── tests/ |
| :---- |

### **Drill 3 \- Mars Router**

over terrain cost → GeoJSON route

**Target:** Algorithms

| routing/ ├── astar.py ├── grid.py ├── heuristic.py ├── route.py └── tests/ |
| :---- |

### **Drill 4 \- Mini Periapsis**

Dataset → backend → map → result

**Target:** Integration 

| NASA data    ↓ preprocessing    ↓ terrain calculation    ↓ routing    ↓ FastAPI    ↓ basic interactive map |
| :---- |
