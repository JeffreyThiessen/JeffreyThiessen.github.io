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

#### February 12, 2018
Just a small update this week. I have been taking a look at different public data sets that could possibly be used to try to isolate eye movement interference.

The data set that showed the most promise was [this EEG data on sleep activity.](https://physionet.org/pn6/capslpdb/) There are 16 sets of control data in this set that should provide a good base to try to analyse.

My plan going forward will be to run the data through a modified version of the Braindecode algorithms we saw last week and use the MNE tools to analyse the results.

I'll be using the epochs marked for REM and NREM sleep as the difference between eye movement and no eye movement. Them I'll see if we can see localization in the regions near the front of the head where eye movement would cause the most interference.

---

[Read the full blog here](/projects/bci/blog)
