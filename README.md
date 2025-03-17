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
docker pull crpi-7a9vueif1b7jprb7.cn-hangzhou.personal.cr.aliyuncs.com/huangxin970221/wt02_human_ecoli:v1.0.2.0
docker tag crpi-7a9vueif1b7jprb7.cn-hangzhou.personal.cr.aliyuncs.com/huangxin970221/wt02_human_ecoli:v1.0.2.0 wt02_human_ecoli:v1.0.2.0
docker rmi crpi-7a9vueif1b7jprb7.cn-hangzhou.personal.cr.aliyuncs.com/huangxin970221/wt02_human_ecoli:v1.0.2.0
# method 2: docker load (local installation network is not needed, but you should provide wt02_human_ecoli_v1.0.2.0.tar files)
docker load -i wt02_human_ecoli_v1.0.2.0.tar
```
## 2. usage
```r
### Usage 
docker run wt02_human_ecoli:v1.0.2.0 --help
```
## 3. demo
```r
newgrp docker
## HG002
# only for HG002 (input directory)
docker run --rm \
  --user $(id -u):$(id -g) \
  -v /data/2407B03221011:/app/input/2407B03221011 \
  -v /data/output/2407B03221011:/app/output \
  wt02_human_ecoli:v1.0.2.0 \
  --fastq_fn1=/app/input/2407B03221011 \
  --sample_ID1="HG002" \
  --output_dir=/app/output \
  --output_fn="2407B03221011.txt" \
  --threads=20
# only for HG002 (input fastq file)
docker run --rm \
  --user $(id -u):$(id -g) \
  -v /data/2407B03221011/2407B03221011.fastq.gz:/app/input/2407B03221011/2407B03221011.fastq.gz \
  -v /data/output/2407B03221011:/app/output \
  wt02_human_ecoli:v1.0.2.0 \
  --fastq_fn1=/app/input/2407B03221011/2407B03221011.fastq.gz \
  --sample_ID1="HG002" \
  --output_dir=/app/output \
  --output_fn="2407B03221011.txt" \
  --threads=20

## UHRR
# only for UHRR (input directory)
docker run --rm \
  --user $(id -u):$(id -g) \
  -v /data/2407B03221011:/app/input/2407B03221011 \
  -v /data/output/2407B03221011:/app/output \
  wt02_human_ecoli:v1.0.2.0 \
  --fastq_fn2=/app/input/2407B03221011 \
  --sample_ID2="UHRR" \
  --output_dir=/app/output \
  --output_fn="2407B03221011.txt" \
  --threads=20
# only for UHRR (input fastq file)
docker run --rm \
  --user $(id -u):$(id -g) \
  -v /data/2407B03221011/2407B03221011.fastq.gz:/app/input/2407B03221011/2407B03221011.fastq.gz \
  -v /data/output/2407B03221011:/app/output \
  wt02_human_ecoli:v1.0.2.0 \
  --fastq_fn2=/app/input/2407B03221011/2407B03221011.fastq.gz \
  --sample_ID2="UHRR" \
  --output_dir=/app/output \
  --output_fn="2407B03221011.txt" \
  --threads=20 

## Ecoli
# only for ecoli (input directory)
docker run --rm \
  --user $(id -u):$(id -g) \
  -v /data/2407B03221011:/app/input/2407B03221011 \
  -v /data/output/2407B03221011:/app/output \
  wt02_human_ecoli:v1.0.2.0 \
  --fastq_fn3=/app/input/2407B03221011 \
  --sample_ID3="Ecoli" \
  --output_dir=/app/output \
  --output_fn="2407B03221011.txt" \
  --threads=20
