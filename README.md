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
# method 2： docker load (local installation network is not needed, but you should provide wt02_human_ecoli_v1.0.1.0.tar files)
docker load -i wt02_human_ecoli_v1.0.1.0.tar
```
## 3. software usage
```r
### Usage 
docker run wt02_human_ecoli:v1.0.1.0 --help
```
![image](https://github.com/user-attachments/assets/c0bf0b9c-0592-483d-bed2-2f6316ec32c3)

