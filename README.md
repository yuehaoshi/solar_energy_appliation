# Solar-Energy-Appliation

This project is to make visualization about solar energy application potential, including explanation of solar energy distribution by solar-earth system model visualization, solar intensity map visualization as well as solar panel installation and usage suggestion for specific locations. The whole project is to be divided into three parts:

## Part 1. Solar Energy Distribution Explanation

The first part is to explain solar energy distribution with a visualization model for solar-earth system. In this part, a model of solar-sun 3D system is going to be constructed to illustrate why solar energy is distributed unevenly on the earth. The idea of solar system simulation model comes from the code developed by Aman Kharwal (Kharwal, 2020).

To simulate the solar-earth system, two functions, “spheres” and “orbits” were defined to represent the shape and movement trace of sun and earth with “graph_objects” module in Python Plotly. To better illustrate the visualization effect, the diameter of the earth sphere was made ten times larger than the real size. The system then was constructed with “Layout” method in graph_objects module by applying the sizes of sun and earth in “spheres” function and the distance between sun and earth into the “orbits” function. The generated system is shown as Figure 1 below:

<p align="center">
  <img src="https://github.com/yuehaoshi/myFiles/blob/main/WebPics/Solar%20Visualization%20Project/SolarVis1.png" alt="Oops, this image disappeared.."/>
</p>
<h6 align="center">Figure 1: Model of earth-solar system</h6>

The goal of this part of the project was to visually illustrate why solar energy varies in the different time and location of the earth surface. To achieve this goal, the color of the earth was modified as gradient color, with brighter color on the side of the earth towards sun, and darker color on the side of the earth backwards to the sun. The surface color of the earth was set to be positively related to the coordinate of the point on the sphere. More specifically, the color of each pixel on the surface of the sphere was set to be proportional to “x0**2 - y0**2 - z0**2”, where x0, y0, and z0 were the coordinates to each point. After changing the surface color, the solar-earth system was shown in the Figure 2 below, where the surface of the earth was brighter in the side closer to the sun and vice versa. This model shows the basic principle of the solar energy application in different places of the earth: generally speaking, the equator area where can get most of the direct sunlight, has more sunlight intensity compared to polar areas of the earth, thus has more efficiency if applied infrastructures by solar energy industry.

<p align="center">
  <img src="https://github.com/yuehaoshi/myFiles/blob/main/WebPics/Solar%20Visualization%20Project/SolarVis2.png" alt="Oops, this image disappeared.."/>
</p>
<h6 align="center">Figure 2: Visualization about sunlight effect to earth</h6>

## Part 2: Peak Sun Hour (PSH) Distribution in Different US States

The second part of this project is to visualize the solar energy usage potential, defined as peak sun hour (PSH), of different state in the United States. Peak sun hour is a term related to the expected energy production of solar energy in one place. Since different states in the US are in different latitude with various topographic and climatic condition, the potential of solar energy usage is unevenly distributed. To be specific, since the majority states of the US are in the north hemisphere, south states and states with more sunny days would have higher PSHs.

The first step of this part was to import the data of state boundaries in the US. The geography information was retrieved through the Boundary Shapefile from United States Census Bureau in 2018. The Boundary Shapefile file was imported through “mpl_toolkits.basecamp” module in Python, which shows the boundary of states, as shown in Figure 3 below.

<p align="center">
  <img src="https://github.com/yuehaoshi/myFiles/blob/main/WebPics/Solar%20Visualization%20Project/SolarVis3.png" alt="Oops, this image disappeared.."/>
</p>
<h6 align="center">Figure 3: States boundary of US</h6>

The next step was to implement the information of PSH into different colors on the boundary map. This step was achieved by the “Polygon” method in “matplotlib” method in Python. The PSH data were acquired from Renogy (Renogy, 2013). To match the PSH value with corresponding state by state name, the values of PSHs were shown in the “YlOrRd” colormap, with higher PSH having darker red color. Meanwhile, the state of Hawaii and Alaska were also move to the left bottom corner of the map to make the map in a proper scale. By setting the original boundary to be transparent and adding the corresponding color legend bar, the generated map was shown as Figure 4 below.

<p align="center">
  <img src="https://github.com/yuehaoshi/myFiles/blob/main/WebPics/Solar%20Visualization%20Project/SolarVis4.png" alt="Oops, this image disappeared.."/>
</p>
<h6 align="center">Figure 4: PSH map for each state</h6>

