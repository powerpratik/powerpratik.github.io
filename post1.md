# Installing CEPH IN UBUNTU 20 LTS


## Step 1 Get your Nodes Ready
Installed Ubuntu 20 LTS(Focal Fossa Release) for 4 node architechture. In this case is the 4 VMS that run on a server.
Enable Bridge Adapter from the VM ware settings>network tab to let the VM to access internet via bridge network.
The information about ubuntu is as follows:-


- SERVER UBUNTU 
- NAME="Ubuntu"
- VERSION="20.04.4 LTS (Focal Fossa)"
- ID=ubuntu
- ID_LIKE=debian
- PRETTY_NAME="Ubuntu 20.04.4 LTS"
- VERSION_ID="20.04"
- HOME_URL="https://www.ubuntu.com/"
- SUPPORT_URL="https://help.ubuntu.com/"
- BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
- PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
- VERSION_CODENAME=focal
- UBUNTU_CODENAME=focal

## Step 2 Pre-Requisite Packages
### net-tools
By default ifconfig option is not available and net-tools installs network related tools that enables that.
	sudo apt install net-tools

### Open SSH Server
This will allow you to ssh into the differnt nodes(VM) from the server:
	sudo apt-get install openssh-server
Enable the ssh service by typing:
	sudo systemctl enable ssh
Start the ssh service by typing:
	sudo systemctl start ssh

#Enabling remote x11 forwarding to open applications remotely
This enables the remote execution of application and accessing ceph dashboard from remote server command line.
Under root privileges open /etc/ssh/sshd_config and uncomment the following lines if they are commented:

    X11Forwarding yes

    X11DisplayOffset 10

    X11UseLocalhost yes
And reboot

# Step 3 Preparing Cephadmin Side
- Ceph can be installed using one of the three methods:
- Ceph-deploy <br>
- Ceph-adm <br>
- Ansible <br>
- Manual installation  <br>

We are going with ceph-adm becuase the older method ceph-deploy is now deprecated according to redhat and Ansible and Manual Installation provides ceomplexity and need for handling many dependencies that might be missed  but cephadm which is a new tool and in official ceph docs, will automate some processes in bootstrap cluster phase to make it easier to deploy cluster.
## First we need curl in order to fetch the cephadm application

sudo apt install -y curl

sudo apt install -y cephadm
## Then we download the application and make it executable.
### *** Installation using repo ***
curl --silent --remote-name --location https://github.com/ceph/ceph/raw/pacific/src/cephadm/cephadm <br>

chmod +x cephadm

## CephAdm could be used to set which version we want to install. In this case we choose Pacific as this is the first version that has full support for cephadm install. We also will run the command to install the tooling locally.

sudo ./cephadm add-repo --release pacific
sudo ./cephadm install <br>

### *** Installation using apt install if the above method does not work***
sudo apt install -y cephadm

## Bootstraping a cluster means to install the packages required to run the cluster from this administration host. After that is done you will have a cluster with one host, not something you could run any services on but something that you could administrate and work with your cluster. Supplying the IP address is important for the cluster to know where to connect, when done you'll get an address, username and password to reach the administration GUI.

<tab> sudo cephadm bootstrap --mon-ip *ip* <br>
After bootstrap is done, the success message will give the link to open cephcli and also provide url and login credentials for ceph dashboard on the ceph admin node. Running
the link in the cephadmin browser gives access to ceph dashboard. Step 2 ensures that the ceph dashboard can be accessed via command line remotely.

#### ceph bootstrap logs ####
URL: https://cephadmin-VirtualBox:8443/<br>
	    User: admin<br>
	Password: eb9ovl7l0j <br>

You can access the Ceph CLI with: <br>

	sudo /usr/sbin/cephadm shell --fsid 1a3786f2-f704-11ec-9f0c-4322a9959107 -c /etc/ceph/ceph.conf -k /etc/ceph/ceph.client.admin.keyring


### After ceph has been bootstrapped, installing ceph-common and ceph-osd lets you execuite ceph based command directly in the terminal rather than going to the ceph CLI like ceph status.

sudo apt install ceph-common
sudo apt install ceph-osd

	

### Optional step: Create Password file in cephadmin node and save the ceph password for future use.
sudo nano password



# Step 4 Preparing Other Nodes: 
## Do the same for Ceph monitor node, cephosd1, cephosd2
Use sudo cat /etc/ceph/ceph.pub on cephadmin node to get the public key.<br>
Create a folder called .ssh and create authorized_keys files and copy the cephadmin public key to the file


## First, update your existing list of packages:

    sudo apt update

