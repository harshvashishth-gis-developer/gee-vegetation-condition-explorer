# 🌱 Western Kentucky Vegetation Condition Explorer

An interactive **Google Earth Engine (GEE)** application for comparing Landsat-derived vegetation conditions and satellite imagery across multiple years in **Western Kentucky, USA**.

The project combines **remote sensing, Landsat 8/9 imagery, NDVI analysis, JavaScript, interactive UI development, linked maps, and split-panel visualization** into a portfolio-ready geospatial application.

---

## 🌎 Project Overview

The **Western Kentucky Vegetation Condition Explorer** was developed as the final integrated mini-project of a Google Earth Engine application-development training workflow.

The project brings together concepts including:

- Client-side and server-side processing in Google Earth Engine
- Landsat image processing
- NDVI calculation
- Interactive UI widgets
- Callback functions
- Earth Engine App development
- Multi-year comparison
- Linked maps
- Split-panel visualization
- Application publishing

The application allows a user to select **two different years** and compare vegetation conditions or satellite imagery for the same geographic area.

Available visualization modes include:

- 🌿 NDVI
- 🛰️ True Color Satellite Imagery
- 🌱 False Color Vegetation Imagery

The two maps are linked so that zooming or panning one map automatically updates the other map to the same geographic extent.

---

## 🎯 Project Objectives

The main objectives of this project were to:

- Retrieve Landsat imagery using Google Earth Engine
- Work with Landsat 8 and Landsat 9 surface reflectance products
- Filter imagery by geographic area
- Filter imagery by date
- Apply cloud-cover filtering
- Scale Landsat surface reflectance bands
- Generate seasonal median composites
- Calculate NDVI
- Compare vegetation conditions across multiple years
- Build interactive UI controls
- Implement callback functions
- Allow dynamic year selection
- Provide multiple visualization options
- Create two independent map views
- Synchronize map navigation
- Build a split-panel comparison interface
- Prepare an interactive Earth Engine application for publishing

---

## 📍 Study Area

The project focuses on **Western Kentucky, USA**.

A regional study area was defined in Google Earth Engine to support multi-year comparison of vegetation and satellite imagery.

The application uses summer imagery to represent growing-season conditions.

---

## 📅 Available Years

The application currently supports comparisons between:

- 2018
- 2019
- 2020
- 2021
- 2022
- 2023
- 2024

Users can independently select a year for the **left map** and another year for the **right map**.

This allows both consecutive-year and longer-term comparisons.

---

## 🛰️ Satellite Data

The project uses **Landsat Collection 2 Level-2 Surface Reflectance** imagery.

### Landsat 8

```text
LANDSAT/LC08/C02/T1_L2
```

### Landsat 9

```text
LANDSAT/LC09/C02/T1_L2
```

The Landsat collections are filtered according to:

- Study area
- Analysis year
- Summer growing-season period
- Scene-level cloud cover

Landsat 8 and Landsat 9 imagery are merged where applicable before the seasonal composite is generated.

---

## 🌿 NDVI Analysis

The application calculates the **Normalized Difference Vegetation Index (NDVI)**.

NDVI is a commonly used remote-sensing index for representing relative vegetation greenness.

### NDVI Formula

```text
NDVI = (NIR - Red) / (NIR + Red)
```

For Landsat 8 and Landsat 9:

```text
Near Infrared = SR_B5
Red           = SR_B4
```

Higher positive NDVI values generally indicate greener vegetation.

Lower values can represent areas with less green vegetation as well as water, developed surfaces, bare soil, or other non-green surfaces.

---

## ⚙️ Remote Sensing Workflow

The application follows the workflow below.

### 1. Define Study Area

A regional geometry covering Western Kentucky is created in Google Earth Engine.

### 2. Select Analysis Years

The user independently selects years for the left and right maps.

### 3. Retrieve Landsat Data

Landsat 8 and Landsat 9 Collection 2 Level-2 imagery is retrieved.

### 4. Spatial Filtering

The image collections are filtered to imagery intersecting the study area.

### 5. Temporal Filtering

The imagery is filtered to the summer growing-season period for each selected year.

### 6. Cloud Filtering

