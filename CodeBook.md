 
Here's the reworded version of your text:
Week 4 Project — Data Acquisition and Cleaning in R
Author: Benedict Neo
Data Source:[UCI Machine Learning Repository](http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones). 
 
This codebook has been put together to provide a clearer understanding of the dataset's variables, the transformations applied to the data within the script, and other pertinent details.
Dataset Overview (sourced from the website)
A series of experiments were conducted involving 30 participants, all between the ages of 19 and 48. Each volunteer completed six distinct physical activities — WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, and LAYING — while wearing a Samsung Galaxy S II smartphone secured at the waist. The device's built-in accelerometer and gyroscope were used to record 3-axial linear acceleration and 3-axial angular velocity at a sampling rate of 50Hz. All sessions were video-recorded to enable manual activity labeling. The resulting dataset was then divided randomly, with 70% of participants contributing to the training set and the remaining 30% forming the test set.
Raw sensor data from both the accelerometer and gyroscope underwent noise filtering and were then segmented using fixed-width sliding windows of 2.56 seconds with 50% overlap (128 readings per window). The accelerometer signal — comprising both gravitational and body motion components — was decomposed using a Butterworth low-pass filter. Since gravity is assumed to operate predominantly at low frequencies, a cutoff of 0.3 Hz was applied. A feature vector was then derived from each window by computing variables across both time and frequency domains. Refer to 'features_info.txt' for further details.
Each record contains the following:
Total acceleration and estimated body acceleration along three axes (from the accelerometer)
Three-axis angular velocity measurements (from the gyroscope)
A 561-element feature vector spanning time and frequency domain variables
A label identifying the activity performed
A subject identifier corresponding to the individual who conducted the experiment

The pre-cleaned dataset consists of the following files:
README.txt
features_info.txt — Describes the variables comprising the feature vector
features.txt — A complete list of all features
activity_labels.txt — Maps class labels to their corresponding activity names
train/X_train.txt — Training dataset
train/y_train.txt — Training labels
test/X_test.txt — Test dataset
test/y_test.txt — Test labels

The files listed below are available for both training and test sets and follow equivalent structures:
train/subject_train.txt — Identifies the subject associated with each window sample; values range from 1 to 30
train/Inertial Signals/total_acc_x_train.txt — X-axis accelerometer signal in standard gravity units ('g'), with each row representing a 128-element vector; equivalent files exist for the Y and Z axes
train/Inertial Signals/body_acc_x_train.txt — Body acceleration signal derived by removing the gravitational component from the total acceleration
train/Inertial Signals/body_gyro_x_train.txt — Angular velocity from the gyroscope for each window sample, measured in radians/second

Project Tasks
Combine the training and test datasets into a single unified dataset.
Retain only the mean and standard deviation measurements for each recorded variable.
Replace activity codes with meaningful, human-readable activity names.
Assign clear and descriptive labels to all dataset variables.
Using the dataset from Step 4, produce a separate, independent tidy dataset containing the average value of each variable, grouped by activity and subject.

Summary of Approach
Data was downloaded and imported using standard methods covered in the course, specifically download.file and fread. Before merging the training and test sets, mean and standard deviation columns were isolated using grep on the loaded features and activity label files — targeting patterns matching "mean" and "std". A measurements variable was constructed to hold the cleaned variable names, with gsub used for string tidying. The filtered column indices were then used to load the respective train and test files, and variables were renamed using setnames(). Both datasets were subsequently combined via rbind.
Once merged, the key step involved generating a new summary dataset with per-activity, per-subject averages. This required converting the Activity and SubjectNo. columns to factors, after which the reshape library's melt and cast functions were applied to compute the means. The final tidy dataset was then exported to a new file.
                         
