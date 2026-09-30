**Goal**
 - [x] explain latitude and longitude geometrically
 - [x] identify valid latitude ranges
 - [x] understand longitude wrapping
 - [x] distinguish (lat, lon) from (x, y) and (row, col)
 - [x] understand how a geographic grid relates to raster cells
 - [x] recognize why longitude becomes troublesome near the ±180° boundary
 - [x] query the conceptual cell containing a planetary coordinate

**Mental Model**

```
North Pole
                     +90°
                       ●
                       │
             latitude  │
                       │
 -180° ────────────────┼──────────────── +180°
        longitude      │
                       │
                       ●
                     -90°
                   South Pole
```


**latitude** = north -- south
```
-90° ≤ latitude ≤ +90°
```

```python
if not -90 <= lat <= 90:
    raise ValueError(...)
```

**longitude** = east -- west from meridian
```
                   0°
                   │
                   │
        -90° ──────●────── +90°
                   │
                   │
                ±180°
```

problem:
```
180° ≡ -180°
350° ≡ -10°
```

lines of longitude (aka meridian) - converge at poles

angular coordinates ≠ metres

**Coordinates Tuples**

```
(-4.5, 137.4)
```

can mean (latitude, longitude) or (longitude, latitude) depending on API/library

GeoJSON = [x, y] =  [longitude, latitude]

own python function recommendation:
```python
route(lat=-4.5, lon=137.4)
```

API boundary:
```json
{
  "lat": -4.5,
  "lon": 137.4
}
```

**Geographic Grids**
```
             longitude →

            10   11   12   13   14
          ┌────┬────┬────┬────┐
lat 3°    │    │    │    │    │
          ├────┼────┼────┼────┤
lat 2°    │    │ X  │    │    │
          ├────┼────┼────┼────┤
lat 1°    │    │    │    │    │
          ├────┼────┼────┼────┤
lat 0°    │    │    │    │    │
          └────┴────┴────┴────┘
```

**Pixel Centre v Pixel Boundary**

cell might span:
```
lat 10.0° → 11.0°
lon 20.0° → 21.0°
```

while its centre is approximately:
```
lat = 10.5°
lon = 20.5°
```

Later, when converting:
```
pixel → geographic coordinate
```

must know whether you're requesting:
```
upper-left corner
centre
another pixel corner etc.
```

Rasterio explicitly lets us handle this

**Geographic vs Projected coordinates**
```
lat = -4.5°
lon = 137.4°
```
```
x = 523482 m
y = 918273 m
```

**important distinction**
```
lat/lon → angular geographic coordinates
x/y     → map coordinates, often projected
row/col → array coordinates
```

```
ARRAY SPACE
(row, col)
        ↓ transform
MAP SPACE
(x, y)
        ↓ interpretation / CRS
PLANETARY LOCATION
(latitude, longitude)
```

**Longitude Wrapping**
```
        seam
                  │
            179°  │ -179°
              A ● │ ● B
                  │
```

naïvely : ∆ = 358°, physically = 2°

anti-meridian/dateline-type problem -- coordinate convections + normalisation

**Model**
```
user clicks Mars map
        ↓
lat/lon
(-4.5°, 137.4°)
        ↓
coordinate transformation
        ↓
raster row/column
(1827, 3914)
        ↓
array lookup
        ↓
DEM value
-2410 m
```

query elevation at a coordinate and convert pixel ↔ geographic coordinates

**Practice**

A fictional Mars raster covers:
```
Latitude:  -10° to +10°
Longitude: 100° to 140°
```
and represents elevation.

Answer:
### A
Is this valid?
```
lat = 8°
lon = 120°
```
Explain.
*Yes as it's within the range*
### B
Is this valid?
```
lat = 105°
lon = 120°
```
Explain. 
*Latitude is not within range*
### C
A pixel is:
```
row = 200
col = 500
```
Can you determine its latitude and longitude from those numbers alone?
*No, as transformation details aren't given*
### D
Two locations are:
```
P = (lat=0°, lon=179°)
Q = (lat=0°, lon=-179°)
```
What's wrong with simply calculating:
```
|-179 - 179| = 358°
```
and treating that as their actual angular separation?
*Physically, the longitudes are 2° apart - anti-meridian/dateline-type problem*
### E
A GeoJSON coordinate appears as:
```
[137.4, -4.5]
```
Under standard GeoJSON coordinate ordering, which value is longitude and which is latitude?
*longitude, latitude*
### F
Why does `1°` of longitude correspond to a smaller physical east-west distance near the poles than near the equator?
*as longitudes converge going to poles from meridian*

**Applied challenge**

You are debugging Periapsis and encounter:

```python
def elevation_at(lat, lon):    
	row = int(lat)
	col = int(lon)   
	return dem[row, col]
```

A teammate claims:
> "We're passing latitude and longitude in, so this should retrieve the elevation."
Give me the **technical reason this implementation is wrong**.

*Latitude and longitude cannot be cast directly to raster indices. We first interpret/transform the geographic coordinates into the raster's CRS, producing map coordinates `(x, y)` if necessary. Then we apply the inverse raster affine transform to obtain `(row, col)` and index the array.*