To better illustrate the solar energy usage potential of the states, the map was divided into five different solar energy application level. This step was inspired by the application of drawing contours in UIUC CS519 class. The generated map in the last step was saved and each pixel of it was read and stored in a new list containing the RGB values. The RGB values were then converted into each unique value by “65536 * R + 256 * G + B”, which was later used as the parameter to draw a contour based on different color level with “contour” method in “matplotlib” module in Python. The contour was divided in five different level. The colormap used for this figure was “summer”, where the darker green region in the map indicates better potential and benefits for developing solar panel as a kind of “green energy” implementation.

<p align="center">
  <img src="https://github.com/yuehaoshi/myFiles/blob/main/WebPics/Solar%20Visualization%20Project/SolarVis5.png" alt="Oops, this image disappeared.."/>
</p>
<h6 align="center">Figure 5: Solar Energy Usage Potential Regions</h6>

## Part 3: Best Solar Panel Usage Angle

The last part of this project is to make a visualization for the solar intensity changing with different tilts and azimuths of the installation of the solar panel. As the rotation and revolution of earth, the sunlight intensity of one place is also changing, which is impacted not only by the latitude of the position, but also the sunlight irradiate angles, which are solar azimuth and solar elevation. Thus, the optimal position for a solar energy to maximize the sunlight intensity should be also changing with the sunlight irradiate angles. More specific, the equation used to decide the best solar panel working angles is:

S_module=S_incident * [cos⁡(α) * sin⁡(β) * cos⁡(Ψ-Θ) + sin⁡(α) * cos⁡(β)]

Where:

S_module: Light intensity on solar panel,

S_incident: Sunlight intensity,

α: Sun elevation angle,

Θ: Sun azimuth angle,

β: Solar panel tilt angle,

Ψ: Solar panel azimuth angle (PVEducation, n.a.)

Among those parameters, α, Θ can be calculated through the latitude and time of the solar panel installation position, and S_incident can be measured or inferred from historical data. To simplify this equation, once the position and time are known, the light intensity on solar panel can be represented as a function related to solar panel tilt and azimuth, which is: S_module=f(β,Ψ). Take the sunlight data of Chicago in 11/29/2021 as an example, at 12:00pm, the solar azimuth will be 185.43 and the solar elevation will be 26.39, calculated by the “Solar Position Calculator” provided by NOAA (Cornwall et al, 2021). Using this information, the relationship between solar panel light intensity and installation angles can be depicted.

The first step of this part was to calculate the solar panel light intensity using the equation mentioned above in tilts between 0 to 90 degrees as well as azimuths between 90 to 270 degrees. The intensity as well as the corresponding tilt and azimuth are then drawn using the “Layout” method in the “graph_objects” module. The colormap used in this plotting was “Portland”, where the warmer color in the contour corresponds the higher solar intensity, which is the ideal angle the solar panel should face to acquire the higher efficiency. The contour was shown in the Figure 6 below. The idea of showing the solar panel installation angles instruction was acquired by the code from Alan Mitchell (Mitchell, 2017)

<p align="center">
  <img src="https://github.com/yuehaoshi/myFiles/blob/main/WebPics/Solar%20Visualization%20Project/SolarVis6.png" alt="Oops, this image disappeared.."/>
</p>
<h6 align="center">Figure 6: Solar panel light intensity in different tilts and azimuths</h6>

To better illustrate the relationship between installation tilt and the expected energy produced, the contour was represented into 3d axis using “plotly.graph_objects” module. By converting to the 3d visualization, the impact of tilts and azimuths can be better shown for the user to get the best installation angles. The updated 3d plotting was shown in the Figure 7 below.

<p align="center">
  <img src="https://github.com/yuehaoshi/myFiles/blob/main/WebPics/Solar%20Visualization%20Project/SolarVis7.png" alt="Oops, this image disappeared.."/>
</p>
<h6 align="center">Figure 7: Solar panel light intensity in different tilts and azimuths in 3D</h6>

## References:
- Cornwall, C. et al (2021, November 28). [Solar Position Calculator](https://gml.noaa.gov/grad/solcalc/azel.html), Retrieved November 28, 2021.

- Kharwal, A. (2020, October 22). [Visualize a solar system with python](https://thecleverprogrammer.com/2020/10/07/visualize-a-solar-system-with-python/), Retrieved November 15, 2021.

- Renogy. (2013) Average Peak Sun Hours by State.

- Mitchell, A. (2017). [Data and Sample code for Creating a Solar Contour Plot](https://miscellaneous-analysis-north-project-documentation.readthedocs.io/en/latest/solar-contour-plot.html).

- PVEducation, [Arbitrary orientation and tilt. PVEducation](https://www.pveducation.org/pvcdrom/properties-of-sunlight/arbitrary-orientation-and-tilt). Retrieved November 29, 2021.
