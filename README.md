
Particular Matter Forecast
 
PMF Documentation:

___

 
System Requirements:
 
1. CPU with AVX/AVX2 support 
2. GPU with CUDA support beneficial 
3. Linux operating system with GUI (Ubuntu 20.04) 
4. Internet connection
 
___
 
Configuration:
 
Install Docker
 
SET UP THE REPOSITORY Update the apt package index and install packages to allow apt to use a repository over HTTPS:
 
$ sudo apt-get update
 
$ sudo apt-get install apt-transport-https <br>
$ sudo apt-get install ca-certificates<br>
$ sudo apt-get install curl<br>
$ sudo apt-get install gnupg-agent<br>
$ sudo apt-get install software-properties-common<br>
 
Add Docker’s official GPG key:<br>
 
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
 
Use the following command to set up the stable repository.
 
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
 
$ sudo apt update
 
$ apt-cache policy docker-ce
 
Install Docker (Docker version 20.10.3): <br>
 $ sudo apt install docker-ce
 
Check if Docker installation worked: "Status Active" <br>
 $ sudo systemctl status docker
 
Run Docker test image to verify installation(might need root permissions)
 
$docker run hello-world
 
Install Docker Compose (version 1.26.0)
 
sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
 
Set user permissions
 
$ sudo chmod +x /usr/local/bin/docker-compose
 
Verify installation <br>
$ docker-compose --version
 
 ___
 
In your terminal switch to the folder "KafkaCluster", inside the "PMF_FINAL-main" repository. This folder  contains the docker-compose.yml file, with the configurations for Kafka Cluster.
 
$ cd home/ 'user'/'downloadLocation'/PMF_FINAL-main/KafkaCluster
 
Start Docker Container via Yaml-File, the Kafka Cluster is named "kafka-cluster" in the Yaml-File.
 
$ sudo docker-compose up kafka-cluster

This will download the required Docker-Image and start your Cluster
 
Wait 1-2 min for the cluster to start up
 
Access LensesIO-Webinterface via "127.0.0.1:3030" to monitor and check the status of your Kafka Cluster

Your Kafka Cluster should now be ready to use
 
Switch to a new terminal and leave the cluster running in the background

___
 
 Install Python and additional requirements needed to run the ML-model and Python Kafka Consumer
 
 ___
 
Check Python installation with: <br>
 $ python3 --version
 
Install Python if its not installed or is an older version than 3.6
 
$ sudo apt-get update <br>
$ sudo apt-get install python 3.8
 
Install pip3 ( version 20.0.2): 
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
 
4) Within the active environment we can install the required pip3 packages. You can check the versions of the packages with 
 $ pip show "seaborn/tensorflow-cpu....".
 
 This also shows you any required other pip3 packages for each individual package (should be installed by pip automatically, if not manually add them using the pip3 install command.)

 Install Seaborn (version 0.11.1): 
$ pip3 install seaborn 

Install Tensorflow (version 2.4.1):
$ pip3 install tensorflow-cpu 

Install Kafka-Python (version 2.0.2):
$ pip3 install kafka-python 

Install Xlrd (version 2.0.1):
$ pip3 install xlrd 

Install Xlutils (version 2.0.0):
$ pip3 install xlutils 



___

Launch the Kafka Producer and the Kafka Consumer to start making predictions:

___
 
We are now set to start the Kafka Producer to write messages to our topic. The topic name is specified in the producer.py file as well as the path to the json file containing the data. Currently the producer is producing to a topic "JSONFINA" (line 31 producer.send('JSONFINA'. data[index])). It is also possible to change the waiting time between messages at line 33 sleep(2), 2 means it is currently set to wait 2 seconds between every new message.
Start the producer located at the PMF_FINAL-main directory from within the virtual environment:
 
$ python3 producer.py
 
To confirm that the producer is working as intended confirm that your topic has been created in Apache Kafka using the webinterface at 127.0.0.1/3030/kafka-topics-ui/
 

The next step is to start our consumer who will consume from our topic "JSONFINA" and make predictions.
Start the consumer by opening a new terminal and starting the consumer.py from within the virtual environment.
 
1) lets activate our virtual environment in the PMF_FINAL-main directory
$ source PMF-venv/bin/activate
 
2) lets start our consumer
$ python3 consumer.py

The consumer is set to make 1600 predictions and makes one prediction every time there arrives a new message.
