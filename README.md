# 16SrRNA
-----------
### Installation of Qiime2 in Conda enviroment in Ubuntu

Follow the linux section
https://docs.qiime2.org/2024.10/install/native/#install-qiime-2-within-a-conda-environment

```
###Databases
wget -O "gg-13-8-99-515-806-nb-classifier.qza" "https://data.qiime2.org/2023.5/common/gg-13-8-99-515-806-nb-classifier.qza"
wget -O "gg-13-8-99-515-806-nb-classifier.qza" "https://data.qiime2.org/2022.2/common/silva-138-99-515-806-nb-classifier.qza"

#Importing_data
qiime tools import   --type 'SampleData[PairedEndSequencesWithQuality]'   --input-path manifest.txt   --output-path paired-end-demux.qza   --input-format PairedEndFastqManifestPhred33

#debluring/filtering

qiime deblur denoise-16S --i-demultiplexed-seqs paired-end-demux.qza --p-trim-length 70 --o-representative-sequences rep-seqs-deblur.qza --o-table table-deblur.qza --p-sample-stats --o-stats deblur-stats.qza


```
