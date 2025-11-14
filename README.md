# Amazon Fine Food Product Review - Sentiment Analysis

This repository contains all of the files and documentation for the Sentiment Analyses of Amazon Fine Food Products, as part of the Code Institute Data Analytics with AI Bootcamp Hackathon project 2.

## Dataset Content

This data is freely available on [Kaggle](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews/data). The dataset contains ~500,000 reviews of fine food products on Amazon over a 10 year period. The data includes product and user ID's, timestamps, ratings (1-5) and a plain text review. This raw dataset can be found [here](https://github.com/AmuKanda99/ci-hackathon-sentiment-analysis-of-product-reviews/blob/main/data/Reviews.csv).

## Business Requirements

The E-commerce platform Amazon wants to improve customer experience and product recommendations based on review sentiment. They need to identify common themes across products that drive positive or negative sentiments, as well as track product performance. In addition, they want to better understand the users leaving the reviews, and whether frequent reviewers are more or less 'picky'. Finally, they need a tool to predict sentiments based on review text in real-time, to help improve product recommendations.

## Hypotheses and validation

**H1: Sentiment Analysis.** Sentiments vary by product and over time, and are associated with common words/phrases. To understand these patterns, we will track sentiment changes by product/time and identify key themes/attributes correlated with ratings.

**H2: User Analysis.** Users that leave reviews more often tend to leave better reviews, on average i.e. there is a positive relationship between number of reviews and average rating per user.

**H3: Predictive Modelling.** Ratings and sentiments (positive/negative) can be accurately predicted from the review text. We will build a sentiment prediction model to deploy a tool for real-time prediction of product ratings based on reviews.

## Project Plan

