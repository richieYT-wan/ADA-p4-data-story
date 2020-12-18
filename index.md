# Signed Networks in Social Media

Related paper : J. Leskovec, D. Huttenlocher, and J. Kleinberg, ‘Signed networks in social media’, in Proceedings of the 28th international conference on Human factors in computing systems

## Structure in social media, [*birds of a feather...*](https://github.com/richieYT-wan/ADA-p4-data-story/blob/gh-pages/index.md#homophily--flock-together)

Now you may wonder what social media has to do with birds, right? Buckle

Most of the current popular social networks only showcase positive links. Think of Facebook, Instagram, Twitter, where one can like, befriend, follow, etc., but never actually "dislike". In real life, though, relationships can be a little more complex. People can dislike each other, leading to some form of *distance*, not only on a personal level but also on a group level. 

The balance between positive and negative links may both play a role in the overall structure of a network. More specifically, negative relationships may split the overall network. Think of a practical example: a group of 10 persons, say `group A`, may share something in common, such as hobbies, interests, way of thinking, etc. They become friends, and thus have `positive edges` between them. On the other hand, another group of friends, say `group B` think differently, and highly dislike `group A`, and thus have `negative edges` towards `group A`. This effectively separates the network into two, as you are less likely to be friend with someone of the other group if your group dislike their group overall. For the sake of the argument, although Twitter, Facebook, etc. does not allow to create negative links, groups with different views are still likely to be separated, for example due to political views, reflecting both their background (geographical as well as classical) and real life social network.

