## 1. software install
### （1）add current user to docker group [need root authority]
```r
sudo usermod -a -G docker $(whoami)
sudo service docker restart
newgrp docker
```
### （2）software install

```r
# method 1: docker pull (online installation requires network connection) slow
docker pull crpi-7a9vueif1b7jprb7.cn-hangzhou.personal.cr.aliyuncs.com/huangxin970221/wt02_human_ecoli:v1.0.1.0
docker tag crpi-7a9vueif1b7jprb7.cn-hangzhou.personal.cr.aliyuncs.com/huangxin970221/wt02_human_ecoli:v1.0.1.0 wt02_human_ecoli:v1.0.1.0
docker rmi crpi-7a9vueif1b7jprb7.cn-hangzhou.personal.cr.aliyuncs.com/huangxin970221/wt02_human_ecoli:v1.0.1.0
# method 2: docker load (local installation network is not needed, but you should provide wt02_human_ecoli_v1.0.1.0.tar files)
docker load -i wt02_human_ecoli_v1.0.1.0.tar
```
## 2. usage
```r
### Usage 
docker run wt02_human_ecoli:v1.0.1.0 --help
```
## 3. demo
```r
# run HG002, UHRR, and ecoli
newgrp docker
docker run --rm \
  --user $(id -u):$(id -g) \
  -v /path/to/hg002/fastq or fastq directory:/app/input/fastq filename or RUN ID  \  # HG002 fastq file or directory [if provide fastq file, make sure fastq filename is the same as raw fastq filename. If provide fastq directory, please provide RUN ID]
                                                                                     # no need to change /app/input/, but you should provide fastq filename or RUN ID
  -v /path/to/uhrr/fastq or fastq directory:/app/input/fastq filename or RUN ID \    # UHRR fastq file or directory [same as HG002]
  -v /path/to/ecoli/fastq or fastq directory:/app/input/fastq filename or RUN ID \   # Ecoli fastq file or directory [same as HG002]    
  -v /path/to/output/directory:/app/output \                                         # You need create output directory by yourself, and ensure output directory is empty
  wt02_human_ecoli:v1.0.1.0 \
  --fastq_fn1=/app/input/fastq filename or RUN ID \                                  # HG002 fastq file or directory (consistent with the previous fastq or folder)
  --fastq_fn2=/app/input/fastq filename or RUN ID \                                  # UHRR fastq file or directory (consistent with the previous fastq or folder)
  --fastq_fn3=/app/input/fastq filename or RUN ID \                                  # Ecoli fastq file or directory (consistent with the previous fastq or folder)
  --sample_ID1="HG002" \                                                             # HG002 sample id (default: HG002)      
  --sample_ID2="UHRR" \                                                              # UHRR sample id (default: UHRR)
  --sample_ID3="Ecoli" \                                                             # Ecoli sample id (default: Ecoli)
  --output_dir=/app/output/ \                                                        # output directory (no need to change it) 
  --output_fn="WT02.txt" \                                                           # output filename (default: WT02.txt)
  --threads=20                                                                       # number of threads (default: 20) 
# run ecoli
newgrp docker
docker run --rm \
  --user $(id -u):$(id -g) \
  -v /path/to/ecoli/fastq or fastq directory:/app/input/fastq filename or RUN ID \   # Ecoli fastq file or directory  
  -v /path/to/output/directory:/app/output \                                         # You need create output directory by yourself, and ensure output directory is empty
  wt02_human_ecoli:v1.0.1.0 \
  --fastq_fn3=/app/input/fastq filename or RUN ID \                                  # Ecoli fastq file or directory (consistent with the previous fastq or folder)
  --sample_ID3="Ecoli" \                                                             # Ecoli sample id (default: Ecoli)
  --output_dir=/app/output/ \                                                        # output directory (no need to change it) 
  --output_fn="WT02.txt" \                                                           # output filename (default: WT02.txt)
  --threads=20                                                                       # number of threads (default: 20) 
```