Scenes with relatively high cloud-cover metadata values are excluded from the collection.

### 7. Surface Reflectance Scaling

The Landsat Collection 2 Level-2 optical bands are scaled using the appropriate scale factor and offset.

### 8. Merge Landsat Collections

Landsat 8 and Landsat 9 imagery are combined where applicable.

### 9. Create Seasonal Composite

A median composite is generated from the available imagery for each selected year.

### 10. Calculate NDVI

The red and near-infrared bands are used to calculate NDVI.

### 11. Display Results

The resulting imagery is sent to the interactive map interface for visualization and comparison.

---

## 🖥️ Interactive Application

The application provides a custom user interface built with the **Google Earth Engine UI API**.

The control panel contains:

- Application title
- Instructions
- Left map year selector
- Right map year selector
- Display layer selector
- Current comparison status
- Reset button
- NDVI information
- Application limitations

Users can change the analysis without modifying the underlying JavaScript code.

---

## 🎛️ Interactive Controls

### Left Map Year

The first dropdown controls the year displayed on the left map.

### Right Map Year

The second dropdown controls the year displayed on the right map.

### Display Layer

Users can select between three visualization modes:

```text
NDVI
True Color
False Color Vegetation
```

### Reset Application

The **Reset Application** button restores the application to its default configuration.

---

## 🗺️ Split-Panel Visualization

The application creates two separate Earth Engine map objects using:

```javascript
ui.Map()
```

The maps are displayed side-by-side using:

```javascript
ui.SplitPanel()
```

The left and right maps display the same geographic area but can represent different years.

This makes it possible to directly compare spatial patterns between two time periods.

---

## 🔗 Linked Map Navigation

The two maps are synchronized using:

```javascript
ui.Map.Linker()
```

This means that when a user:

- Pans the left map
- Pans the right map
- Zooms into the left map
- Zooms into the right map

the other map automatically follows.

The linked-map design allows direct comparison of exactly the same geographic area.

---

## 🔄 Application Workflow

```text
                  Landsat 8 + Landsat 9
                           │
                           ▼
                   Study Area Filter
                           │
                           ▼
                    Date Filtering
                           │
                           ▼
                    Cloud Filtering
                           │
                           ▼
              Surface Reflectance Scaling
                           │
                           ▼
                Seasonal Median Composite
                           │
            ┌──────────────┼──────────────┐
            │              │              │
            ▼              ▼              ▼
          NDVI        True Color     False Color
            │              │              │
            └──────────────┼──────────────┘
                           │
                           ▼
                    UI Layer Selector
                           │
              ┌────────────┴────────────┐
              ▼                         ▼
         Left Year                  Right Year
              │                         │
              ▼                         ▼
         Left ui.Map                Right ui.Map
              │                         │
              └────────────┬────────────┘
                           │
                           ▼
                     ui.Map.Linker
                           │
                           ▼
                     ui.SplitPanel
                           │
                           ▼
               Interactive GEE Application
```

---

# 📸 Project Results

## 1. NDVI Comparison — 2021 vs 2022

The application can compare vegetation conditions between two consecutive years.

The example below displays **2021 NDVI on the left** and **2022 NDVI on the right**.

![NDVI 2021 vs 2022](screenshots/01_NDVI_2021_vs_2022.png)

---

## 2. Multi-Year NDVI Comparison — 2018 vs 2024

The year-selection controls also support longer-term comparisons.

This example compares **2018 with 2024**, demonstrating the ability to explore vegetation patterns across a six-year interval.

![NDVI 2018 vs 2024](screenshots/02_NDVI_2018_vs_2024.png)

---

## 3. True Color Comparison — 2021 vs 2022

Users can switch from NDVI to **True Color Landsat imagery**.

This provides a more natural visual representation of the landscape and allows satellite imagery from two years to be compared directly.

![True Color 2021 vs 2022](screenshots/03_TrueColor_2021_vs_2022.png)

---

## 4. False Color Vegetation Comparison — 2021 vs 2022

The application also provides a **False Color Vegetation** visualization.

Near-infrared information is used to emphasize vegetation patterns that may be less obvious in true-color imagery.

