Particular Matter Forecast
 
PMF Documentation:

 
System Requirements:
 
-CPU with AVX/AVX2 support -GPU with CUDA support beneficial -Linux operating system with GUI (Ubuntu 20.04) -Internet connection
 
___
Contents:
 
Configuration:
 
Install Docker
 
SET UP THE REPOSITORY Update the apt package index and install packages to allow apt to use a repository over HTTPS:
 
$ sudo apt-get update
 
$ sudo apt-get install apt-transport-https
ca-certificates
curl
gnupg-agent
software-properties-common
 
Add Docker’s official GPG key:
 
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
 
Use the following command to set up the stable repository.
 
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
 
$ sudo apt update
 
$ apt-cache policy docker-ce
 
Install Docker $ sudo apt install docker-ce
 
Check if Docker installation worked: "Status Active" $ sudo systemctl status docker
 
Run Docker test image to verify installation
 
$docker run hello-world
 
Install Docker Compose
 
sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
 
Set user permissions
 
$ sudo chmod +x /usr/local/bin/docker-compose
 
Verify installation $ docker-compose --version
 
 
In your terminal switch to the folder "KafkaCluster", inside the "PMF_FINAL-main" repository. This folder  contains the docker-compose.yml file, with the configurations for Kafka Cluster.
 
$ cd home/<user>/<downloadLocation>/PMF_FINAL-main/KafkaCluster
 
Start Docker Container via Yaml-File, the Kafka Cluster is named kafka-cluster in the Yaml-File.
 
$ sudo docker-compose up kafka-cluster
 
Wait 1-2 min for the cluster to start up
 
Access LensesIO-Webinterface via "127.0.0.1:3030" to monitor and check the status of your Kafka Cluster
 
Switch to a new terminal and leave the cluster running in the background
 
Check Python installation with $ python3 --version
 
Install Python if its not installed or not version 3.6 or higher
 
$ sudo apt-get update $ sudo apt-get install python3.8
 
Install pip: 
$ sudo apt install python3-pip 
 
Check pip version: 
$ pip3 --version
 

Setting up the virtual environment: 
 
1) install python virtual environment
$ sudo apt install python3-venv
 
2) create a python virtual environment in the main directory of the repository (../PMF_FINAL-main) 
$ python3 -m venv PMF-venv 
 
3) activate the environment
$ source PMF-venv/bin/activate
 
4) Within the active environment we can innstall the required pip3 packages
 
$ pip3 install seaborn
$ pip3 install tensorflow-cpu
$ pip3 install kafka-python
$ pip3 install xlrd
$ pip3 install xlutils
 
We are now set to start the Kafka Producer to write messages to our topic. The topic name is specified in the producer.py file as well as the path to the json file containing the data. Currently the producer is producing to a topic "JSONFINA" (line 31 producer.send('JSONFINA'. data[index])). It is also possible to change the waiting time between messages at line 33 sleep(2), 2 means it is currently set to wait 2 seconds between every new message.
Start the producer located at the PMF_FINAL-main directory from within the virtual environment:
 
$ python3 producer.py
 
To confirm that the producer is working as intended confirm that your topic has been created using the webinterface at 127.0.0.1/3030/kafka-topics-ui/
 

The next step is to start our consumer who will consume from our topic "JSONFINA" and make predictions.
Start the consumer by opening a new terminal and starting the consumer.py from within the virtual environment.
 
1) lets activate our virtual environment in the PMF_FINAL-main directory
$ source PMF-venv/bin/activate
 
2) lets start our producer
$ python3 consumer.py
 
There are still a few warning but predictions are being made every time a new message arrives, after the initial first 48 messages.


