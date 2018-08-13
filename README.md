## VarClust

[![License: MIT][1]][2]

`VarClust` is a Python package performs clustering of high-throughput
sequencing (HTS) data using single nucleotide variants (SNVs). `VarClust`
analyses variants stored in [VCF files][3], which are the output of variant
callers such as the [Genome Analysis ToolKit][4]. While `VarClust` was
developed for the analysis of single cell RNA sequencing (scRNA-seq) data, any
variant data stored in VCF files may be analysed whether it originates in DNA-
or RNA-based methods.

## Installation

`VarClust` can be installed from GitHub using [pip][5]:

```bash
pip install git+https://github.com/fasterius/VarClust
```

## Usage

While `VarClust` is a Python package and may thus be utilised as such (*i.e.* by
importing it and using each included function as desired), its main
interface is through the command line. It has five modules, each performing a
separate function: creation of SNV profiles, calculation of genetic distance
matrices, aggregation of specified profiles into "pseudo-profiles" and, lastly,
clustering using either hierarchical agglomerative clustering (HAC) or
t-distributed stochastic neighbour embedding (tSNE).

A brief guide on how to use each of `VarClust`'s modules is provided here, but 
additional details can be accessed by passing the `-h` or `--help` flag after
the command. There are a number of parameters that may be changed according to
your specific needs, such as using only a specific subset of variants for the
distance calculation (*e.g* excluding variants present in the dbSNP database
or those that do not pass some quality threshold).

Given a directory of single-sample VCF files, the first step is to create an
SNV profile for each:

```bash
varclust_create_profiles <VCF directory> <output profile directory>
```

A pairwise distance matrix for the genetic similarities between each sample
must then be calculated:

```bash
varclust_distance_matrix <profile directory> <output distance matrix path>
```

Clustering using either HAC or tSNE may then be performed using the resulting
distance matrix:

```bash
varclust_heatmap <distance matrix> <output figure path>
varclust_tsne <distance matrix> <output figure path> -m <metadata file>
              -M <metadata ID col> -c <colour col> -s <shape col>
```

The variants in the profiles may also be aggregated into pseudo-profiles, where
the variants and the number of times they occur in each included profile will
be enumerated:

```bash
varclust_pseudo <profile directory> <output pseudo-profile path>
```

## Licence

`VarClust` is released with a MIT licence. `VarClust` is free software: you may
redistribute it and/or modify it under the terms of the MIT license. For more
information, please see the `LICENCE` file that comes with the package.

[1]: https://img.shields.io/badge/License-MIT-blue.svg
[2]: https://opensource.org/licenses/MIT
[3]: http://www.internationalgenome.org/wiki/analysis/variant-call-format
[4]: https://software.broadinstitute.org/gatk/
[5]: https://pypi.org/project/pip/
