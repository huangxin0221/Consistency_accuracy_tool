## 1. realted software install
### (1). configure the conda source (install mamba and add related channels)
```r
conda install mamba -n base -c conda-forge
conda config --add channels bioconda
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/pro
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
```
### (2). install bamboo
```r
BAMBOO_VERSION=$(curl -s https://api.github.com/repos/CycloneSEQ-Bioinformatics/Bamboo/releases/latest | grep "tag_name" | awk -F'"' '{print $4}' | sed 's/^v//')
wget https://github.com/CycloneSEQ-Bioinformatics/Bamboo/releases/download/v$BAMBOO_VERSION/bamboo-$BAMBOO_VERSION.tar.gz
tar xvzf bamboo-$BAMBOO_VERSION.tar.gz
cd bamboo-$BAMBOO_VERSION
chmod +x bamboo
```
### (3). create conda env1 and env2, and install related software 
```r
## conda env1
conda create -n WT02 -y
conda activate WT02
# clair3 
mamba install clair3=1.0.10 python=3.9.0 -y
# minimap2
mamba install minimap2=2.28 -y
# mosdepth
mamba install mosdepth=0.3.3 -y 
# sniffles
mamba install sniffles=2.0.7 -y
# truvari
mamba install truvari=4.1.0 -y 
# bcftools
mamba install bcftools=1.10.2 -y
# pandas
mamba install pandas=1.5.3 -y
```
```r
## conda env2
# hap.py (SNV benchmark)  ---- need create a new python environment
conda create -n happy hap.py rtg-tools -y
mamba install libgfortran==1 -y
```
## 2. realted file description
```r
#### Related file
## reference genome
database/Ref/GRch37/hs37d5.fa                                                        # Human-GRch37
database/Ref/Ecoli/synII_sb_genome.fasta                                             # Ecoli-SynII
## benchmark
database/Benchmark/HG002_SNV/HG002_GRCh37_1_22_v4.2.1_benchmark.vcf.gz               # HG002 SNV benchmark
database/Benchmark/HG002_SNV/HG002_GRCh37_1_22_v4.2.1_benchmark_noinconsistent.bed   # HG002 SNV high confident region
database/Benchmark/HG002_SV/HG002_SVs_Tier1_v0.6.vcf.gz                              # HG002 SV benchmark
database/Benchmark/HG002_SV/HG002_SVs_Tier1_v0.6.bed                                 # HG002 SV high confident region
database/Benchmark/HG002_SV/hs37d5.trf.bed                                           # Human-GRch37 tandem repeat region
```
## 3. software usage
```r
#### Usage
bash WT02_human_ecoli.sh --fastq_fn1=/path/to/HG002/FASTQ \                                      # HG002 fastq
                         --fastq_fn2=/path/to/UHRR/FASTQ \                                       # UHRR fastq
                         --fastq_fn3=/path/to/Ecoli/FASTQ \                                      # Ecoli fastq
                         --ref_fn1=/path/to/GRch37/Ref \                                         # Human GRch37 reference genome
                         --ref_fn2=/path/to/Ecoli/Ref \                                          # Ecoli SynII reference genome
                         --sample_ID1="HG002" \                                                  # Sample ID is used when conduct variant calling 
                         --sample_ID2="UHRR" \
                         --sample_ID3="SynII" \
                         --output_dir=/path/to/output_dir \                                      # Output directory
                         --output_fn=WT02.txt \                                                  # Output filename (store results)      
                         --threads=30 \  
                         --bamboo=/path/to/bamboo/executable/file                                # Bamboo software        
                         --conda_env1=/path/to/conda/envs1 \               
                         --conda_env2=/path/to/conda/envs2 \
                         --snv_benchmark=/path/to/HG002/snv/benchmark \                          # HG002 SNV benchmark
                         --sv_benchmark=/path/to/HG002/sv/benchmark \                            # HG002 SV benchmark
                         --snv_high_confident_region=/path/to/HG002/snv/high_confident_region \  # HG002 SNV high confident region
                         --sv_high_confident_region=/path/to/HG002/sv/high_confident_region \    # HG002 SV high confident region                                        
                         --tandem_repeats=/path/to/GRch37/tandem_repeat_region                   # Human-GRch37 tandem repeat region
```
