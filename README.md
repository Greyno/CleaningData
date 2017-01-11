# CleaningData
This README discusses how data were gathered and cleaned.
The run_analysis.R program includes the 'plyr' library

The data are loaded from https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 
and are unzipped into a folder "~/data/UCI HAR Dataset". This folder contains a "test"" and a "train" folder. 
A program, run_analysis.R, was written to do the following:

A. Merge the training and the test sets to create one data set.

+ Load the X_/Y_test, X_/Y_train and subject_test/train data from the "test"" and "train" folders, respectively. 
+ Join the train and test data, join the train and test labels and join the train and test subjects, by row

B. Extract only the measurements on the mean and standard deviation for each measurement. 

+ Load the features.txt data and find the rows that correspond to the mean and standard deviation measurements. 
These rows were designated with "mean() or "std()" at the end of the variable name. 
+ Use 'grep' to find which row numbers in the file have 'mean()' or 'std()' at the end of the feature name.
+ Apply these to the data columns and remove the '()' from the names 
+ Change the column names of the Subject and Label data sets from V1 to "Label" and "Subject"
+ Merge the Subjects, Labels and Data
+ Convert column names to lower case


C. Use descriptive activity names to name the activities in the data set.

+ Load the activity data, change the names in column 2 to lower case and remove the '-' from the names
+ Cleaned activity name examples: WALKING -> walking; WALKING_UPSTAIRS -> walkingupstairs

D. Appropriately label the data set with descriptive variable names.

+ Clean up the column names in the merged data by removing '_' and converting names to lower case
+ This created a wide data set with column 1 being the Subject, column 2 being the Activity and columns 3-68 
representing the various measured mean and std
+ Cleaned column name examples: Subject -> subject; Activity -> activity; tBodyAcc-mean-Y -> tbodyaccmeany; tBodyAcc-std-X -> tbodyaccstdx

E. From the data set in step D, create a second, independent tidy data set with the average of each variable for 
each activity and each subject.

+ Use ddply to capture the average of the columns by subject and activity
+ The resulting tidy data is in a wide format - each measured variable is in one column and each observation of that 
variable is in one row i.e. each of the 6 activities is reported once for each subject; each measured observation is 
in its own column. There are 180 observations over 68 variables (including the subject and activity).
