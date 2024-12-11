---
type: posts
title: "Satellite Image Analysis - NDVI Change Over Time"
header:
  image: /files/images/headers/satellite.jpg 
  caption: "Photo credit: [**unsplash@usgs**](https://unsplash.com/@usgs)"
date: 2024-12-10 22:10:00 -0800
last_modified_at: 2024-12-10 22:10:00 -0800
categories: [satellite]
tags: 
  - 2024 Q4
  - satellite image
published: true
---

I've always wanted to dive into satellite image analysis. It’s one of the first things that comes to mind when I think about the intersection of sustainability and computer vision. This week, I spent some time setting up Google Earth Engine and experimenting with its APIs. I wrote a script to visualize how the Normalized Difference Vegetation Index (NDVI) changes over time. 

This project was more about getting familiar with the tools rather than performing a detailed analysis. If you’re curious about how I implemented everything, check out my repo! And if you're interested in exploring satellite analysis during your free time, feel free to reach out.

### Quick Learnings and Disclaimers

Before jumping into the plots, here are a few things to keep in mind:

- **The data here is for practice, not analysis.**
  - My code hasn’t been tested, so there could be bugs or logical errors.
  - While I understand the NDVI formula, I don’t fully grasp what specific values (e.g., NDVI = 0.2) represent in real-world terms.
  - The regions of interest (ROI) I selected aren’t entirely accurate. For instance, some areas include large portions of the ocean, while others don’t, making direct comparisons unreliable. For example, if City A has an average NDVI of 0.2 and City B has 0.7, we can’t say City B is “greener.”
- **Sudden NDVI changes (2012–2013):** Some places show abrupt shifts in NDVI values during this period. This is likely due to a mistake in my `get_landsat_collection` function.

### California

![California NDVI](/files/images/satellite-ndvi/California/average_ndvi.png)
![California NDVI GIF](/files/images/satellite-ndvi/California/ndvi_over_time.gif)

### Los Angeles

![Los Angeles NDVI](/files/images/satellite-ndvi/Los Angeles/average_ndvi.png)
![Los Angeles NDVI GIF](/files/images/satellite-ndvi/Los Angeles/ndvi_over_time.gif)

### New York

![New York NDVI](/files/images/satellite-ndvi/New York/average_ndvi.png)
![New York NDVI GIF](/files/images/satellite-ndvi/New York/ndvi_over_time.gif)

### South Korea

![South Korea NDVI](/files/images/satellite-ndvi/South Korea/average_ndvi.png)
![South Korea NDVI GIF](/files/images/satellite-ndvi/South Korea/ndvi_over_time.gif)

### Seoul

![Seoul NDVI](/files/images/satellite-ndvi/Seoul/average_ndvi.png)
![Seoul NDVI GIF](/files/images/satellite-ndvi/Seoul/ndvi_over_time.gif)

### Bangalore

![Bangalore NDVI](/files/images/satellite-ndvi/Bangalore/average_ndvi.png)
![Bangalore NDVI GIF](/files/images/satellite-ndvi/Bangalore/ndvi_over_time.gif)
