# California Housing: Area and Population Analysis

A data visualization and geospatial analysis project exploring the relationship between geographical location, population density, and housing characteristics across California. This project demonstrates advanced matplotlib techniques, spatial data visualization, and statistical analysis of real-world census data.

## 📋 Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Dataset](#dataset)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Usage](#usage)
- [Visualizations](#visualizations)
- [Analysis Insights](#analysis-insights)
- [Methodology](#methodology)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## 🎯 Overview

This project creates stunning geospatial visualizations of California housing data, mapping the relationship between geographical coordinates, population density, and median house values. Using sophisticated scatter plot techniques with the Viridis colormap, the project produces an intuitive visual representation that resembles the actual geography of California, revealing population concentration patterns and housing market dynamics.

**Project Objectives:**
- Visualize California's population distribution geographically
- Analyze relationship between location and population density
- Create publication-quality data visualizations
- Demonstrate advanced matplotlib techniques
- Explore housing characteristics across California

## ✨ Features

- **Geospatial Visualization**: Location-based scatter plots with longitude/latitude mapping
- **Population Density Mapping**: Color-coded representation using logarithmic scale
- **Proportional Markers**: Bubble sizes represent population magnitude
- **Professional Styling**: Seaborn styling for publication-quality plots
- **Custom Legend**: City area representation with interpretable markers
- **Statistical Analysis**: Comprehensive descriptive statistics
- **Data Quality**: Complete dataset with no missing values
- **Multiple Housing Metrics**: Income, house value, and demographic features

## 📊 Dataset

### Dataset Overview
- **Source**: California Housing Dataset (sklearn sample_data)
- **Total Records**: 17,000 observations
- **Features**: 9 columns
- **Geographic Coverage**: Entire state of California
- **Time Period**: 1990 Census data

### Features Description

| Feature | Description | Type | Range |
|---------|-------------|------|-------|
| longitude | Longitude coordinate | Float | -124.35 to -114.31 |
| latitude | Latitude coordinate | Float | 32.54 to 41.95 |
| housing_median_age | Median age of houses in block | Integer | 1 to 52 years |
| total_rooms | Total rooms in block | Integer | 2 to 39,320 |
| total_bedrooms | Total bedrooms in block | Integer | 1 to 6,445 |
| population | Block population | Integer | 3 to 35,682 |
| households | Number of households in block | Integer | 1 to 6,082 |
| median_income | Median income (tens of thousands) | Float | 0.4999 to 15.0001 |
| median_house_value | Median house value | Integer | 14,999 to 500,001 |

### Sample Data
```
   longitude  latitude  housing_median_age  total_rooms  total_bedrooms
0    -114.31     34.19                15.0       5612.0          1283.0
1    -114.47     34.40                19.0       7650.0          1901.0
2    -114.56     33.69                17.0        720.0           174.0
3    -114.57     33.64                14.0       1501.0           337.0
4    -114.57     33.57                20.0       1454.0           326.0

   population  households  median_income  median_house_value
0      1015.0       472.0         1.4936             66900.0
1      1129.0       463.0         1.8200             80100.0
2       333.0       117.0         1.6509             85700.0
3       515.0       226.0         3.1917             73400.0
4       624.0       262.0         1.9250             65500.0
```

## 🛠 Technologies Used

### Core Technologies
- **Python 3.x**: Primary programming language
- **Pandas**: Data manipulation and analysis
- **NumPy**: Numerical computing
- **Matplotlib**: Data visualization
- **Seaborn**: Statistical visualization styling

### Development Environment
- **Google Colab**: Cloud-based development
- **Jupyter Notebook**: Interactive computing

### Python Dependencies
```python
pandas==1.5.3
numpy==1.23.5
matplotlib==3.7.1
seaborn==0.12.2
```

## 📥 Installation

### Prerequisites
- Python 3.8 or higher
- pip package manager

### Local Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/california-housing-visualization.git
   cd california-housing-visualization
   ```

2. **Create virtual environment** (recommended)
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install required packages**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the analysis**
   ```bash
   jupyter notebook California_Area-and-Population.ipynb
   ```

### Google Colab Setup

1. Upload the notebook to Google Colab
2. The dataset is available in Colab's sample_data
3. Run all cells to generate visualizations

## 💻 Usage

### Loading and Preprocessing

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn

# Set seaborn style for better aesthetics
seaborn.set()

# Load the California housing dataset
cities = pd.read_csv("/content/sample_data/california_housing_train.csv")

# Display basic information
print(cities.head())
print(cities.shape)
print(cities.info())
```

### Extracting Key Features

```python
# Extract coordinates and population
latitude = cities["latitude"]
longitude = cities["longitude"]
population = cities["population"]
```

### Creating the Visualization

```python
# Define area for marker size (scale population data)
area = population / 100

# Create scatter plot with population density coloring
plt.scatter(longitude, latitude, 
           label=None, 
           c=np.log10(population),
           cmap='viridis', 
           s=area, 
           linewidth=0, 
           alpha=0.5)

# Set aspect ratio to match geographical proportions
plt.gca().set_aspect('equal')

# Add labels and colorbar
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.colorbar(label='log$_{10}$(population)')
plt.clim(3, 7)

# Create custom legend for city areas
for area_legend in [100, 300, 500]:
    plt.scatter([], [], c='k', alpha=0.3, s=area_legend, 
               label=str(area_legend) + 'km$^2$')

plt.legend(scatterpoints=1, frameon=False, 
          labelspacing=1, title='City Areas')
plt.title("Area and Population of California Cities")
plt.show()
```

## 📊 Visualizations

### Main Visualization: Geospatial Population Map

The primary visualization creates a scatter plot that reveals California's geography through data:

**Visual Elements:**
1. **Position**: Longitude (x-axis) and Latitude (y-axis) create geographical layout
2. **Color**: Log-scale population density (Viridis colormap)
   - Purple/Blue: Lower population (10³ to 10⁴)
   - Green/Yellow: Higher population (10⁵ to 10⁷)
3. **Size**: Bubble area represents population magnitude
4. **Transparency**: Alpha=0.5 allows visualization of overlapping points

**Geographical Features Revealed:**
- **Coastal concentration**: Dense population along the coast
- **Bay Area**: Clear visualization of San Francisco Bay Area population
- **Los Angeles Basin**: Dense population cluster in Southern California
- **Central Valley**: Agricultural areas with distributed population
- **Mountain regions**: Sparse population in Sierra Nevada
- **Desert areas**: Low density in southeastern California

### Color Mapping

The logarithmic scale (log₁₀) is essential because:
- Raw population values span orders of magnitude
- Linear scale would make low-population areas invisible
- Log scale provides better visual discrimination
- Range: 10³ (1,000) to 10⁷ (10,000,000) people

### Legend Interpretation

The custom legend shows three reference sizes:
- **100 km²**: Small city/neighborhood area
- **300 km²**: Medium-sized urban area
- **500 km²**: Large metropolitan area

## 📈 Analysis Insights

### Population Distribution Patterns

1. **Coastal Dominance**
   - Majority of California's population lives within 50 miles of coast
   - Clear visualization of coastal cities and metropolitan areas

2. **Urban Concentration**
   - Three major metropolitan regions clearly visible:
     * San Francisco Bay Area (37°N, -122°W)
     * Los Angeles Basin (34°N, -118°W)
     * San Diego Area (33°N, -117°W)

3. **Geographic Constraints**
   - Mountains and deserts create natural population boundaries
   - Population follows habitable and economically viable areas

4. **Housing Characteristics**
   - Median house values correlate with coastal proximity
   - Population density influences housing prices
   - Geographic features impact development patterns

### Statistical Observations

- **Longitude Range**: -124° to -114° (approximately 600 miles wide)
- **Latitude Range**: 33° to 42° (approximately 600 miles north-south)
- **Population Centers**: Concentrated in coastal regions
- **Rural Areas**: Visible gaps in Central Valley and mountain regions

## 🔬 Methodology

### Data Processing Steps

1. **Data Loading**: Import California housing dataset
2. **Feature Selection**: Extract longitude, latitude, population
3. **Data Transformation**: Apply log₁₀ transformation to population
4. **Scaling**: Scale population to appropriate marker sizes
5. **Visualization**: Create scatter plot with custom styling
6. **Annotation**: Add colorbar, legend, and labels

### Visualization Techniques

- **Aspect Ratio**: Equal aspect ratio maintains geographical accuracy
- **Transparency**: Alpha blending reveals overlapping data points
- **Color Mapping**: Viridis colormap (perceptually uniform, colorblind-friendly)
- **Size Encoding**: Proportional sizing for intuitive interpretation
- **Log Scale**: Handles wide range of population values

### Design Principles Applied

1. **Perceptual Uniformity**: Viridis colormap ensures consistent perception
2. **Accessibility**: Colorblind-safe color scheme
3. **Data-Ink Ratio**: Minimal non-data elements
4. **Multi-dimensional Encoding**: Position, color, and size convey information
5. **Context Preservation**: Geographic layout maintains spatial relationships

## 🚀 Future Enhancements

### Analysis Extensions
- [ ] **Interactive Maps**: Implement Folium or Plotly for interactive exploration
- [ ] **Time Series Analysis**: Analyze housing trends over time
- [ ] **Predictive Modeling**: Build models for house value prediction
- [ ] **Clustering Analysis**: Identify housing market segments
- [ ] **Correlation Studies**: Analyze feature relationships

### Visualization Improvements
- [ ] **3D Visualization**: Add house value as third dimension
- [ ] **Animation**: Show temporal changes in housing market
- [ ] **Heatmaps**: Create density heatmaps for population
- [ ] **Choropleth Maps**: County-level aggregation
- [ ] **Dashboard**: Interactive Plotly Dash application

### Technical Enhancements
- [ ] **API Integration**: Real-time housing data
- [ ] **Web Application**: Deploy as web-based tool
- [ ] **Database Integration**: PostgreSQL with PostGIS
- [ ] **Machine Learning**: Implement price prediction models
- [ ] **Comparative Analysis**: Compare with other states

## 🤝 Contributing

Contributions are welcome! Areas for contribution:

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/NewVisualization`)
3. Commit your Changes (`git commit -m 'Add density heatmap'`)
4. Push to the Branch (`git push origin feature/NewVisualization`)
5. Open a Pull Request

### Contribution Ideas
- Additional visualization types
- Statistical analysis methods
- Code optimization
- Documentation improvements
- Interactive features

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📧 Contact

**Veera Ajay Kumar Angajala**
- Email: your.email@example.com
- LinkedIn: [Your LinkedIn Profile](https://linkedin.com/in/yourprofile)
- GitHub: [@yourusername](https://github.com/yourusername)
- Portfolio: [Your Portfolio](https://yourportfolio.com)

## 🙏 Acknowledgments

- **Scikit-learn** for providing the California Housing dataset
- **Matplotlib** and **Seaborn** teams for excellent visualization libraries
- **Viridis colormap** creators for perceptually uniform color scheme
- **Google Colab** for computational resources
- Python data science community

## 📚 References

- [California Housing Dataset Documentation](https://scikit-learn.org/stable/datasets/real_world.html#california-housing-dataset)
- [Matplotlib Scatter Plot Documentation](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.scatter.html)
- [Viridis Colormap](https://cran.r-project.org/web/packages/viridis/vignettes/intro-to-viridis.html)
- [Geospatial Data Visualization Best Practices](https://www.axismaps.com/guide/)

## 🎨 Visualization Gallery

This project demonstrates:
- **Publication-quality graphics** suitable for academic papers
- **Professional styling** appropriate for business presentations
- **Clear communication** of complex spatial relationships
- **Aesthetic design** following data visualization principles

---

**⭐ If you found this visualization project helpful, please consider giving it a star!**

*Last Updated: December 2025*