![False Color Vegetation 2021 vs 2022](screenshots/04_FalseColor_2021_vs_2022.png)

---

## 5. Zoomed Split-Panel Comparison — 2018 vs 2024

The synchronized map views allow the user to zoom into a specific location while maintaining the same geographic extent on both sides.

The example below demonstrates a more detailed NDVI comparison between **2018 and 2024**.

![Split Panel Zoomed Comparison](screenshots/05_SplitPanel_Zoomed_Comparison.png)

---

## 💻 Technologies Used

| Technology | Application |
|---|---|
| Google Earth Engine | Cloud-based geospatial processing |
| JavaScript | Application development |
| Landsat 8 | Satellite surface reflectance imagery |
| Landsat 9 | Satellite surface reflectance imagery |
| NDVI | Vegetation greenness analysis |
| Earth Engine UI API | Interactive application controls |
| `ui.Map` | Independent map views |
| `ui.Map.Linker` | Synchronized map navigation |
| `ui.SplitPanel` | Side-by-side comparison |
| GitHub | Project documentation and portfolio hosting |

---

## 🧠 Google Earth Engine Concepts Demonstrated

### Client vs. Server

The project applies concepts related to the distinction between normal JavaScript client-side values and Earth Engine server-side objects.

Examples of Earth Engine server-side objects used in the application include:

```javascript
ee.Image()
ee.ImageCollection()
ee.Geometry()
```

---

### Image Collections

Satellite imagery is handled through:

```javascript
ee.ImageCollection()
```

The collections are filtered spatially and temporally before being processed.

---

### UI Panels

The application's control interface uses:

```javascript
ui.Panel()
```

---

### UI Labels

Titles, instructions, status information, and explanatory text use:

```javascript
ui.Label()
```

---

### Dropdown Controls

Interactive year and visualization selection uses:

```javascript
ui.Select()
```

---

### Buttons

The reset functionality is implemented with:

```javascript
ui.Button()
```

---

### Callback Functions

User selections trigger callback functions through:

```javascript
.onChange()
```

When a user changes a year or visualization type, the application automatically updates both maps.

---

### Map Objects

Two independent maps are created with:

```javascript
ui.Map()
```

---

### Linked Maps

Navigation is synchronized with:

```javascript
ui.Map.Linker()
```

---

### Split Panel

The two maps are displayed side-by-side with:

```javascript
ui.SplitPanel()
```

---

## 🛠️ Skills Demonstrated

This project demonstrates practical experience with:

- Google Earth Engine
- JavaScript
- Remote sensing
- Landsat 8/9 processing
- Satellite image filtering
- Surface reflectance processing
- ImageCollection operations
- Seasonal composite generation
- NDVI calculation
- Multi-temporal analysis
- Vegetation visualization
- True-color visualization
- False-color visualization
- Client/server concepts
- Interactive UI design
- Callback functions
- Dynamic map updates
- Linked map navigation
- Split-panel visualization
- Interactive web mapping
- Geospatial application development
- Application testing
- Technical documentation
- GitHub project organization

---

## 📂 Repository Structure

```text
gee-vegetation-condition-explorer/
│
├── README.md
│
├── scripts/
│   └── vegetation-condition-explorer.js
│
├── screenshots/
│   ├── 01_NDVI_2021_vs_2022.png
│   ├── 02_NDVI_2018_vs_2024.png
│   ├── 03_TrueColor_2021_vs_2022.png
│   ├── 04_FalseColor_2021_vs_2022.png
│   └── 05_SplitPanel_Zoomed_Comparison.png
│
└── documentation/
    └── workflow-summary.md
```

---

## 🚀 Live Google Earth Engine Application

A published interactive version of the project can be accessed through Google Earth Engine Apps.

**Live Application:**

`ADD_FINAL_GEE_APP_URL_HERE`

> Replace the placeholder above with the final published Earth Engine App URL.

---

## ⚠️ Limitations

This project is intended as an **interactive remote-sensing visualization and portfolio demonstration**.

The application currently uses:

- Seasonal Landsat median composites
- Scene-level cloud-cover filtering
- A fixed summer analysis period
- NDVI as the primary vegetation indicator

