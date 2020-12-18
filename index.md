# Signed Networks in Social Media

Related paper : J. Leskovec, D. Huttenlocher, and J. Kleinberg, ‘Signed networks in social media’, in Proceedings of the 28th international conference on Human factors in computing systems

## Structure in social media, *birds of a feather...* : 
Most of the current popular social networks only showcase positive links. Think of Facebook, Instagram, Twitter, where one can like, befriend, follow, etc., but never actually "dislike". In real life, though, relationships can be a little more complex. People can dislike each other, leading to some form of *distance*, not only on a personal level but also on a group level. 

The balance between positive and negative links may both play a role in the overall structure of a network. More specifically, negative relationships may split the overall network. Think of a practical example: a group of 10 persons, say `group A`, may share something in common, such as hobbies, interests, way of thinking, etc. They become friends, and thus have `positive edges` between them. On the other hand, another group of friends, say `group B` think differently, and highly dislike `group A`, and thus have `negative edges` towards `group A`. This effectively separates the network into two, as you are less likely to be friend with someone of the other group if your group dislike their group overall. For the sake of the argument, although Twitter, Facebook, etc. does not allow to create negative links, groups with different views are still likely to be separated, for example due to political views, reflecting both their background (geographical as well as classical) and real life social network.

## Dataset 
Some social medias, though, allow the formation of negative links. In our case, we have three datasets coming from [Stanford](https://snap.stanford.edu/data/), collected 2010. These are three social networks where negative edge take different forms: 
 
1. The first one is from [Epinions](https://snap.stanford.edu/data/soc-sign-epinions.html) , where users can create consumer review of products. The basis of links are as follows : any given user can `trust`, or `distrust` another, thus creating a `positive` or `negative edge`. The trust relationships form the `Web of Trust` which, combined with the actual ratings tailor the reviews shown to any given user based on his circle. _Interestingly, Epinions is now **dead**. Here's an [interesting read](https://www.forbes.com/sites/ericgoldman/2014/03/12/epinions-the-path-breaking-website-is-dead-some-lessons-it-taught-us/?sh=3e9d9f5967ad)._

2. The second one is from [Slashdot](https://snap.stanford.edu/data/soc-sign-Slashdot090221.html), a technology-related news website. The particularity is that the news are user-submitted and editor-evaluated. On top of that, users can tag each other as `friend` or `foe`, which serve as the basis for our `positive` and `negative edges`.

3. The last one is from [Wikipedia](https://snap.stanford.edu/data/wiki-Elec.html), more specifically Wikipedia election data. Some Wikipedia users can be elected to become administrator, granting them additional rights and access. A user can be nominated for election through a Request for Adminship (RfA), and a public voting ensues. The sign of the edge directly relates to the vote casted on a given election. Given the nature of this dataset, there are many _one-way_ edges, in the sense that since one must be nominated for election to receive votes, many edges are not reciprocated. 

## Sociology ?

<img src="https://raw.githubusercontent.com/richieYT-wan/ADA-p4-data-story/main/figs/troll.png" width="350" />

Now of course, anybody can vote the way they can. There have been countless accounts of trolls on the internet, and you should be careful to _not feed them_. Nonetheless, social theories still apply and we may expect trolls to be outliers rather than the norm. In the context of our dataset, trolls may simply refer to people who give negative votes, or links, to everybody, with no apparent reason other. Despite that, some social theories still apply. For example, the theory of balance, proposed by [F. Harary and D. Cartwright](https://en.wikipedia.org/wiki/Social_balance_theory), which considers the way triangles (relationships between 3 nodes) can be signed. This theory suggests that the most common types of triangles are three mutual friends (3 `positive edges`), or two friends with a common enemy (two `negative` and one `positive edges`). Overall, this theory combined with the social nature of humans, which tend to form communities and connect (_as opposed to Trolls who only want despair!_), results in an overall trend to have higher frequencies of `positive edges` vs `negative edges` in a given social network.

You can take our word for it, or look at the statistics recaps below for each of the 3 datasets:

|        |         Epinions |         Slashdot |   Wikipedia |
|:-------|-----------------:|-----------------:|------------:|
| Nodes  | 131828           |  82140           |      7118   |
| Edges  | 841372           | 549202           |    103747   |
| +edge  |     85.3         |     77.4         |        78.8 |
| -edge  |     14.7         |     22.6         |        21.2 |
| Triads |      13317672    |      1508105     |    790532   |

	13317672	1508105	790532


