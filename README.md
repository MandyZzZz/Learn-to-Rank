# Learn-to-Rank
1. Base datasets:

-anime_info_df.columns.tolist()

['anime_id',
'Genres',
'is_tv',
'year_aired',
'is_adult',
'above_five_star_users',
'above_five_star_ratings',
'above_five_star_ratio']

-user_info.columns.tolist()

['user_id',
'review_count',
'avg_score',
'score_stddev',
 'above_five_star_count',
'above_five_star_ratio']

-relevance_scores.columns.tolist()
['anime_id', 'anime_name', 'user_id', 'relevance_score']


2. Data preprocessing
   
   Fill in null values.
   
   Merging all features (both anime features and user features) into one df for model training purposes.
   
   get train dataframe:
   ['anime_id', 'Name', 'user_id', 'relavence_score',
   'USER_FEATURE REVIEW_COUNT', 'USER_FEATURE AVG_SCORE',
       'USER_FEATURE SCORE_STDDEV', 'USER_FEATURE ABOVE_FIVE_STAR_COUNT',
       'USER_FEATURE ABOVE_FIVE_STAR_RATIO', 'ANIME_FEATURE GENRES',
       'ANIME_FEATURE IS_TV', 'ANIME_FEATURE YEAR_AIRED',
       'ANIME_FEATURE IS_ADULT', 'ANIME_FEATURE ABOVE_FIVE_STAR_USERS',
       'ANIME_FEATURE ABOVE_FIVE_STAR_RATINGS',
       'ANIME_FEATURE ABOVE_FIVE_STAR_RATIO', 'ANIME_FEATURE COMEDY',
       'ANIME_FEATURE ACTION', 'ANIME_FEATURE FANTASY',
       'ANIME_FEATURE ADVENTURE', 'ANIME_FEATURE KIDS', 'ANIME_FEATURE DRAMA',
       'ANIME_FEATURE SCI-FI', 'ANIME_FEATURE MUSIC', 'ANIME_FEATURE SHOUNEN',
       'ANIME_FEATURE SLICE OF LIFE', 'ANIME_FEATURE SUPERNATURAL']

3. Training
      
      Training data voulme is 4678575, and test data volume is 200000. Features are input. relevance_score are target.
      
      model = lgb.LGBMRanker(objective="lambdarank")
model.fit(xtrain,ytrain,group=train_groups,eval_set=[(xtest,ytest)],eval_group=[test_groups],eval_metric=['ndcg'])

4. Prediction
   
   Choose user_id=1.
   
   use candidates that have not been liked by this user as model input.
   
   Plug in model to predict relevance (ranking) score of candidates.

5. Evaluation
   
   import shap to evaluate model performance.
   
   Plot summary of how each candidate contribute to the output.
