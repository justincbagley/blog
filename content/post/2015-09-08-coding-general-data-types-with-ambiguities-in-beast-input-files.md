---
author: justin
comments: true
date: 2015-09-08 03:07:12+00:00
layout: post
link: http://www.justinbagley.org/1202/coding-general-data-types-with-ambiguities-in-beast-input-files
slug: coding-general-data-types-with-ambiguities-in-beast-input-files
title: Coding general data types with ambiguities in BEAST input files
wordpress_id: 1202
categories:
- BEAST
- blog posts
- Morphological data
tags:
- Alex Pyron
- ambiguity code
- BEAST
- generalDataType
- Mkv model
- morphological data
- total-evidence dating
---

##### The generalDataType Problem

BEAST allows users to specify general data types--formally, tag "generalDataType"--with codes representing ambiguities reflecting multiple character states. People have questions/problems creating and using these general data types, e.g. [here](https://www.biostars.org/p/57815/) and [here](https://groups.google.com/forum/#!topic/beast-users/jQV9RCxEt1Q). The main issues are understanding what general data types are, as well as how to code them in the BEAST XML input file so that BEAST runs without errors.

##### Specifying general data types

To solve the first issue, you should first know that a generalDataType tag can be specified in input files for BEAST v1 or BEAST2. Here, I will discuss what has worked for me using BEAST 1.5.4 or 1.8.2 (latest v1 software distribution). Next, a generalDataType block allows the user to specify discrete morphological, distributional, or DNA characters, while allowing ambiguities between multiple states to be coded with a question mark (?) or another character of choice, so long as the ambiguity character is not included in the set of character state codes specified for the generalDataType.

Second, you need to play with coding generalDataTypes to get a feel for how to implement them. Of course, there are various reasons why you might want to put generalDataType sections into your BEAST input files, and we can think about those as we practice. For example, generalDataTypes can be a useful way of telling BEAST that DNA nucleotides coded as missing data (?'s) or gaps (-'s) in a given DNA alignment could represent any of the four DNA bases, A, C, G, or T. As noted in the relevant [tutorial](http://beast.bio.ed.ac.uk/general-data-type), this is accomplished by placing the following code before the alignments are given in the input file:
    
    <generalDataType id="general">
    	<state code="A"/> <!-- A -->
    	<state code="C"/> <!-- C -->
    	<state code="G"/> <!-- G -->
    	<state code="T"/> <!-- T -->
    	<ambiguity code="-" states="ACGT"/>
    	<ambiguity code="?" states="ACGT"/>
    </generalDataType>
    

Here, as usual, text enclosed by "<!--" and "-->" is commented out, and this text can be added by the user wherever they feel more information or clarification is necessary. Also, once a generalDataType tag is opened, it must be filled with the relevant info and then closed out using "</generalDataType>". As shown in the example, multiple ambiguity codes can be used to represent the same set of characters.

##### Multiple generalDataTypes

If desired, multiple generalDataTypes can be identified and used in the same XML input file. For example, in addition to the code above for DNA base ambiguities, you could also include generalDataType tags for two- and three-state unordered morphological characters that you wanted to include along with DNA sequence data, to conduct a "total-evidence" dating analysis. Setting these once, before the morpho alignment, will allow you to place a Z as an ambiguous character for any number of two- or three-state characters. I will provide code for doing this. However, it is important to note that question marks should be avoided when coding morphological data in this case, because using the same character "?" to indicate missing data as well as ambiguity codes can cause problems, specifically an "invalid state index" error. So, one way to solve this problem is to use another character such as "Z" as the ambiguity code. Thanks to Alex Pyron for [answering his own question](https://code.google.com/p/beast-mcmc/issues/detail?id=275) on this topic, and for providing XML files from his 2011 paper on total-evidence dating using fossils as tip taxa that show how to do this, which are on Dryad ([doi:10.5061/dryad.8120](http://datadryad.org/resource/doi:10.5061/dryad.8120); Pyron, 2011). Here is some code for two- and three-state morpho characters:
    
    <generalDataType id="Morph_2stateUNOrdered">
     <state code="0"/>
     <state code="1"/>
     <ambiguity code="Z" states="01"/>
    </generalDataType>
    
    <generalDataType id="Morph_3stateUNOrdered">
     <state code="0"/>
     <state code="1"/>
     <state code="2"/>
     <ambiguity code="Z" states="012"/>
    </generalDataType>

Last, once generalDataType ids are introduced, it is very important to refer to them throughout the remainder of the XML file. For coding a simple character for ancestral state reconstruction, which gets no site model for example, you should only need to go down to the treeLikelihood section of the XML file and set useAmbiguities="true". However, for characters used during phylogeny reconstruction in BEAST, you will minimally need to refer to your generalDataTypes when coding the corresponding frequencyModel, generalSubstitutionModel, and siteModel, in addition to the tree likelihood part of the code. Examples of this are provided back in the basic [tutorial](http://beast.bio.ed.ac.uk/general-data-type), as well as example XML files. However, for morphological data, which you will need to give the Lewis (2001) Mkv model in BEAST, you will need to specify individual "patterns" and "treeLikelihood" sections, for each set of morphological generalDataTypes, like this:
    
     <patterns id="morph_2state_UNOrd.patterns">
     <alignment idref="alignment_2stateUNOrdered"/>
     </patterns>
     
     <patterns id="morph_3state_Ord.patterns">
     <alignment idref="alignment_3stateOrdered"/>
     </patterns>
    .
    .
    .
    <treeLikelihood id="morph.2state_UNOrd.treeLikelihood" useAmbiguities="true">
     <patterns idref="morph_2state_UNOrd.patterns"/>
     <treeModel idref="treeModel"/>
     <siteModel idref="morph_2state_UNOrd.siteModel"/>
     <discretizedBranchRates idref="branchRates"/>
     </treeLikelihood>
    <treeLikelihood id="morph_3state_Ord.treeLikelihood" useAmbiguities="true">
    <patterns idref="morph_3state_Ord.patterns"/>
    <treeModel idref="treeModel"/>
    <siteModel idref="morph_3state_Ord.siteModel"/>
    <discretizedBranchRates idref="branchRates"/>
    </treeLikelihood>

And this is in addition to frequencyModel and site and substitution model (Mkv) code sandwiched in between these, somewhere between ". . ."

[More Later]

~J

**References**

Lewis, P.O. 2001. A likelihood approach to estimating phylogeny from discrete morphological character data. Syst. Biol. 50, 913-925.

Pyron, R.A., 2011. Divergence time estimation using fossils as terminal taxa and the origins of Lissamphibia. Syst. Biol. 60(4), 466-481.
