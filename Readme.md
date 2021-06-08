# Monte-Carlo simulation to estimate the cost of a complete Panini sticker album

## Background
It is now almost a tradition that with each new football cup, a new collection of Panini stickers is available. The Panini sticker album of the UEFA Euro 2020
contains 678 stickers, where the stickers can be bought in packs of 5 stickers. It has been shown [1] that the stickers are uniformly distributed and that there is no planned shortage of some stickers.

For collectors, the question arises of how much they have to spend to fill the complete album. Furthermore, the influence of swapping stickers is a very interesting question. 

Here, I present the analysis of some Monte-Carlo simulations in order to answer these questions.


## Assumptions
- The Panini sticker album contains 678 stickers
- A pack of Panini stickers costs 1.1 CHF and contains 5 stickers
- The stickers are distributed uniformly. This means, a pack might contain duplicates.

# Results

## No swapping
The first analysis assumes a person trying to complete the album without swapping stickers. This situation leads to the analytical solution for the expectation of the number of required packets to fill the album [1, 2, 3].

```math
{N \choose k} \sum_{i=1}^{N} (-1)^{i+1} \dfrac{{N \choose i}}{{N \choose k} - {N-i \choose k} }
```
where `N =  # of sticker in the album`, `k = # of sticker in one pack`.

The Monte-Carlo simulation can be found in Panini_MonteCarlo.ipny. The simulation works a follows:

1) Initialize the album as an array of zeros with the length = # of sticker in the album
2) Repeat the following steps until the album array does not contain any zeros entries anymore
	2.1) Generate a pack of five uniformly, randomly distributed stickers 
	2.2) For each sticker in the pack, increase the entry with the sticker ID in the album array by one.

This simulation is the run for 10000 times. 

### Amount of packs to buy to fill the album
![No_of_Packs](img/no_swapping/no_of_packs.png)

|Probability | 10% | 20% | 30% | 40% | 50% | 
| --- | --- | --- | --- | --- | --- |
|# Packs to buy | < 770 | < 818 | < 859 | < 594 | < 933 |
|  | < 1193 | < 1088 | < 1025 | > 976 |  |

The median is at 933 packs. This means that 50% of the simulations needed more than 933 and 50% needed less than 933 packs to fill the album. In other words, from the table one can see that the "lucky" 10% need less than 770 packs to 
fill the album. However, there is an equal probability that one has to buy more than 1193 packs to complete the album.

### Amount of duplicates when completing the album

![No_of_Duplicates](img/no_swapping/no_of_duplicates.png)

|Probability | 10% | 20% | 30% | 40% | 50% | 
| --- | --- | --- | --- | --- | --- |
|# of duplicates | < 3172 | < 3412 | < 3617 | < 3792 | < 3987 |
| | < 5287 | < 4762 | < 4447 | > 4202 |  |

If one does not swap any stickers, the median of the amount of duplicated stickers is 3987. 

** In conclusion, it is a very expensive strategy to fill the album without swapping stickers**

## With swapping

[Todo]



## References
[1] https://www.unige.ch/math/folks/velenik/Vulg/Paninimania.pdf

[2] Adler, Ilan and Ross, Sheldon M.:The  coupon  subset  collection  problem, J. Appl. Probab.38 (2001), no. 3, 737–746.

[3] Stadje, Wolfgang:The  collector’s  problem  with  group  drawings., Adv. in Appl. Probab. 22(1990), no. 4, 866–882