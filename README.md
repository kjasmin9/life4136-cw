# life4136-cw

## Description 
This script serves to obtain a consensus file from a reference fasta and vcf files. the coordinates of the genes of interest are obtained from a gff3 file. 

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
   '''
   grep 