Differences observed between two years can result from multiple factors, including:

- Vegetation condition
- Crop phenology
- Crop type
- Planting and harvesting timing
- Weather conditions
- Image availability
- Residual clouds
- Cloud shadows
- Land-cover change
- Soil conditions
- Surface moisture
- Other environmental factors

Therefore, differences in NDVI **should not automatically be interpreted as drought**.

The application is a vegetation-condition visualization and comparison tool rather than an operational drought-classification system.

---

## 🔮 Future Improvements

Several improvements could expand the capabilities of the application.

### Improved Cloud Masking

Implement pixel-level cloud and cloud-shadow masking using Landsat quality-assurance information.

### NDVI Anomalies

Compare annual NDVI against a long-term vegetation baseline.

### Precipitation

Integrate precipitation datasets such as CHIRPS to evaluate rainfall anomalies.

### Land Surface Temperature

Add thermal information to examine temperature-related vegetation stress.

### Evapotranspiration

Integrate ET datasets for additional agricultural water-stress information.

### Agricultural Land Mask

Restrict analysis to cropland and pasture areas.

### Interactive Charts

Allow users to click a location and display vegetation time-series information.

### Dynamic Dates

Allow users to select custom start and end dates.

### Difference Maps

Calculate direct NDVI differences between selected years.

### Additional Vegetation Indices

Future versions could incorporate additional spectral indices for vegetation and environmental monitoring.

### Downloadable Results

Allow users to export statistics or processed data for further analysis.

---

## 📚 Training Progression

This final project consolidated concepts developed throughout the week's Google Earth Engine training.

```text
Day 1
Client vs. Server
        │
        ▼
Day 2
Using Earth Engine UI Elements
        │
        ▼
Day 3
Building an Earth Engine App
        │
        ▼
Day 4
Publishing an Earth Engine App
        │
        ▼
Day 5
Creating a Split-Panel App
        │
        ▼
Final Integrated Mini-Project
        │
        ▼
Western Kentucky Vegetation Condition Explorer
```

### Day 1 — Client vs. Server

Practiced the difference between JavaScript client-side values and Earth Engine server-side objects and reviewed appropriate handling of server-side computations.

### Day 2 — UI Elements

Worked with interactive Earth Engine widgets including panels, labels, dropdown menus, and buttons.

### Day 3 — Building an App

Combined satellite processing, UI controls, callback functions, and dynamic map updates into an interactive Earth Engine application.

### Day 4 — Publishing

Practiced the Earth Engine App publishing workflow and application settings.

### Day 5 — Split Panel

Created multiple `ui.Map` objects, synchronized their navigation, and displayed them using a split-panel layout.

### Final Mini-Project

Combined these skills into the **Western Kentucky Vegetation Condition Explorer**.

---

## 📋 Project Deliverables

The completed project includes:

- Final Google Earth Engine JavaScript application
- Interactive year-selection controls
- NDVI visualization
- True-color visualization
- False-color vegetation visualization
- Linked split-panel maps
- Multi-year comparison functionality
- Application screenshots
- GitHub documentation
- Workflow summary
- Published Earth Engine App when available

---

## 📌 Key Learning Outcome

The primary outcome of this project was learning how to move beyond a standard Earth Engine analysis script and develop a more complete **interactive geospatial application**.

The project connects:

**Satellite Data → Remote Sensing Processing → JavaScript Logic → UI Controls → Interactive Visualization → Web Application**

This workflow demonstrates how cloud-based geospatial analysis can be transformed into an interface that allows users to explore results without editing the underlying code.

---

## 👤 Author

**Harsh Vashishth**

GIS | Remote Sensing | Google Earth Engine | ArcGIS Pro | QGIS | Python

GitHub:  
https://github.com/harshvashishth-gis-developer

---

## 📌 Portfolio Purpose

This project was developed as a portfolio demonstration of **Google Earth Engine application development, Landsat remote sensing, vegetation analysis, multi-temporal comparison, and interactive geospatial visualization**.

It demonstrates the progression from satellite-data processing and NDVI calculation to the development of a functional interactive mapping application.
