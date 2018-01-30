---
layout: default
---

# Filtering Muscular Interference from EEG Brain Data on Consumer Grade Device using Neural Networks

A Computer Honours Project under supervision of Dr. Neil Bruce for the University of Manitoba.

---

## Project Overview

#### Problem Statement
To determine the extent to which a computer or devices can be controlled via neural
activation and EEG while controlling for activation associated with muscle control.

#### Background
There exist numerous types of devices for measuring brain activity, or imaging the brain. Some
measurements consider blood flow (e.g. fMRI), while others consider magnetic (MEG) or
electrical (EEG) fields elicited by neuronal signalling.

In the realm of relatively cost effective and lightweight devices, EEG is the most pervasive. Even
restricted to EEG, the instrumentation for these measurements shows considerable variability in
resolution and signal fidelity. Some consumer targeted EEG headsets (e.g. Emotiv) are relatively
inexpensive, but include poor contact with the scalp, and only few sensors. More complex
arrangements comprised on hundreds of sensors and contact through gel are used in clinical
settings, but are impractical for everyday use.

There is a large gap between these two categories of instrumentation for EEG measurements, and
currently nothing that elicits a trade-off between cost, resolution and ease of use above consumer
facing products that cost in the realm of a few hundred to a few thousand dollars. Moreover,
there is some indication that much of the control that can be derived from cheaper consumer
facing EEG setups is derived through muscular signalling such as blinking, or clenching of the
jaw.

Recent efforts have sought to democratize brain computer interfaces in allowing design and
creation of custom headsets using relatively inexpensive boards and 3D printing. It is an open
question whether a 3D printed headset that sits between low-end consumer facing products and
clinical setups can allow for neural control of machine or devices to be exercised while explicitly
factoring out signalling that may be attributed to muscular control.

#### Methodology
The methodology of the proposed research is as follows:

1. To make use of raw EEG data requires processing of multiple time varying signals
captured at a high temporal resolution. Given the recent success of neural networks in
addressing a variety of difficult problems, we endeavour to use deep (or recurrent) neural
networks to encode raw EEG data.
2. Initial stages of the project will be directed at becoming comfortable with some standard
neural network frameworks suitable for data processing (e.g. tensorflow or pytorch).
3. Efforts will shift from examining general time series to available temporal signals from
EEG and MEG that are publicly available.
4. Neural networks will be directed towards producing an embedding of temporal brain
imaging data (EEG / MEG), and efforts made to examine whether there is explicit
separation of muscular artifacts and other signal in these data.
5. Assuming success in the preceding stages (and time permitting), a headset will be used
from the open source OpenBCI project. Experimentation with real-time brain-computer
control, coupled with a camera facing the observer (me) will allow for a dataset that
includes both neural time-series and facial movements.
6. An embedding can be created using neural networks that is specifically designed to be
incapable of predicting changes to facial expression (or musculature) but capable of
allowing simple operations to be apply through cognition.
Overall this investigation will establish the extent to which a device and neural networks may
allow for cognitive control of computers and devices while explicitly factoring out signalling tied
to motor control. Success in this endeavour would mark a significant advance in brain computer
interaction.

