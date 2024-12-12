# 16SrRNA
-----------

```
###Databases
wget -O "gg-13-8-99-515-806-nb-classifier.qza" "https://data.qiime2.org/2023.5/common/gg-13-8-99-515-806-nb-classifier.qza"
wget -O "gg-13-8-99-515-806-nb-classifier.qza" "https://data.qiime2.org/2022.2/common/silva-138-99-515-806-nb-classifier.qza"

#Importing_data
qiime tools import   --type 'SampleData[PairedEndSequencesWithQuality]'   --input-path manifest.txt   --output-path paired-end-demux.qza   --input-format PairedEndFastqManifestPhred33

```
