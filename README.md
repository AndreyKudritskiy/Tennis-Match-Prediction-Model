# Tennis-Match-Prediction-Model
A project from my Predictive Analytics class. The notebook file is written as a report so the notebook explains itself.
I found very quickly that as much as this is a project that was initially intended for applying a classification algorithm to predict future events, It became apparent very quickly that the model development and evaluation was only 5% of the work, most of the difficulty lied in preparing, transforming and engineering features into a format that would enable our model to perform at it's best. Here is a brief summary of the notebook

## Data & Setup

Cloned the Jeff Sackmann ATP tennis dataset (~195K matches from 1968–2024) and loaded it alongside a player info file
Optimized memory by downcasting dtypes and converting categorical columns, reducing DataFrame size from ~188MB to ~62MB

## Data Leakage Prevention & Feature Engineering

Recognized that raw match data (winner/loser stats, hands, ranks) directly reveals the outcome, so restructured data into a neutral "player1 vs player2" format with randomized assignment
Engineered an ELO rating system: all players start at 1500, and ratings update after each match chronologically — only the pre-match ELO is used as a feature to prevent leakage
Final feature set includes ELO, ATP rank, rank points, height, age, dominant hand, country, surface, and tournament level

## EDA example questions 

Discovered small advantage for Left-handed players win ~52% of matches against right-handed players
ATP players debut at ~21.5 years old on average and retire around 26.6
No significant birth-month skew (unlike hockey), and the USA produces the most ATP match appearances

## Modeling

Used XGBoost with RandomizedSearchCV (10 iterations, 3-fold CV) for hyperparameter tuning
Split: all matches before 2024 for training (~192K), 2024 matches for testing (~3K)

## Results

Test accuracy: 64.1%, Precision: 63.4%, Recall: 66.1%, F1: 64.7%
Top features by importance: player ELO (most important by far), ATP rank, dominant hand, and height

## Future improvements
* Cleaner code and coding principles to not be overwhlemed by technical debt
* More engineered features that track recent and long term performance like
  * average serve rates for past 10,15 or 20 games
  * most recent recorded match
  * win streaks
  * make more binary  
  * tennis court surface elo (clay court elo vs grass court elo)
  many of these features are discussed in the notebook, however I did not have time to implement them due to time constraints and incoming due dates
* Research elo calculations in other sports/games like chess or competitive matchmaking in online video games. apply findings to current elo approach
* review model for leakage: it's unexpected that right/left handedness was one of the most important features
* explore ensembling approaches to optimize trees by feature types (categorical, binary, 

