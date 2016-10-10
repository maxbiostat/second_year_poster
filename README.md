# Second Year PhD Poster
This is the poster I presented at the [Graduate School Poster Day 2016](http://www.iad.ed.ac.uk/bio/pgconference.htm) at the Institute of Evolutionary Biology, School of Biological Sciences, University of Edinburgh, UK.

Here I present the work I have done on Ebola phylodynamics, which has been partially published in  [Dudas et al. (2016)](http://biorxiv.org/content/early/2016/09/02/071779.1) and [Diehl et al. (2016)](). 

Click to see the [poster](https://github.com/maxbiostat/second_year_poster/blob/master/carvalho_2016_poster_edinburgh.pdf).

## Uncovering factors associated with outbreak size

One of the questions [Dudas et al. (2016)](http://biorxiv.org/content/early/2016/09/02/071779.1) posed was what climatic and socio-economical factors were associated with outbreak size, i.e, total number of cases, in a given location. To answer that, we employed a negative binomial GLM to model outbreak sizes as dependent variable, using several attributes measured at the location level as covariates. To achieve a parsimonious model specification, we employed stochastic search variable selection (SSVS), in a very similar way to the one suggested by [George & McCulloch (1993)](http://amstat.tandfonline.com/doi/abs/10.1080/01621459.1993.10476353)  and later explored by [Lemey et al. 2009](http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1000520).
SSVS is convenient because it allows us to calculate [Bayes factors](https://en.wikipedia.org/wiki/Bayes_factor) (BF) analytically for each covariate/predictor and hence determine its "significance".

<img src="https://github.com/maxbiostat/second_year_poster/blob/master/images/case-count_coefficients.png" alt="coefficients" width="800" height="200" />

**Predictors of EVD outbreak size in West Africa**.
Here I report predictors (covariates) with Bayes factor support greater than 3.
Notice the estimated coefficients for temperature seasonality (`TempSS`) and travel times (`tt50K` and `tt100K`) are negative, suggesting that the more seasonal the climate and the more far away from urban centres, the fewer cases a region tended to have. Taken together, these results suggest an important role of urbanicity on the epidemic potential of EVD. 

## Association between the GP-A82V mutation and disease severity
[Diehl et al. (2016)]() presented experimental evidence that a mutation from Alanine to Valine in the Glycoprotein (82nd position) conferred increased infectivity specific to human cells.
The question was then if the mutation also had an impact on disease severity.

To address this, we collected data for ``236`` patients regarding

* which `genotype`, A or V the virus sampled had;
* the `Ct` value obtained during sequencing, inversely correlated with `viral load`;
* the `outcome`, i.e., whether the patient died or survived.

With this information in hand, we then fitted a binomial [generalised linear model](https://en.wikipedia.org/wiki/Generalized_linear_model) using `outcome` as a response variable and `genotype` and `Ct` as covariates. Details of data transformation, etc can be found in the STAR methods section of [Diehl et al. (2016)]().

<img src="https://github.com/maxbiostat/second_year_poster/blob/master/images/predicted_fatality_rates.png" alt="fatality_rates" width="600" height="600" />

**Predicted fatality rates per genotype** We transformed `Ct` to reflect viral load. Prediction curves from the fitted binomial GLM. Notice the considerable uncertainty in the predictions, evidenced by the overlap between the 95% confidence bands for each genotype.

Here is a phylogeny onto which I mapped viral load and outcome.
For viral load I used a Brownian motion continuous diffusion model ([Lemey et al. 2010](http://mbe.oxfordjournals.org/content/27/8/1877)) and I modelled outcome as discrete trait using a [continuous-time Markov chain](https://en.wikipedia.org/wiki/Markov_chain#Continuous-time_Markov_chain) (CTMC) ([Lemey et al. 2009](http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1000520)).

<img src="https://github.com/maxbiostat/second_year_poster/blob/master/images/EVD_traits_tree.png" alt="traits_tree" width="800" height="600" />

**Annotated phylogeny of 236 EBOV sequences from Guinea**
Maximum clade credibility (MCC) tree obtained from a posterior distribution approximated with [BEAST](http://beast.bio.ed.ac.uk/). Clearly, branches with lower viral load (transformed `Ct`) have higher probability of leading to a surviving tip.

More details and a cool animation showing the spread of A82V in West Africa can be found in the [public repository](https://github.com/maxbiostat/diehl_ebola_cell_2016) for the paper.

## Combining phylogenetic and epidemiological data

## Future steps
