# 16SrRNA
-----------
### Installation of Qiime2 in Conda enviroment in Ubuntu

Follow the linux section
https://docs.qiime2.org/2024.10/install/native/#install-qiime-2-within-a-conda-environment

```
###Databases
wget -O "gg-13-8-99-515-806-nb-classifier.qza" "https://data.qiime2.org/2023.5/common/gg-13-8-99-515-806-nb-classifier.qza"
wget -O "silva-138-99-515-806-nb-classifier.qza" "https://data.qiime2.org/2022.2/common/silva-138-99-515-806-nb-classifier.qza"

#Importing_data
qiime tools import   --type 'SampleData[PairedEndSequencesWithQuality]'   --input-path manifest.txt   --output-path paired-end-demux.qza   --input-format PairedEndFastqManifestPhred33

#debluring/filtering

qiime deblur denoise-16S --i-demultiplexed-seqs paired-end-demux.qza --p-trim-length 70 --o-representative-sequences rep-seqs-deblur.qza --o-table table-deblur.qza --p-sample-stats --o-stats deblur-stats.qza

qiime feature-table summarize --i-table table-deblur.qza --o-visualization table.qzv --m-sample-metadata-file metadata.txt

qiime feature-table tabulate-seqs --i-data rep-seqs-deblur.qza --o-visualization rep-seqs-deblur.qzv

qiime alignment mafft --i-sequences rep-seqs-deblur.qza --o-alignment aligned-rep-seqs.qza

qiime alignment mask --i-alignment aligned-rep-seqs.qza --o-masked-alignment masked-aligned-rep-seqs.qza

qiime phylogeny fasttree --i-alignment masked-aligned-rep-seqs.qza --o-tree unrooted-tree.qza

qiime phylogeny midpoint-root --i-tree unrooted-tree.qza --o-rooted-tree rooted-tree.qza

qiime diversity core-metrics-phylogenetic   --i-phylogeny rooted-tree.qza   --i-table table.qza   --p-sampling-depth 5152 --m-metadata-file metadata.txt   --output-dir core-metrics-results  

qiime diversity alpha-group-significance   --i-alpha-diversity core-metrics-results/faith_pd_vector.qza   --m-metadata-file metadata.txt   --o-visualization core-metrics-results/faith-pd-group-significance.qzv

qiime diversity alpha-group-significance   --i-alpha-diversity core-metrics-results/evenness_vector.qza   --m-metadata-file metadata.txt   --o-visualization core-metrics-results/evenness-group-significance.qzv

qiime diversity beta-group-significance --i-distance-matrix core-metrics-results/unweighted_unifrac_distance_matrix.qza --m-metadata-file metadata.txt --m-metadata-column Site --o-visualization core-metrics-results/unweighted-unifrac-body-site-significance.qzv --p-pairwise

qiime diversity beta-group-significance   --i-distance-matrix core-metrics-results/unweighted_unifrac_distance_matrix.qza   --m-metadata-file metadata.txt   --m-metadata-column Plant   --o-visualization core-metrics-results/unweighted-unifrac-subject-group-significance.qzv   --p-pairwise

qiime feature-classifier classify-sklearn --i-classifier gg-13-8-99-515-806-nb-classifier.qza --i-reads rep-seqs-dada2.qza --o-classification taxonomy.qza

qiime taxa barplot --i-table table-deblur.qza --i-taxonomy taxonomy.qza --m-metadata-file metadata.txt --o-visualization taxa-bar-plots.qzv

qiime feature-table group --i-table tabledada2.qza --p-axis 'sample' --m-metadata-file metadataCTDm.txt --m-metadata-column "sampletag" --p-mode 'mean-ceiling' --o-grouped-table table_grouped.qza

qiime taxa barplot --i-table table_grouped.qza --i-taxonomy taxonomy.qza --m-metadata-file metadataCTDmGroup.txt --o-visualization taxa-barplot_grouped.qzv

qiime taxa barplot --i-table table-no-mitochondria-no-chloroplast.qza --i-taxonomy taxonomy.qza --m-metadata-file metadataCTDmGroup.txt --o-visualization taxa-barplot_group
edfiltered.qzv

qiime taxa filter-table --i-table table_grouped.qza --i-taxonomy taxonomy.qza --p-exclude mitochondria,chloroplast,wolbachia --o-filtered-table table-no-mitochondria-no-chloroplast.qza

qiime taxa filter-table --i-table table_grouped.qza --i-taxonomy taxonomy.qza --p-exclude mitochondria,chloroplast,lactobacillus --o-filtered-table table-no-MitCloLacto.qza

qiime taxa barplot --i-table table-no-MitCloLacto.qza --i-taxonomy taxonomy.qza --m-metadata-file metadataCTDmGroup.txt --o-visualization taxa-bar-plotsF.qzv

#phylogenyexport
qiime tools export --input-path unrooted-tree.qza --output-path phylogeny

#biom to tsv
biom convert -i feature-table.biom -o feature-table.tsv --to-tsv


```
