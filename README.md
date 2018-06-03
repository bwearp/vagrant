# vagrant
minimal/centos7 box with ansible and f5-sdk installed

To use the box:

1. Install Virtualbox: https://www.virtualbox.org/wiki/Downloads
2. Install the Virtual Box Extension Pack - the download link is on the same page above.
3. Install Vagrant: https://www.vagrantup.com/downloads.html

Once vagrant is installed, create a folder on your local PC/MAC where you would like to download/store the Virtual Device image; and then in a command prompt cd to that folder.
You can now optionally install some vagrant plugins. On the command line run:

$ vagrant plugin install vagrant-vbguest

$ vagrant plugin install vagrant-rekey-ssh 

This can take a few minutes...

Once the optional plugins have installed, on the command line run the below

$ vagrant init bwearp/f5-ansible

This will create a Vagrantfile
To execute the Vagrantfile which will then download and start the Virtual Device:

$ vagrant up

Once it has downloaded and started, log in by typing:

$ vagrant ssh

Once you are logged onto the box, change to the root user by typing "su" and pressing enter. The password (if required) is "vagrant"

Now you are root, you will now need to create a root ssh-key pair, and then copy the public cert to BOTH the bigip devices in your HA pair:

$ ssh-keygen 

Accept the defaults. The ssh-key pair will be created
Copy the public cert to the BIG-IP devices

$ ssh-copy-id -i /root/.ssh/id_rsa.pub root@<bigip-management-ip>

Example:

$ ssh-copy-id -i /root/.ssh/id_rsa.pub root@192.168.1.203

Then cd to the /home/vagrant/f5-ansible folder and list the contents. The contents in that folder are also synced/accessible from your local PC in the folder you created above in which the vagrant box is stored.

From your local PC, edit the xlsx files to suit you environment, and then on the vagrant box execute the playbook as the root user:

$ ansible-playbook simple-ha-pair.yml

For additional info/notes please see:

https://github.com/bwearp/simple-ha-pair

https://github.com/bwearp/single-bigip
