# Genome annotation workflow with Helixer

This workflow allows you to annotate a genome with Helixer and evaluate the quality of the annotation using BUSCO and Genome Annotation statistics. GFFRead is also used to predict protein sequences derived from this annotation, and BUSCO and OMArk are used to assess proteome quality. 


Helixer is an annotation software with a new and different approach: it performs evidence-free predictions (no need for RNASeq data or sequence aligments), using Graphics Processing Unit (GPU), with a much faster execution time. The annotation is based on the development and use of a cross-species deep learning model. The software is used to configure and train models for ab initio prediction of gene structure. In other words, it identifies the base pairs in a genome that belong to the UTR/CDS/Intron genes.

To assess the quality of the proteome, we will use the GFFRead tool to extract the predicted protein sequences from the annotation (i.e. the Helixer annotation).

To assess the quality of the annotation, we will use different tools:
- Genome Annotation Statistics: is a program designed to analyze and provide statistics on genomic annotations. This software performs its analyses from a GFF3 file.
- BUSCO (Benchmarking Universal Single-Copy Orthologs):  is a tool allowing to evaluate the quality of a genome assembly or of a genome annotation. By comparing genomes from various more or less related species, the authors determined sets of ortholog genes that are present in single copy in (almost) all the species of a clade (Bacteria, Fungi, Plants, Insects, Mammals, …). Most of these genes are essential for the organism to live, and are expected to be found in any newly sequenced and annotated genome from the corresponding clade. Using this data, BUSCO is able to evaluate the proportion of these essential genes (also named BUSCOs) found in a set of (predicted) transcript or protein sequences. This is a good evaluation of the “completeness” of the annotation.
- OMArk: is proteome quality assessment software. It provides measures of proteome completeness, characterises the consistency of all protein-coding genes with their homologues and identifies the presence of contamination by other species. OMArk is based on the OMA orthology database, from which it exploits orthology relationships, and on the OMAmer software for rapid placement of all proteins in gene families.

The final step is to view the generated annotation using a genome browser such as JBrowse. This browser allows you to navigate along the chromosomes of the genome and view the structure of each predicted gene.

## Input dataset for Helixer
Helixer requires the genome sequence to be annotated, in fasta format.

## Output dataset for Helixer
Helixer produces a single output dataset: a GFF3 file. The GFF3 format is a standard bioinformatics format for storing genome annotations. Each row describes a genomic entity, with columns detailing its identifier, location, score and other attributes.

## Input dataset for Genome Annotation Statistics
This software requires a GFF3 file. In this workflow, the output generated is Helixer.

## Output dataset for Genome Annotation Statistics
Two output files are generated:
- a file containing graphs in pdf format
- a summary in txt format

## Input dataset for GFFRead
In this workflow, GFFRead requires two inputs:
- an annotation file in GFF3 format (the Helixer format)
- the genome sequence in fasta format

## Output dataset for GFFRead
In this workflow, a unique output will be generated. This file, in fasta format, contains the protein sequences predicted from the annotation.


## Input dataset for BUSCO
BUSCO requires a fasta file.
BUSCO will be used twice for this workflow. Firstly on the predicted protein sequences and secondly on the genome sequence. 

## Output dataset for BUSCO
With BUSCO, we can obtain different output files:
- short summary : statistical summary of the quality of genomic assembly or annotation, including total number of genes evaluated, percentage of complete genes, percentage of partial genes, etc.
- full table : list of universal orthologs found in the assembled or annotated genome, with information on their completeness, location in the genome, quality score, etc.
- missing BUSCOs : list of orthologs not found in the genome, which may indicate gaps in assembly or annotation.
- summary image : graphics and visualizations to visually represent the results of the evaluation, such as bar charts showing the proportion of complete, partial and missing genes.
- GFF : contain information on gene locations, exons, introns, etc.

## Input dataset for OMArk
OMAk requires the fasta file produced by GFFRead, containing the predicted protein sequences. 

## Output dataset for OMArk
In this tutorial, a single output file will be generated: a file detailing the assessment of completeness, consistency and species composition. 

## Input dataset for JBrowse
JBrowse requires two inputs:
- the genome sequence in fasta format
- the annotation file in gff3 format, generated by Helixer

## Output dataset for JBrowse
An html file is generated for browsing the genome.