---
layout: post
title: The curious case of T. melophagium in my kitchen
subtitle: Whilst many turned to baking and homebrewing, I turned to another single celled Eukaryote to keep me entertained.
gh-repo: goldrieve
cover-img: /assets/img/Montage of Stack.jpg
thumbnail-img: /assets/img/run.png
share-img: /assets/img/IMG_3396.png
gh-badge: [star, follow]
tags: [genome sequencing]
comments: true
---

## Motivation

As with many folks during the long dark winter months, I needed something to keep me busy. As part of my PhD, I have had the opportunity to sequence a few genomes. Each time it has taken weeks or months between DNA and data. To circumnavigate this, I trialled Oxford Nanopore's miniature genome sequencer which plugs right into your laptop and gives you super long reads! 

In the Matthew's lab, we work on a broad diversity of the protozoan genus, _Trypanosoma_. _T. melophagium_ is a fascinating example of a _Trypanosoma_ which, in contrast to the more infamous _T. brucei_, is non-pathogenic. _T. melophagium_ can be found in temperate regions where pesticide has not been widely used, such as the barren and desolate isles of St. Kilda, off of the Scottish coast. _T. melophagium_ is transmitted from host to host (_Ovinus_) via the sheep ked. It is supposedly closely related to another _Trypanosoma_, _T. theileri_ which can be found in similar climates but is transmitted between bovids via tabanids.  

Interest has grown around these trypanosomes as researchers in Edinburgh, some from the Matthews lab,  have begun a study using _T. melophagium_ and _T. theileri_ as a [vaccine vechicle](https://roslintech.com/roslin-technologies-building-breakthrough-vaccine-vehicle-for-sheep-and-goats-using-trypanosomes/).  

_T. theileri_ has had its [genome sequenced](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5737535/) which revealed an alternative survival technique in the mammalian bloodstream, compared to _T. brucei_. 

_T. melophagium_ represented an exciting opportunity to test out the minION sequencer whilst providing a fascinating study to identify the genomic basis of host/ vector specificity in two closely related _Trypanosomes_.  

## Data acquisition

High molecular weight DNA was extracted and loaded onto the minION. The flow cell happily chugged away for ~10 hours and produced ~30x coverage of the genome. It wasn't a spectacular run but I was happy with my first solo minION run! 30x coverage would do fine for creating a scaffold assembly. Especially with a few miniature whale reads (max read length = 249,891). I also generated ~100x coverage with BGI's DNBseq.

![Sequencer](/assets/img/IMG_3396.png)

## Initial data assessment

This project also provided my first opportunity to supervise a project. I entailed the help of a final year honours student who started as a near novice to the command line and bioinformatics. Within a couple of weeks, she was swiftly navigating the command line like the high seas and it was time to sink her teeth into the data. 

Firstly, we wanted to check the predicted genome size and heterozygosity with an assembly independent tool. We selected a k-mer counting based approach of [Jellyfish](https://github.com/gmarcais/Jellyfish)/ [Genomscope](http://qb.cshl.edu/genomescope/). We chucked the _T. melophagium_ and _T. theileri_ short reads at it and to our surprise, the supposedly closely related _T. theileri_ genome was 5.4Mb larger than _T. melophagium_! A large proportion of this variation was precited to arise from repeats in _T. theileri_. Looking at phylogenetic trees, _T. grayi_ is the next closest relative to _T. melophagium_ and has a genome ~21Mb. Therefore, unless both _T. theileri_ and _T. grayi_ separately underwent genome loss, _T. theileri_ appears to have expanded its genome. 

With our interest truly peaked, we proceeded to genome assembly.  

## Genome assembly

After scanning recent papers which assembled minION data with short reads to polish, we narrowed down our pipeline to a combination of [redbean](https://github.com/ruanjue/wtdbg2) to generate a raw assembly and a combination of [racon](https://github.com/isovic/racon), [medaka](https://github.com/nanoporetech/medaka) and [pilon](https://github.com/broadinstitute/pilon) which used the long and/or and short reads as inputs. After each round of polishing [BUSCO](https://busco.ezlab.org/busco_userguide.html) and scaffold stats were calculated.  Our final round of polishing produced a 66 contig assembly which hit a BUSCO score of 100% complete and an N50 of 505,851 🎉 

## Hello host/vector specific genes, my old friends

With a decent draft _T. melophagium_ genome to add to the ~40 [TriTrypdDB](https://tritrypdb.org/tritrypdb/app) genomes, we began clustering orthologous proteins with [Orthofinder](https://github.com/davidemms/OrthoFinder). 

Where has that 5.4Mb come from!! Some tantalisingly low hanging fruit jumped out, such as the absence of a surface protein family in _T. melophagium_ and hugely expanded surface protein families in _T. theileri_.  

And that’s all the progress so far, stay tuned!
