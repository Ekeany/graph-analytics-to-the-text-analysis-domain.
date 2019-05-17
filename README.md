# graph-analytics-to-the-text-analysis-domain.

## Introduction.

The brain reads information in a linear fashion with the eye moving from left to right, from top to bottom. However, this is not the most efficient method of obtaining a brief summary of the information at hand. Using a combination of both natural language processing and network science a graphical approach was used in an attempt to summarize the main themes and relationships of a novel.

Representing text through the framework of a network, provides numerous graphical tools that can be used to detect communities of interrelated concepts, find the most influential characters/concepts, and more importantly offer a quantitative evaluation of textual data. In essence, a network allows the user to visualize the topical structure of the text and use the graph’s inherent structural property to evaluate the relative importance of the topics, to formulate meaning.

The methodology used to create the text networks within this report was inspired by a paper titled “Visualization of Text’s Polysingularity Using Network Analysis” (Dmitry Paranyushkin, 2012). This process involved encoding every word in the preprocessed text as a node where the co-occurrence between words was used as the connection between them. The algorithm was predicated upon a sliding window that is moved incrementally through the text. Every word within this window is considered to be connected, although the weight of this connection is based upon their element wise distance in the window.

### Novel Summary.

The novel chosen for this report was John Steinbeck’s well-known classic, “Of Mice & Men”. A brief description of the novel is provided below to inform the reader about the basic content of the novel in order to qualitatively understand the analysis;

“One evening, two men, on their way to a ranch, stop at a stream near the Salinas River. George, who is short and dark, leads the way. The person following him is Lennie, a giant of a man with huge arms. During their conversation by the stream, George repeatedly asks Lennie to keep his mouth shut on the ranch, suggesting that Lennie has some kind of problem. After supper and before going to sleep, the two of them talk about their dream to own a piece of land.

The next day, George and Lennie travel to the ranch to start work. They are given two beds in the bunkhouse. Then Old Candy introduces them to almost everybody on the ranch. They meet the boss and the boss’s son Curley, who is quite rude. They also meet Curley’s wife when she comes looking for her husband. She wears heavy make-up and possesses a flirtatious attitude. George warns Lennie to behave his best around Curley and his wife. He also suggests that they should meet by the pool if anything unfortunate happens to either of them on the ranch.

George and Lennie are assigned to work with Slim, who is sensible and ‘civilized’ and talks with authority. George finds Slim an understanding confidante, and a bond forms between the two of them. When Curley wrongly accuses Slim for talking to his wife, Slim gets very angry. Curley apologizes to him in the bunkhouse in front of everybody, but his apology is rejected. Curley vents his frustration on Lennie, trying to pick a fight. Lennie does not hit back initially, but when George asks him to, Lennie obliges and crushes Curley’s hand. Curley agrees that he will not tell anyone about his hand, for it would mean losing his self-respect.

While working on the ranch, George and Lennie continue to dream about owning their own piece of land and make plans accordingly. Old Candy, one of the ranch hands, overhears their planning and asks to join them. He even offers to contribute all of his savings to purchase the land. George and Lennie accept his proposal.

One evening, Lennie, looking for his puppy, enters the room of Crooks; since he is the only black man on the ranch, Crooks lives alone, segregated from the other ranch workers. Candy enters, looking for Lennie; the two of them tell Crooks about their dream of owning their own ranch, but Crooks tells them that it will never happen, foreshadowing the truth. Curley’s wife comes in and interrupts them. When Crooks objects to her presence in his room, she threatens him with a false rape charge. Later on, Lennie is seen alone in the barn, petting his dead pup. He has unintentionally killed it by handling it too hard. Now he is grieving over the loss. Curley’s wife walks into the barn and strikes up a conversation with Lennie. As they talk, she asks him to stroke her hair. She panics when she feels Lennie’s strong hands. When she raises her voice to him, Lennie covers her mouth. In the process, he accidentally breaks her neck and she dies. Knowing he has done something terrible, he leaves the ranch. When the ranch hands learn that Curley’s wife has been killed, they rightly guess the guilty party. Led by an angry Curley, they all go out to search for Lennie. They plan to murder him in retribution.

