# SeqTech_2024
**CSHL Advanced Sequencing Technologies Course**  
Jon Preall  
Research Associate Professor @ CSHL

## Lecture Slides
[11/11: Single Cell Sequencing](https://www.dropbox.com/scl/fi/o2kjzpdcm5iuokdotdh3p/Preall_SeqTech_2023.pptx?rlkey=bfl3n7vw1ubz0jq93v8hr65mv&dl=0) (142MB .pptx file)  
[11/21: Intro to scRNA-seq Analysis](https://www.dropbox.com/scl/fi/yrkwawtortfgwq8hfsiyn/Intro_to_scRNAseq_2023.pptx?rlkey=we58cjp366l7z5v1yzm8vnhix&dl=0) (36MB .pptx file)

## Single Cell Wet Lab: Profiling PBMCs of Disease-Affected Donors
We went shopping at the [blood store](https://www.stemcell.com/products/product-types/primary-and-cultured-cells.html?cell_type=Whole%7C%7CMononuclear+Cells&p=2) and bought vials of Peripheral Blood Mononuclear Cells (PBMCs) from donors representing 4 conditions:  
  - Healthy Normal
  - Osteoarthritis
  - Rheumatoid Arthritis
  - Celiac Disease

In the lab, we ran a 10X Genomics experiment with the following parameters:
  -  **NextGEM 5' Gene Expression (v2) Chemistry**
  -  **TCR + BCR V(D)J Enrichment**

We counted cells and made a uniform pool of all 4 donors that were loaded in replicates across 2 channels of a 10X Chip. On the side, we saved a small aliquot of each donor's cells and made 4 low-cost, barcoded 3' digital gene expression libraries in parallel. 

---

## Demux
Demultiplexing strategy schematic:  
<img src="https://github.com/jpreall/SeqTech_2023/blob/main/images/Demux_schematic.png" width="500">

**Demuxing tools used:**  
- [cellsnp-lite](https://cellsnp-lite.readthedocs.io/en/latest/#)  
- [vireo](https://vireosnp.readthedocs.io/en/latest/)
  
Note: there are many options we could have used here. An excellent meta-package called [Demuxafy](https://demultiplexing-doublet-detecting-docs.readthedocs.io/en/latest/index.html) has also been compiled by [Joseph Powell's group](https://www.garvan.org.au/people/researchers/joseph-powell) that incorporates many useful methods and software packages. 

---
## Sequencing

Libraries were prepared according to the 10X Genomics User Guide and loaded onto a NextSeq2000 P3 flow cell with the following read lengths:  

| Read1 | Index1 | Index2 | Read2 |
|---|---|---|---|
|26bp|10bp|10bp|90bp|

**Flowcell Summary**
| Clusters (Raw) | Clusters(PF) | Yield (MBases) |
| --------- | :-------------: | :--------:  |
| 3,390,170,112 | 1,314,887,047 | 152,527 |

<img src="https://github.com/jpreall/SeqTech_2023/blob/main/images/base_coverage.png" width="500">

### <a name="section1">Creating 10X-compatible FASTQ files with `cellranger mkfastq`</a>
**Cellranger** is 10X Genomic's free-to-use software that carries out FASTQ generation, mapping, and primary data analysis for all 10X Genomics sequencing-based pipelines. Cellranger expects its input FASTQ files to be in a very specific format, which is ever-so-slightly different than the default format produced by Illumina's FASTQ generation pipeline.  For this reason, they bundled their own version of Illumina's `bcl2fastq` into a program called `mkfastq` that spits out files in a Cellranger-compatible format. You may never have to do this part yourself, since it is likely that NGS core will be the one generating your 10X- FASTQ files that will plug nicely into the subsequent `count` pipeline.  
[Cellranger mkfastq instructions](https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/using/mkfastq)

```bash
cellranger mkfastq \
	--localcores=12 \
	--run=/path/to/basecalls/ \
	--samplesheet=/path/to/SampleSheet.csv \
```
---

## Single Cell Dry Lab


### Mapping and "Primary" Analysis using Cellranger
Mapping and transcript counting are carried out using the `cellranger count` pipeline.  In parallel, V(D)J analysis can be carried out with the `cellranger vdj` command. *This is not meant to be run on your personal laptop.* It is an intensive, memory-hungry Linux application that is built to run on high-performance workstations or clusters. For the purposes of this course, the Cellranger steps will be carried out ahead of time before our interactive session, partly because it takes several hours to complete.  

Cellranger can be run on a local server / cluster:  
[Cellranger Installation Help](https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/using/tutorial_in)

Or on the cloud:  
[10X Genomics Cloud](https://www.10xgenomics.com/products/cloud-analysis)

### Bulk RNA-seq Library Analysis for Demux  
blah blah STARsolo CellSNP  

### <a name="section4"> Combining samples with `cellranger aggr`</a>
The two replicate 10X channels were combined into a single unified data matrix using `cellranger aggr`  
Cellranger provides two normalization options for doing this:  
  - `Normalize=none`
  	- *simply concatenates the matrices together with no modifications*
  - `Normalize=mapped`
  	- *downsamples more deeply sequenced samples to approximately match number of mapped reads-per-cell to the worst sample in the data*

We used `Normalize=none` here, because it seems to be the most commonly used strategy in the wild

---
## Download the data from Jon's Instance
```
JP=3.86.4.253
cd /workspace/
wget http://$JP/SingleCell.tar.gz
tar -zxvf SingleCell.tar.gz
```

## Install the packages I forgot to have pre-installed
```
source activate scRNAseq_env
pip install celltypist ipywidgets gseapy matplotlib-venn
```
  
