# BritishAirways

## Airline Reviews Analysis

### Overview

This repository contains code for analyzing airline reviews, specifically focusing on British Airways (BA). The dataset used for this analysis is sourced from Kaggle, providing a comprehensive set of reviews on various aspects of the airline.

### Data Source

The dataset, named `BA_AirlineReviews.csv`, was obtained from Kaggle and is included in this repository. It provides information on Overall Ratings, Verified Reviews, Type of Traveler, Seat Type, Route, and Date Flown.

### Tools and Dependencies

To run this code, make sure you have the following R packages installed:

```R
install.packages('tidyverse')
install.packages('extrafont')
install.packages('googlesheets4')
```

### Data Exploration and Analysis

The code reads the CSV file into a data frame (`BA_Reviews`) and extracts relevant columns (`OverallRating`, `VerifiedReview`, `TypeOfTraveller`, `SeatType`, `Route`, `DateFlown`). It then performs various analyses on the dataset.

#### 1. Missing Data

Identifies and views missing information in the dataset.

```R
missinginfo <- !complete.cases(Important_Reviews)
view(missinginfo)
```

#### 2. Grouping and Filtering

Groups the data by `OverallRating` and `VerifiedReview`, then filters verified and unverified reviews.

```R
BAReviewsGrouped <- Important_Reviews %>% group_by(OverallRating, VerifiedReview)
VerifiedReview <- subset(BAReviewsGrouped, VerifiedReview == 'TRUE')
UnverifiedReview <- subset(BAReviewsGrouped, VerifiedReview == 'FALSE')
```

#### 3. Average Ratings by Traveler Type (Unverified)

Calculates and visualizes the average ratings for unverified reviews by traveler type.

```R
ggplot(drop_na(UnverifiedReview), aes(x = TypeOfTraveller , y=OverallRating,fill=TypeOfTraveller)) + 
  stat_summary(fun.y = "mean", geom = 'bar') + 
  ggtitle('Unverified Reviews Average') + 
  ylab('Average Rating') + 
  xlab('Traveler Type') + 
  theme(legend.position = 'none', ...)
```

#### 4. Average Ratings by Traveler Type (Verified)

Calculates and visualizes the average ratings for verified reviews by traveler type.

```R
ggplot(drop_na(VerifiedReview), aes(x = TypeOfTraveller , y=OverallRating,fill=TypeOfTraveller)) + 
  stat_summary(fun.y = "mean", geom = 'bar') + 
  ggtitle('Verified Reviews Average') + 
  ylab('Average Rating') + 
  xlab('Traveler Type') + 
  theme(legend.position = 'none', ...)
```

### Exporting Data to Google Sheets

The code exports the unverified reviews to a Google Sheets document for further analysis or visualization.

```R
UnverifiedReview %>% 
  write_sheet(
    ss=gs4_get(
      "https://docs.google.com/spreadsheets/d/1rNMh9oGjEe8LNvXRPleF59NIa8V2T4WhonQWMKo8Ipw/edit?usp=sharing"
    ), 
    sheet = 'Original'
  )
```

## Tableau Dashboard

Explore the Tableau dashboard to visualize and interact with the British Airways reviews data:

[Tableau Dashboard](https://public.tableau.com/views/BritishAirwaysReviews/Dashboard1?:language=en-US&:display_count=n&:origin=viz_share_link)

## Kaggle Dataset

The dataset used for this analysis is sourced from Kaggle. You can access and download the dataset from the following Kaggle link:

[Kaggle Dataset](https://www.kaggle.com/datasets/praveensaik/british-airways-passenger-reviews-2016-2023)

### Conclusion

This analysis provides insights into the average ratings of British Airways reviews, categorized by traveler type. The code and visualizations aim to facilitate a better understanding of customer sentiment and preferences.


**Note:** Ensure you have the necessary permissions to access the Google Sheets document specified in the code.
