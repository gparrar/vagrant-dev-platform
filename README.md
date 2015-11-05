# vagrant-mammuut-dev-platform
This repository contains all files to create a virtual machine with docker as development platform

## Usage

1. Clone the repository in a folder of your preference
2. Clone your project inside the folder _workspace_
3. Build the mammuut-listener-0.1-SNAPSHOT.jar package
4. Start the virtual machine by runnning `vagrant up` on the root of the project 
5. Enter the virtual machine by running  `vagrant ssh` on the root of the project
6. List running containers by running the following command `docker-compose ps`
7. Copy the ID of the container
8. Submit the application by running the following command:
`docker exec {CONTAINER ID} spark-submit --class com.mammuut.ReceiverActor --master yarn-cluster --executor-memory 4G --total-executor-cores 4 /root/spark/bin/mammuut-listener/target/mammuut-listener-0.1-SNAPSHOT.jar 21160  600`
_Spark is expecting **mammuut-listener-0.1-SNAPSHOT.jar** to be in the **target** folder, make sure to build it before_

## Host Config
In your /etc/hosts file add _vagrant IP (192.168.70.249)_ as host 'sandbox' to make it easier to access your sandbox UI.

### More commands
To stop all containers, from the virtual machine run `docker stop $(docker ps -a -q)`.

To stop the virtual machine, from the Host run `vagrant halt` in the root of the project.

## Updates
- Run Spark container automatically in detached mode to listen for applications.