# only for ecoli (input fastq file)
docker run --rm \
  --user $(id -u):$(id -g) \
  -v /data/2407B03221011/2407B03221011.fastq.gz:/app/input/2407B03221011/2407B03221011.fastq.gz \
  -v /data/output/2407B03221011:/app/output \
  wt02_human_ecoli:v1.0.2.0 \
  --fastq_fn3=/app/input/2407B03221011/2407B03221011.fastq.gz \
  --sample_ID3="Ecoli" \
  --output_dir=/app/output \
  --output_fn="2407B03221011.txt" \
  --threads=20  

## HPV11
# only for HPV11 (input directory)
docker run --rm \
  --user $(id -u):$(id -g) \
  -v /data/2407B03221011:/app/input/2407B03221011 \
  -v /data/output/2407B03221011:/app/output \
  wt02_human_ecoli:v1.0.2.0 \
  --fastq_fn4=/app/input/2407B03221011 \
  --sample_ID4="HPV11" \
  --output_dir=/app/output \
  --output_fn="2407B03221011.txt" \
  --threads=20
# only for HPV11 (input fastq file)
docker run --rm \
  --user $(id -u):$(id -g) \
  -v /data/2407B03221011/2407B03221011.fastq.gz:/app/input/2407B03221011/2407B03221011.fastq.gz \
  -v /data/output/2407B03221011:/app/output \
  wt02_human_ecoli:v1.0.2.0 \
  --fastq_fn4=/app/input/2407B03221011/2407B03221011.fastq.gz \
  --sample_ID4="HPV11" \
  --output_dir=/app/output \
  --output_fn="2407B03221011.txt" \
  --threads=20  

## HG002, UHRR, Ecoli, and HPV11
# HG002, UHRR and Ecoli (input directory)
docker run --rm \
  --user $(id -u):$(id -g) \
  -v /data/2407B03221011:/app/input/2407B03221011 \
  -v /data/2407B03221012:/app/input/2407B03221012 \
  -v /data/2407B03221013:/app/input/2407B03221013 \
  -v /data/2407B03221014:/app/input/2407B03221014 \
  -v /data/output/2407B032210:/app/output \
  wt02_human_ecoli:v1.0.2.0 \
  --fastq_fn1=/app/input/2407B03221011 \
  --fastq_fn2=/app/input/2407B03221012 \
  --fastq_fn3=/app/input/2407B03221013 \
  --fastq_fn4=/app/input/2407B03221014 \
  --sample_ID1="HG002" \
  --sample_ID2="UHRR" \
  --sample_ID3="Ecoli" \
  --sample_ID4="HPV11" \
  --output_dir=/app/output \
  --output_fn="2407B032210.txt" \
  --threads=20 

# HG002, UHRR and Ecoli (input fastq files)
docker run --rm \
  --user $(id -u):$(id -g) \
  -v /data/2407B03221011/2407B03221011.fastq.gz:/app/input/2407B03221011/2407B03221011.fastq.gz \
  -v /data/2407B03221012/2407B03221012.fastq.gz:/app/input/2407B03221012/2407B03221012.fastq.gz \
  -v /data/2407B03221013/2407B03221013.fastq.gz:/app/input/2407B03221013/2407B03221013.fastq.gz \
  -v /data/2407B03221013/2407B03221014.fastq.gz:/app/input/2407B03221013/2407B03221014.fastq.gz \
  -v /data/output/2407B032210:/app/output \
  wt02_human_ecoli:v1.0.2.0 \
  --fastq_fn1=/app/input/2407B03221011/2407B03221011.fastq.gz \
  --fastq_fn2=/app/input/2407B03221012/2407B03221012.fastq.gz \
  --fastq_fn3=/app/input/2407B03221013/2407B03221013.fastq.gz \
  --fastq_fn4=/app/input/2407B03221013/2407B03221014.fastq.gz \
  --sample_ID1="HG002" \
  --sample_ID2="UHRR" \
  --sample_ID3="Ecoli" \
  --sample_ID4="HPV11" \
  --output_dir=/app/output \
  --output_fn="2407B032210.txt" \
  --threads=20 
```



