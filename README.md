
# Sarcasm Detector ( in Reddit Comments )

<img src="figures/unrelated_pngs_gifs_for_README/pblogo01.png" width=100%/>

<br>
<br>

2025 Spring\
Diablo Valley College\
Project Bracket Computer Science Club

<br>

---
<br>

<img src="figures/unrelated_gifs_for_README/kitty-stuck.gif" width="50%" height="50%"/><img src="figures/unrelated_gifs_for_README/matrix-cat.gif" width="50%" height="50%"/>

<small>The above gifs are retrieved from [tenor.com](https://tenor.com).</small>

---

### __Team__

Johnson Liu\
<sub><small>
GitHub: [@johnson-liu-code](https://github.com/johnson-liu-code)\
</small></sub>
<sup><small>
Email: [liujohnson.jl@gmail.com](mailto:liujohnson.jl@gmail.com)
</small></sup>

Heidi\
<sub><small>
GitHub: [@heidi415D](https://github.com/heidi415D)
</small></sub>

Bryan\
<sub><small>
GitHub: [@hBrymiri](https://github.com/hBrymiri)
</small></sub>

## __Contents__

1. [Project Overview](#project-overview)\
    1.1. [Background](#background)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1.1.1. [Natural Language Processing NLP](#natural-language-processing---nlp)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1.1.2. [Word Embedding](#word-embedding)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1.1.3. [Word2Vec](#word2vec)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1.1.4. [GloVe](#glove)\
    1.2. [Data Used](#data-used)\
    1.3. [Variable Definitions](#variable-definitions)\
    1.4. [Mathematical Foundations](#mathematical-foundations)\
    1.5. [Workflow](#workflow)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1.5.1. [Collect comments classified as sarcastic/not sarcastic](#collect-comments-classified-as-sarcasticnot-sarcastic)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1.5.2. [GloVe model](#glove-model)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1.5.3. [Collect comments and classify them](#collect-comments-and-classify-them)
2. [Resources and Background Information](#resources-and-background-information)\
    2.1. [Data](#data)\
    2.2. [Theoretical Foundations](#theoretical-foundations)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.2.1. [Natural Language Processing](#natural-language-processing)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.2.2. [word2vec Model](#word2vec-model)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.2.3. [GloVe Model](#glove-model)\
    2.3. [Sample Works](#sample-works)\
    2.4. [Documentation and Tutorials](#documentation-and-tutorials)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.4.1. [Neural Networks](#neural-networks)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.4.2. [Gensim](#gensim)\
    2.5. [Other Theoretical Backgrounds](#other-theoretical-backgrounds)\
    2.6. [Mathematical References](#mathematical-references)\
    2.7. [Graphical Visualization Guides](#graphical-visualization-guides)
3. [Graphics](#graphics)\
    3.1. [Data Visualization](#data-visualization)\
    3.2. [Machine Learning Visualization](#machine-learning-visualization)
4. [Results](#results)
5. [The Codebase](#the-codebase)\
    5.1. [Python Libraries Used](#python-libraries-used)
6. [Future Direction and Possible Improvements](#future-direction-and-possible-improvements)
7. [Miscellaneous notes for collaborators working on the project](#miscellaneous-notes-for-collaborators-working-on-the-project)\
    6.1. [Important Dates](#important-dates)\
    6.2. [Records](#records)




## __Project Overview__

### __Background__

**... write some text talking about the background of sentiment analysis ...**

##### <ins>Natural Language Processing - NLP</ins>

Natural Language Processing (NLP) can be used for sentiment analysis, which helps identify whether a piece of text expresses a positive, negative, or neutral emotion. NLP allows us to organize unstructured data—like social media posts, emails, and other forms of natural text—into a form that machines can work with by applying text classification techniques.

This is usually done by training a classifier on a dataset that has been labeled in advance. For example, some texts might be labeled as sarcastic while others are not. The classifier learns patterns in the language based on these labels and tries to apply what it learns to new, unseen data.

##### <ins>Word Embedding</ins>
ML algorthims struggle to work well with words. Instead we will work with numbers by assigning random numbers to words. Since words can be used in different contexts, like in *sarcasm* assigning certain words more than one number is best practice so that the **Neural Network** can adjust based on context.

##### <ins>Word2Vec</ins>
Word2Vec is a model that learns word meanings based on the words that commonly appear around them. For example, the words “*doctor*” and “*nurse*” often show up in similar contexts, so Word2Vec places them close together in vector space. This helps the model understand how words relate to one another. In sarcasm detection, understanding context is key, and Word2Vec helps capture that by noticing patterns in how words are used together.

##### <ins>GloVe</ins>
Global Vectors for Word Representation, is another word embedding model. Unlike Word2Vec, which focuses on small windows of text, GloVe looks at word co-occurrence across an entire dataset. This gives it a more global understanding of word relationships. GloVe can help highlight unusual or ironic word pairings—something that often happens in sarcastic sentences.

Some users on Kaggle have successfully used Word2Vec and GloVe to detect sarcasm in news headlines. In one project, they trained their model using headlines from The Onion (a satirical site) and The Huffington Post (a more traditional news source). The model achieved around 83% accuracy in detecting sarcasm.

We can apply a similar approach in our project using Reddit posts. Instead of news headlines, we’ll train our model on a dataset of labeled Reddit comments, using Word2Vec or GloVe to create embeddings. This will allow our classifier to learn the difference between sincere and sarcastic language based on context—just like in the Kaggle example.




### __Data Used__

The data that was used in this project was taken from the *Sarcasm on Reddit* notebook from Kaggle.com ( see [2.1 Data](#data) ).


### __Variable Definitions__

See reference [2.2.3. GloVe model](#theoretical-foundations) in the Theoretical Foundations section.

1. $C$ is the collection of all comments in the dataset.

2. $c \in C$ is comment.

3. $k$ is the number of words contained within comment $c$.

4. $W$ is the set of all unique words that appear in the corpus ( the collection of written text ).

5. $N = |W|$ is the cardinality of $W$.

6. $V$ is the set of all word vectors.

7. $v \in V$ is a word vector.
There is a word vector $v_i \in V$ associated with each $w_i \in W$.
Let $g$ be the mapping from $W$ to $V$.
Then

$$V \ = \ g(W)$$
$$ v_i \ = \ g(w_i) .$$

8. $m = \text{dim}(v)$ is the dimensionality of the word vectors.

9. $X$ is the co-occurrence matrix for every possible pair of words $(w_i, w_j) \in W^2$.

10. $X_{ij}$ is the $i$-th row, $j$-th column entry in $X$ which gives the number of times word $w_j$ appears in the context of word $w_i$.

11. $X_i$ is the summation over all $X_{ik}$ for $k \leq N$. In other words,

$$X_i \ \ = \ \ \sum_{\substack{k = 1, \\ k \neq i}}^{N} X_{ik} \ \ . $$

12. $P$ is the co-occurrence probabilities matrix for every possible pair of words $(w_i, w_j) \in W^2$.

13. $P_{ij}$ is the $i$-th row, $j$-th column entry in $P$ which gives the probability that word $w_j$ appears in the context of word $w_i$. You can also think of $P_{ij}$ as the chance of finding word $w_j$ given that you have word $w_i$. This probability is defined as

$$P_{ij} \ \ = \ \ P(\text{word}_j|\text{word}_i) \ \ \\ $$

$$P_{ij} \ \ = \ \ \frac{X_{ij}}{X_i} \ \ . $$




### __Mathematical Foundations__

##### <ins>... something something ...</ins>

##### <ins>Fréchet Mean</ins>
Given a set of vectors, the Fréchet mean is a single point that averages over all of the vectors.
The mean acts as a point of central tendency for the word vectors associated with a specific comment.

##### <ins>... something something ...</ins>

### __Workflow__

##### <ins>Collect comments classified as sarcastic/not sarcastic</ins>

1. ... text here ...

2. ... text here ...

<!-- #### <ins>word2vec model</ins>

1. ... text here ...

2. ... text here ... -->

##### <ins>GloVe model</ins>
General workflow when applying the GloVe model ...
1. Process raw data

    1. Remove stopwords, punctuation, and other words and/or characters that are deemed not important to the context of a comment.

        1. Stopwords are commonly used words within a language that appear frequently in many contexts. These words are assumed to be not important when discerning between comments that are meant to be sarcastic and comments that are not meant to be sarcastic.

        1. Although punctuations might be important in lending context to comments with sarcastic tones, we will assume that they do not in order to simplify our project. Future works might look into the importance of punctuations in sarcastic comments as well as developing a way to incorporate punctuations into the classification of such comments.

        1. Miscellaneous words/phrases/characters that are troublesome to work with ( such as emoticons, words from other languages, mathematical notation, etc. ) or otherwise deemed unimportant can be treated like stopwords and punctuations and removed from the data.

    1. Generate the vocabulary.

        1. The vocabulary is the set containing all of the words present within the corpus ( dataset ).

1. Compute the co-occurrence probability matrix.

    1. Compute the co-occurence matrix with a specified context window size.

        1. The co-occurence matrix tabulates the amount of times word $w_i$ appears in the context of word $w_j$.

        2. The context window is the range centered on the target word from which we count the number of times the context word shows up.

    1. Compute the pairwise co-occurrence probabilities using the co-occurrence matrix.

        1. ... text here about computing co-occurrence probabilities ...

1. Train word vectors for each unique word.

    1. We have to decide on the dimensionality of each word vector. Greater dimensionality might capture more nuances between words, but will also increase the demand on computational resources.

    1. ...text here...

    1. ...text here...

1. Train the neural network.

    1. In order to able to pass our data as input into the neural network, the input shape across all comments must be uniform. Since each comment in the dataset can have varying number of words, we have to decide on a way of aggregating all of the words in a comment into a single input.

        1. ... text here on one possibility ... using the Frechet mean ... \
        One possibility is to take the average of all of the word vectors contained within a comment.

            1. ... text here about the Frechet mean being a measure of central tendency ...

            1. In the context of this project, the Frechet mean for all of the word vectors associated with a specific comment is simply the arithmetic mean of the collection of vectors. This mean is found by taking the component-wise mean of each vector component.

    1. ... text here on structure of neural network ...

    1. ... text here on passing the data as input into the neural network ...


##### <ins>Collect comments and classify them</ins>

1. ... text here ...

1. ... text here ...

## __Resources and Background Information__

### __Data__
1. [*Sarcasm on Reddit* (Kaggle dataset with Reddit posts classified as either sarcastic or not sarcastic).](https://www.kaggle.com/datasets/danofer/sarcasm/data?select=train-balanced-sarcasm.csv)

### __Theoretical Foundations__

##### <ins>Natural Language Processing</ins>
1. [Natural language processing (Wikipedia article).](https://en.wikipedia.org/wiki/Natural_language_processing)

1. [*Text Classification & Sentiment Analysis* (blog post).](https://mlarchive.com/natural-language-processing/text-classification-sentiment-analysis/)

1. [*Text Embeddings: Comprehensive Guide* (blog post).](https://towardsdatascience.com/text-embeddings-comprehensive-guide-afd97fce8fb5/)

1. [*Word Embeddings – Explained!* (blog post).](https://towardsdatascience.com/word-embeddings-explained-c07c5ea44d64/)

##### <ins>word2vec Model</ins>
1. [*Word2Vec: NLP with Contextual Understanding* (theoretical guide for word2vec and GloVe models).](https://mlarchive.com/natural-language-processing/word2vec-nlp-with-contextual-understanding/)

1. [Word2vec model (Wikipedia article).](https://en.wikipedia.org/wiki/Word2vec)

1. [*CBOW — Word2Vec* (continous bag of words and word2vec models).](https://medium.com/@anmoltalwar/cbow-word2vec-854a043ee8f3)

1. [*Efficient Estimation of Word Representations in Vector Space* (original academic paper).](https://arxiv.org/abs/1301.3781v3)

##### <ins>GloVe Model</ins>
1. [GloVe model (Wikipedia article).](https://en.wikipedia.org/wiki/GloVe)

1. [*GloVe: Global Vectors for Word Representation* (original manusript/academic paper).](https://nlp.stanford.edu/pubs/glove.pdf)

### __Sample Works__
1. [*Sarcasm Detection with GloVe/Word2Vec* (project on Kaggle applying the word2vec and GloVe models to classifying news headlines from _The Onion_ and the _The Huffington Post_).](https://www.kaggle.com/code/madz2000/sarcasm-detection-with-glove-word2vec-83-accuracy)

### __Documentation and Tutorials__

#### <ins>Neural Networks</ins>
1. [*Your First Deep Learning Project in Python with Keras Step-by-Step* (building and training a neural network in Python with Keras).](https://machinelearningmastery.com/tutorial-first-neural-network-python-keras/)

1. [*Your First Deep Learning Project in Python with Keras Step-by-Step* (tutorial on building neural networks in Python (_GeeksforGeeks_)).](https://www.geeksforgeeks.org/training-a-neural-network-using-keras-api-in-tensorflow/)

1. [*Python AI: How to Build a Neural Network & Make Predictions* (tutorial on building your own neural network in Python from scratch (_Real Python_)).](https://realpython.com/python-ai-neural-network/) 

#### <ins>Gensim</ins>
1. [*Gensim Word2Vec Tutorial* (notebook posted on Kaggle by one of the developers of Gensim).](https://www.kaggle.com/code/pierremegret/gensim-word2vec-tutorial)

1. [*Word2vec embeddings* (word2vec module documation from the Gensim website).](https://radimrehurek.com/gensim/models/word2vec.html)

1. [*Word2Vec Model* (word2vec tutorial from the Gensim website).](https://radimrehurek.com/gensim/auto_examples/tutorials/run_word2vec.html)

### __Other Theoretical Backgrounds__
1. [*Machine Learning Tutorial* (general overview/tutorial on machine learning (_GeeksforGeeks_)).](https://www.geeksforgeeks.org/machine-learning/)

1. [*AI ML DS - How To Get Started?* (general overview on artificial intelligence, machine learning, and data science (_GeeksforGeeks_)).](https://www.geeksforgeeks.org/ai-ml-ds/)

1. [Bag of words model (Wikipedia article).](https://en.wikipedia.org/wiki/Bag-of-words_model)

1. [Logistic regression (Wikipedia article).](https://en.wikipedia.org/wiki/Logistic_regression)

1. [Multinomial logistic regression (Wikipedia article).](https://en.wikipedia.org/wiki/Multinomial_logistic_regression)

1. [Least squares (Wikipedia article).](https://en.wikipedia.org/wiki/Least_squares)

1. [Tf-idf [ term frequency-inverse document frequency ] (Wikipedia article).](https://en.wikipedia.org/wiki/Tf%E2%80%93idf)

### __Mathematical References__

1. [Dot product (Wikipedia article).](https://en.wikipedia.org/wiki/Dot_product)

1. [Cosine similarity (Wikipedia article).](https://en.wikipedia.org/wiki/Cosine_similarity)

1. [Linear least squares (Wikipedia article).](https://en.wikipedia.org/wiki/Linear_least_squares)

1. [Fréchet mean (Wikipedia article).](https://en.wikipedia.org/wiki/Fr%C3%A9chet_mean)

### __Graphical Visualization Guides__
1. [*The Art of Effective Visualization of Multi-dimensional Data* (guide on plotting multidimensional data).](https://towardsdatascience.com/the-art-of-effective-visualization-of-multi-dimensional-data-6c7202990c57/)

1. [*Top Python Data Visualization Libraries in 2024: A Complete Guide*](https://www.fusioncharts.com/blog/best-python-data-visualization-libraries/)

1. [*A Complete Beginner’s Guide to Data Visualization*](https://www.analyticsvidhya.com/blog/2021/04/a-complete-beginners-guide-to-data-visualization/)

1. [*Tableau for Beginners: Data Visualisation Made Easy*](https://www.analyticsvidhya.com/blog/2017/07/data-visualisation-made-easy/)

1. [*Intermediate Tableau guide for data science and business intelligence professionals*](https://www.analyticsvidhya.com/blog/2018/01/tableau-for-intermediate-data-science/)



## __Graphics__

### __Data Visualization__

_**Preliminary figures.\
Not for use in final product.**_

##### <ins>Word cloud - Sarcastic</ins>
![placeholder-text](figures/raw_data_visualization/wordcloud_sarcastic.png)

##### <ins>Word cloud - Not Sarcastic</ins>
![placeholder-text](figures/raw_data_visualization/wordcloud_not_sarcastic.png)

##### <ins>Word frequency within comments</ins>
![placeholder-text](figures/raw_data_visualization/words_in_comments.png)

##### <ins>Co-occurrence probabilities</ins>
![placeholder-text](figures/testing_02/cooccurrence_probability_heatmap.png)




### __Machine Learning Visualization__

_**Figures used for testing.\
Not for use in final product.**_

_**Fix this**_

![placeholder-text](figures/testing_01/J_and_log_J_over_time_animation.gif)

![placeholder-text](figures/testing_01/test_word_vectors_over_time_animation.gif)




## __Results__

**... text here ...**

**... text here ...**


## __The Codebase__

#### Python Libraries Used


## __Future Direction and Possible Improvements__
1. Machine learning / classification.
    1. Extend project to sentiment and tone classificaiton of text.

1. Browser application.
    1. Develop an app that can be used in a web browser that allows the user to directly take a comment and its associated data straight from the Reddit website.
    1. Develop the app further to display in real time the predicted tone of all of the Reddit comments seen in the current browser window.




## Miscellaneous notes for collaborators working on the project

### __Important Dates__

##### <ins>Week 5/6 — April 16 & April 23, 2025</ins>
Development continues on in week 5 in preparation for the **mid-semester showcase in week 6**. Groups are now in the middle of the semester meaning that they will present what progress they have so far. The mid-semester showcase does not mean that groups have to be halfway done with their projects.

##### <ins>Week 7 — April 30, 2025</ins>
At this point **groups should be more than halfway done with their project** or close to finished in preparation for the final week as well as finals. Project managers should check with members on the final schedule to ensure projects are done and not rushed in the final week.

##### <ins>Week 8 — May 7, 2025</ins>
**Groups should be close to wrapping up their projects** or should be completely done with the projects. This week will be focused mainly on the final project showcase in which judges will determine who has the best project. Groups may want to **prepare ahead of time with presentations**, graphics, and props to enhance their presentations.

---

### __Records__

#### <ins>20250404</ins>

##### Notes
— Johnson
1. Heidi and Brymiri, I will be using this file to keep track of out progress and to assign tasks amongst the team members.
2. I will also use this file to keep track of important dates specified by the club.
3. Please use this file to record any important thoughts that you come up with during the course of the project.
4. You can also use this file to add important notes that you want the team to remember.

##### To-do —
###### For Johnson:
1. [x] Create Github repository.
1. [x] Look up relavant resources.
1. [x] Look up relavant data.
1. [ ] Plan out our timeline and general to-do's / tasks for each team member.

---

#### <ins>20250408</ins>

##### To-do —
###### For Heidi:
1. [x] Review the theoretical resources and begin drafting a short write-up for our team to reference.
1. [ ] Optional - Also look up introductory machine learning resources to clarify specific topics in the write-up, especially if you think they’d be helpful for the team.

###### For Bryan:
1. [x] Write code to extract a specific Reddit post, along with its parent post and the name of the subreddit where it was posted.

---

#### <ins>20250412</ins>

##### Notes
— Johnson
1. Organized files into folders based on their purpose for better structure and clarity.
2. Expanded and refined the files used for data extraction.
3. Developed files dedicated to data visualization.
4. Generated figures to help us better understand the data.

---

#### <ins>20250418</ins>

##### To-do —
###### For Heidi:
1. [ ] Experiment / explore with creating and training neural networks.
1. [ ] Familiarize yourself with the use of the Gensim Python module for word vectors.
1. [ ] Start building and training neural networks to take in word vectors as input and outputs a binary classification ( sarcastic or not sarcastic ).

###### For Bryan:
1. [x] Continue working on code to extract a specific comment from Reddit along with its parent comment and subreddit name.
2. [ ] Possible future feature: create an app that can be used in the browser to predict whether a selected comment is sarcastic or not.

---

#### <ins>20250421</ins>

##### To-do —
###### For Heidi:
1. [ ] Continue updating WriteUp.md as you better understand the theory behind the word embedding and machine learning techniques used in the project.

###### For Johnson:
1. [ ] Start documenting the directory structure and its organization.
1. [ ] Start documenting the workflow and the theory and mathematics behind each model that we use.

---

<br>

<img src="figures/unrelated_pngs_gifs_for_README/pblogo01.png" width=100%/>
