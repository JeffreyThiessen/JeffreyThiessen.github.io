---
layout: default
---

# Filtering Muscular Interference from EEG Brain Data on Consumer Grade Devices using Neural Networks

A Computer Honours Project under supervision of Dr. Neil Bruce for the University of Manitoba.

---

## Blog Updates

#### April 7th, 2018

##### Analysis Part 1

The first part of our analysis of will be to look at encoded data as a whole, and compare it to other sampled encoded data. After training the encoders as we saw last week, we ran t-SNE on the data.

In these t-SNE data plots, a single point on the graph is reduced from 45 or 18 dimensions (Encoder A or B) down to 2 dimensions. We ran t-SNE at multiple perplexities to try to get a better sense of the data.

See last weeks blog entry for more information on the encoders.

The following all have 1000 randomly chosen samples, each represented by a single data point.

Perplexity|Encoder A|Encoder B
---|---|---
5|![](A_1000_tsne_2_45_5.png)|![](B_1000_tsne_2_18_5.png)
10|![](A_1000_tsne_2_45_10.png)|![](B_1000_tsne_2_18_10.png)
20|![](A_1000_tsne_2_45_20.png)|![](B_1000_tsne_2_18_20.png)

If the encoders was able differentiate large differences in the different sleeps states, we would expect to see a few larger groups of data points in these images. We instead see small groupings, with most of the distribution of points and groups being similar to what we would expect of random data. Since our model reduced our data with very little loss, we know that it must be encoding it in some way, but sleep state may not have as big of an impact on the data as we thought.

I also ran t-SNE on a larger sample size (5000) reducing from 18 dimensions to 3, at a perplexity of 5. The following images are all of the same t-SNE plotting at slightly different angles so you can better see the data groupings in 3 dimensions.

![](B_5000_tsne_3_18_5_a.png)
![](B_5000_tsne_3_18_5_b.png)
![](B_5000_tsne_3_18_5_c.png)

##### Analysis Part 2
In the second part of our analysis we will be looking at how the encoded data in 45 and 18 dimensions relate to each other.

This is done by either randomly sampling data to encode, or taking data sequentially from a given starting point and encoding it. Once again, it will be encoded down to 45 or 18 dimensions for any given data. From encoded data, we would like to create a point for each of the 45 or 18 encoded points and plot it, doing the same for many sets of encoded data. Unfortunately when doing this it becomes computationally expensive very quickly, and there is no guarantee that that single encoded data points will be good representations of the data as a whole.

For example, Here we are using 100 random data points for each of the 45 dimensions, resulting in independent lines of points for each, not giving us any valuable grouping information.|| ![](A_rand_100x1_tsne_2_45_20.png)

So instead of taking single data points, we line up our encoded data such that each of the 18 or 45 points has 50 or 500 values. This means that each of the 18 or 45 points has either 50 or 500 values (depending on which trial) to represent it. We repeat this process 10 times so that we have 10 points to plot for each of our 18 or 45 points. This way we can see if the 18 or 45 point have similarities in data (are encoding similar things from the data).

We run the t-SNE at multiple reduction values to get a better understanding of the shape of the data, always reducing it down to 2 dimensions. A perplexity of 20 was used in all cases.

Each colour in the plot represent a different point from the 18 or 45 points that get plotted. It may also be good to note that similar colours does not always mean relation, only that the points are next to each other in the original encoding. 2 points may be next to each other but encoding completely unrelated things while points that are related an be spread far apart in the encoding.

