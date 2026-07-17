# AntarcticPyVistaVisualization
Workflow for mapping regions of the Antarctic continent based on bed and surface topography, with a focus on bed elevation. 
This project uses GeoTIFF Digital ELevation Maps (DEMs) to plot regions of Antarctica in 3D space to help visualize the 
topographic difference between bed and surface in an interactive and visually cohesive manner. 
The following graph is a section of the Ronne Ice Shelf chosen to display the capabilities of the project.

<img src="Images/TestRegion.png">

This project also seeks to plot and compare the bed elevation data created by stochastic realizations of glacial bed topography
as part of an ongoing project to improve textural representations of sub-glacial topography. More information can be found at 
https://github.com/GatorGlaciology/DEMOGORGN-Antarctica. The following graph is the difference between Bedmap, 
an Antarctic bed topography dataset, and one stochastic bed realization of Scott Glacier.

<img src="Images/ScottDifference.png">

# Data Access
The data used in this project can be accessed via GEBCO's interactive grid (https://download.gebco.net/). 
To download the dataset used in this project, change the data in the top left corner of the screen to *GEBCO 2025 South Polar*, 
select subset options, change the top and right bounds to 4400000 and the left and bottom bounds to -4400000. 
Issues may arise if bounds are different. Click 'layers and formats', select both *Bathymetry* and *Bathymetry (sub ice)*. 
Only *GeoTIFF* is required for the data format. Click add to basket and then make sure the basket icon in the top right is green, click it, then submit. 
Go to the download section to the right of the basket and the data is available there after some time. Below is a screenshot of the process for clarity.

<img src="Images/Process.png">

The data for the example bed is being used as part of an ongoing project, DEMOGORGN, to iteratively determine subglacial 
topography for various fast flowing glacial regions. Scott Glacier is one of these and the example used in the project.

The grounding line data `moa2014_grounding_line_v01.shp` is provided in the repository. Unfortunately, it is not currently integrated into the 3D
PyVista plot.

# Jupyter Notebook Activation
All dependencies are listed in the `geo-python-polar.yml` file for use in a Conda Jupyter Notebook environment.

To activate, open the command line and using the *cd* command, navigate to the folder with the `geo-python-polar.yml` file. 
Then, type the following into the command line:


- conda env create -f geo-python-polar.yml

- conda activate geo-python-polar

- jupyter lab


This will launch Jupyter Notebook in the browser. When reopenning the environment after is has been created, only use the second and third lines of code.

# Usage

All code is found in the `PolarTiff.ipynb` jupyter notebook file. Before running the code, find the polar stereographic coordinates 
of the region you are interested in displaying and, if applicable, have a csv of a study region containing the bedmap bed 
topography for the region and a bed realization. The following are cells where significant change can and might need to be made. 
All other cells can be run without modification. If issues arise, check and change them first:

- In cells 5 or 6, replace *xminpolar*, *xmaxpolar*, *yminpolar*, and *ymaxpolar* with the new coordinates.
  The GEBCO interactive grid can be used to visualize coordinate region and is a helpful reference for where a region is on the continental scale.

- In cell 18, change the coefficients for *xminpolar*, *yminpolar*, and the *cmax* exponent to change the position of the camera in the following plot.
  They are already based on region-specific data, so only fine-tuning should be required, though exceptions exist.

- In cell 19, change *zscale* to better match elevation difference in region, *color* and *opacity* for surface transparency,
  *cmap* if you want to, and any other numerical value.

If running the code without the `ScottDataGridded.csv` and `bed_10000k.npy` files or another bed csv and realization file, stop the code here. 
The following code will not work.

- In cells 20 and 22, change the `ScottDataGridded.csv` and `bed_10000k.npy` file locations to your csv and bed realization respectively.

- In cell 24, change camera position as in cell 18.

- In cells 25 and 28, change variables as in cell 19

To recreate `TestRegion.png`, run cell 5 and not 6 and end after cell 19. 
To recreate `ScottDifference.png`, download `ScottDataGridded.csv` and `bed_10000k.npy`, place them in the same folder as the `PolarTiff.ipynb` 
and run the code from start to finish (cell 5 will be overwritten).

# References

GEBCO Compilation Group (2025) GEBCO 2025 Grid (doi:10.5285/ 37c52e96-24ea-67ce-e063-7086abc05f29)

Haran, T., M. Klinger, J. Bohlander, M. Fahnestock, T. Painter, and T. Scambos. 2018, updated
2019. MEaSUREs MODIS Mosaic of Antarctica 2013-2014 (MOA2014) Image Map, Version 1.
[Indicate subset used]. Boulder, Colorado USA. NASA National Snow and Ice Data Center Distributed
Active Archive Center. https://doi.org/10.5067/RNF17BP824UM

# Authorship and Liscense
This project was authored by Milo Rasz. Liscense information is in the corresponding LISCENSE file. No generative AI was used in this project.
