---
author: justin
comments: true
date: 2016-10-11 19:52:55+00:00
layout: post
link: http://www.justinbagley.org/1058/setting-dna-substitution-models-beast
slug: setting-dna-substitution-models-beast
title: Setting DNA substitution models in BEAST
wordpress_id: 1058
categories:
- Bayesian
- BEAST
- BEAUti
- blog posts
- data analysis
- Molecular evolution
- Software
- XML
tags:
- BEAST
- F81
- gamma
- GTR
- HKY
- invariant sites
- JC69
- K80
- substitution models
- SYM
- Tamura
- TrN
---

[caption id="" align="alignleft" width="139"]![](http://www.justinbagley.org/wp-content/uploads/2016/10/jc-revised.png) JC model of sequence evolution from [TreeThinkers](http://treethinkers.org/jukes-cantor-model-of-dna-substitution/).[/caption]


BEAST (Bayesian Evolutionary Analysis Sampling Trees) software provides a growing set of _clear_ options for specifying evolutionary models of DNA substitution for alignments loaded into the program. However, the set of models that are readily available and "spelled out" in drop-down menus in the BEAUti (Bayesian Evolutionary Analysis Utility) GUI is much smaller compared to the standard set of 11 substitution schemes considered by other software programs for model selection (giving rise to a total of 88 models in [jModelTest](https://github.com/ddarriba/jmodeltest2), or 56 models in [PartitionFinder](http://www.robertlanfear.com/partitionfinder/)). This poses a problem that I have heard several BEAST users bring up in online discussion groups, and that several people have asked me about personally. In this post, I shed some light on this problem and clear up some of the confusion by giving details on how users can easily specify different substitution models for their BEAST runs. 




##### Background: Substitution models in BEAST




I will assume that readers are familiar with [DNA substitution models](https://en.wikipedia.org/wiki/Models_of_DNA_evolution). Also, there are a number of details about how BEAST handles DNA substitution models, which you can learn from the [BEAST2](http://beast2.org) book or the manual, but that I will not cover. For example, by default, BEAST normalizes the rate matrix so that the mean rate is 1.0, and so on. Moving on to the issues...




It seems that many people are having issues with the fact that it's not a simple "one-click" procedure to specify the diverse variety of substitution models that are frequently selected during model selection inference conducted prior to setting up BEAST runs. This is because [BEAST1](http://beast.bio.ed.ac.uk) only gives the _obvious_ options to specify three of the most popular models of DNA substitution: TrN, HKY, and GTR, while BEAST2 versions give users _obvious_ options to specify one of four models: JC69, TrN, HKY, and GTR. Thus other models such as TIM, K80, and F81 can seem cryptic to some users, who will often exclaim in dismay, "Where is the option for model _X???_" or "I don't see how to specify model _Y!!!_" and then post a question about it (that may languish, never to even be directly answered, who knows).




##### **Solving the problem: Learning BEAST functionalities "under your nose"**




The real solution to the above problems is to realize the options available to you, especially that BEAUti actually gives several important options in the Site Model panel that each user must learn to use to tailor the models of evolution for each alignment/partition. These options are located right "under your nose," but I'll show you where they are and how to use them in **Tables 1 and 2 below**, as follows:




**Table 1. Details for setting substitution models in BEAST1 (e.g. v1.8.3).**


<table >
<tbody >
<tr >

<td >**Best-fit substitution model**
</td>

<td >**(Base) Model to select in BEAUti**
</td>

<td >**Additional specifications in BEAUti**
</td>
</tr>
<tr >

<td >JC69
</td>

<td >JC69
</td>

<td >None 
</td>
</tr>
<tr >

<td >TrN
</td>

<td >TN93
</td>

<td >None 
</td>
</tr>
<tr >

<td >TrNef
</td>

<td >TN93
</td>

<td >base Frequencies set to "All Equal"
</td>
</tr>
<tr >

<td >K80 (K2P)
</td>

<td >HKY
</td>

<td >base Frequencies set to "All Equal"
</td>
</tr>
<tr >

<td >F81
</td>

<td >GTR
</td>

<td >turn off operators for all rate   

 parameters
</td>
</tr>
<tr >

<td >HKY
</td>

<td >HKY
</td>

<td >None
</td>
</tr>
<tr >

<td >SYM
</td>

<td >GTR
</td>

<td >base Frequencies set to "All Equal"
</td>
</tr>
<tr >

<td >TIM
</td>

<td >GTR
</td>

<td >


edit XML file by hand so that all other rates are equal to the AG rate



</td>
</tr>
<tr >

<td >TVM
</td>

<td >GTR
</td>

<td >unchecking AG rate operator
</td>
</tr>
<tr >

<td >TVMef
</td>

<td >GTR
</td>

<td >unchecking AG rate operator and setting base Frequencies to "All Equal"
</td>
</tr>
<tr >

<td >GTR
</td>

<td >GTR
</td>

<td >None
</td>
</tr>
</tbody>
</table>


**Table 2. Details for setting substitution models in BEAST2 (e.g. 2.4.0+).**


<table >
<tbody >
<tr >

<td >**Best-fit substitution model**
</td>

<td >**(Base) Model to select in BEAUti 2**
</td>

<td >**Additional specifications in BEAUti 2**
</td>
</tr>
<tr >

<td >JC69
</td>

<td >JC69
</td>

<td >None 
</td>
</tr>
<tr >

<td >TrN
</td>

<td >TN93
</td>

<td >None
</td>
</tr>
<tr >

<td >TrNef
</td>

<td >TN93
</td>

<td >base Frequencies set to "All Equal"
</td>
</tr>
<tr >

<td >K80 (K2P)
</td>

<td >HKY
</td>

<td >base Frequencies set to "All Equal"
</td>
</tr>
<tr >

<td >F81
</td>

<td >GTR
</td>

<td >fix all rate parameters to 1.0 (uncheck the "estimate" box)
</td>
</tr>
<tr >

<td >HKY
</td>

<td >HKY
</td>

<td > None
</td>
</tr>
<tr >

<td >SYM
</td>

<td >GTR
</td>

<td >base Frequencies set to "All Equal"
</td>
</tr>
<tr >

<td >TIM
</td>

<td >GTR
</td>

<td >fix CT and AG rate parameters to 1.0 (uncheck the "estimate" box)
</td>
</tr>
<tr >

<td >TVM
</td>

<td >GTR
</td>

<td >fix the AG rate parameter to 1.0 (uncheck the "estimate" box)
</td>
</tr>
<tr >

<td >TVMef
</td>

<td >GTR
</td>

<td >fix the AG rate parameter to 1.0 (uncheck the "estimate" box), and also set base Frequencies to "All Equal"
</td>
</tr>
<tr >

<td >GTR
</td>

<td >GTR
</td>

<td > None
</td>
</tr>
</tbody>
</table>








I have quickly constructed these tables based on different options available in BEAST versions, my knowledge of the substitution models, and the list of model code for different substitution models on the [BEAST1 website](http://beast.bio.ed.ac.uk/Substitution-model-code) (information for XML format for BEAST1 / earlier versions than present). How can you use the above tables to set a desired site model? Easy. You simply check **Tables 1 and 2 **and for a given model you might want to set (**first column**), the tables tell you which model to select in BEAUti (**second column**) and the modifications, if any, you will need to make to that model or the XML file itself to get the model you want (**third column**). 




**Another way...**




If you would like more detail, you can also draw on other resources available online to do this properly. For example, if you wanted to set the F81 model for a partition of your dataset, you could also search the [substitution model code page](http://beast.bio.ed.ac.uk/Substitution-model-code) mentioned above for "F81". If you did this you would find the following block for BEAST1:



    
    <!-- *** SUBSTITUTION MODEL FOR PARTITION Gene2 *** -->
    <!-- The F81 substitution model (Felsenstein, 1981) -->
    <gtrModel id="F81_Gene2">
    	<frequencies>
    		<frequencyModel dataType="nucleotide">
    			<frequencies>
    				<parameter id="F81_Gene2.frequencies" value="0.25 0.25 0.25 0.25"/>
    			</frequencies>
    		</frequencyModel>
    	</frequencies>
    	<rateAC>
    		<parameter id="F81_Gene2.ac" value="1.0"/>
    	</rateAC>
    	<rateAG>
    		<parameter id="F81_Gene2.ag" value="1.0"/>
    	</rateAG>
    	<rateAT>
    		<parameter id="F81_Gene2.at" value="1.0"/>
    	</rateAT>
    	<rateCG>
    		<parameter id="F81_Gene2.cg" value="1.0"/>
    	</rateCG>
    	<rateGT>
    		<parameter id="F81_Gene2.gt" value="1.0"/>
    	</rateGT>
    </gtrModel>




We can infer from this that the F81 model can be specified in any BEAST version by first specifying the GTR model, and then setting all rates to 1.0 and also setting all base frequencies to be equal "All Equal" (i.e. each equal to 0.25). And you would specify this information in the Site Model panel in BEAUti. You would also need to make sure that the priors were not included for these parameters, since they will be fixed; so you do that by commenting out the rate priors within the XML file. Accordingly, you would also need to delete the rate parameters from the log, because you won't need to log those parameters since you won't be estimating them.




~J




_**Additional Reading**_




**Substitution model basics from Wikipedia: **[substitution model](https://en.wikipedia.org/wiki/Substitution_model), [models of DNA evolution](https://en.wikipedia.org/wiki/Models_of_DNA_evolution)  




**Beast users google group threads:**





	
  * [BEAUti can set 40 models?](https://groups.google.com/forum/#!topic/beast-users/_zCoCTSkWRs)

	
  * [F81 mutation model?](https://groups.google.com/forum/#!topic/beast-users/FqmhFT0UOnU)




**BEAST2 website FAQ:** [link](http://www.beast2.org/wiki/index.php/FAQ#How_to_make_use_of_other_substitution_models_not_given_in_Beauti.3F_Specifically.2C_Jukes-Cantor_model.3F)




**PartitionFinder website: **[PartitionFinder](http://www.robertlanfear.com/partitionfinder/)
