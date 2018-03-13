# PyRate Tutorial \#4
#### Daniele Silvestro – Jan 2018
***
Useful links:  
[PyRate code](https://github.com/dsilvestro/PyRate)  
[Paleobiology Database](https://paleobiodb.org)  
***

# Multivariate Birth-Death models (this tutorial is work in progress)

The MBD model allow the estimation of speciation and extinction rates as a function of multiple time-continuous variables [(Lehtonen, Silvestro et al. 2017)](https://www.nature.com/articles/s41598-017-05263-7). The model assumes linear or exponential functions linking the temporal variation of birth-death rates with changes in one or more variables.
Under the MBD model a correlation parameter is estimated for each variable (for speciation and extinction).

A Horseshoe prior algorithm (more details provided [here)](https://www.nature.com/articles/s41598-017-05263-7) is used to shrink around zero the correlation parameters, thus reducing the risk of overparameterization and the need for explicit model testing. 

The MBD model is implemented in the program `PyRateMBD.py` and requires as main input file a [table with estimated speciation and extinction times](https://github.com/dsilvestro/PyRate/blob/master/tutorials/pyrate_tutorial_2.md#generate-input-file-for-pyratecontinuous). It additionally requires a set of predictors provided as separate files in a single directory.
Each predictor should be provided as a tab-separated table with a header and two columns for time before present and predictor values, e.g.

time | predictor
----- | -------
0	| 0.06
1	| 0.0665
2	| 0.073
3	| 0.0795
4	| 0.086

Example files are available [here](https://github.com/dsilvestro/PyRate/tree/master/example_files/predictors_MBDmodel).

To launch an MBD analysis, you must provide the input file and the path to all predictor files:

`./PyRateMBD.py -d /example_files/Ferns_SE.txt -var /example_files/predictors_MBDmodel -m 1`

where `-m 1` specifies the type of correlation model, the options being `-m 0` for linear correlations and `-m 1` for exponential correlations. 

Other available options are:  
`-out outname` add a string to output file names   
`-rmDD 1` remove self-diversity dependence  
`-T 23` truncate at max time  
`plot <logfile>` plot marginal rates through time as predicted by the MBD model  

![Example RTT](https://github.com/dsilvestro/PyRate/blob/master/example_files/plots/Ferns_MBD_short_run.png)


