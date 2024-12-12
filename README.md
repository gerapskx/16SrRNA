# 16SrRNA

'''
wget -O "gg-13-8-99-515-806-nb-classifier.qza" "https://data.qiime2.org/2023.5/common/gg-13-8-99-515-806-nb-classifier.qza"
wget -O "gg-13-8-99-515-806-nb-classifier.qza" "https://data.qiime2.org/2022.2/common/silva-138-99-515-806-nb-classifier.qza"

qiime tools import   --type 'SampleData[PairedEndSequencesWithQuality]'   --input-path manifest.txt   --output-path paired-end-demux.qza   --input-format PairedEndFastqManifestPhred33

qiime tools import --type 'SampleData[SequencesWithQuality]' --input-path manifestCTDm.txt --output-path single-end-demux.qza --input-format SingleEndFastqManifestPhred33V2

'''"