1. **ETL:** The dataset will be extracted from Kaggle and uploaded to the github repository using [git-lfs](https://git-lfs.com/) due to the size of the dataset. The data will then be transformed in the followings ways; reduction of the size of the dataset for easier handling using stratification on the ratings variable, removal of duplicate reviews, cleaning and formatting of variables (timestamps), addition of new variables (sentiment). This cleaned dataset will then be saved as a .csv file and shared on the repository [here](https://github.com/AmuKanda99/ci-hackathon-sentiment-analysis-of-product-reviews/blob/main/data/Reviews_Sample_Cleaned.csv). The notebook containing the code for this step can be found [here](https://github.com/AmuKanda99/ci-hackathon-sentiment-analysis-of-product-reviews/blob/main/jupyter_notebooks/01_ETL.ipynb).
2. **EDA:** The cleaned data will then be used to perform exploratory data analysis, in order to understand the distributions of key variables as well as broad patterns and correlations between variables. This will be used to inform downstream analyses. The notebook for this step can be found [here](https://github.com/AmuKanda99/ci-hackathon-sentiment-analysis-of-product-reviews/blob/main/jupyter_notebooks/02_EDA.ipynb).
4. **Predictive model:** Machine learning methods will be used to build a model predicting review sentiment based on the review text. This model will then be tested with novel reviews to show its utility as a tool for real-time predictions of review ratings (H3). The notebook containing the code for this step can be found [here](https://github.com/AmuKanda99/ci-hackathon-sentiment-analysis-of-product-reviews/blob/main/jupyter_notebooks/03_ML.ipynb).
5. **Dashboard:** Advanced, interactive visualisations will be created using a dashboard to aid data storytelling and meet business requirements (H1 and H2). The dashboard file can be found [here](https://github.com/AmuKanda99/ci-hackathon-sentiment-analysis-of-product-reviews/blob/main/dashboard/amazon_product_review_sentiment_analysis_dashboard.pbix), and is published on the PowerBI platform [here](https://app.powerbi.com/groups/me/reports/b54498ef-9596-486d-9bb4-5dd0fd185e55/4514eb57e092d691e490?experience=power-bi).

## The rationale to map the business requirements to the Data Visualisations

1. Identifying common themes driving postiive and negative reviews: Wordclouds produced in the Dashboard and EDA notebook show common words associated with postive and negative reviews.
2. Track product performance: Tables showing best and worst performing products (based on number of reviews and average rating). Line graph tracking average ratings over time.
3. Understand users leaving reviews: Scatterplot of number of reviews left and average ratings given per user.
4. Real-time sentiment prediction: Confusion matrix shows performance of the prediction model.

## Analysis techniques used

#### **Exploratory Data Analysis (EDA)**

- **Method**: Analysed data patterns using statistical summaries and visualisations
- **Impelementation**:
  - Examined score and sentiment distributions
  - Identified class imbalance
  - Analysed review trends over time
- **Limitations**: Heavy imbalance toward positive reviews; sample size of 20,000 may not represent full dataset
- **Alternatives**: Could balance classes through sampling or use full dataset

#### **Text Preprocessing**

- **Method**: Cleaned and prepared text data for machine learning
- **Implementation**:
  - Removed HTML tags, special characters, and stop words
  - Converted text to lowercase
  - Used TF-IDF to convert text into 5,000 numerical features
- **Limitations**: TF-IDF doesn't understand context or word order

#### **Sentiment Classification**

- **Method**: Trained machine learning model to predict sentiment
- **Implementation**:
  - Used Logistic Regression classifier
  - Split data 80/20 for training and testing
  - Achieved 84.30% accuracy
- **Limitations**: Struggles with neutral sentiment due to limited examples; linear model may miss complex patterns

#### **Data Cleaning & Privacy**

- **Method**: Removed duplicates and protected user privacy
- **Implementation**:
  - Removed ProfileName column
  - Deleted duplicate reviews
  - Cleaned HTML from review text
- **Limitations**: May have removed some legitimate similar reviews; cannot verify complete anonymisation
- **Alternatives**: Could use less aggressive duplicate threshold or add additional anonymisation layers

### Structure Justification

Used sequential pipeline: **ETL → EDA → ML → Evaluation**

- Clean data first
- Understand patterns before modeling
- Build model on quality data
- Evaluate honestly and identify improvements

### Generative AI Usage

- **Ideation**
- **Design**
- **Code Optimisation**
- **Documentation**
- **Problem Solving**:

## Conclusions

**H1:** Review sentiments are associated with common words. For instance, the words 'delicious', 'great' and 'love' were used frequently in positive reviews (ratings 3 or more). In contrast, the words 'disappointed' and 'waste' were used frequently in negative reviews (ratings of 2 or less). Some words were common to both positive and negative reviews, such as 'taste', 'flavour' and 'price', highlighting these factors as key indicators of product performance.

**H2:** Most users leave reviews infrequently (5 reviews or less per user), and for these infrequent reviews there is a large range of average ratings. Users that leave reviews more often (more than 5 reviews) are less common, but those that do leave reviews regularly tend to leave higher ratings (averages between 3-5). This suggests that frequent reviewers are less 'picky' on average than those who rarely leave reviews.

**H3:** Review sentiments can be accurately predicted from review text using machine learning methods. The model performed with an accuracy of 84.3% and could correctly predict the sentiment of novel reviews. Neutral reviews were harder for the model to predict, with lower precision, recall and f1-score compared to positive and negative review categories. This highlights the use of stronger language in positive and negative vs. neutral reviews.

## Ethical considerations

User's profile names (the ProfileName column) were removed during the ETL process to comply with GDPR, as this contained personally identifiable information.

## Dashboard Design

**Main Dashboard:**

- Wordclouds for positive and negative review sentiment categories highlight common words used in the review text.
- Tables list the best and worst performing products, along with the number of reviews and and average rating. These are pre-filtered to give a quick and easy view of the best and worst products.
- Line graph shows temporal reviews trends, with average ratings over time. In addition, a forecast is given, projecting future ratings.
- A scatterplot provides a user analysis of average ratings per user based on the number of reviews left.
- A slider for date and a search bar for product ID allows drill-down into patterns for specific product and/or time periods.

**Product performance:**

- This page drill-downs further into the best and worst performing products, showing a less strigent filtering than that shown on the main page.

## Unfixed Bugs

The product ID column contains uninformative alpha-numeric codes. In order to gain further insight into this dataset, we should look to decipher these codes in order to group products by type (e.g. food, drink).

## Development Roadmap

The size of the dataset proved challenging to handle. We overcame this by using git-lfs to upload the raw dataset into the repository, and subsequently subsetting the data a fraction of the size in order to complete downstream analyses.

## Main Data Analysis Libraries

- **Pandas** - Data loading and manipulation
- **NumPy** - Numerical calculations
- **Scikit-learn** - Machine learning models and text vectorisation
- **Matplotlib, Seaborn and Plotly** - Data visualisation and charts
- **re** - Text preprocessing with regular expressions

## Credits

Amu: Project Manager and Data Analyst. Set up project repo and kanban. Performed ETL and built predictive model.

Kirsty: Data Analyst. Created dashboard report and wrote documentation (with input from others).

Diana: Data Analyst. Performed EDA and provided feedback on other elements.

### Resources

Using git-lfs: https://github.com/git-lfs/git-lfs/wiki/Tutorial#git-lfs-tutorial

## Acknowledgements (optional)

Thank you to the instructors and fellow coursemates at Code Institute for their support during this process.
