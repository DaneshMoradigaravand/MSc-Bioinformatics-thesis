# MSc-Bioinformatics-thesis
Supplementary data and code for the MSc thesis titled "Genomic  epidemiology of E. coli strains within wild hosts".

**Contense**

  1.[Figures](https://github.com/Lamm-a/MSc-Bioinformatics-thesis#supplementary-figures)
  
  2.[Methods](https://github.com/Lamm-a/MSc-Bioinformatics-thesis#supplementary-methods)
  
  3.[Data](https://github.com/Lamm-a/MSc-Bioinformatics-thesis#data)

Supplementary figures
------------------------------------------------------------------------------
![alt text](https://github.com/Lamm-a/MSc-Bioinformatics-thesis/blob/master/supplementary%20figure%201.png)
Supplementary figure 1: Multi-dimensional scaling of pairwise distances between the Roary core genome alignment. A- separating the isolates by phylogroup showing clearly defined clustering. B- separating the isolates by order of species the isolate came from.

Supplementary methods
------------------------------------------------------
**Isolate acquisition:** The isolate collection from North America consisted of 107 E. coli isolates and 11 Enterobacter cloacae, which were excluded from downstream analysis, from Mexico and one E. coli isolate from Costa Rica. Three E. coli isolates were provided from Venezuela in South America and one Unclassified isolate from Africa. Thirteen of the contributed E. coli isolates and two E. cloacae isolates came from unknown continents and countries. A total of 138 isolates were provided with 123 being E. coli. The E. coli isolates were recovered from the faeces 50 different genus’s consisting of 64 different species covering both land and sky-based animals. The isolates were sequenced as described by Moradigaravand et al<sup>51</sup>.

Antibiotic susceptibility data for the isolates had been established for Ampicilin, Cefotaxime, Ceftazidime, Cefuroxime, Cephalothin, Ciprofloxacin, Gentamycin, Tobramycin and Trimethoprim through phenotypic testing measures. 

**Quality control of short paired end reads:** The pair end reads need to be quality controlled to ensure the reads are E. coli and are of high enough quality to be used in downstream analysis. The Kraken52 taxonomical assignment tool uses alignment of K-mers and a custom classification algorithm to produce fast and sensitive assignment of taxonomical labels. The outputs are a percent of the reads belonging to a certain species and from this we identifed and remove contaminate isolates that were below 40% E. coli from all analysis.

The stats.sh shell tool from BBMap<sup>53</sup> was used to obtain the N50 and number of contigs for each assembly file. Combined the N50 value (higher the better) sand number of contigs (lower the better) show the quality of the assembly and how well we have retrieved the whole genome sequence of the isolate. A custom shell script was compiled to calculate these values and extract then via the Awk language.

**De novo assembly and pangenome analysis:**  Paired end reads were de novo assembled via Velvet<sup>54</sup> following the work flow and parameters of Moradigaravand *et al*<sup>51</sup>. The assembled genomes were then annotated via Prokka, the rapid prokaryotic whole genome annotator<sup>55</sup>. The annotated .gff files were used as input for the pangenome pipeline Roary<sup>20</sup> using fast core alignment to create a multiFASTA alignment of core genes (roary -n -e -z  *.gff). Roary works via extracting the coding regions and performs BLASTP on them with a defined identity threshold. The output summary stats and core genome alignment use in downstream analysis. The SNPs within the core genome were identified with SNP-Sites from the sanger institute<sup>24</sup>. Neighbour-joining phylogenetic trees were generated using the ape package in R with visualisation of trees and associated metadata in [FigTree](http://tree.bio.ed.ac.uk/software/figtree/) and iTOL<sup>56</sup>. R was used to generate MDS plots of the pairwise distance between isolates, clustering by phenotypic groups and isolate taxonomic levels.

**Pairwise distance analysis:** The pairwise distance between the core gene alignment and core SNP alignment of isolates was analysed using the R package ape<sup>57</sup> to read  and generate a pairwise distance matrix for each multi-fasta alignment file. The upper triangle of the square matrix was isolated and melted into a ggplot2 usable matrix of pairwise distances. The distribution of pairwise distance, excluding the phylogroup Clade I and isolates with a not found (NF) clade, was plotted and analysed by splitting into same and different phylogroup of the isolate/taxonomical level of the isolated species. The clustering of the pairwise distances was analysed via multi-dimensional scaling (MDS) using the build in R stats cmdscale functionality on the pairwise distance matrices. The output of which is directly readable into ggplot2, however clade I and those with no clade found (NF) were excluded. Data points were labelled by phylogroup of the isolate and differing taxonomical levels of the isolated species to observe the clustering patterns.

**Correlation analysis of virulence factor frequency and adult body mass of isolate:** Linear regression of virulence factor frequency to adult body mass of the species the isolate came from was conducted using adult body masses from the PanTHERIA<sup>18</sup> ecological database with NAs being removed and merging extrapolated data and actual data. The integrated virulence factor frequency and adult body mass dataset was bootstrapped to produce 100 datasets consisting of 82 observations each,  producing a distribution of adjusted R squared, f-statistic and p-values. Correlation between the two data types was also analysed by Spearman’s correlation tests on the same bootstrapped datasets to get a distribution of t-statistic, correlation and p-values. Spearman’s was employed to allow a dropping of the linear assumption of correlation.

Data
---------------
[Virulence Finder data](https://github.com/Lamm-a/MSc-Bioinformatics-thesis/blob/master/ResFinder_binary_gene_frequency_perIsolate.csv)

[ResFinder data](https://github.com/Lamm-a/MSc-Bioinformatics-thesis/blob/master/Vir_freq_grouped_PerIsolate_orderd_withHomo.csv)
