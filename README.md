# ENM Final Project: Smash Ultimate Match Outcome Prediction

![Head](/assets/smash.png)

## Question

What factors have the most impact on the outcome on a match in the game Super Smash Bros Ultimate?

### Abstract

#### Gap

Smash Ultimate is an immensely popular game with a large following and immense presence in the e-sports community. There are many in-person bets for smash tournaments, with a large audience of watchers trying to predict who the winner of a match set might b, whether it be for compensation or for enjoyment. The game is very complex with many moving parts, involving over 80 playable characters with a variety of playstyles, and can be described as a fighting game where each player has 3 lives. There is no such model out there to predict the outcome of a match based on previous fine-grained game data, given the large magnitude of variables involved with the game. In this project, we attempt to study the game as a whole to determine such signals for predicting game outcomes, and create the final product in the form of a website that predicts the probability of a winner given the strongest input signals.

#### How

We reference Smash Ultimate tournament data from the [smash.gg](https://smash.gg/) platform, where it was aggregated into a CSV file via [ultimategamedata.com/about](https://ultimategamedata.com/about) – each match holds data on the players involved, the characters they used, the stage they played on, and the outcome of the match, among many other fields. We fetch character abilities and statistics from the [https://ultimateframedata.com/smash](ultimate frame data) website. We also retrieve a character-playstyle mapping from [reddit](https://www.reddit.com/r/coolguides/comments/qwz76v/smash_ultimate_character_archetype_tier_list/).

#### Findings

We find that the game is generally very balanced as a whole when it comes to character and playstyle interactions, but that the player specialty (in terms of characters) and overall skill is a heavy factor in the outcome of a game, as well as the character performances on a particular stage. Our final model had an accuracy of 73%, which is a fair amount higher than the baseline 50% prediction of a randomized model.

Given this, our model has immense potential for a first step of a probability-based betting model, after our overall study of the game, with a good grasp on what gives the most weight advantage-wise to a match-up.

## Approach

### Feature Investigation

For the full exploratory data analysis, feature derivation, and model engineering, please visit the [Jupyter notebook write-up](https://drive.google.com/file/d/1GaBkGPVTLT_6Sc6Vtfav_ksToTPogC8y/view?usp=sharing), which has the full code and results. Overall, we conduct a deep correlation analysis on players and their past games, character matchups, player-character specialties, stages, character abilities (advanced statistics), and a character's stage performance.

### Predictive Model

We landed on using a logistic regression model to bind our final output to predicting whether player 1 or player 2 would win. We determined the strongest coefficients to be the ones highlighted below, which we then use accordingly in our final product. Both training and test performed at the same 73% benchmark accuracy.

![Head](/assets/coefficients.png)

### Final Product

The final product can be found at [https://enm-final.web.app/](https://enm-final.web.app/) – please feel free to try it out! The source code for the website [here](https://github.com/pat-liu/enm-final) – most of the logic is in src/App.js, with our exported dataframe data from the Jupyter notebook analysis in the public/ directory (in the form of processed json maps: character_stage_map.json, characters.json, player_char_map.json, player_games_map.json, player_map.json). We hard-coded the final coefficients from our logistic regression model into the underlying frontend code itself.

![Head](/assets/website.png)

How it essentially works is we select both parties involved in the match, along with the fighters they are using: (player1, character1) and (player2, character2). Finally, we select the battlefield they will play on. The website will then output our final model's prediction at the bottom in terms of probability, on whether player 1 will win the match.

![Head](/assets/chat.png)

We were able to reference ChatGPT to convert the initial prediction of 0 or 1 (the former predicting that player 1 would win, and the latter predicting player 2 would win) into instead a probability of player 1 winning, as seen above – this is a bit more useful for betting purposes. ChatGPT was extremely helpful in brainstorming potential features and approaches in exploring our data, as well as website styling in our final final product.
