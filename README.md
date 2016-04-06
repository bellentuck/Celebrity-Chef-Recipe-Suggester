# Celebrity Chef Recipe Suggester

You’ve got a fridge full of food...what do you <i>do</i> with it? Lacking the know-how to know what to do with it, what’s preventing you from inadvertently making gross or even boring choices? Or for that matter giving up and going with GrubHub?

<b>Wouldn’t you like to see what celebrity chefs could do with your ingredients?</b> Part of our cultural obsession with celebrities, chefs being no exception, is that not only are we curious about what our days would be like if we were celebrities--we’re also curious about what celebrities might do if they were us.

Calling all wannabe Julia Childs out there: what if you got to set up your very own “celebrity <i>Iron Chef</i>”, in which chefs incorporate <i>your</i> ingredients into <i>their</i> recipes, and you get to see how well things blend?

At Metis, data science helped me realize this goal. This repo contains the code to make it happen. 

The `data` folder contains the following ipython notebooks:
- `foodnetwork_cleaner` is a notebook for cleaning celebrity chef recipe data and putting it in a local MongoDB collection.
- `foodnetwork_scraper` is a notebook for gathering celebrity chef recipe data via Food Network, as one could were one given permission to do so.
- `twitter_cleaner` is a notebook for cleaning celebrity chef Tweet data and putting it in a local MongoDB collection.
- `twitter_streamer` is a notebook for gathering celebrity chef Tweet data via the Twitter streaming API.
- `yummly_querier` is a notebook for gathering non-celebrity-chef recipe data via the Yummly rest API.

The `data` folder also contains a `datafiles` sub-folder with the info itself to help you get started.

The `analysis` folder contains the following ipython notebooks:
- `celebrity_recipes_exploratory_analysis` is a notebook for implementing exploratory statistical analysis on celebrity chef recipes' difficulty and durations. 
- `celebrity_recipes_recommendations` is a notebook for making recipe recommendations based on what ingredients you have/want to use, as well as basic statistical parameters, using word2vec and cosine similarity between lists of ingredients (as constrained by the other parameters).
- `clustering_recipes` is a notebook for clustering celebrity chef recipes. 
- `ingredients_similarities_jaccard_vs_cosine` (to come) is a notebook comparing the efficacy of jaccard versus cosine similarity scores for gauging similarities between recipes based on their ingredients.
- `opinion_mining_tweets` is a notebook for performing sentiment analysis on celebrity chef tweets. While this analysis didn't get a place at the table vis-a-vis the final thrust of the current iteration of this project, it adds a touch of joy to the proceedings. 
- `word2vec_ingredients_model_training` is a notebook for training a word2vec model on a corpus of recipes' ingredients.

The `analysis` folder also contains a `modelfiles` sub-folder with the kmeans and word2vec models themselves.

For suggestion-making, I ultimately went with the neural network Word2Vec to come up with context-based cosine similarity scores between ingredient vectors. The idea here is that the more your ingredients have in common with those already called for in a recipe, the better your ingredients can <i>blend into</i> said recipe--whether they’re explicitly called for or not. 

Results rank a given celebrity chef recipe based on a matrix of cosine similarities between the vectors for ingredients you’ve got, and the vectors for those ingredients called for in the recipe. Aggregated scores are further binned into interpretable indications of how well your ingredients will blend, ranging from a “yes”, to a “sure”, to a “why not?”, to even “...it’s an experiment”.

Why stick to celebrity chef recipes? I want to end by overviewing a few business applications enabled by the work I’ve done so far.

First, consider restaurants or food distributors wanting to know how optimize foodstock purchases based on what they've already got, and want to do with it. Put in recipes, input ingredients at hand, and get back the recipes that can be made most easily with these ingredients, as well as what other ingredients will be required. Plugging in information about shortages or gluts of particular ingredients, you'd be able to easily discern which recipe-products will be cheaper or more expensive to produce, and so be able to price accordingly (not to mention dynamically).

Second, consider a grocery purchase app like Instacart (or, for that matter, any of the recipe-based grocery delivery apps currently being advertised throughout the New York City subway system). Imagine if such a grocery app contained the following sort of call-to-action message: "based on the ingredients you've already selected, you're in good shape to make recipes A, B, or C! All you'd need are additional ingredients X, Y, and Z. Would you like to add one or more of these ingredients to your cart?" Alternatively, you could enter ingredients you already have lying around into such an app, and the app could make recipe recommendations and additional ingredient suggestions accordingly. 

Finally, consider smart refrigerators. Imagine integrating features of a fridge like the Samsung Family Hub--a fridge that takes stock of what's inside it--with a program that not merely allows users to look up recipes on the web but uses machine learning to make recipe recommendations and even coordinate the purchase of additional ingredients based on consumer preferences, dietary restrictions, time constraints and the like. In this way data science can enable creative, cosmopolitan cooking. You’d never have to be bored by your food again.