Info|Encoder A|Encoder B
---|---|---
Data points length|50|50
Data selection|Random|Random
Starting Dims = 45|![](A_rand_10x50_tsne_2_45_20.png)|![](B_rand_10x50_tsne_2_45_20.png)
Starting Dims = 9|![](A_rand_10x50_tsne_2_9_20.png)|![](B_rand_10x50_tsne_2_9_20.png)
Starting Dims = 1|![](A_rand_10x50_tsne_2_1_20.png)|![](B_rand_10x50_tsne_2_1_20.png)
—|—|—
Data points length|500|500
Data selection|Random|Random
Starting Dims = 45|![](A_rand_10x500_tsne_2_45_20.png)|![](B_rand_10x500_tsne_2_45_20.png)
Starting Dims = 9|![](A_rand_10x500_tsne_2_9_20.png)|![](B_rand_10x500_tsne_2_9_20.png)
Starting Dims = 1|![](A_rand_10x500_tsne_2_1_20.png)|![](B_rand_10x500_tsne_2_1_20.png)
---|---|---

From these plots we can see that there are some obvious groupings and banding of the same colours through some of graphs, while others have a semi structured random distribution of points.

When starting dims is set to 1, we do not get very much meaningful information. The groupings that do show are the same as we see in higher dimensions which also give more clarity.

When using sequential data and specifying the starting point to be the start of the data we got some results with nice banding||![](A_spec_0_10x500_tsne_2_45_20.png)

But most results looked closer to random noise. It is possible that the starting area of data was not as clean as we would like and should have been removed before we trained our encoder.||![](A_spec_0_10x50_tsne_2_45_20.png)

We moved the starting point in for the following sequential data point plots

Info|Encoder A|Encoder B
---|---|---
Data points length|50|50
Data selection|Sequential|Sequential
Starting Dims = 45|![](A_spec_9000_10x50_tsne_2_45_20.png)|![](B_spec_9000_10x50_tsne_2_45_20.png)
Starting Dims = 9|![](A_spec_9000_10x50_tsne_2_9_20.png)|![](B_spec_9000_10x50_tsne_2_9_20.png)
—|—|—
Data points length|500|500
Data selection|Sequential|Sequential
Starting Dims = 45|![](A_spec_1000_10x500_tsne_2_45_20.png)|![](B_spec_1000_10x500_tsne_2_45_20.png)
Starting Dims = 9|![](A_spec_1000_10x500_tsne_2_9_20.png)|![](B_spec_1000_10x500_tsne_2_9_20.png)
---|---|---

As we might expect, data that is sequential, and thus in the same sleep state, has more similarity between the values in the hidden vectors. We can see much clearer banding and groupings in this data set than we did in the randomly selected ones.

The banding of points could likely be that the different values in the hidden vector are each doing different jobs within the encoding itself. Another interesting observation is that when we look at the plots we can often see pairs of different colours overlapping in multiple places on the plot. This suggests that these points are pairwise encoding together and may be working in tandem to encode some information in a "one on, one off" manner.

The t-SNE analysis gave us a lot of good information about how our neural net is encoding the EEG data, and would be very useful going forward if we had the time to follow up with data that we generate ourselves.

##### Final Thoughts

I feel as though we have begun to understand more about EEG data and now have a better understanding on how we can approach machine learning solutions to EEG problems. Unfortunately we did not get to do all the things we originally set out to do at the beginning of this project but looking back we see that we were extremely optimistic about what we could accomplish. Adding hardware and live data reading to the mix would have been fun to do but in the short amount of time we had, it would not have been possible. Learning and implementing the tools and networks on sample EEG data took quite a bit of time so once we begun analysis on the models we made, the semester was in it's final month. We can see that these techniques are successful and would likely warrant another honours project as a follow up, or even a masters thesis to take it further. 

---

#### April 1st, 2018
Jumping off of my last blog post, this week I focused on cleaning up the basic auto-encoder, training it on our EEG data, and running analysis tools on it.

I started by training the encoder in two slightly different ways, with the key difference being the size of the hidden vector.

Both were trained on the same dataset, selecting chunks of data at random. For each dataset we iterated randomly over the dataset 20 times.

desc|Method A|Method B
---|---|---
Length Per Channel|100|100
Hidden Nodes Per Channel|5|2
Channels|9|9
Input Size|900|900
Hidden Size|45|18
Output Size|900|900
Dataset ittr|20|20
Total train ittr|3545080|3545080
Time To Train|102m 20s|92m 17s
Loss over time|![](A losses.png)|![](B losses.png)
Final Average Loss|0.0151|0.0256

