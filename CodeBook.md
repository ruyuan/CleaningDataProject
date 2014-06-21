===============================================================================================
Obtaining tidy data from raw data name is Human Activity Recognition Using Smartphones Dataset
===============================================================================================
Ruifeng Liu
=============================================================

First, based on the requirement of course project, download zip file form web, unzip it.

Second, read test and train data into R, Human Activity Recognition using smartphones dataset has several
files that we can use it to build a new data so that we can get a tidy dataset. 
step 1, create a category variable with six levels (WALKING, WALKING_UPSTAIRS, 
WALKING_DOWNSTAIRS, SITTING, LAYING) in testy and trainy, 
Step 2, Set up column names for each rows in testx, testy, testsub, trainx, trainy, trainsub datasets.
step 3, merge test dataset one by one and merge train dataset one by one using cbind command, so we have new file name's test which is new 
data come from test files, and train dataset comes from train files.
step 4, test and train dataset have same colnames, put two of them together using rbind command, and get newdata name's datat.

based on the datat, we can easily calculate mean and standard deviation using sapply.

Transform datat to data.table name's dt, so that we can calculate datatable into a tidy data using lapply command

Store tidy data on local disk using write.table. 
