---
title: "CodeBook"
author: "Susanne"
date: "31 1 2022"
output: pdf_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```


## Getting and Cleaning Data Course Project

The goal of the course project is to prepare tidy data that can be used for later analysis.The following information will have to be submitted:

1) a **tidy data set** as described below

2) a link to a Github repository with your **script** for performing the analysis, and 

3) a **code book** that describes the variables, the data, and any transformations or work that you performed to clean up the data called CodeBook.md. You should also include a **README.md** in the repo with your scripts. This repo explains how all of the scripts work and how they are connected.

## Data

The data for the project represents data collected from the accelerometers from the Samsung Galaxy S smartphone that can be downloaded here:

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip  

A full description is available at the site where the data was obtained:

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones 

The data has been carried collected in an experiment with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain. 

## VARIABLES

The final dataset provided for the course project contains the following variables that were imported into R 

- Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration 
  (body_acc_x, body_acc_y, body_acc_z,total_acc_x,total_acc_y, total_acc_z) -> 128 observations per sample window for each variable

- Triaxial Angular velocity from the gyroscope 
  (body_gyro_x, body_gyro_y, body_gyro_z) -> 128 observations per sample window for each variable

- A 561-feature vector with time and frequency domain variables.-> the individual variables are detailed in the *features.txt* as part of the provided dataset

- Its activity label (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) 

- An identifier of the subject who carried out the experiment.(1-30)