A point of interest here is that that with less than half the hidden channel nodes, we less than twice the loss. This might be able to be mitigated with a longer training time.

To analyze these encoders we will be examining what the hidden states look like when a single data entry is given to the encoder. During the training process we do the following:

`input (900)` --> `encode` --> `hidden (45 || 18)` --> `decode` --> `output (900)`

But we will be stopping after the encode step and keeping the hidden vector. We do this repeatedly to get a collection of encoded data that we can use to see if we can find patterns of how it is encoded. To do this we use t-SNE to change the data into a plot graph while retaining the relative positions of the data. This should give us an idea of how the different data points relate to each other.

[Click here for a great resource on t-SNE](https://lvdmaaten.github.io/tsne/)

For now here are a few example pictures of what the t-SNE plots I generated look like. Next week I will have more details on the parameters used, and an in-depth analysis on our results.

Method A|Method B
---|---
![](A_rand_10x50_tsne_2_45_20.png)|![](B_rand_10x50_tsne_2_45_20.png)
![](A_rand_10x500_tsne_2_9_20.png)|![](B_rand_10x500_tsne_2_9_20.png)
![](A_spec_1000_10x500_tsne_2_9_20.png)|![](B_spec_1000_10x500_tsne_2_9_20.png)

The above were generated with the same parameters for the Method A/B counterparts (although some are zoomed in so the dots are larger/smaller).

[Click here to view the encoders code and examples of code used to generate t-SNE graphs](https://github.com/JeffreyThiessen/eeg_basic_autoencoder)

---

#### March 20th, 2018
In the last 2 weeks I created a simple auto-encoder to run on the BCI sleep data. The encoder was built by adapting the [language translating encoder that is shown in the pytorch tutorials](http://pytorch.org/tutorials/intermediate/seq2seq_translation_tutorial.html), and have it run on EEG data instead.

My first attempt at using the auto-encoder was to encode a single channel of data by first reading in 100 data points, compressing it down (linear) to a hidden vector of 5 in length, and input into the recurrent net. This hidden vector is then fed into the decoder, which runs the vector through a recurrent net, then expanding (linear) back up to 100 points. We compare this output to our original input, calculate the loss, and propagate it back through the encoder/decoder.

By repeating this process the auto-encoder gets more efficient at compressing decompressing the data. We start with ~17725400 data points (512 points per second real time) which we break into 100 point chunks, and randomly select chunks 177254 x 2 times to run through the auto encoder. This process takes approximately 10 minutes on my Intel i5-3570K CPU.

When running the train function a single time, the loss we see ranges from 50-70%, at that point it is essentially random data as it has not encoded any structure yet. After running the auto encoder for the full 354508 times, we see a very tiny loss of between 0.5-1.5%.

This graph plots the the average loss over time as the encoder is trained.

![](first.png)

Next I used the Sequence to Sequence techniques to try to predict sections of data points given some sequence of data points. My first idea was to encode 1 second of data at a time over 30 seconds for a data sequence of 512 x 30 long, resulting in approximately 1154 inputs to train on, then train this data 5 times over. (reducing in size to 1/10th size)

This takes about 12 minutes to run.

Unfortunately this did not converge nicely as the previous one did

![](second.png)

Then I tried to scale down my encoding down to 1/4 second increments for a 4 second sequence to try to have better convergence during the training. 128 x 4, for ~34620 inputs, again running 5x over.

In addition to this change in size, I added in teacher forcing at a rate of 50% to try to improve the convergence rate.

This takes almost 20 minutes to run.

![](third.png)

At this point we are seeing about double the convergence that we saw in our second trial (50-70% loss to 25-40%), and based off our 50% teacher forcing ratio this shows that the encoder is not learning to predict well enough based off the training. This might be a good candidate for a longer training to see if it can encode better with more data inputs after more tweaks to the encoder.

Based off these results, it looks like a simple sequence to sequence model is not powerful enough to encode sequences of brain data. Using the simple recurrent model however did show promising results so we will be moving away from sequence to sequence and focusing on the simple model for the remainder of the project.

Note: I have omitted many of my failed attempts as they would have taken anywhere from days (or months) to run to completion. With better hardware and more time there might be some more interesting training options to try.

[Click here to view the code used to run these trials](https://github.com/JeffreyThiessen/eeg_timeseries_autoencoder)

---

#### March 3rd, 2018
After working on trying to use the EEG data I showed last week, I ran into a few issues. Mainly that the data itself did not have the events in their own channel in the data and instead were attached to a separate text file. I lost more time than I would have liked to this and other issues (such as my home machine only has 8GB of ram which caused loading problems that took some time to fix). Between that and Midterm exams, progress was slow but I feel that I have learned a lot in the last weeks.

After talking with Dr. Bruce we felt that going forward we will want to start with a simpler approach. Specifically I will be using/creating an autoencoder on the data to encode the REM/NREM states and examining what we can see in the data from there.

---

#### February 12, 2018
Just a small update this week. I have been taking a look at different public data sets that could possibly be used to try to isolate eye movement interference.

The data set that showed the most promise was [this EEG data on sleep activity.](https://physionet.org/pn6/capslpdb/) There are 16 sets of control data in this set that should provide a good base to try to analyse.

My plan going forward will be to run the data through a modified version of the Braindecode algorithms we saw last week and use the MNE tools to analyse the results.

I'll be using the epochs marked for REM and NREM sleep as the difference between eye movement and no eye movement. Them I'll see if we can see localization in the regions near the front of the head where eye movement would cause the most interference.

---

#### February 4, 2018
This last week I looked more closely at some of the available EEG related machine learning libraries and tools. One particular toolbox [Braindecode](https://robintibor.github.io/braindecode/) looked very promising so I decided to go through the tutorials and see what it all can do. 
 
Branedecode is a toolbox designed to decode raw time-domain EEG data. It works with PyTorch and [MNE](https://www.martinos.org/mne/stable/index.html) to create easy to use neural net tools. 
 
By shaping the data to the Braindecode format we can easily create a neural network to decode, crop-decode, and visualize data. One really nice tool I tried was their method for computing correlation. It can be used to plot the localized predictions the model is making on the data channels. 
 
Unfortunately my home computer is not powerful enough to handle the full trial data they recommend in their tutorial. I was only able to to use ~40% of the data while creating the model without running out of memory. Even so I was able to generate this figure showing the localized correlations between the data channels and right hand vs left hand movement. 
 
![](hands.png) 
 
To see the data and code provided by Braindecode [click here for the full tutorial](https://robintibor.github.io/braindecode/notebooks/visualization/Perturbation.html)

---

#### January 28, 2018
In the last week I have been familiarizing myself with the pytorch machine learning environment as it looks to be a solid framework to use for this project. I have found a few different projects others have done on BCI and EEG data that might prove to be a great foundation for this project, but I'll need to look more closely at them before making any decisions. 

I have also been updating my knowledge on modern CNN and RNN algorithms, as the amount of machine learning I knew before starting the project was not nearly enough to create and understand the workings of a recurrent neural network.

I found the following resources to be the most helpful in my learning so I figured I would link them here so you too can get a better understanding of neural networks.

[Mind: How to build a neural network](http://stevenmiller888.github.io/mind-how-to-build-a-neural-network/): A great introduction to neural networks.

[Video Lecture: Recurrent Neural Networks by Stanford University](https://www.youtube.com/watch?v=6niqTuYFZLQ): An indepth look at recurrent neural networks and how they can be used.

[PyTorch tutorials overview](http://pytorch.org/tutorials/index.html): The basics of using PyTorch.

[PyTorch tutorial on RNN classification](http://pytorch.org/tutorials/intermediate/char_rnn_classification_tutorial.html): A more advanced tutorial on RNN and how they can be built.
