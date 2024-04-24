# life4136-cw

## Description 
This script serves to obtain a consensus file from a reference fasta and vcf files. the coordinates of the genes of interest are obtained from a gff3 file. 
The aim for this script is to visualise protein 3D structure and compare synomymous mutations in diploid vs teraploid *Arabidopsis Thaliana*. 

## Requirements 
samtools: Required for indexing FASTA files and handling VCF files.
bcftools: Necessary for variant extraction and consensus sequence generation.
pymol: Used for visualizing consensus sequences in 3D molecular structures.

## Installation 
Samtools: https://github.com/samtools/htslib/releases/
```
wget https://github.com/samtools/htslib/archive/refs/tags/1.20.zip
nano ~/.bashrc
export PATH="$PATH:/path/to/samtools"
```

Bcftools: https://github.com/samtools/bcftools
```
wget https://github.com/samtools/bcftools/releases/download/1.20/bcftools-1.20.tar.bz2
nano ~/.bashrc
export PATH="$PATH:/path/to/bcftools"
```

Pymol
licence: https://pymol.org/2/buy.html
download: https://pymol.org/#download


## Process

1. follow steps from ``` create consensus file ``` script
2. Obtain DNA sequence of each consensus file and translate each on https://web.expasy.org/translate/
   ```
   grep -v '>' g45503_dips_consensus.fasta
   #output example (partial sequence included for demonstration) 
   ATGAACTCCGATGGATCTAAATCTGGTCGAAACAGACGCGAGATTCGAGCTAAGCATCTG
   AAGAAGTTCACGAGCGTCGGTGACGGTGACGATGACTCTGTTAAAATTGTAGCCAAGGAC
   AATAAGAAGGGTTCAAAGAGGGAAAGAGAAAGCCAATTCGATGATCACGATGAAGAAGAA
   GAGCCTCTTGTTAAGAAAGCAGCTTCTACTAAAGCTGTAGAAGCTCCCAAACCTTCAGAT
   TCTTATTTGTCAAAGACAAG
   ```
input the DNA sequence in Expasy, hte optimal result is a sequence fully highlighted in red, with no amino acids with a value of X

3. align diploid and tetraploid amino acid sequences to identify dissimilarity regions
   https://www.ebi.ac.uk/jdispatcher/psa/emboss_needle

   ```
   #expected outcome (partial outcome shown for demonstration) 
   EMBOSS_001         1 MNSDGSKSGRNRREIRAKHLKKFTSVGDGDDDSVKIVAKDNKKGSKRERE     50
                     ||.||||||||||||||||||||||||||||.|.||:.|.||||||||||
   EMBOSS_001         1 MNFDGSKSGRNRREIRAKHLKKFTSVGDGDDVSAKIIVKCNKKGSKRERE     50

   EMBOSS_001        51 SQFDDHDEEEEPLVKKAASTKAVEAPKPSDSYLSKTRFDQFPLSPLSLKA    100
                     |:|||:||||||||||||.||||||||.||||||||||||||||||||||
   EMBOSS_001        51 SKFDDYDEEEEPLVKKAAFTKAVEAPKTSDSYLSKTRFDQFPLSPLSLKA    100
   ```
4. compute predicted structure using AlphaFold: https://colab.research.google.com/github/sokrypton/ColabFold/blob/main/AlphaFold2.ipynb
5. import AlphaFold PBD output into Pymol

## Visualising structure in Pymol: an example

``` 
load your_protein.pdb
#visualise surface
show suface

#visualise hydrophobicity with residual range
color blue, (hydro; resi 1-100) and hydro; threshold=0.3
color white, (hydro; resi 1-100) and not hydro

#colour resiudes that differ in tetraploid vs diploid
colour purple, resi 52

```
refer to https://pymolwiki.org/index.php/CheatSheet for additional commands

## Additional resources: 
InterPro: https://www.ebi.ac.uk/interpro/
input protein sequences to find about functions and evolutionary relationships for protein of interest


## Citations 
Pymol
The PyMOL Molecular Graphics System, Version 2.5.8 Schrödinger, LLC.


    
