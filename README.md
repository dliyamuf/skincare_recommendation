# **MACHINE LEARNING PROJECT REPORT - DLIYA AWLIYA MUFIDAH**
# **Project Overview**
In growing fast of brand skincare in the world, many skincare's consumer often struggles to find similar product based in their preferences. The use of Artificial Intellegence (AI) for cosmetic brands to help consumers find their suitable products become future trends nowadays [(Lin et al., 2022)](https://doi.org/10.3390/electronics11010143). Conten-based filtering of recommender system is one of the most useful techniques to find similarity between products. This system leverages machine learning and natural language processing (NLP) to analyze skincare product descriptions, ratings, and user reviews to generate personalized recommendations [(Vinutha et al, 2024)](https://ieeexplore.ieee.org/document/10626458).


***

# **Business Understanding**
## **Problem Statements**
1. What are best skincare products based on rating given by consumers?
2. How to build content-based recommender system to help users find top 5 skincare product that similar with their preferences?
3. What are the best similarity metrics for comparing skincare products?

## **Goals**
1. Find best skincare product based on rating given by consumers on the website.
2. Get top 5 skincare recommendation products to users.
3. Investigate what best similarity metrics based on their performance metrics.

## **Solution Statements**
1. Use mutlivariate analysis EDA on rating and skincare product (type, name, and brand).
2. Develop content-based recommender system suggests products based on their attributes (type, brand, name, and rating) and recommend top best 5 product according to similarity.
3. Compare two different similarity metrics (cosine similarity and jaccard distance) and find the best based on their performance metrics (MAP, MRR, precision, and recall).

# **Data Understanding**
The [dataset](https://www.kaggle.com/datasets/prastyasusanto/indonesia-skincare-from-female-daily-reviews) containing skincare information obtained from femaledaily.com. The data was collected using web scraping with the BeautifulSoup library in Python that has been collected by Prastya Susanto, Rimba Erlangga, and Rama Wijaya and posted on Kaggle.

## **Variables**
- **Type** : type of skincare product.
- **Name** : name of skincare product.
- **Brand** : brand name of skincare product in Indonesia
- **Rating** : rating given by consumers. The range of value is from 1.0 to 5.0.
- **Total Reviewers** : number of consumer that reviewes the product in website.
- **Link** : link to the website.

(gambar data info)
There are 7432 rows and 6 column contain object(5) and float(1) data types.

## **Data Condition**
- There's no missing values.
- There are two duplicated data.
- There are some outliers with value below 2.5 on **Rating** feature.
  
(gambar outlier)

## **Exploratory Data Analysis**
### **Univariate Analysis**
(gambar univ1)
- There are 1204 brand name of skincare product. We make histogram plot of top 5 most counts brand name.
- The most counts skincare brand is Innisfree with 134 counts.

(gambar univ2)
There are 6 types of skincare product, **moisturizer cream** is the most counts skincare product type.

### **Multivariate Analysis**
(gambar multi1)

The most reviewed skincare type product is **Facial Wash** with more than 140.000 reviewers on the website.

(gambar multi2)

Top 10 the most reviewed skincare brand name is **Garnier, Wardah, Pond's, Hada Labo, Emina, Viva Cosmetics, Azarine Cosmetics, Cosrx, Cetaphil,** and **Skin Aqua**.

(gambar multi3)

Skincare type with average rating above mean average rating of skincare type product are **Moisturizer Cream, Toner, Facial Wash,** and **Moisturizer Gel**.

(gambar multi4)

Popular brand name with highest average rating is **Missha**.

# **Data Preparation**
## **Handling Duplicated Data**
Based on Data Understanding, there's 2 duplicated data. Drop two duplicated data.
## **Handling Outlier**
There's some outlier on **Rating** feature with value below 2.5. Keep it because it might contains low rating skincare brand or type informations.
## **Feature Engineering**
- **Total Reviewers** dtypes must be an integer.
- Combine relevant text columns into a single feature and initialize TF-IDF Vectorizer (remove stop words and use unigrams & bigrams). Matrix with shape (7430, 22556) created successfully.

# **Modeling**
There are two metrics to compute this recommendation system.
## **Cosine Similarity**
- Measures the angle between two vectors in a multi-dimensional space.
- Used for continuous or high-dimensional data, like TF-IDF in NLP or feature vectors in recommendation systems.

Pros:
- Works well with high-dimensional data (e.g., TF-IDF, embeddings).
- Not affected by vector length (good for text and numerical data).

Cons:
- Doesn't consider absolute differences (two vectors with similar directions but different magnitudes can still be close).
- Requires dense vector representation, which may need feature engineering.

(gambar hasil cosine)

## **Jaccard Distance**
- Measures the similarity between two sets by comparing their intersection and union.
- Used for categorical data, like tags, product attributes, or binary data.

Pros:
- Works well with binary and categorical data (e.g., tags, product attributes).
- Easy to interpret.

Cons:
- Ignores feature frequency (e.g., if one product has SPF 30 and another SPF 50, Jaccard treats them the same).
- Doesn't work well with high-dimensional or continuous data.

# **Evaluation**
There are 4 performance metrics to evaluate each models of top-K recommendation.

- Precision@K: How many recommended items are relevant?
  
$Precision@K = \frac{\text{Relevant  Items in top K}}{K}$

- Recall@K: How many relevant items were recommended?
  
$Recall@K = \frac{\text{Relevant Items in retrieved}}{\text{Total relevant items in dataset}}$

- MAP@K (Mean Average Precision): Measures ranking quality.

$\[
MAP@K = \frac{1}{|Q|} \sum_{q=1}^{|Q|} AP@K_q
\]$

where

$\[
AP@K = \frac{1}{m} \sum_{i=1}^{m} Precision@i \times (Relevant@i)
\]$

- MRR@K (Mean Reciprocal Rank): Measures ranking effectiveness of the first relevant item.

$\[
MRR@K = \frac{1}{|Q|} \sum_{q=1}^{|Q|} \frac{1}{\text{rank of first relevant item}}
\]$

(gambar comparison)

Observations:
- Both models has same value for **Precision@5** and **Recall@5**. It means that both models recommend 40% relevant products in the top 5 results and retrieve 67% of all relevant products.
- Based on **MAP@5** score, Jaccard ranks relevant items better than Cosine.
- Based on **MRR@5** score, Jaccard finds the first relevant item faster than Cosine.

# **Conclusion**
- Best skincare product type based on mean average rating are **Moisturizer Cream, Toner, Facial Wash,** and **Moisturizer Gel** and best popular model based on average rating is **Missha** with 63 number of ratings and 4.439 average rating.
- Build content-based filtering recommender system with cosine similarity and jaccard distance to find similarities between product names.
- Jaccard Similarity is the better model because it ranks relevant items higher and retrieves relevant products more effectively.

