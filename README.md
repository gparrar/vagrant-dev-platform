# vagrant-mammuut-dev-platform
This repository contains all files to create a virtual machine with docker as development platform

## Usage

1. Clone the repository in a folder of your preference
2. Clone your project inside the folder _workspace_
3. Build the mammuut-listener-0.1-SNAPSHOT.jar package
4. Start the virtual machine by runnning `vagrant up` on the root of the project 
5. Enter the virtual machine by running  `vagrant ssh` on the root of the project
6. Start _spark docker container_ by running the following command:
`docker run -d -name spark-container -p 8088:8088 -p 8042:8042  -p 21160:21160 -v /home/docker/vagrant/workspace/mammuut-listener:/root/spark/bin/mammuut-listener/ -h sandbox sequenceiq/spark:1.5.1 -d`
_This process may take a while (Downloading 2GB)_
7. Submit the application by running the following command:
`spark-submit --class com.mammuut.ReceiverActor --master yarn-cluster --executor-memory 4G --total-executor-cores 4 /root/spark/bin/mammuut-listener/target/mammuut-listener-0.1-SNAPSHOT.jar 21160  600`
_Spark is expecting **mammuut-listener-0.1-SNAPSHOT.jar** to be in the **target** folder, make sure to build it before_

## Host Config
In your /etc/hosts file add _vagrant IP (192.168.70.249)_ as host 'sandbox' to make it easier to access your sandbox UI.