## Dataset 
Some social medias, though, allow the formation of negative links. In our case, we have three datasets coming from [Stanford](https://snap.stanford.edu/data/), collected 2010. These are three social networks where negative edge take different forms: 
 
1. The first one is from [Epinions](https://snap.stanford.edu/data/soc-sign-epinions.html) , where users can create consumer review of products. The basis of links are as follows : any given user can `trust`, or `distrust` another, thus creating a `positive` or `negative edge`. The trust relationships form the `Web of Trust` which, combined with the actual ratings tailor the reviews shown to any given user based on his circle. _Interestingly, Epinions is now **dead**. Here's an [interesting read](https://www.forbes.com/sites/ericgoldman/2014/03/12/epinions-the-path-breaking-website-is-dead-some-lessons-it-taught-us/?sh=3e9d9f5967ad)._

2. The second one is from [Slashdot](https://snap.stanford.edu/data/soc-sign-Slashdot090221.html), a technology-related news website. The particularity is that the news are user-submitted and editor-evaluated. On top of that, users can tag each other as `friend` or `foe`, which serve as the basis for our `positive` and `negative edges`.

3. The last one is from [Wikipedia](https://snap.stanford.edu/data/wiki-Elec.html), more specifically Wikipedia election data. Some Wikipedia users can be elected to become administrator, granting them additional rights and access. A user can be nominated for election through a Request for Adminship (RfA), and a public voting ensues. The sign of the edge directly relates to the vote casted on a given election. Given the nature of this dataset, there are many _one-way_ edges, in the sense that since one must be nominated for election to receive votes, many edges are not reciprocated. 

All datasets are roughly in the same format, i.e. an edgelist with columns `"FromNodeId", "ToNodeId", "Sign"` which represents all the connections in their respective network.


## Sociology : putting the **social** in social networks

<p align="center">
<img src="https://raw.githubusercontent.com/richieYT-wan/ADA-p4-data-story/main/figs/troll.png" width="350" />
</p>

Now of course, anybody can vote the way they can. There have been countless accounts of trolls on the internet, and you should be careful to _not feed them_. Nonetheless, social theories still apply and we may expect trolls to be outliers rather than the norm. In the context of our dataset, trolls may simply refer to people who give negative votes, or links, to everybody, with no apparent reason other. Despite that, some social theories still apply. For example, the theory of balance, proposed by [F. Harary and D. Cartwright](https://en.wikipedia.org/wiki/Social_balance_theory), which considers the way triangles (relationships between 3 nodes) can be signed. This theory suggests that the most common types of triangles are three mutual friends (3 `positive edges`), or two friends with a common enemy (two `negative` and one `positive edges`).

Overall, this theory combined with the social nature of humans, which tend to form communities and connect (_as opposed to Trolls who only want despair!_), results in a trend to have higher frequencies of `positive edges` rather than `negative edges` in a given social network.

**You can take our word for it!**
_Or you should probably take a glance at the statistics recaps computed for each of the 3 datasets below_ :


|        | Epinions |  Slashdot | Wikipedia |
|:-------|---------:|----------:|----------:|
| Nodes  | 131828   |  82140    |    7118   |
| Edges  | 841372   | 549202    |  103747   |
| +edge  |     85.3 |    77.4   |      78.8 |
| -edge  |     14.7 |    22.6   |      21.2 |
| Triads | 13317672 |  1508105  |  790532   |


`+edge` and `-edge` show the proportion of positive and negative edges within the network. As mentioned above, our networks are all made up majoritarily of `+edges`, with over 77% positive edges. 

But now then, how connected is our network? If we are naïve, for starter, we can take a look at the average number of edges per node :

|Avg. per node  | Epinions |  Slashdot | Wikipedia |
|:--------------|---------:|----------:|----------:|
|Avg. # of edges| 6.38     |  6.69     |   14.57   |
|Avg. % of +edge| 5.44     | 5.18      |  11.48    |
|Avg. % of -edge| 0.94     |   1.52    |  3.089    |

The Wikipedia dataset has more than twice as many average number of edges per node. This is due to the fact that edges can't be formed at will, since they are the results of voting on someone nominated for an election. On the other hand, Epinions and Slashdot have similar average number of edges per node, given that any user can form an edge towards any other user, though Epinions has a bigger share of positive links than Slashdot. 

But averages don't tell us much about the actual structure of the networks. For example, everyone may have on average 6 to more connections, with a very few subset that are **sparsely** connected (_think of a normal distribution with minimal standard deviation!_). Or, on the other hand, there may be a subset of users with an overwhelmingly large amount of connections (_surely, these must be very popular_), with another subset of users who have close to no edges such as _casual users_.

With a slightly less naïve approach, we look for the node degree distributions for each network. The node degree is simply the number of edges of a node, or more simply the number of connections a given node has. We decided to also show, on the left, what it looks like if we take the `sign` of `edges` as a parameter. 

<p align="center">
<img src="https://raw.githubusercontent.com/richieYT-wan/ADA-p4-data-story/main/figs/epi.png" width="650" />
</p>

<p align="center">
<img src="https://raw.githubusercontent.com/richieYT-wan/ADA-p4-data-story/main/figs/slash.png" width="650" />
</p>

<p align="center">
<img src="https://raw.githubusercontent.com/richieYT-wan/ADA-p4-data-story/main/figs/wiki.png" width="650" />
</p>

Without counting the `sign`, we see that the degree distribution follow a power law. It becomes evident that most users have very few connections, suggesting the networks may be sparsely connected. We verify this by looking at the checking the density of the network which are all below 5e-3. By taking the sign into account for calculating the degree, we see that the distribution is mostly skewed towards the right, showcasing once again the major proportion of `positive edges`. 

|                | Epinions |  Slashdot | Wikipedia |
|:---------------|---------:|----------:|----------:|
|Density         | 4.86 e-5 |  8.14 e-5 | 2.05e-3   |
|Max Deg (Signed)| 3142     |  2495     | 695       |
|Max Deg. (Not)  | 3622     |  2557     | 1167      |


## Homophily, *... flock together!*

Given the size of Epinions and the nature of the Wikipedia dataset, we decided to focus on Slashdot for this part. Homophily refers to the 
_Birds of a feather flock together_, test


<p align="center">
<img src="https://raw.githubusercontent.com/richieYT-wan/ADA-p4-data-story/main/figs/reciprocated_net.png" width="650" />
</p>
Taken from _Ciotti, Valerio. Positive and negative connections and homophily in complex networks. Diss. Queen Mary University of London, 2018._

