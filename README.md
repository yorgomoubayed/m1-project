# Install HiCUP

~~~
conda create -n Hicup python=3.7
~~~

~~~
conda activate Hicup
conda env update -f Hicup.yml
~~~

Install the HiCUP repository : https://www.bioinformatics.babraham.ac.uk/projects/hicup/hicup_v0.7.3.tar.gz

# Running HiCUP Tutorial

The hicup_config_file.conf file is a configuration file for the hicup Perl script - edit as required

The snake.hicup.yml contains a workflow that: 
  -downloads the HiCUP training datasets.
  -downloads the reference genome.
  -builds the Bowtie2 index from the reference genome.
  -digests the reference genome with hicup-digester.
  -runs the HiCUP pipeline.
  
## Local run

~~~
snakemake --cores 6 -p -d out -s snake.hicup.yml
~~~

## Cluster run

The cluster.json file is a configuration that provides the cluster with user-input settings to run the workflow. Edit as required.
~~~
snakemake -d out -s snake.hicup.yml -p -j 999 --cluster-config cluster.json --cluster "sbatch --account {cluster.account} --partition {cluster.partition} --time {cluster.time} --job-name {cluster.job-name} --ntasks-per-node {cluster.ntasks-per-node} --output {cluster.output} --error {cluster.error}"
~~~



