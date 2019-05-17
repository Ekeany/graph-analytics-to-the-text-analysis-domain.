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

