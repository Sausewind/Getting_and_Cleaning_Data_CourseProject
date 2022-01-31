---
title: "README"
author: "Susanne"
date: "31 1 2022"
output: pdf_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```


## Getting and Cleaning Data Course Project: the script

As part of the course project, an R script called run_analysis.R has to be submitted that does the following: 

1.Merges the training and the test sets to create one data set.

2.Extracts only the measurements on the mean and standard deviation for each measurement. 

3.Uses descriptive activity names to name the activities in the data set

4.Appropriately labels the data set with descriptive variable names. 

5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

As a first step, the complete dataset is imported into R. In order to do so the location of the individual files has to be provided.

```
```{r}
## Reads the test data
  
  setwd(test_dir)
  
  subject_test <- read.table(file ="subject_test.txt",header = FALSE) 
  
  x_test <- read.table(file = "X_test.txt", header = FALSE) 
  y_test <- read.table(file = "y_test.txt", header = FALSE) 
 
  setwd(test_IS_dir)
  
  body_acc_x_test <- read.table(file="body_acc_x_test.txt", header=FALSE)
  body_acc_y_test <- read.table(file="body_acc_y_test.txt", header=FALSE)
  body_acc_z_test <- read.table(file="body_acc_z_test.txt", header=FALSE)
  body_gyro_x_test <- read.table(file="body_gyro_x_test.txt", header=FALSE)
  body_gyro_y_test <- read.table(file="body_gyro_y_test.txt", header=FALSE)
  body_gyro_z_test <- read.table(file="body_gyro_z_test.txt", header=FALSE)
  total_acc_x_test <- read.table(file="total_acc_x_test.txt", header=FALSE)
  total_acc_y_test <- read.table(file="total_acc_y_test.txt", header=FALSE)
  total_acc_z_test <- read.table(file="total_acc_z_test.txt", header=FALSE)
  
  ## Reads the train data
  
  setwd(train_dir)
  
  subject_train <- read.table(file = "subject_train.txt", header = FALSE) 

  x_train <- read.table(file = "X_train.txt", header = FALSE) 
  y_train <- read.table(file = "y_train.txt", header = FALSE)   
  
  setwd(train_IS_dir)
  
  body_acc_x_train <- read.table(file="body_acc_x_train.txt", header=FALSE)
  body_acc_y_train <- read.table(file="body_acc_y_train.txt", header=FALSE)
  body_acc_z_train <- read.table(file="body_acc_z_train.txt", header=FALSE)
  body_gyro_x_train <- read.table(file="body_gyro_x_train.txt", header=FALSE)
  body_gyro_y_train <- read.table(file="body_gyro_y_train.txt", header=FALSE)
  body_gyro_z_train <- read.table(file="body_gyro_z_train.txt", header=FALSE)
  total_acc_x_train <- read.table(file="total_acc_x_train.txt", header=FALSE)
  total_acc_y_train <- read.table(file="total_acc_y_train.txt", header=FALSE)
  total_acc_z_train <- read.table(file="total_acc_z_train.txt", header=FALSE)
 
```

 
As a second step, the meaningful variables names are provided

```{r}
## Labels the data set with descriptive variable names
  
  colnames(subject_test) <- c("Subject")
  colnames(subject_train) <- c("Subject")
  colnames(y_test) <- c("Activity")
  colnames(y_train) <- c("Activity")
  
  setwd(UCI_dir)
  
  features <- read.table(file= "features.txt")
  colnames(x_test) <-features$V2
  colnames(x_train) <-features$V2
  
  obs <-1:128
  bax <-rep("body_acc_x_", 128)
  bay <-rep("body_acc_y_", 128)
  baz <-rep("body_acc_z_", 128)
  bgx <-rep("body_gyro_x_", 128)
  bgy <-rep("body_gyro_y_", 128)
  bgz <-rep("body_gyro_z_", 128)
  tax <-rep("total_acc_x_", 128)
  tay <-rep("total_acc_y_", 128)
  taz <-rep("total_acc_z_", 128)
  colnames(body_acc_x_test) <-paste0(bax, obs)
  colnames(body_acc_x_train) <-paste0(bax, obs)
  colnames(body_acc_y_test) <-paste0(bay, obs)
  colnames(body_acc_y_train) <-paste0(bay, obs)
  colnames(body_acc_z_test) <-paste0(baz, obs)
  colnames(body_acc_z_train) <-paste0(baz, obs)
  colnames(body_gyro_x_test) <-paste0(bgx, obs)
  colnames(body_gyro_x_train) <-paste0(bgx, obs)
  colnames(body_gyro_y_test) <-paste0(bgy, obs)
  colnames(body_gyro_y_train) <-paste0(bgy, obs)
  colnames(body_gyro_z_test) <-paste0(bgz, obs)
  colnames(body_gyro_z_train) <-paste0(bgz, obs)
  colnames(total_acc_x_test) <-paste0(tax, obs)
  colnames(total_acc_x_train) <-paste0(tax, obs)
  colnames(total_acc_y_test) <-paste0(tay, obs)
  colnames(total_acc_y_train) <-paste0(tay, obs)
  colnames(total_acc_z_test) <-paste0(taz, obs)
  colnames(total_acc_z_train) <-paste0(taz, obs)
```

As a third step, the train data is merged with the test data

```{r}
  ## Merges the training and the test sets to create one data set
  
  test<-cbind(subject_test, y_test, total_acc_x_test, total_acc_y_test, total_acc_z_test, body_acc_x_test, body_acc_y_test, body_acc_z_test,body_gyro_x_test, body_gyro_y_test, body_gyro_z_test, x_test)
  train<-cbind(subject_train, y_train, total_acc_x_train, total_acc_y_train, total_acc_z_train, body_acc_x_train, body_acc_y_train, body_acc_z_train, body_gyro_x_train, body_gyro_y_train, body_gyro_z_train, x_train)
  dset <-rbind(test,train)
```

As a next step, the mean and the standard ddeviation measurements are extracted from the combined dataset

```{r}
## Extracts the measurements on the mean and standard deviation for each measurement
  
  library(dplyr)
  d_extracts <-select(dset,c(Subject,Activity), contains("mean")| contains("std"))
```

Now, the activity ID (1 to 6) are replaced by the actual activity  and the variable is transformed to factor variable

```{r}
  ## Changes to descriptive activity names to name the activities in the data set
 
  d_extracts$Activity <- factor(d_extracts$Activity,levels = c(1,2,3,4,5,6),labels = c("WALKING", "WALKING_UPSTAIRS", "WALKING_DOWNSTAIRS", "SITTING", "STANDING", "LAYING"))
```

As a final step, the datset is summarised and the average of each variable for each activity and each subject is calculated

```{r}
  
  ## Creates a second, independent tidy data set with the average of each variable for each activity and each subject
  
  d_extracts <- mutate(d_extracts, Act_Sub =paste(Activity,Subject))
  
  library(reshape2)
  d_extracts <- melt(d_extracts, id.vars=c("Activity","Subject","Act_Sub"))
  d_mean <- dcast(d_extracts,  Act_Sub ~ variable, mean)
  
  library(tidyr)
  d_mean <-separate(d_mean, Act_Sub, c("Activity", "Subject"), sep= " ")
  
```

The final tidy dataset is then exported

```{r}
  ## Exports the finaldata set with the average of each variable for each activity and each subject to a table
  
  
  write.table(d_mean, file="HAR_Course_project.txt",sep=";", row.name=FALSE)
```

