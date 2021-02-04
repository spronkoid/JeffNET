
![](https://cdn-images-1.medium.com/max/3600/1*-ItX6TCOg1ii4mJWN1ZJMQ.jpeg)

## JeffNet — A More Reasonable Approach to a Wine Recommendation Service Automated with ML

(A Satirical and Very Unprofessional Response to “DeepWine”)

*Chloe Reams — [https://spronkoid.medium.com](https://spronkoid.medium.com) — I’m sorry in advance I like making fun of people that have done nothing wrong*

## 1. Introduction

While viewing selections of wines, be it in a store or online, we usually find them along with detailed reviews from magical higher-up wine reviewers. Though if there happened to be a catalogue of some very large amount of wines, it may be hard to find time for humans to rate all of them by taste. Reviews like this are integral parts of the marketing for wines and new emerging wine companies may have no way to break the surface without them.

This project attempts to have a solution, albeit quite temporary, though more suited to online shops and recommendation engines, to this problem. We have a corpus of thousands of human-written and curated pre-existing reviews for wines, and feed them through this system in hopes that it can generate coherent reviews from scratch.

## 2. Related Work

Another wine review generation technique, using code from the author of this paper, has been called “DeepWine” and was the Final Report for three students’ Standford CS230-Fall course. Where they compared OpenAI’s GPT2 to text generated from an RNN/GRU. They reference another student project that had generated “obviously machine generated” text that “lacked common sense and English structure.” This paper seeks to only make that problem worse, by giving the bare minimum.

## 3. Dataset

A dataset available on Kaggle was used to train this system. It contains 150k pre-existing wine reviews as well as details about the origin of the wines. “Key columns include grape variety, points, region and the review itself.” (DeepWine, pg.1) Most points were left out of view of this system.

## 4. Methods

### 4.1 Results of DeepWine

The results of DeepWine’s RNN/GRU were nothing short of boring and lack basic English structure, just as they had criticized with previous results. They also had not taken into account modern techniques of utilizing RNN/GRU and LSTM models, and it can be assumed their model was not large enough. It was also comical to read the words

"Similar to the dinosaur language exercise in Coursera, we used our model to do character level prediction,"

as character level prediction is generally the worst way to go here.

### 4.2 JeffNet (JesusForF’s-sake Neural Network)

*also known as Multi-Layer Perceptron based Dense Representation Prediction*

First the Tensorflow-Hub model “Universal Sentence Encoder,” a model trained by Google to do exactly what the name implies, is used to encode the reviews into 512 dimensional vectors, as well as all the other data about the wine, such as Country and Region of origin, variety of wine, and winery it came from.

There are now two lists of 512 dimensional vectors, one for the data about the wine, and one for the reviews. This will be used in conjunction with a custom Feed Forward Network (or Multi-Layer Perceptron) to predict the review vector based on the data vector.

Now the MLP is trained to do as proposed previous, predict what review vector for a new bit of data. Then a search is performed on the already existing reviews to pick out which would be the best match, as there are 150,000 reviews in this dataset, it’s bound to find one that matches almost perfectly, that’s the beauty with Big Data.

### 4.2.1 POS Tagging to Extract Key-words

Now a Parts of Speech Tagger is used, which comes with the SpaCy library, to highlight any adjectives within the review. These are then used to create “tags,” which may be used by a recommendation engine to recommend similar wines, or as a feature for a search engine to find a certain type of wine. From here we can go on to experimentally generate new reviews based on the tags

## 5. Results

An output for Country: France, Province: Provence, Region: Bandol, Winery: Domaine de la Bégude, Designation: La Brûlade, Variety: Provence red blend, and Price: 66.0 reads:
>  Best Match: second, ripe, broad, full, bright, red, fresh, gentle

The true review for this specific wine was
>  “This is the top wine from La Bégude, named after the highest point in the vineyard at 1200 feet. It has structure, density and considerable acidity that is still calming down. With 18 months in wood, the wine has developing an extra richness and concentration. Produced by the Tari family, formerly of Château Giscours in Margaux, it is a wine made for aging. Drink from 2020.”

I feel the acidity and richness are accurately reflected within the tags with the words “Ripe,” “Broad,” and “Bright.” Though this could be confirmation bias peeking it’s way through.

## 6. Conclusion and Future Work

I will continue to develop this, playing with different architectures and employing genetic algorithms to find the best suited model for the job, but for a one-off project I completed within a couple hours, I think this was pretty good.

[-Chloe](https://github.com/spronkoid)

*p.s. a notebook with all the code can be found [here](https://colab.research.google.com/drive/1sPxlJc4OFnlQvip7rw6baf-pmHF1T_6V?usp=sharing)*

![](https://cdn-images-1.medium.com/max/2000/0*sBrnF-N2P0gWak2n.png)

This work and accompanying code is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-nc-sa/4.0/).

