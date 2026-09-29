**Goal**
 - [x] distinguish raster and vector data instantly
 - [x] explain how a raster represents Mars
 - [x] understand rows, columns, pixels/cells, bands, and values
 - [x] distinguish **pixel coordinates** from **geographic coordinates**
 - [x] identify when raster or vector is appropriate for Periapsis
 - [x] avoid one extremely common GIS mistake: treating an array index as a latitude/longitude

**Mental Model**
Raster = numpy array -- planet

|       |  0  |  1  |  2  |     |
| :---: | :-: | :-: | :-: | :-: |
| **0** | 120 | 125 | 131 | 140 |
| **1** | 118 | 121 | 129 | 139 |
| **2** | 110 | 115 | 122 | 130 |
DEM = ==Digital Elevation Model== - each cell -- *elevation*

dem[1,2] ≠ 1° latitude, 2° longitude -- pixel coordinates

raster's spatial metadata -- what geographical area the pixel refers to

Raster = grid + values + spatial metadata

Raster
├── array of values
├── width / height
├── spatial resolution
├── coordinate reference system
├── transformation
├── geographic bounds
├── NoData definition
└── metadata / provenance

relavent for NSA:
- elevation
- slope
- temperature
- surface roughness
- thermal inertia
- mineral abundance
- imagery
- terrain suitability
- hazard score

**Vectors**
-discrete geometric identities

1. `POINT` - landing sites, rover position, crater centre, sampling location, candidate habitat location
2. `LINE` - rover route, traverse, geological boundary, path
3. `POLYGON` - dangerous terrain region, scientific region of interest, crater boundary, map selection region

**Raster vs Vector**

|                               |   Raster    |           Vector           |
| :---------------------------- | :---------: | :------------------------: |
| Representation                | Grid cells  |         Geometries         |
| Typical Python representation | NumPy array | Geometry objects / GeoJSON |
| Elevation                     |      ✅      |             ❌              |
| Satellite imagery             |      ✅      |             ❌              |
| Hazard surface                |      ✅      |         sometimes          |
| Rover position                |      ❌      |          ✅ point           |
| Rover route                   |      ❌      |           ✅ line           |
| Region boundary               |  possible   |         ✅ polygon          |
| Continuous variables          |      ✅      |         usually no         |
| Discrete objects              |  sometimes  |             ✅              |

eg:
```
MOLA DEM [raster]
   ↓
slope calculation [raster]
   ↓
terrain cost [raster]
   ↓
A*
   ↓
rover route [vector lineString]
```

Algorithm computes over raster grid & front-end receives:
```python
{
  "type": "LineString",
  "coordinates": [
    [137.40, -4.50],
    [137.41, -4.51],
    [137.43, -4.52]
  ]
}
```

**Raster Coordinates**

dem.shape --> (4000,8000) - rows, columns

need metadata to determine latitude, longitude coordinates

**dataset.transform**
```
pixel coordinates
(row, column)

      ↕ transform

geographic/projected coordinates
(x, y)
```

**Cells**

cell (25,91) = elevation: -3120m

metadata reveals if *elevation value* is:
- the cell centre
- an averaged region
- a sampled observation
- an interpolated value

**Bands**

raster contains many arrays
```
height × width × bands
```

band examples: DEM, Grayscale, Binary mask (eg: 0 & 1 to represent presence of water)

```python
elevation = src.read(1)
```

**Continuous vs Categorical rasters**

**Continuous**
Values represent quantities:

```
120.2
121.8
124.1
126.7
```

eg:
- elevation
- temperature
- slope
- distance
- terrain cost

**Categorical**
Values represent classes:

```
1 = plain
2 = crater
3 = rocky terrain
```


**EXAMPLE**
```python
import numpy as np

dem = np.array([
	[100,102,105],
	[98,103,110],
	[95,100,108]
])

dem[1,2] # query result = 110
```

**Important Distincition**
```
1. ARRAY INDEX
   row=300, col=800

2. MAP COORDINATE
   x=..., y=...

3. PLANETARY COORDINATE
   latitude=-4.5°, longitude=137.4°

4. PHYSICAL VALUE
   elevation=-2410 m
```

---

**Practice**
Consider a future Periapsis system with these six datasets:

```
A. Global Mars elevation
B. Rover's current position
C. Calculated slope across the terrain
D. Proposed rover route
E. Region judged unsafe
F. Terrain difficulty score from 0–1
```

For each one, classify it as:

```
Raster
or
Vector
```

If vector, also specify:

```
Point
Line
Polygon
```

Then classify the **data meaning** as one of:

```
observed
derived
modelled/scored
```

where applicable.

```
A - Global Mars elevation:
representation = raster
type = observed

B - Rover's current position:
representation = vector (point)
type = observed

C - Calculated slope across the terrain
representation = raster
type = derived

D - Proposed rover route
representation = vector (line)
type = modeleled

E - Region judged unsafe
representation = vector (polygon) OR raster (categorical)
type = modelled

F - Terrain difficulty score from 0–1
representation = raster
type = modelled
```

**Checkpoint**
Answer these without looking back if possible.

1. A DEM contains a value at:

```
dem[450, 782]
```

What do `450` and `782` represent? *the row and column of the raster array*

2. Why can't you immediately say that the location is:

```
lat = 450
lon = 782
```

*metadata is required to transform rows and columns to coordinates*

3. Which representation is normally better for:

```
terrain slope across an entire region
```

Raster or vector? Explain **why**, not merely the answer.

*raster as it is a continuous model with cell-based calculations*

4. Which representation would you use for:

```
rover route
```

and what geometry type? *vector - line*

5. Suppose a raster stores:

```
1 = safe
2 = hazardous
3 = impassable
```

Is this continuous or categorical and why might that matter later?

*categorical - it will matter later as we can only use the discrete values in a band - eg: 2.4 has no semantic meaning*

---

**Hackathon connection**
```
NASA dataset
     ↓
RASTER
[elevation grid]
     ↓
NumPy processing
     ↓
RASTER
[slope grid]
     ↓
RASTER
[cost grid]
     ↓
routing algorithm
     ↓
VECTOR
[GeoJSON route]
     ↓
frontend map
```
