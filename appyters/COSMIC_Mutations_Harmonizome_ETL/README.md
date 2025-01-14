# Harmonizome ETL: COSMIC (Mutations)

[The Catalogue of Somatic Mutations in Cancer](https://cancer.sanger.ac.uk/cosmic) (COSMIC) is an expert-curated database of somatic mutation information related to human cancers. It combines high-precision data from peer reviewed papers with genome-wide screen data to provide extensive converage of the cancer genomic landscape.

This appyter takes data from the Copy Number Variants dataset and outputs files that are usable for the Harmonizome. It pre-processes the raw data  in order to construct an expression matrix with gene names as rows and sample names as column attributes. It then draws from the current NCBI database to map the gene names to a set of approved gene symbols, so that synonymous genes are mapped to the same symbol. 

From here, it merges duplicate genes and attributes by averaging the expression value and removes genes and attributes that have more than 95% missing data, imputing any remaining missing data for each gene by taking its average expression. It performs normalization by log2 transformation and then quantile normalization for the attributes, and z-scores for the genes.

From this normalized matrix, it creates a matrix of standardized values between -1 and 1. From this standard matrix, it creates a ternary matrix, which stores whether a gene and attribute are negatively, positively, or not correlated. It also creates gene and attribute similarity matrices, which store the cosine distance between any two genes or attributes.

The downloadable file will have the following outputs:
* Unfiltered matrix: the expression matrix before normalization
* Filtered matrix: the normalized matrix
* Gene list
* Attribute list
* Standard matrix
* Ternary matrix
* Up/down gene set library: for each attribute, a list of genes that are positively/negatively correlated, respectively
* Up/down attribute set library: for each gene, a list of attributes that are positively/negatively correlated, respectively
* Gene similarity matrix
* Attribute similarity matrix
* Gene-attribute edge list: a list of gene-attribute pairs and the standard value for each pair 
