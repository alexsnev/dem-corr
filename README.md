# Displacement Vectors Calculation Executable

Author: Alexis Neven (alexis.neven@gmail.com)
Date: 2022305-10
Info: This executable computes displacement vectors between two GeoTIFF images, to be applied in LandSlide displacement quantification using repeated DEM.

---

## Principle

This program calculates the displacement vectors between two georeferenced TIFF images using the maximum correlation of patterns method. It works by comparing small sub-images (boxes) from the first image to the corresponding areas in the second image and finding the maximum correlation between them. The displacement vector is then calculated based on the position difference of the maximum correlation.

**Note:** For large images, the code can take significant time to compute.

---

## Input Requirements

The input images must meet the following requirements:
- File format: GeoTIFF (.tif)
- Georeferenced
- Same resolution
- Single grayscale band

**Note:** Either HillShade or DEM can be used. Hillshade often provides good results.

---

## Usage

```displacement_vectors.exe image1 image2 nx_box ny_box overlap max_disp```

- `image1`: Path to the first GeoTIFF image
- `image2`: Path to the second GeoTIFF image
- `nx_box`: Width of the comparison box (in cells of the raster)
- `ny_box`: Height of the comparison box (in cells of the raster)
- `overlap`: Overlap ratio between comparison boxes (0-1) (1 == one point in each cell, 0 == one point every nx_box,ny_box)
- `max_disp`: Maximum expected displacement (used for both vertical and horizontal) (in cells of the raster)

The output will be saved in a shapefile with the prefix "output_displacement_points.shp". The shape points have 3 fields:
- `x_displace` (displacement in X)
- `y_displace` (displacement in Y)
- `total_displace` (sqrt(x_displace^2 + y_displace^2))

**Note:** The launch of the program can be long because of the Windows antimalware.

---

## Example

Two example images are provided in the repo. These images are hillshades from the same area, acquired in 2019 and 2021. They were freely downloaded from the SwissTopo website. (https://www.swisstopo.admin.ch/fr/geodata/height/alti3d.html) and are only provided as example

```displacement_vectors.exe data/image1.tif data/image2.tiff 50 50 0.5 20```

This example will compute the displacement between two images (`image1` and `image2`). In this case, the images have a resolution of 0.5 meters, then:

- `nx_box = 50`, which is equal to 50 * 0.5m = 25 meters
- `ny_box = 50`, which is equal to 50 * 0.5m = 25 meters
- `max_disp = 20`, which is equal to 20 * 0.5 = 20 meters
