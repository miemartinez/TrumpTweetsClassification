# Tracking the development of Topics in Trump Tweets
### Unsupervised machine learning
**This project was developed as part of the spring 2021 elective course Cultural Data Science - Language Analytics at Aarhus University.** <br>

__Task:__ The task for this project is to examine the development of topics depicted in Donald Trump's tweets by training a Latent Dirichlet Allocation (LDA) model on data from his Twitter account. 

The data used for this project can be found on Kaggle (https://www.kaggle.com/codebreaker619/donald-trump-tweets-dataset). The tweets are from around 2011 (with a few tweets from 2009 and 2010) to the beginning of 2021 (when he was banned from Twitter). I wanted to see if it was possible to train a model that could detect a development in trends that Trump wrote about. The csv file can also be found in the data folder. <br>

The output of the topic model is provided in the output folder. This contains a visualization of the created topics saved as an interactive html file. Furthermore, the scripts creates a lineplot that illustrates Trumps development of topics across time. This is saved as a png file and can also be seen in the bottom of this README. 

The script development_of_trump.py is in the src and it can run without any input. However, the user can define the path to the csv file if they choose to place it differently than in this repo. Similarly, the user can specify filename of the lineplot, the number of topics and the types of words they wish to examine. If nothing is chosen for the parameters, defaults are set instead.

__Dependencies:__ <br>
To ensure dependencies are in accordance with the ones used for the script, you can create the virtual environment "classifier_venv" from the command line by running the bash script create_classify_venv.sh

```
    $ bash ./create_classify_venv.sh
```
This will install an interactive command-line terminal for Python and Jupyter as well as all packages specified in the ‘requirements.txt’ in a virtual environment. 
After creating the environment, it will have to be activated before running the topic model.
```    
    $ source classifier_venv/bin/activate
```
After running these two lines of code, the user can commence running the script. <br>

### How to run development_of_trump.py <br>

__Parameters:__ <br>
```
    filepath: str <filepath-of-csv-file>
    output_filename: str <name-of-png-file>, default = "trumps_development.png"
    n_topics: int <number-of-topics>, default = 15
    word_types: list <list-of-word-types>, default = "NOUN"
```
    
__Usage:__ <br>
```
    development_of_trump.py -f <filepath-of-csv-file> -o <name-of-png-file> -n <number-of-topics> -w <list-of-word-types>
```
    
__Example:__ <br>
```
    $ cd src
    $ python3 development_of_trump.py -f ../data/Trump_tweets.csv -o trumps_development.png -n 10 -w "['NOUN', 'VERB']"

```

The code has been developed in Jupyter Notebook and tested in the terminal on Jupyter Hub on worker02. I therefore recommend cloning the Github repository to worker02 and running the scripts from there. 

### Results:
The results of the final model had a perplexity score of -7.85 and a coherence score of 0.29. The coherence score got higher as I increased number of topics. However, as this interfered with the interpretability of the lineplot I decided to only include 10 topics in the final run.

When looking at the three most dominant topics (topics 1-3 in the html file), the topics that Trump has been most occupied with seems to be about i) the elections (with a focus on tax cuts and jobs), ii) being the target of a media witch hunt, and iii) a topic of presidential campaign, denial and rebuttals to news statements and a bit about the stock market as well. The latter topic is a bit harder to label as it contains many different features but it includes words like "respect", "women", "refuse" and "source". Looking through the tweets, these words are often related to rebuttals of something from the media press. <br>
All three topics line up with my expectation and knowledge about Trump and his agenda as a politician. <br>

I think using both nouns and verbs gave me the most clearly defined topics. In contrast, I also tried using adjectives and adjectives and nouns as well as just nouns.
As I wanted to examine the development of topics, I created a lineplot with a rolling mean using seaborn. For this, 10 topics gave the clearest visibility as 15-20 topics made it almost impossible to make inferences about how the topics were distinct across time. <br>

Looking at the plot in the png file, it is evident that the dominant topics are 4, 8 and 6 (see plot below). When comparing with the print of topics in the terminal, it becomes clear that these topics are equal to topics 3, 1 and 2 in the html, respectively. So, the development appears to go from being about Trump running for president for the first time and handling the accusations that are thrown at him (topic 4). It then seems to evolve into being more about his political agenda of tax cuts and creating jobs and then rerunning for president (topic 8). During his second presidential campaign, a rise can also be detected in a topic revolved around battling with the news and media in an alleged "witch hunt". With this he refers both to the impeachment and accusations of collusion. Interestingly, it should be noted that the topic for running from president differ slightly from the first to the second time as these are represented by different feature spaces (4 and 8). <br>

![alt text](https://github.com/miemartinez/TrumpTweetsClassification/blob/main/output/trumps_development.png?raw=true)

Of course, many more topics are present in the topic modeling (like topic 9 and 10 in the HTML being about the rigged election and ballot fraud) but this was just to give an overview of the three most dominant topics. <br>
It should also be noted that these are just my interpretations of the topics. I do not dismiss that there might be more correct and profound interpretations.
