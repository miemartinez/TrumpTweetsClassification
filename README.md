# Tracking the development of Topics in Trump Tweets
### Unsupervised machine learning
**This project was developed as part of the spring 2021 elective course Cultural Data Science - Language Analytics at Aarhus University.** <br>

__Task:__ The task for this project is to train an LDA model on data from Twitter to extract structured information that can provide insight into the development of topics in Trumps tweets.

For this assignment, I chose to examine the development of topics depicted in Donald Trump's tweets. For this, I found a dataset on Kaggle (https://www.kaggle.com/codebreaker619/donald-trump-tweets-dataset). The tweets are from around 2011 (with a few tweets from 2009 and 2010) to the beginning of 2021. I wanted to see if it was possible to train a model that could detect a development in trends that Trump wrote about.

In the data folder there is a csv file with tweets from Trumps twitter account up until he was banned in the beginning of 2021. The output of the python script is also provided in the data folder in the created output folder. This contains a visualization of the created topics saved as an interactive html file. Furthermore, the scripts creates a lineplot that illustrates Trumps development of topics across time. This is saved as a png file.

The script development_of_trump.py is in the src and it takes the filepath to a csv as input. Optionally, you can define the filename of the lineplot, the number of topics and the types of words you wish to examine. If nothing is chosen for the three parameters, defaults are set instead.

A weighted edgelist of the data fake-or-real-news.csv (from Kaggle https://www.kaggle.com/rchitic17/real-or-fake) can be found in the data folder.
Using spacy, all mentions of persons was extracted and it was counted how many times two names co-occured. 
So, the weighted edgelist hold the name of two people (nodeA and nodeB) and number of times they co-occured in a document (weight).

The script is located in the src folder and can be run without specifying further parameters. 
The repository also contains the results from running the unsupervised topic model. 
In the viz folder, two plots can be found visualizing the network of the edgelist with and without labels when filtered at 500. 
In the output folder, the centralities measures for the network are saved as a csv. <br> 

__Dependencies:__ <br>
To ensure dependencies are in accordance with the ones used for the script, you can create the virtual environment ‘network_environment"’ from the command line by executing the bash script ‘create_network_venv.sh’. 
```
    $ bash ./create_sentiment_venv.sh
```
This will install an interactive command-line terminal for Python and Jupyter as well as all packages specified in the ‘requirements.txt’ in a virtual environment. 
After creating the environment, it will have to be activated before running the network analysis script.
```    
    $ source network_environment/bin/activate
```
After running these two lines of code, the user can commence running the script. <br>

### How to run development_of_trump.py <br>
The script network.py can run from command line without additional input. 
However, the user can specify path to the weighted edgelist csv file, a minimum threshold for filtering away edge pairs and 
whether to include labels or not on the network visualization.
The output of the script is a png file of the network and a csv file with three centrality measures (degree, betweenness and eigenvector).

__Parameters:__ <br>
```
    filepath: str <filepath-of-csv-file>, default = "../data/weighted_edgelist.csv"
    weight_threshold: int <filtering-threshold>, default = 500
    include_labels: str <True-or-False>, default = False

```
    
__Usage:__ <br>
```
    network.py -f <filepath-of-csv-file> -w <filtering-threshold> -l <True-or-False>
```
    
__Example:__ <br>
```
    $ cd src
    $ python3 network.py -p -f ../data/weighted_edgelist.csv -w 300 -l True

```

The code has been developed in Jupyter Notebook and tested in the terminal on Jupyter Hub on worker02. I therefore recommend cloning the Github repository to worker02 and running the scripts from there. 

### Results:
The results of the network analysis can be seen in the output and viz folders. Looking at the centrality measures one can see three measures: degree, betweenness and eigenvector centrality. These measures refer to how central the persons are to the network. The most central person seems to be Clinton as it is the node with the most edges/ties (degree centrality = 0.79). Similarly, it is the most important node for the flow of the network since it is the one that best connects many of the other nodes (betweenness centrality = 0.73). Lastly, it is also the node connected to the most central nodes in the network (eigenvector centrality = 0.53). <br>
However, in the csv file of the centrality measures the problem of coreference becomes very apparent. For instance, Hillary Clinton is referred to as “Hillary Rodham Clinton”, “Hillary Clinton”, “Hillary Rodham”, “Hillary”, “Hillary Clinton’s”, “Rodham”, “Clintons” and “Clinton” (which might also refer to Bill Clinton). As these are all connected to the Clinton node this greatly influence the results of the analysis as they all refer to the same person and therefore should constitute only one node and not eight. The only way to solve this problem is to resolve all mentions of the same person entity within a document. <br>

Here, you can see what the network looks like without labels:
![alt text](https://github.com/miemartinez/TrumpTweetsClassification/blob/main/output/trumps_development.png?raw=true)
