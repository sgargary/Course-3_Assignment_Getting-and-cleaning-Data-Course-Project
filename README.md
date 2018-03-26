# Course-3_Assignment_Getting and cleaning Data Course Project.git
#imported data
X_test <- read.table("C:/Users/Sahar/Desktop/Data_Sahar/Courses/3_Getting and Cleaning Data/W4/HW/UCI HAR Dataset/test/X_test.txt", quote="\"", comment.char="")
X_train <- read.table("C:/Users/Sahar/Desktop/Data_Sahar/Courses/3_Getting and Cleaning Data/W4/HW/UCI HAR Dataset/train/X_train.txt", quote="\"", comment.char="")
subject_train <- read.table("C:/Users/Sahar/Desktop/Data_Sahar/Courses/3_Getting and Cleaning Data/W4/HW/UCI HAR Dataset/train/subject_train.txt", quote="\"", comment.char="")
subject_test <- read.table("C:/Users/Sahar/Desktop/Data_Sahar/Courses/3_Getting and Cleaning Data/W4/HW/UCI HAR Dataset/test/subject_test.txt", quote="\"", comment.char="")
y_test <- read.table("C:/Users/Sahar/Desktop/Data_Sahar/Courses/3_Getting and Cleaning Data/W4/HW/UCI HAR Dataset/test/y_test.txt", quote="\"", comment.char="")
y_train <- read.table("C:/Users/Sahar/Desktop/Data_Sahar/Courses/3_Getting and Cleaning Data/W4/HW/UCI HAR Dataset/train/y_train.txt", quote="\"", comment.char="")
activity_labels <- read.table("C:/Users/Sahar/Desktop/Data_Sahar/Courses/3_Getting and Cleaning Data/W4/HW/UCI HAR Dataset/activity_labels.txt", quote="\"", comment.char="")
features <- read.table("C:/Users/Sahar/Desktop/Data_Sahar/Courses/3_Getting and Cleaning Data/W4/HW/UCI HAR Dataset/features.txt", quote="\"", comment.char="")


#merging X_test & X_train: part 1 of the assignment
X_all <- rbind(X_test, X_train)

#merging y_test & y_train: part 1 of the assignment
y_all <- rbind(y_test, y_train)

#merging subject_test & subject_train: part 1 of the assignment
subject_all <- rbind(subject_test, subject_train)
               

#sel_1 : this is part 2 of the assignment 
sel_1 <- grep("mean|std", features$V2)
X_sel <- X_all[sel_1]

#descriptive activity name: Part 3&4 of the assignment
library(dplyr)
y_all <- mutate(y_all, activity_labels = activity_labels[V1,2])
X_sel <- cbind(activity_labels=y_all$activity_labels, X_sel)

# average of each variable: Part 5 of the assignment
X_sel <- cbind(subject=subject_all$V1, X_sel)
X_tidy5 <- X_sel %>%
  group_by(subject, activity_labels) %>%
  summarise_all(mean)
