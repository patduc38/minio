# minio installation and basic configuration on linux


## Installations

### Download an install the rpm 

mkdir mlflow; cd mlflow/

wget https://dl.min.io/server/minio/release/linux-amd64/archive/minio-20230324214123.0.0.x86_64.rpm -O minio.rpm

dnf install -y  minio.rpm

### Create data dir (+ one bucket) 

mkdir -p mlflow/data/mlflow-bucket/

### Start minio server  

nohup minio server ./data/ &

netstat -nlpa |grep 9000

### Download minio command line client 

curl https://dl.min.io/client/mc/release/linux-amd64/mc --create-dirs -o $HOME/minio-binaries/mc

chmod +x $HOME/minio-binaries/mc

export PATH=$PATH:$HOME/minio-binaries

### Create an alias (mycloud) to your local server

mc alias set mycloud http://127.0.0.1:9000

mc alias list

mc ls mycloud

### Create a new bucket 

mc mb mycloud/newb

### Copy a file in that bucket 

mc cp /tmp/toto mycloud/newb
