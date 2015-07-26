Course Project CodeBook

1. Download and unzip the source data (https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip)
2. Original description is here. (http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones)

The R script run_analysis.R in the repo cleans up the data in the following ways:

- Merges the training and test sets to create one data set: 
    UCI HAR Dataset/train/X_train.txt with UCI HAR Dataset/test/X_test.txt.
    The result is a 10299x561 data frame. ("Number of Instances: 10299" and "Number of Attributes: 561").
    UCI HAR Dataset/train/subject_train.txt with UCI HAR Dataset/test/subject_test.txt.
    The result is a 10299x1 data frame with subject IDs.
    UCI HAR Dataset/train/y_train.txt with UCI HAR Dataset/test/y_test.txt.
    The result is a 10299x1 data frame with activity IDs.

- Reads UCI HAR Dataset/features.txt and extracts the measurements on the mean and standard deviation for each measurement. 
    The result is a 10299x66 data frame, as only 66 out of 561 attributes are measurements on the mean and standard deviation. 
    All measurements appear to be floating point numbers in the range (-1, 1).

- Reads UCI HAR Dataset/activity_labels.txt, and applies descriptive activity names to name the activities in the data set:

    walking
    walkingupstairs
    walkingdownstairs
    sitting
    standing
    laying

- The script labels the data set appropriately with descriptive names. 
All feature names and activity names are converted to lower case, underscores and brackets () are removed. 
It merges the 10299x66 data frame containing features with 10299x1 data frames containing activity labels and subject IDs. 
The result is saved as merged_cleaned_dataset.txt. 

It is a 10299x68 data frame. The first column contains subject IDs, the second column contains activity names. 
The last 66 columns are measurements. Subject IDs are integers between 1 and 30 inclusive. 

The names of the attributes are similar to:

    tbodyacc-mean-x 
    tbodyacc-mean-y 
    tbodyacc-mean-z 
    tbodyacc-std-x 
    tbodyacc-std-y 
    tbodyacc-std-z 
    tgravityacc-mean-x 
    tgravityacc-mean-y

- Finally, the script creates the 2nd, independent tidy data set with the average of each measurement for each activity and each subject. 
  The result is saved as final_dataset_with_avg.txt, a 180x68 data frame, with 30 subjects and 6 activities, 180 rows with averages.
