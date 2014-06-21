CleaningDataProject
===================
##download file from web###3
myurl<-"http://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
download.file(myurl, destfile="Dataset.zip", method="auto")
###unzip file###
unzip("Dataset.zip")
##Read data into R###
testx<-read.table("./UCI HAR Dataset/test/X_test.txt", header=F)
testy<-read.table("./UCI HAR Dataset/test/y_test.txt", header=F)
testsub<-read.table("./UCI HAR Dataset/test/subject_test.txt", header=F)
trainx<-read.table("./UCI HAR Dataset/train/X_train.txt", header=F)
trainy<-read.table("./UCI HAR Dataset/train/y_train.txt", header=F)
trainsub<-read.table("./UCI HAR Dataset/train/subject_train.txt", header=F)
##Read labels into R##
activities <- read.table("./UCI HAR Dataset/activity_labels.txt",header=FALSE,colClasses="character")
###build a category variable in datase testy and trainy, so make a connection between activities and testy, trainy###
testy$V1 <- factor(testy$V1,levels=activities$V1,labels=activities$V2)
trainy$V1 <- factor(trainy$V1,levels=activities$V1,labels=activities$V2)

###set up colnames for file test and train###

feature<-read.table("./UCI HAR Dataset/features.txt",header=FALSE,colClasses="character")
colnames(testx)<- feature$V2
colnames(trainx)<- feature$V2
colnames(testy)<-c("Activity")
colnames(trainy)<-c("Activity")
colnames(testsub)<-c("Subject")
colnames(trainsub)<-c("Subject")
###merges the training and the test sets to create a new data set##
test<-cbind(testx, testy)
test<-cbind(test, testsub)
train<-cbind(trainx, trainy)
train<-cbind(train, trainsub)
datat<-rbind(test, train)

###Extract only the measurements on the mean and standard deviation for each measurement##
datatmean<-sapply(datat, mean, na.rm=T)
datatsd<-sapply(datat, sd, na.rm=T)

###creates a tidy dataset with average of each variable for each activity and subject##
dt<-data.table(datat)
tidy<-dt[,lapply(.SD, mean),by="Activity,Subject"]

