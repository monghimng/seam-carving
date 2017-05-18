# Seam Carving
Seam Carving for Content Aware Image Resizing and Object Removal

## Introduction
The goal of this project is to perform content-aware image resizing for both reduction and expansion and image object removal with seam carving operator. This allows image to be resized without losing or distorting meaningful content from scaling. The code in this repository and technique described below is an implementation of the algorithm presented in [Avidan and Shamir](http://graphics.cs.cmu.edu/courses/15-463/2007_fall/hw/proj2/imret.pdf) and [Avidan, Rubinstein, and Shamir](http://www.merl.com/publications/docs/TR2008-064.pdf) algorithms.

## Algorithm Overview
### Seam Removal
1. Calculate energy map
*Energy is calculated by sum the absolute value of the gradient in both x direction and y direction for all three channel (B, G, R). Energy map is a 2D image with the same dimension as input image. 

2. Build accumulated cost matrix using forward energy
This step is implemented with dynamic programming. The value of each pixel is equal to its corresponding value in the energy map added to the minimum new neighbor energy introduced by removing one of its three top neighbors (top-left, top-center, and top-right)

3. Find and remove minimum seam from top to bottom edge
Backtracking from the bottom to the top edge of the accumulated cost matrix to find the minimum seam. All the pixels in each row after the pixel to be removed are shifted over one column to the left if it has index greater than the minimum seam.

4. Repeat step 1 - 3 until achieving targeting width 
The energy map needs to be calculated everytime a seam is removed.

5. Rotate image and repeat step 1 - 4 for vertical resizing
Rotating image 90 degree counter-clockwise and repeat the same steps to remove rows.







