---
layout: post
title: Groa
subtitle: an elegant Movie Recommendation Engine
gh-repo: Gabe-flomo/Groa
gh-badge: [star, fork, follow]
comments: true
---

## Project Description


The companies which have the resources to create an elegant Movie Recommendation Engine have a profit motive aligned with recommending high cost proprietary content rather than films their customers would genuinely enjoy.

Existing web sites geared towards providing a recommendation rely entirely on basic rating models which are weighted heavily towards popular films and generally do a poor job identifying unique outliers.

Groa combines the public data available on IMDb with tried-and-true recommendation techniques to provide a user-driven movie discovery experience. We use two similar language embedding models to acheive this.

We trained Word2Vec on positive user ratings histories to create a user-based collaborative filtering recommender. The algorithm embeds over 97,000 movie IDs into a 100-dimensional vector space according to their co-occurence in a user's positive ratings history. The ID for each movie is a key for its vector, which can be called from the model and compared with any other vector in that space for cosine-similarity. To provide recommendations given a new user's watch history, we simply find the vector average of the user's choice of "good movies" and find the top-n cosine-similar vectors from the model. We can improve the recommendations by subtracting a "bad movies" vector from the "good movies" vector before inferencing. Models trained in this way can be tested by treating a user's watchlist (unwatched movies saved for later) as a validation set.

The above model fulfills most requirements for a general-purpose movie recommender system. However, it is unable to make riskier recommendations for movies that a majority of reviewers do not enjoy (cult movies). To satisfy users who seek underrated movies, we also trained Doc2Vec on user review histories to create a review-based collaborative filtering model. This model does not recommend movies, but finds reviewers who write similarly to a new user. We then query the review database for positive reviews from these users, both in cases where the ratings count is 1k-10k (hidden gems), and where the reviewer rates a movie 3 stars more than the average.

The lightning-fast inferencing of the Word2Vec/Doc2vec algorithms allows us to incorporate user feedback into progressively updating recommendations. If the user elects to approve or disapprove of a movie, its corresponding vector is added to, or subtracted from, the user's overall taste vector. Weighting these feedback vectors by a factor like 1.2 increases the influence of that feedback on the user's taste vector, and this factor can be tweaked to change the effective "learning rate" of the re-recommendations process.

## Demo
If you would like to try Groa out for yourself [here's a link](https://www.groa.us/)

If you're a more visual learner here's our [demo video](https://vimeo.com/397993197) 
