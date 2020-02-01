Predicting NFL game winners with ELO rating
================
Frank Lu, Simardeep Kaur, Tani Barasch </br>
2020/01/25 (updated: 2020-01-31)

# Summary

In this project we attempt to predict NFL game winners using
classification algorithems, Random Forest and Logistic Regression, in
order to test the hypothesis that ELO ratings can be used to predict the
outcome as presented by the website FiveThirtyEight.com in their ‘NFL
Prediction Game’.

We find that both models achieve similar results, with 0.771% accuracy
for the logistic regression and 0.756% accuracy for the random forest
classifier. Which overall is a pretty unreliable prediction model,
casting doubt over the method presented by FiveThirtyEight.

# Introduction

The sport of american football has succesfully built a reputation of an
unpredictable sport where every game is important and anyone can win,
coining the saying “any given Sunday” to mean that anything can happen
on a football field, which are usually played on Sundays in the National
Football League (NFL). Having several movies being made to this theme
such as “Any Given Sunday” (1999), “Remember the Titans” (2000), or more
recently the Netflix documentry “Last Chance U” (2016).

At the begining of the 2019 NFL season the website FiveThirtyEight
(FiveThirtyEight 2019) launched a [Prediction
Game](https://fivethirtyeight.com/features/how-to-play-our-nfl-predictions-game/),
in which the website challenges the readers to “beat the experts” who
are using the ELO ranking system and prediction formulas to assign a win
probability to each team for each game.

In order to test whether or not the hypothesis that NFL games can be
predicted using this ELO system, as presented by FiveThirtyEight we
train two machine learning classification algorithems, Random Forest and
Logistic Regression to predict game winners using only pregame elo
ratings for the teams and the starting quarterbacks.

# Methods

## Data

The data set used to train and test our algorithems is the same data
used by FiveThirtyEight(FiveThirtyEight 2019) in their game, which can
be found
[here](https://github.com/fivethirtyeight/data/tree/master/nfl-elo).
Specifically the file found
[here](https://projects.fivethirtyeight.com/nfl-api/nfl_elo.csv)
containing historic nfl ratings and outcomes starting in 1920 was used
to train the algorithems, and testing the predictions were done on the
following file containing all
[2019-2020](https://projects.fivethirtyeight.com/nfl-api/nfl_elo_latest.csv)
NFL games and outcomes (excluding the superbowl which has yet to be
played.)

Each row in each file contains the ELO ratings pre and post game for the
two NFL teams and starting Quarterbacks participating in that specific
game, along with the date, season, and final score of the game. Where
the home team is logged as team1 and the away team as team2.

## Analysis

We have used two classification models to see how the elo ratings will
affect the the predicted scores. Using Python (Van Rossum and Drake
2009) programming language, and the Scikit-Learn package (Pedregosa et
al. 2011) we trained a Logistic Regression and Random Forest
classification algorithems. Since it would be redundent to predict both
winner and loser for a single game, all predictions were made in
relation to the home team, with 3 possible outcomes: Win, Tie, Lose.

For the data used to train the model, all seasons prior to the 1970 NFL
merger were filtered out, which is the year the NFL started its shift
towards the current league structure.

\#\#\#Variables used: From the original file, any variable relating to
the outcome of the game was removed, such as post game elo score, each
teams actual score etc’. In addition information which uniquely
identifies a team outside of the ELO framework, such as team name and QB
name, were removed since it could bias the results by relating
information such as team performence for any given season. So, removing
this identifiers for different teams was an important step to get
unbiased results.

\#\#\#Hyperparameters: For the Random Forest modle, the hyperparameter
“max\_depth” is chosen using k-fold cross validation using k=5. The
best hyperparameter was then used to train the model.

The code used to run the training and testing of the algorithems can be
found at the projects github repo
[here](https://github.com/UBC-MDS/Workflows_Group_306):

# Results & Discussion

Examining the results of our model, we find that both models, the
Logistic Regression and Random Forest performed very similarly at 0.771%
and 0.756% accurace respectively. Indicating that although the results
are better then randomly guessing, or flipping a coin, such results are
hardly reliable.

In the confusion matrix below we can see the “hits and misses” of the
logistic regression model on the 2019-2020 season games, missing
relatively more often when the home team loses with a 36.5% error rate
and a 23.2% error rate for home team
wins.

<div class="figure">

<img src="../img/disp_lr.jpg" alt="Figure 1. Logistic Regression Confusion Matrix." width="90%" />

<p class="caption">

Figure 1. Logistic Regression Confusion Matrix.

</p>

</div>

And when looking at the random forest confusion matrix, we see an even
higher error rate for home team loses at 51.2%, but a lower error rate
for home team wins at
22%.

<div class="figure">

<img src="../img/disp_rf.jpg" alt="Figure 1. Logistic Regression Confusion Matrix." width="90%" />

<p class="caption">

Figure 1. Logistic Regression Confusion Matrix.

</p>

</div>

Unsuprisingly both models failed to predict the tie with only one such
occurrence in all of the 2019-2020 season.

With both models prediction accuracy below 80%, its would be hard to
proclaim the ELO rating system as a reliable method to predict NFL game
winners.

That being said it is possible that a regression method to predict the
scores would do better, or alternatively including ELO ratings in a more
complex and robust model could prove usefull.

# References

<div id="refs" class="references">

<div id="ref-docopt">

de Jonge, Edwin. 2018. *Docopt: Command-Line Interface Specification
Language*. <https://CRAN.R-project.org/package=docopt>.

</div>

<div id="ref-fivethirtyeight">

FiveThirtyEight. 2019. “Fivethirtyeight Data Repository.”
fivethirtyeight. <https://data.fivethirtyeight.com/>.

</div>

<div id="ref-docoptpython">

Keleshev, Vladimir. 2014. *Docopt: Command-Line Interface Description
Language*. <https://github.com/docopt/docopt>.

</div>

<div id="ref-mckinney-proc-scipy-2010">

McKinney, Wes. 2010. “Data Structures for Statistical Computing in
Python.” In *Proceedings of the 9th Python in Science Conference*,
edited by Stéfan van der Walt and Jarrod Millman, 51–56.

</div>

<div id="ref-scikit-learn">

Pedregosa, F., G. Varoquaux, A. Gramfort, V. Michel, B. Thirion, O.
Grisel, M. Blondel, et al. 2011. “Scikit-learn: Machine Learning in
Python.” *Journal of Machine Learning Research* 12: 2825–30.

</div>

<div id="ref-R">

R Core Team. 2019. *R: A Language and Environment for Statistical
Computing*. Vienna, Austria: R Foundation for Statistical Computing.
<https://www.R-project.org/>.

</div>

<div id="ref-Python">

Van Rossum, Guido, and Fred L. Drake. 2009. *Python 3 Reference Manual*.
Scotts Valley, CA: CreateSpace.

</div>

<div id="ref-tidyverse">

Wickham, Hadley. 2017. *Tidyverse: Easily Install and Load the
’Tidyverse’*. <https://CRAN.R-project.org/package=tidyverse>.

</div>

<div id="ref-knitr">

Xie, Yihui. 2014. “Knitr: A Comprehensive Tool for Reproducible Research
in R.” In *Implementing Reproducible Computational Research*, edited by
Victoria Stodden, Friedrich Leisch, and Roger D. Peng. Chapman;
Hall/CRC. <http://www.crcpress.com/product/isbn/9781466561595>.

</div>

</div>