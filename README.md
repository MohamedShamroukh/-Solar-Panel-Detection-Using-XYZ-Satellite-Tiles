# 🌞 Solar Panel Detection from Satellite Imagery

Automated detection of solar panels on building rooftops using free satellite imagery and deep learning.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)

## Features

- ✅ **Free satellite imagery** (Google/ESRI tiles - no API key needed)
- ✅ **Pre-trained AI model** from [GeoAI](https://github.com/opengeos/geoai)
- ✅ **Parallel processing** for speed
- ✅ **Fast reruns** (saves imagery locally)
- ✅ **Multiple outputs** (GeoJSON, CSV, maps)

---

## Quick Start

### 1. Installation

```bash
git clone https://github.com/yourusername/solar-panel-detection.git
cd solar-panel-detection
pip install -r requirements.txt
2. Run Detection
bash
jupyter notebook solar_panel_detection_xyz_tiles.ipynb
Update configuration:

python
BUILDINGS_PATH = "path/to/buildings.geojson"  # WGS84 (EPSG:4326)
CONFIDENCE_THRESHOLD = 0.45  # Adjust 0.3-0.6
Runtime: ~30-60 min for 100-200 buildings

Notebooks
solar_panel_detection_xyz_tiles.ipynb
Complete pipeline: download imagery → detect → export results

solar_panel_detection_rerun.ipynb
Fast parameter testing (2-5 min - no re-downloading)

Requirements
text
geoai-py>=0.11.0
geopandas>=0.14.0
rasterio>=1.3.0
earthengine-api>=0.1.0
pillow>=10.0.0
requests>=2.31.0
pandas>=2.0.0
numpy>=1.24.0
matplotlib>=3.7.0
Input/Output
Input
Building footprints in GeoJSON (WGS84 projection)

Output
text
output/solar_detection/
├── imagery/                        # 512×512 px satellite tiles
├── solar_panels_detected.geojson   # Point locations
├── solar_panels_detected.csv       # Tabular results
└── detection_map.png               # Visualization
GeoJSON attributes:

building_id: Building identifier

confidence: Detection confidence (0-1)

coverage_pct: Solar panel coverage percentage

detection_date: Processing date

Parameters
Parameter	Description	Default	Range
CONFIDENCE_THRESHOLD	Minimum detection confidence	0.45	0.3-0.6
MIN_COVERAGE_PCT	Minimum solar coverage	0.02	0.01-0.05
MAX_COVERAGE_PCT	Maximum solar coverage	0.35	0.25-0.45
MIN_OBJECT_AREA	Minimum size (sq m)	10	5-20
MAX_WORKERS	Parallel threads	4	2-8
Tip: Lower thresholds = more detections, Higher thresholds = fewer but higher quality

Methodology
Imagery Acquisition

Downloads satellite tiles from Google/ESRI (zoom 20, ~0.6m/pixel)

Stitches 3×3 tile grid and crops 512×512 px around each building

Detection

Uses GeoAI pre-trained U-Net model

Generates confidence masks for solar panel locations

Applies thresholding and coverage filters

Export

Extracts building centroids with solar detections

Outputs georeferenced points with metadata

Model Citation
This project uses the solar panel detection model from GeoAI:

text
@software{geoai2024,
  author = {Wu, Qiusheng and others},
  title = {GeoAI: Artificial Intelligence for Geospatial Data},
  year = {2024},
  url = {https://github.com/opengeos/geoai}
}
Reference: Wu, Q., et al. (2024). "GeoAI: A Python package for integrating artificial intelligence with geospatial data." Journal of Open Source Software.

Example Usage
python
import geopandas as gpd
import geoai

# Load buildings
buildings = gpd.read_file("buildings.geojson")

# Download imagery and detect
detector = geoai.SolarPanelDetector()
for idx, building in buildings.iterrows():
    img = download_centered_imagery(lat, lon, zoom=20)
    masks = detector.generate_masks(img, confidence_threshold=0.45)

# Export results
solar_gdf.to_file("solar_panels_detected.geojson")
Troubleshooting
Black/empty imagery?

Tile servers may be rate-limited - add delays between downloads

Check internet connection

No detections?

Lower CONFIDENCE_THRESHOLD (try 0.35)

Adjust MIN_COVERAGE_PCT and MAX_COVERAGE_PCT

Out of memory?

Reduce MAX_WORKERS (try 2)

Process smaller batches

Contributing
Contributions welcome! Areas for improvement:

Additional imagery sources (Planet, Sentinel-2)

Confidence score calibration

Validation metrics

GUI interface

License
MIT License - see LICENSE

Note: GeoAI model has its own license - see GeoAI repository

Acknowledgments
GeoAI - Pre-trained detection model

GeoPandas - Geospatial processing

Google & ESRI - Satellite tile services

Contact
Mohamed Shamroukh
📧 M.Shamroukh@lboro.ac.uk
🌐 mohamedshamroukh.github.io/portfolio

Issues: GitHub Issues

Last updated: February 2026

text

***

This shorter version:
- ✅ **~50% shorter** than the full version
- ✅ Includes all essential information
- ✅ Credits GeoAI with proper citation
- ✅ Has your contact details
- ✅ Clear structure and quick to scan
- ✅ Professional and GitHub-ready

Perfect for researchers and developers who want the key information quickly! 🚀
