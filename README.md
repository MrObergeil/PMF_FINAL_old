# PMF_FINAL
Particular Matter Forecast


PMF Documentation



System Requirements:


-CPU with AVX/AVX2 support
-GPU with CUDA support beneficial
-Linux operating system with GUI (Ubuntu 20.04)
-Internet connection


Contents:






Configuration:

Install Docker

SET UP THE REPOSITORY
Update the apt package index and install packages to allow apt to use a repository over HTTPS:


$ sudo apt-get update


$ sudo apt-get install 
							apt-transport-https \
							ca-certificates \
							curl \
							gnupg-agent \
							software-properties-common


Add Docker’s official GPG key:

$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

Use the following command to set up the stable repository.

$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"


$ sudo apt update

$ apt-cache policy docker-ce

Install Docker
$ sudo apt install docker-ce

Check if Docker installation worked: "Status Active"
$ sudo systemctl status docker

Run Docker test image to verify installation

$docker run hello-world

Install Docker Compose

sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

Set user permissions

$ sudo chmod +x /usr/local/bin/docker-compose

Verify installation
$ docker-compose --version

Switch to folder containing the docker-compose.yml file

$ cd home/pmf/PMF/Kafka Cluster

Start Docker Container via Yaml-File

$ sudo docker-compose up kafka-cluster

Wait 1-2 min for the cluster to start up

Access LensesIO-Webinterface via "127.0.0.1:3030"


Switch to a new terminal and leave the cluster running in the background


Check Python installation with $ python3 --version


Install Python if its not installed or not version 3.6 or higher

$ sudo apt-get update
$ sudo apt-get install python3.8

Install pip
sudo apt install python3-pip
Check version
pip3 --version

Setting up the virtual environment:
$ sudo apt install python3-venv

$ python3 -m venv PMF-venv
$ source PMF-venv/bin/activate

Install required pip3 packages

$ pip3 install seaborn
$ pip3 install tensorflow-cpu
$ pip3 install kafka-python
$ pip3 install xlrd
$ pip3 install xlutils





Start Kafka-Producer via producer.py file


Start Kafka-Consumer via consumerfinal.py file