# For docker installation on Other nodes:
At this point docker is installed on cephadmin node but for ceph installation, docker needs to be present in all the other nodes too. check the full requirements for ceph here (https://docs.ceph.com/en/quincy/cephadm/install/#requirements)


## Next, install a few prerequisite packages which let apt use packages over HTTPS:

    sudo apt install apt-transport-https ca-certificates curl software-properties-common

## Then add the GPG key for the official Docker repository to your system:

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

## Add the Docker repository to APT sources:

    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"

This will also update our package database with the Docker packages from the newly added repo.

## Make sure you are about to install from the Docker repo instead of the default Ubuntu repo:

    apt-cache policy docker-ce

## Install necessary docker resources
sudo apt install -y docker-ce docker-ce-cli containerd.io

# Install lvm for adding drives in best way using lvm volumes
sudo apt install -y lvm2





## Note: Copy ceph-keyring and ceph-conf from cephadmin /etc/ceph/ if you cannot run ceph command on other nodes, this is because if you install ceph-common separately on other nodes, since the cephadm bootstrap only copies the container image to other nodes, the new tools is not added from admin node and needs to be manually added or copied from the cephadmin for the cephconf and keyring.


# Step 5 Adding Ceph hosts to the cluster
## To add ceph hosts to the cluster created in the bootstrap process using shell.
First be a root user in other nodes using sudo su - and create a dir called .ssh and create a file authorized_keys in which copy the content of /etc/ceph/ceph.pub from main cephadmin to other nodes. Once this has been done ceph admin can get access to install necessary images and dependencies on other nodes and add them to the cluster.
Finally, use " ceph orch host add hostname host_ip " to add hosts in the cluster. Once this is successful you can create OSDs from the dashboard or shell.

## Use ceph dashboard to create OSD
Make sure to have a seperate disk allocated to setup as OSD and follow the prompts in ceph dash board. On the left hand side, GOTO CLUSTER-> OSDs -> CREATE and follow the dialog box to create using dashboard.




# Step 6 Create RBD POOL and Rados Block Device
## Creating an rbd pool

First, we will create a pool to store the images we create later. We could supply placement groups and other information if needed.

	sudo ceph osd pool create rbdpool

## Next, we will initialize the pool so it will have the application of the rbd set. This command will add the meta required to host images.

	sudo rbd pool init rbdpool

## Creating an rbd image

Now the image needs to be created for the rbd pool, the disk image has various options that enables features like erasure coded pool support layering etc. Full list of features are:


    layering: layering support
    striping: striping v2 support
    exclusive-lock: exclusive locking support
    object-map: object map support (requires exclusive-lock)
    fast-diff: fast diff calculations (requires object-map)
    deep-flatten: snapshot flatten support
    journaling: journaled IO support (requires exclusive-lock)
    data-pool: erasure-coded pool support

The one that is most appropriate here is layering. Next, if not already mentioned in your configuration(/etc/ceph/ceph.conf), we could supply the monitor IP. Next, we could provide the key file if not present in the regular place. And lastly, we will add which pool to create the image.

sudo rbd create rbddevice --size 4096 --image-feature layering -m 192.168.6.43 -k /etc/ceph/ceph.client.admin.keyring -p rbdpool

## On the client, we can now map the drive. This command will use the same parameters with the addition of the client's name to connect.

	sudo rbd map rbddevice --name client.admin -m 192.168.6.43 -k /etc/ceph/ceph.client.admin.keyring -p rbdpool

## Next, we will create a filesystem on the image available as a device on your system under /dev/rdb, then there will be a directory with the name of your pool and lastly, the name of the image as a link to the rbd device created.

sudo mkfs.ext4 -m0 /dev/rbd/rbdpool/rbddevice

Lastly, mounting the device is just using the device and mounting to a mount-point exactly as typical mounting.

sudo mount /dev/rbd/rbdpool/rbddevice /mnt/rados-block-device

This will ensure that the rados block device is created and we can view that in the dashboard status too.

## Creating image and writing to the rbd can be done using python api provided in the docs too. (https://docs.ceph.com/en/latest/rbd/api/librbdpy/)

# Additional Errors and fixes
## Solving 1 daemons recently crahsed warning in cluster status.
ceph crash archive *id*

Get ID via sudo ceph crash ls


## Docker installation
Installing docker by adding the linux architecture based repository like: <br>
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

This results in failing to install docker on other nodes because docker might not be available for that particular release of OS. example ubuntu 22. Instead using the step 4 approach solves the release mismatch case for docker installation.

## if X11 forwarding is not working by making changes to /etc/ssh/sshd_config file
You can manually ssh into the node by providing -X parameter to ssh hostname@ip


