---
layout: default
---

# Filtering Muscular Interference from EEG Brain Data on Consumer Grade Devices using Neural Networks

A Computer Honours Project under supervision of Dr. Neil Bruce for the University of Manitoba.

---

### About This Project
The goal of this project is to determine the extent to which a computer or devices can be controlled via neural activation and EEG while controlling for activation associated with muscle control.

[Read more about the project here](/projects/bci/overview)

---

### Latest Project Blog Update

#### February 4, 2018
This last week I looked more closely at some of the available EEG related machine learning libraries and tools. One particular toolbox [Braindecode](https://robintibor.github.io/braindecode/) looked very promising so I decided to go through the tutorials and see what it all can do. 
 
Branedecode is a toolbox designed to decode raw time-domain EEG data. It works with PyTorch and [MNE](https://www.martinos.org/mne/stable/index.html) to create easy to use neural net tools. 
 
By shaping the data to the Braindecode format we can easily create a neural network to decode, crop-decode, and visualize data. One really nice tool I tried was their method for computing correlation. It can be used to plot the localized predictions the model is making on the data channels. 
 
Unfortunately my home computer is not powerful enough to handle the full trial data they recommend in their tutorial so I was only able to to use ~40% of the data while creating the model without running out of memory. Even so I was able to generate this figure showing the localized correlations between the data channels and right hand vs left hand movement. 
 
![](hands.png) 
 
To see the data and code provided by Braindecode [click here for the full tutorial](https://robintibor.github.io/braindecode/notebooks/visualization/Perturbation.html)

---

[Read the full blog here](/projects/bci/blog)
