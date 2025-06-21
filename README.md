# VG-sales-prediction

**Authors:** Sam Caesar, Mayra Leon Sandoval, Nicholai Martinsen
## 📌 Introduction:
In this project, we aim to predict the **global sales performance** of video games using various game attributes. Our goal is to develop a regression model that can estimate global sales (in millions of units) based on features like platform, genre, publisher, year of release, and other relevant charasteristiics. We will utilize a dataset containing historical sales data and game attributes to train our model.

## 📂 Dataset Description:
**Source:** Video Game Sales Dataset (vgsales.csv file from Kaggle)

- **Rows:** Over 16000 rows, each representing a unique video game title
- **Columns:** Includes features like:
  - `Name`: Title of the video game
  - `Platform`: The console or platform on which the game was released (e.g., Wii, PS3, Xbox360)
  - `Year`: Year the game was released
  - `Genre`: The category or type of the game (e.g., Action, Sports, Racing)
  - `Publisher`: Company of that published the game
  - `NA_Sales`: Sales in North America (millions of units)
  - `EU_Sales`: Sales in Europe (millions of units)
  - `JP_Sales`: Sales in Japan (millions of units)
  -`Other_Sales`: Sales in other regions (millions of units)
  -`Global_Sales`: Total sales worldwide (millions of units)

**What We Will Predict:**
We will predict the **Global Sales** of a video game (continuous variable in millions of units sold) using a regression model.

**Predictive Features:**
- `Platform` (categorical)
- `Year` (numerical)
- `Genre` (categorical)
- `Publisher` (categorical)
- `Critic_Score` and `User_Score` (numerical, if available)

**Munging & Feature Engineering:**
  1. **Missing values:** dropped any rows with missing `Global_Sales`.  
  2. **Type conversions:**
     - `Year` → integer,
     - `User_Score` “tbd” → NaN → imputed with median.  
  3. **Encoding:** one-hot encoded `Platform`, `Genre`, `Publisher` (top 10 publishers, rest grouped as “Other”).

## Method:
For our analysis, we utilized:
  - Python
  - Pandas for data manipulation
  - Scikit-learn for modeling
  - Matplotlib and Seaborn for visualization
  - Colab for Jupyter Notebook

For modeling, we compared:
  - Linear Regression: Simplicity and interpretability 
  - Random Forest: To capture non-linear relationships and interactions features
  - CatBoost: Same as a random forest and compare it against it for efficiency
  - Stacked Ensemble: Combines predictions from multiple models and yields the best performance

## Results:
The stacked ensemble model achieved a Root Mean Squared Error (RMSE) of 1.80 million units and an R-squareed value of 0.24 on the original scale,
indicating a significant improvement in predictive accuracy. On the log scale, the R-squared value reached 0.69, suggesting that the model 
effectively captures the relative variation in sales. 

These metrics are important in the context of our project. RMSE indicates the average error in our predictions, while the R-squared measures
the proportion of variance explained by the model. The higher the R-squared value signifies a better fit to the data.

## Discussion:
The implications of our findings are significant for the gaming industry. By understanding the factors that influence video game sales, developers 
and publishers can make more informed decisions regarding game developmen tand marketing strategies. our results align with existign research that 
highlights the importance of genre and platform in determining sales performance.

## ✅ Summary
- **Goal:** Predict global sales of video games using game metadata.
- **Dataset:** Cleaned and preprocessed with categorical encoding.
- **Exploration:** Visualized key trends and potential predictors.
- **Modeling:** Performed basic train-test split and linear regression for a baseline.


## Results

| Model                             | RMSE (orig) | MAE (orig) | R² (orig) | R² (log) | MAE (log) |
|:----------------------------------|------------:|-----------:|----------:|---------:|----------:|
| **Baseline (mean)**               | 2.07 M      | —          | —         | —        | —         |
| **Baseline (median)**             | 2.10 M      | —          | —         | —        | —         |
| **Linear Regression**             | 1.97 M      | 0.57 M     | 0.09      | —        | —         |
| **RandomForest**                  | 1.81 M      | 0.32 M     | 0.24      | 0.67     | 0.12      |
| **Poly + Ridge (2-way inter.)**   | 2.00 M      | 0.45 M     | 0.07      | 0.35     | 0.20      |
| **CatBoost (Decade+Shares+TE)**   | 1.81 M      | 0.33 M     | 0.23      | 0.67     | 0.13      |
| **Stacked Ensemble**              | 1.80 M      | 0.32 M     | 0.24      | 0.69     | 0.12      |

- **MAE (orig)**: mean absolute error in millions of units on the original‐sales scale.  
- **R² (log)** & **MAE (log)**: performance on the log-transformed target.  
- The **stacked ensemble** edges out the single models by learning a ridge meta‐model over the RF, Poly+Ridge, and CatBoost log-predictions, boosting log-R² to 0.69 and shaving RMSE to 1.80 M.  



https://github.com/user-attachments/assets/c6f6105a-ae20-43d1-b600-47197b9db724