George guesses where Lennie is and races to the pool. To save him from the brutal assaults of the ranch hands, George mercifully kills his friend himself. Hearing the gunshot, the searchers converge by the pool. They praise George for his act. Only Slim understands the actual purpose of George’s deed." (http://thebestnotes.com, 2017).

### Natural Language Processing.

Natural Language Processing (NLP) is a sub-field of Artificial Intelligence that is focused on enabling computers to understand and process human language. A number of these techniques were implemented in conjunction with the network analysis to complement and highlight certain aspects of the text. Besides the standard preprocessing techniques such as word tokenization, stemming and the removal of stop words. More explanatory techniques such as part of speech tagging, td_idf and sentiment analysis were all implemented within this report. One of the more unique techniques used within this report was text summarization. This was implemented using the LexRanker package in R which constructs a network where each sentence represents a node and the edges are the pairwise correlation between sentences. The Page Rank algorithm is then used to find the most important sentences in the text. This technique was used to shorten the text used within the report and to make more interpretable graph structures

The first technique implemented was simply a frequency count of the top 15 words in each chapter of the book. The frequency of each word was scaled using the inverse document frequency which assigns a higher weight to more important and relevant words in each chapter. The plots give a brief introduction to the content of each chapter however. No theme, relationships or characters are defined

<p align="center">
  <img width="932" height="618" src="/Images_/image1.PNG">
</p>

The second technique utilized was sentiment analysis this was implemented using the Tidytext package in R. This package provided a referenced data frame that contained the sentiment score of a variety of words. The chapter wise emotional sentiment was then calculated using a number of emotional categories including Trust, Sadness, Joy and Fear etc. From the figure below the overall distribution of each chapter varies slightly however there is a large discrepancy in the total number of words in each chapter which can be neglected based upon the relative size of each chapter.

<p align="center">
  <img width="939" height="614" src="/Images_/image2.PNG">
</p>

The third plot encapsulates a more rudimentary sentiment metric which refers to the number of either positive or negative words in a sentence. The total sentiment for each sentence in every chapter was plotted to give an indication on plot progression as a function of time. The two large down spikes at the middle and end of the book correspond to intense parts revolving crook’s the farm hand sheep dog being shot and the death of Candy. The problem with this form of analysis is that the sentiment is predicated upon how the author linguistically describes the scene. This is apparent as the climatic end scene where George shoots his best friend is not indicated by a large negative score as the scene involves George trying to make Lennie feel at ease by painting a picture about a better life where the owned their own land.

<p align="center">
  <img width="956" height="626" src="/Images_/image3.PNG">
</p>

### Pairwise correlation.
The figure below represents the pairwise correlation between co-occurring words throughout the entire book. This metric differs from the bigram count as it quantifies how often word pairs appear together relative to how often they appear separately. Both community detection and centrality measures where implemented on the network in order to identify clustered sub groups of relevant words and to also highlight the most important topical words. Both the Louvain and Walktrap algorithms were implemented in this project. The Louvain algorithm returned a higher modularity value relative to Walktrap. However, as this algorithm is based on modularity maximization it has the tendency to force smaller communities into larger communities thus losing the semantic definition of smaller sub groups of words. Despite this flaw it was chosen over Walktrap as it gave a higher modularity and allowed for a full evaluation of each community. The centrality measures used for this report were betweenness and degree centrality. Both metrics are intuitive and easy to understand the betweenness of a node refers to the number of shortest paths that pass through it. While the degree centrality is the total number of both in and out degree of a specific node. Both algorithms return similar results and do an excellent job at highlight the important bridges in the graph. Other metrics such as eccentricity, intra cluster density and clique analysis were also considered however I felt as if the community subgraph gave enough detail and the eccentricity/intra density give information about the community structure but not about the content or the relationships of the words that the networks represent. The color and size of each node represents the community it belongs to and it’s centrality score. This method does summarize certain aspects of the book such as objects, places and sub characters however it lacks coherence and structure as the correlation between singular word pairs cannot encapsulate the information of the sentences paragraphs and chapters.

