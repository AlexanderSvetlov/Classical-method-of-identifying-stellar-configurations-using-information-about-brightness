# Classical-method-of-identifying-stellar-configurations-using-information-about-brightness

We present an open implementation of a classical geometric algorithm for the initial identification of stellar configurations using both coordinate-only and coordinate–photometric information. The repository is intended for testing classical star identification and attitude determination methods, comparing them with alternative approaches (including neural-network-based ones), and serving as a baseline reference for the development of new algorithms.

The notebooks use efficient tools for working with large datasets, including the Apache Parquet storage format, the Polars library for tabular data processing, and the KDTree data structure for fast spatial searches.

---

## Описание программных компонентов репозитория

### Algorithm.ipynb

The main notebook of the repository, implementing the procedure for the initial identification of stellar configurations.

Two operating modes are implemented:
- coordinate-only (using angular distances only);
- coordinate–photometric (using both angular distances and stellar brightness).

The notebook can be used with both real images and “virtual” images. For each case, verification methods are provided to validate the output results of the algorithm, including the determination of the image frame center coordinates.

Key algorithm parameters include:
- allowable error in angular distance comparison;
- allowable error in stellar magnitude comparison;
- characteristics of the analyzed image.

---

### Dataset.ipynb

This notebook is used to create a star catalog containing navigation stars that are employed by the algorithm for identifying stellar configurations in an image.

The star catalog includes celestial coordinates of navigation stars, their stellar magnitudes, and unique Gaia identifiers. The catalog is constructed using Gaia DR2 data with constraints on the range of celestial coordinates and on the maximum stellar magnitude. The limiting magnitude can be specified by the user and is selected according to the characteristics of the simulated star sensor.

In addition to the data table, the program implements the inclusion of images of the selected region of the celestial sphere. The sky survey used to add images can be changed within the program.
To obtain images, it is necessary to specify their parameters, which are determined by the characteristics of the star sensor image detector:
- field-of-view radius;
- number of pixels in the detector matrix;
- pixel size in degrees.

As a result, a dataset (star catalog and sky images) is formed that enables comprehensive studies of star identification and attitude determination methods. During dataset creation, a file containing information about its characteristics is also generated.

Additionally, information about star coordinates on the images can be added to the catalog using the IRAF tool. These data can be used to study and compare centroiding methods, as well as to analyze the influence of centroid position errors on the algorithm’s performance.

We also provide a ready-made dataset created by us based on the GAIA DR2 catalog and the DSS sky survey, available in ZIP format at https://disk.360.yandex.ru/d/o_NG6FBhhDggcw.
Detailed information about the dataset and the selected image parameters is included in a text file at the same link. Our catalog contains stars covering the full range of right ascension, with declinations limited to the range (−70 deg, 70 deg).

---

### DistsCatalog.ipynb

This notebook is intended for generating the distance catalog of the star sensor database. It allows the creation of a table containing angular distances between navigation stars from the star catalog.

The main configurable parameters are: 
- maximum angular distance between stars in a pair;
- limiting stellar magnitude of the catalog (corresponding to the limiting magnitude of the star catalog).

---
