
#### Follow the steps to get the started with DevOps basic environment setup for you


Download and Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads) depending on the type of OS you are using.


Also, Recommanded, if you are using Windows, use the [Cygwin](link-here) for Windows to get a bash like environment

# VAGRANT
Next Download and Install [Vagrant](https://www.vagrantup.com/downloads.html) from their official website depending on your OS


After completing the above, to check if Vagrant is installed successfully run command:
```
vargant --version
```
This should give the result of the version you have installed


Next, 
To create a new machine using vagrant you need to create a saperate directory for each of the machines. All the commands that you run on the machine are only going to affect the specific machine in that directory


Creating a new machine/box
```
mkdir ubuntu		# create a new directory for this
cd ubuntu 		# navigate to the directory
vagrant init bento/ubuntu-16.10 	# bento/ubuntu-16.10 is the vagrant box
``` 
This command is used to create a Vagrantfile inside that directory which will be the initialisation file for the machine

This file contains instructions that vagrant needs, for deploying the box

If the box is already deployed it will do nothing, else the new box will be downloaded from vagrant and start the machine

Press enter and the run the command
This box will be placed in ``/home/{username}/.vagrant.d/boxes``


```
vim Vagrantfile
```
Run this to view the file content
This file if modified correcly can do a lot of things we will see later below


```
vagrant up
```
This command will run the box and start the machine
First it will try to fetch the box from local machine if it exists else it will download the a fresh copy


```
vagrant ssh
```
To access the machine you need to use this command
This will create a secure connection with the machine 


```
df -h
```
Filesystem inside the machine


Now suppose if you want to transfer files from your host machine to this vagrant machine
Follow these steps


```
cd /vagrant

vim hello.txt 	# sample file to access the show how it works, enter a few thing inside it 

logout # Exit the machine
```


From the current folder where the machine is, you can ``ls -ltr`` to see the file you have created exists inside it

This can also be done the other way, create a new file and login to the machine find the file inside /vagrant folder

If you do not need file sharing at all you need to do is,
```
vim Vagrantfile # go line 46
```
Input the following:
```
config.vm.synced_folder "/vagrant", disabled: true
```
Save and quit the file


```
vagrant reload
```
Run this command after you have made the changes to the file


```
logout
```
This is to exit the machine

```
vagrant suspend
```
This command will stop the system temporarily


```
vagrant resume
```

This will take you the same state of the machine since the last suspend command


```
vagrant halt
```
This is shutting down of the machine

```
vagrant destory
```
This will delete the machine and all the things you have created also the file/folder that you have created


Consider you need to create multiple machine at a time, all you need to do is to add the machine details to the Vagrantfile giving each a name and all the settings you need for them

Find the file in source commit to check the file content
You run the file directly you will have those machines up and ready

Also you can also create a shell script file and run the same to get you the same output

Add this:
```
config.vm.provision "shell", path" "deployFileName.sh", priviledged: false
```


# DOCKER
#### Follow these steps to install Docker CE on Ubuntu:
```
sudo apt-get update

sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo apt-key fingerprint 0EBFCD88

sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

sudo apt-get update

# This will install docker community edition
sudo apt-get install docker-ce

# To check if docker is installed successfully
sudo docker run hello-world
```

<Br>
<Br>

<b> Starting with docker commands</b>
```
docker pull busybox
```
This command will only download an image file with the name "busybox" and not run it
Here this image file contains a set of per defined setup for running 
A basic linux kernel, tiny linux kernel with most basic linux functions

To run the pulled image:
```
docker run busybox
```
This command will also download if not already done and install the image of busybox


```
docker run --detach --name server busybox 
```
This will run the image in background
- 'detach' is used to run the container in background
- 'name' is used to give a user provided name for this image
- lastly the image name

If the name option is not provided docker will create name and a ID by default
```
docker ps
```

This command will give you all the running images
but after you run this command you will notice there are no images running
the images will run only if it has any process to keep it running else 
the image will stop running
for the image to keep running, use the following command

```
docker run --detach --name server busybox sh -c "while true; do sleep 5; done"
```
This command will keep the image to keep it running
It is just an infinite loop which will sleep for 5 seconds

<br>
Consider you have to access this container and view or run some commands on this container

```
docker run -itd --name server busybox
```
- 'itd' this option will make the container interactive
That is, you can issue commands to it

<br>
Suppose the container is stopped and not running:

```
docker start server
```
This will start the container


```
docker attach server
```
This command will give access to the command line of this container


```
docker restart server
```
This will restart the container


```
docker stop server
```
To stop the container named "server"


```
docker rm server
```
This delete the container "server" which was created before


# Ansible
#### Follow these steps carefully:
> These steps are for installing Ansible on a Ubuntu machine 

```
sudo apt-get update

sudo apt-get install software-properties-common

sudo apt-add-repository ppa:ansible/ansible

sudo apt-get update

sudo apt-get install ansible

ansible --version
```

<br>

#### If you wish to Install with the help of Python follow these steps

Verify that you have python installed:
```
python --version
```

We will install using pip:

> If you do not have pip installed already, use: `` sudo easy_install pip`` to install pip

<br>

```
pip install ansible
```
Simple as that
<br>
<br>



  
## Donation
If this page helps you reduce time to develop, you can give me a cup of coffee   :coffee:

[![paypal](https://cdn-images-1.medium.com/max/738/1*G95uyokAH4JC5Ppvx4LmoQ@2x.png)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=ZJM97M6KBLHZY)
