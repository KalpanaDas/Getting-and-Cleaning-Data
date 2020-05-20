This is a code book that describes the variables, the data, and any transformations or work that I performed to clean up the data.

The dataset information -
The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six
activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the
waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a
constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly
partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding
windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion
components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to
have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was
obtained by calculating variables from the time and frequency domain. See 'features_info.txt' for more details. 

The data set includes the following files - 
- 'README.txt'
- 'features_info.txt': Shows information about the variables used on the feature vector.
- 'features.txt': List of all features.
- 'activity_labels.txt': Links the class labels with their activity name.
- 'train/X_train.txt': Training set.
- 'train/y_train.txt': Training labels.
- 'test/X_test.txt': Test set.
- 'test/y_test.txt': Test labels.

The following files are available for the train and test data. Their descriptions are equivalent. 
- 'train/subject_train.txt': Each row identifies the subject who performed the activity for each window sample. Its range is from 1 to
30. 
- 'train/Inertial Signals/total_acc_x_train.txt': The acceleration signal from the smartphone accelerometer X axis in standard gravity
units 'g'. Every row shows a 128 element vector. The same description applies for the 'total_acc_x_train.txt' and
'total_acc_z_train.txt' files for the Y and Z axis. 
- 'train/Inertial Signals/body_acc_x_train.txt': The body acceleration signal obtained by subtracting the gravity from the total
acceleration. 
- 'train/Inertial Signals/body_gyro_x_train.txt': The angular velocity vector measured by the gyroscope for each window sample. The
units are radians/second. 

The data used for this project can be found at the below link.
https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 

The original description of the dataset can be found at the below link. 
http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones 

The run_analysis.R script does the data preparation and then the 5 steps as told in the course project’s definition.
1. Download the dataset - 
   1. Dataset downloaded and extracted under the folder called UCI HAR Dataset

2. Assign each data to variables - 
   1. features <- features.txt :  The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals         tAcc-XYZ and tGyro-XYZ. 561 rows, 2 columns
   2. activities <- activity_labels.txt : List of activities performed when the corresponding measurements were taken and its codes           (labels) 6 rows, 2 columns
   3. subject_test <- test/subject_test.txt : contains test data of 9/30 volunteer test subjects being observed 2947 rows, 1 column
   4. x_test <- test/X_test.txt : contains recorded features test data 2947 rows, 561 columns
   5. y_test <- test/y_test.txt : contains test data of activities’code labels 2947 rows, 1 columns
   6. subject_train <- test/subject_train.txt : contains train data of 21/30 volunteer subjects being observed 7352 rows, 1 column
   7. x_train <- test/X_train.txt : contains recorded features train data 7352 rows, 561 columns
   8. y_train <- test/y_train.txt : contains train data of activities’code labels 7352 rows, 1 columns

3. Merges the training and the test sets to create one data set
   1. X (10299 rows, 561 columns) is created by merging x_train and x_test using rbind() function
   2. Y (10299 rows, 1 column) is created by merging y_train and y_test using rbind() function
   3. Subject (10299 rows, 1 column) is created by merging subject_train and subject_test using rbind() function
   4. Merged_Data (10299 rows, 563 column) is created by merging Subject, Y and X using cbind() function

4. Extracts only the measurements on the mean and standard deviation for each measurement
   1. TidyData (10299 rows, 88 columns) is created by subsetting Merged_Data, selecting only columns: subject, code and the measurements       on the mean and standard deviation (std) for each measurement

5. Uses descriptive activity names to name the activities in the data set
   1. Entire numbers in code column of the TidyData replaced with corresponding activity taken from second column of the activities           variable

6. Appropriately labels the data set with descriptive variable names
   1. code column in TidyData renamed into activities
   2. All Acc in column’s name replaced by Accelerometer
   3. All Gyro in column’s name replaced by Gyroscope
   4. All BodyBody in column’s name replaced by Body
   5. All Mag in column’s name replaced by Magnitude
   6. All start with character f in column’s name replaced by Frequency
   7. All start with character t in column’s name replaced by Time

7. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each    subject
   1. FinalData (180 rows, 88 columns) is created by sumarizing TidyData taking the means of each variable for each activity and each         subject, after groupped by subject and activity.
   2. Export FinalData into FinalData.txt file.