#### Community Detction.
Waltrap is a hierarchical clustering algorithm. It is predicated upon the idea that short distance random walks tend to stay in the same community. Starting from a totally non-clustered partition, the distances between all adjacent nodes are computed. Then, two adjacent communities are chosen, and merged together to form a new one and the distances between communities are updated. This step is repeated N???1 times.

*Louvain* is a greedy optimization method that attempts to optimize the “modularity” of a partition of the network . The algorithm is performed in two steps. First, the method looks for “small” communities by optimizing modularity locally. Second, it aggregates nodes belonging to the same community and builds a new network whose nodes are the communities. These steps are repeated iteratively until a maximum of modularity is attained and a hierarchy of communities is produced.

#### Centrality.
The Betweenness Centrality algorithm calculates the shortest path between every pair of nodes in a connected graph. Each node receives a score, based on the number of these shortest paths that pass through the node. Therfore, nodes that most frequently lie on these shortest paths will have a higher betweenness centrality score.

The Degree centrality algorithm, is defined as the number of edges incident upon a node. In the case of a directed network, we usually define two separate measures of degree centrality, namely outdegree and indegree. Accordingly, indegree is a count of the number of edges directed to the node and outdegree is the number of edges that the node directs to others.

<p align="center">
  <img width="940" height="620" src="/Images_/image4.PNG">
</p>

### Named Entity Network.
Due to the frequency of the main characters, objects and places in the novel their pairwise correlation values were negligible. Thus causing them to be absent from the correlation graph. To combat this and obtain a better understanding of their relationships I constructed a new network that only contained these nodes. This graph was created by using named entity extraction to isolate the main characters places and organizations in the novel. Also a few important objects such as Carlson’s gun was manually added. To create the graph a sliding window was passed over the entire text to calculate the number of occurrences each character, object or place made relative to one another inside the window irrespective of their element wise distance. The number of co-occurrences represented the weighted edges in the graph and the nodes represented each word. The size of each node indicates the centrality measures of each node respectively. The graph clearly indicates that George, Lennie, Curly and Soledad are the most important nodes in the graph which makes sense as George and Lennie are the main protagonists while Curly could be viewed as the antagonist and Soledad is where the story takes place. The color of each node indicates it’s parent community. The communities themselves however are fairly broad or isolated and don’t really resemble the true interactions. Despite this one community does isolate Lennie George Carlson, Curly and the dog to the gun which does replicate the storyline.

<p align="center">
  <img width="909" height="875" src="/Images_/image5.PNG">
</p>

## Visualization of Texts Polysingularity.
In this section the algorithm inspired by Dmitry Paranyushkin’s 2012 paper was implemented on the novel. The book was broken down into three subsections i.e

<p align="center">
  <img width="938" height="155" src="/Images_/image6.PNG">
</p>

Each subsection was then passed through the text summarization algorithm and the most important one hundred sentences were extracted. The sliding window was then applied to this newly summarized text and an edge list representing the weighted co-occurrences of each words was produced. The centrality and community of each word was also calculated using betweeness and Louvain respectively. Each subsection was individually plotted where the color of each node represents the community they belong to and the size of node indicates it’s centrality within the network. The text label of each node could not be displayed on the large graph as it was too confusing to visualize. In each subsection a total of 9 communities were detected using the Louvain algorithm each of these communities were extracted from the graph and plotted individually with the centrality and labels present. Each community represents a cluster of words from the book, examining each cluster gives an indication on how the characters are interacting with their enviorment. Altough other clusters do not provide any relevant information about the story at all. Unfortuantly to intepret each cluster you really would have had read the book previous. Despite this some of the clusters such as community eight in the final subsection details the end scene of the novel where George shoots Lennie. Also other communties describe the sub characters like Curly and his wife or how the book treats crook the black workhand.

<p align="center">
  <img width="883" height="547" src="/Images_/image7.PNG">
</p>

<p align="center">
  <img width="901" height="589" src="/Images_/image8.PNG">
</p>

<p align="center">
  <img width="922" height="569" src="/Images_/image9.PNG">
</p>

<p align="center">
  <img width="917" height="572" src="/Images_/image10.PNG">
</p>
<p align="center">
  <img width="922" height="569" src="/Images_/image11.PNG">
</p>

<p align="center">
  <img width="917" height="572" src="/Images_/image12.PNG">
</p>
