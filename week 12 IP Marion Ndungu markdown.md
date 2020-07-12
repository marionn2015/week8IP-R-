
# Defining the Question
Identify indivuduals who are most likely to will clickon an Ad.
#  Problem Statement
#A Kenyan entrepreneur has created an online cryptography course and would want to advertise it on her blog.
#She currently targets audiences originating from various countries.
#In the past, she ran ads to advertise a related course on the same blog and collected data in the process.
#She would now like to employ your services as a Data Science Consultant to create a solution that would allow her to determine whether ads targeted to audiences of certain characteristics i.e. city, male country, ad topic, etc. would click on her ads.
# Metrics for Success
#Identify users who are likely to click an ad.
#Experimental Design Taken
#Installing packages and loading libraries required
#Loading the data
Exploratory Data Analysis
Data Cleaning
Visualizations



## Importing the required packages

install.packages("iterators")  
install.packages("caret") 
install.packages('ranger')
install.packages('caTools')

##Importing Libraries we need for this Project analysis.

library(tidyverse)
library(data.table)
library(lattice)
library(caret)
library(rmarkdown)
library(tinytex)


# loading the dataset
#dataset_url = http://bit.ly/IPAdvertisingData
advert <- read.csv("http://bit.ly/IPAdvertisingData")


# printing out the dataset
print(advert)


# viewing the first five observations
head(advert)


# viewing the last five observation
tail(advert)

# checking for the number of rows and columns
dim(advert)


# this is to check for attributes
sapply(advert, class)

# this is to get a summary statistics of the dataset
install.packages("iterators")
summary(advert) 

# Data cleaning
## check for missing values in our data
colSums(is.na(advert))

# there are no missing values in all columns

# Duplicates
duplicated_rows <- advert[duplicated(advert),]
duplicated_rows

# Outliers
# we will use boxplot for the various columns

boxplot(advert$Age)
# no outliers

boxplot(advert$'Daily.Time.Spent.on.Site')
# no outliers

boxplot(advert$'Area.Income')
# the area income has outliers

boxplot(advert$'Daily.Internet.Usage')
# daily internet usage column have no outliers

# UNIVARIATE ANALYSIS

#stacked bars

counts <- table(advert$Clicked.on.Ad)
barplot(counts,
        main="A bar chart showing Clicked on Ad distribution",
        xlab="Clicked on Ad or Not",
        ylab = "Frequency",
        col=c("red","gold"),
        legend = rownames(counts))



counts <- table(advert$Age, advert$Clicked.on.Ad)
barplot(counts,
        main="A bar chart showing Age distribution by Clicked on Ad",
        xlab="Age",
        ylab = "Frequency",
        col=c("red","blue"),
        legend = rownames(counts))
#The highest age of the participants was 61 and lowest was 19.
#The people who clicked most on Ads were between age 28 to 36


counts <- table(advert$Daily.Internet.Usage,advert$Clicked.on.Ad)
barplot(counts,
        main="A bar chart showing Daily Internet Usage distribution by Click On AD",
        xlab="Daily.Internet.Usage",
        ylab = "Frequency",
        col=c("green","yellow"),
        legend = rownames(counts))

# Histogram
area_income<-(advert$Area.Income)
time_spent<-(advert$Daily.Time.Spent.on.Site)
internet_usage<-(advert$Daily.Internet.Usage)
hist(area_income)
hist(time_spent)
hist(internet_usage)


#Scatterplots
#1. Time Spent and Internet usage on ADs
time_spent<-(advert$Daily.Time.Spent.on.Site)
internet_usage <- (advert$Daily.Internet.Usage)
plot(time_spent,internet_usage, xlab="Time spent daily on ad", ylab="internet usage on ads")

#2. Age and Internet usage
age<-(advert$Age)
country<-(advert$Country)
plot(age,country,xlab = "Age of people",ylab = "countries they are from")

#3. Clicked on Ad and Age
clicked_on_ad<-(advert$Clicked.on.Ad)
age<-(advert$Age)
plot(clicked_on_ad,age,xlab ="Age",ylab = "Click on Ads")
#4.




# Correlation 
# cor between time_spent and internet usage
#1.time spent and internet usage
time_spent <- (advert$Daily.Time.Spent.on.Site)
internet_usage <- (advert$Daily.Internet.Usage)
cor(time_spent,internet_usage)
# the correlation between time_spent and internet usage is 0.518

#2.age and clicked on ad
age<- (advert$Age)
clicked_on_ad<-(advert$Clicked.on.Ad)
cor(age,clicked_on_ad)
#The cor of age and clicked_on_ad is 0.49

#3.Area income and Internet usage
area_income<-(advert$Area.Income)
internet_usage<-(advert$Daily.Internet.Usage)
cor(area_income,internet_usage)
#The correlation between the two is 0.33


#4. clicked on ad and area income
age<-(advert$Age)
area_income<-(advert$Area.Income)
cor(clicked_ad,age)
#the corr between clicked on ad and age is 0.49

# 
# covariance 
cov(clicked_ad,age)# 2.16
cov(area_income,internet_usage)# 198762.5
cov(time_spent,internet_usage)# 360.9919
cov(age,clicked_on_ad)# 2.164

library(rmarkdown)
library(tinytex)





