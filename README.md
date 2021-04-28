# NFN-phylogenomics

This repository contains data and code resource for the study of phylogenomics of N-fixing nodulating plants.
Please see the publications [1]. 

## Phylogenetic data

XX alignemnts and phylogenetic trees of 200 symbiosis related genes:

## Genomic data

Gff file of NFN-related conserved non-coding elements that mapped to the genome of Medicago trancatula:

## Transcriptomic data

TPM and assemblies of transcriptomes of XX nodulating and XX non-nodulating species:

## Pipelines for detecting genomic signal of convergent evolution

###### An ‘alignment’ method used to detect convergent signals in nodulating species

```
perl Specific_mutation_detector.pl an_aligned_fasta_file list_of_genes_of_interest m n
```
`an_aligned_fasta_file` an aligned fasta file that contains all the genes that you are interested

`list_of_genes_of_interest` a subset of above genes (targets) that you want detect convergent site or specific mutation

`m` larger than  m (a cut-off of proportion, ie 1, 0.9, 0.8) of targets should have the specific/convergent mutation

`n` small than n (a cut-off of proportion, ie 0, 0.1, 0.2) of non-targets allowed to have above specific/convergent mutation


###### A ‘tree topology inference’ method based on large-scale phylogenetic reconstruction of groups of orthologous genes

1. Make an alignment of all the orthologous proteins that you are interested
```
mafft ortholog.pep.fa > ortholog.pep.fa.MSA
```

2. Make an cds alignment guided by the protein alignment
```
Trimal -in ortholog.pep.fa.MSA -backtrans ortholog.cds.fa -gt 0.5 -out ortholog.cds.fa.MSA
```
3. Manually plot your H0, H1 trees based on your own hypothesis; the convergent species should be in one clade. 
4. calcuate the log-likelihood
raxmlHPC-PTHREADS-AVX -f g -s ortholog.cds.fa.MSA -m GTRGAMMA -z retained.species.newick -n ortholog.likehood
