---
layout: post
title: The curious case of _T. melophagium_ in my kitchen
subtitle: Whilst many turned to baking and homebrewing, I turned to another single celled Eukaryote to keep me entertained.
gh-repo: goldrieve
cover-img: /assets/img/Montage of Stack.jpg
thumbnail-img: /assets/img/IMG_3396.png
share-img: /assets/img/IMG_3396.png
gh-badge: [star, follow]
tags: [genome sequencing]
comments: true
---

## Motivation

As with many folk during the long dark winter months, I needed something to keep me busy and the thought of sequencing a genome on my kitchen table was enough to get me up in the morning. As part of my PhD I have been working with Oxford Nanopore's miniature genome sequencer and with the idea of using it in resource poor settings, I decided to give it a trial run in the barren wastelands of Gorgie, Edinburgh.  

In the Matthew's lab, we work on a broad diversity of the ancient protozoan genus, _Trypanosoma_. _T. melophagium_ is a fascinating example of a _Trypanosoma_ which in contrast to the more infamous species, is non-pathogenic. _T. melophagium_ can be found in temperate regions where pesticide has not be widely used, such as the barren and desolate isles of St. Kilda, off of the Scottish coast. _T. melophagium_ is transmitted from host to host (_Ovinus_) via the sheep ked. It is supposedly closely rleated to another _Trypanosoma_, _T. theileri_ which can be found in similar climates but is transmitted between bovids via tabanids.  
Interest has grown around these trypanosomes as researchers in the Matthews's lab, and futher afield, have begun a study using _T. melophagium_ and _T. theileri_ as a [vaccine vechicle](https://roslintech.com/roslin-technologies-building-breakthrough-vaccine-vehicle-for-sheep-and-goats-using-trypanosomes/).  

_T. theileri_ has had its [genome sequenced](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5737535/) which revealed an alterative survival technique in the mammlaian bloodstream, in comparsion to _T. brucei_. _T. theileri_ and _T. melophagium_ are thought to be closely related, however, they have distinct vectors/ hosts.  

_T. melophagium_ represented an exciting opportunity to test out the minION sequencer in resource poor settings, i.e my kitchen table, as access to the lab was severly restricted during the lockdown, whilst providing a fascinating study to identify the genomic basis of host/ vector specificity in two closely related _Trypanosomes_.  

## Data acquisition

At this point, I have to admit I cheated a bit. Whilst the actual genome was sequenced at my kitchen table, the DNA was extracted in the lab. H&S probbaly frown upon taking your parasites home with you. However, with high molecular weight DNA in tow, I took the minION back to my flat and started the run. The flow cell happily chigged away for ~10 hours and produced around 30x coverage of the ~25Mb genome. It wasn't a spectacular run but I was happy with the output, my second ever minION run! 30x coverage would do fine for creating a scaffold assembly of the genome and to polish that scaffold, I generated ~100x coverage with BGI's DNDseq.

![Sequencer](/assets/img/IMG_3396.png)

## Initial data assessment

This project also provided my first opportunity to supervise! I entailed the help of a final year honours student who started the project as a near novice to the command line/ bioinformatics. Within a couple of weeks she was swiftly navigating the command line like the high seas and time to sink her teeth into the data. Firstly, we wanted to check the predicted genome size and heterozygosity with an assembly independent tool. We selected a k-mer counting based approach of [Jellyfish](https://github.com/gmarcais/Jellyfish)/ [Genomscope](http://qb.cshl.edu/genomescope/). We chucked the _T. melophagium_ and _T. theileri_ short reads at it and to our suprise, the supposdly closely related _T. theileri_ genome was 5.4Mb larger than _T. melophagium_! A large proportion of this variaition was precited to arise from repeats in _T. theileri_. Looking at phylogenetic trees, _T. grayi_ is the next closest relative to _T. melophagium_ and has a genome ~21Mb. Therefore, unless both _T. theileri_ and _T. grayi_ underwent seperategenome loss events, _T. theileri_ appears to have expanded its genome. With our interest truly peaked, we proceeded to genome assembly.  

## Genome assembly

After scanning recent papers which assembled minION data with short reads to polish, we narrowed down our pipeline to a combination of [redbean](https://github.com/ruanjue/wtdbg2) to generate a raw assembly and a combination of [racon](https://github.com/isovic/racon), [medaka](https://github.com/nanoporetech/medaka) and [pilon](https://github.com/broadinstitute/pilon) which used the long and/or and short reads as inputs. After each round of polishing [BUSCO](https://busco.ezlab.org/busco_userguide.html) and scaffold stats were calculated. As each round failed to improve the assembly, we moved onto the next step. Our final round of polishing produced a 66 contig assembly which hit 100% completness according to BUSCO 🎉. 

## Hello host/vector specific genes, my old friend

With a seemingly decent _T. melophagium_ genome to add to the ~40 [TriTrypdDB](https://tritrypdb.org/tritrypdb/app) genomes, we began clustering orthologoues proteins with [Orthofinder](https://github.com/davidemms/OrthoFinder). Where has that 5.4Mb come from!! Some tantilisingly low hanging fruit jumped out, such as the absence of some surface protein families in _T. melophagium_ and hugly expanded surface protein families in _T. theileri_. 

