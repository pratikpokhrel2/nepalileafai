# LeafCheck

**LeafCheck — Plant Disease Detection and Outbreak Mapping**



## Project Structure

```text
data/
  diseases.json      Disease information for 38 model labels
  demo-scans.json    13 simulated plant scans
map/
  map.js             Interactive outbreak map
```

## Disease Data

The `data/diseases.json` file contains information for 38 plant disease classification labels, including tomato late blight and healthy apple plants.

Each entry contains:

| Field | Description |
|---|---|
| `plant` | Plant name |
| `condition` | Disease name or healthy status |
| `severity` | Disease severity level |
| `description` | Brief disease explanation |
| `symptoms` | Common symptoms |
| `treatment` | Suggested management actions |
| `prevention` | Prevention methods |
| `source` | Reference for the information |

### Example

```javascript
const { diseases } = await (
  await fetch('data/diseases.json')
).json();

const info = diseases['Tomato___Late_blight'];
console.log(info.severity);
```

Disease information is intended for educational and demonstration purposes. Verify treatment recommendations before practical use.

## Demo Scans

The `data/demo-scans.json` file contains 13 simulated plant scans around Elkins, West Virginia. The sample data includes a cluster of tomato and potato late-blight cases to demonstrate outbreak visualization.

Each scan includes an identifier, disease label, plant name, condition, health status, confidence score, geographic coordinates, and timestamp.

These are demonstration records, not verified real-world outbreak reports.

## Interactive Outbreak Map

The `map/map.js` file displays plant scan locations on an interactive map.

Features include:

- Red markers for diseased plants
- Green markers for healthy plants
- Clickable markers with scan details
- Disease severity and treatment suggestions
- A map legend in the bottom-right corner

## Setup

Include the following code in your HTML page:

```html
<link
  rel="stylesheet"
  href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
/>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<div id="map" style="height: 500px"></div>

<script src="map/map.js"></script>
<script>
  LeafCheckMap.init({ dataPath: 'data/' });
</script>
```

## API

### `LeafCheckMap.init(options)`

Initializes the map and loads the disease and scan data.

- `elementId`: Map container ID; default is `'map'`
- `dataPath`: Data directory; default is `'data/'`
- `center`: Initial coordinates; default is `[38.926, -79.846]`
- `zoom`: Initial zoom level; default is `11`

### `LeafCheckMap.addScan(scan)`

Adds a new plant scan to the map.

```javascript
LeafCheckMap.addScan({
  label: 'Tomato___Early_blight',
  plant: 'Tomato',
  condition: 'Early blight',
  healthy: false,
  confidence: 0.89,
  lat: 38.93,
  lng: -79.85,
  timestamp: new Date().toISOString()
});
```

## Running Locally

Run the following command from the project directory:

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000 in your browser.

## Project Credits

**Developed by Pratik Pokhrel.**

The project uses third-party mapping software, map tiles, and plant disease classification data, which retain their applicable licenses and attribution requirements.
