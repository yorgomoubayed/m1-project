The three-dimensional conformation of the genome is complex, dynamic and crucial for the regulation of gene expression. Chromosome conformation capture methods coupled 
with high-throughput sequencing (Hi-C, capture Hi-C...) have revealed how the organization of the genome is interconnected with the nuclear architecture. This work was carried out 
as part of a tutored project (7 weeks) in the first year of the master's degree in bioinformatics.It focuses on the pre-processing of three-dimensional conformation data of the mammalian 
genome via a bioinformatics pipeline: HiCUP. This is the starting point for the analysis of Hi-C data.

The repository contains the files generated to perform the given analysis. These files include:
- snake.hicup.yml, a snakemake script that automates data pre-processing with HiCUP. Edit as required.
- Hicup.yaml, to generate the conda environment with all dependencies to run the HiCUP pipeline.
- sra_explorer_fastq_download.sh, for downloading the FastQ files of the GSM3682164 dataset.
- cluster.json, configuration file that provides the cluster with user-input settings to run the workflow. Edit as required.
- hicup_config_file.conf, configuration file for the hicup Perl script. Edit as required.

# Installing HiCUP

~~~
conda env create -f Hicup.yaml
~~~

~~~
conda activate Hicup
~~~

~~~
wget https://www.bioinformatics.babraham.ac.uk/projects/hicup/hicup_v0.7.3.tar.gz
~~~

# Running HiCUP

The snake.hicup.yml contains a workflow that: 
  - Downloads the HiCUP training datasets.
  - Downloads the reference genome.
  - Builds the Bowtie2 index from the reference genome.
  - Digests the reference genome with hicup-digester.
  - Runs the HiCUP pipeline.
  
## Local run

~~~
snakemake --cores 6 -p -d out -s snake.hicup.yml
~~~

## Cluster run

~~~
snakemake -d out -s snake.hicup.yml -p -j 999 --cluster-config cluster.json --cluster "sbatch --account {cluster.account} --partition {cluster.partition} --time {cluster.time} --job-name {cluster.job-name} --ntasks-per-node {cluster.ntasks-per-node} --output {cluster.output} --error {cluster.error}"
~~~
