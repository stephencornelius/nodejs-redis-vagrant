# nodejs-redis-vagrant
A vagrant development environment with the most recent versions of NodeJS and Redis installed

### Setup & Installation

I recommend installing the vbguest plugin. This plugin installs the correct version of VirtualBox Guest Additions into the vagrant box so you dont have to worry about it.

```
vagrant plugin install vagrant-vbguest
```

Clone this repository

```
git clone https://github.com/stephencornelius/nodejs-redis-vagrant.git
```

Included in the Vagrantfile but commented out is the option to mount a folder, you will likely want to mount your local development area into your Vagrant box so any changes you make on your local machine are picked up inside your Vagrant box for you to test.
Beware that as this is mounted folder if you delete any files when in the Vagrant box they will also be removed from your local machine (however you should be storing all development files in a git repository)

Remove the # from the following line and update "/development/folder" to the folder location on your local machine.
```
#bbs.vm.synced_folder "/development/folder", "/home/vagrant/dev"
```

As part of the setup process Development tools and some other useful packages such as Vim and HTOP are installed to assist with development. If not required they can be removed from the Vagrantfile
```
sudo yum -y groupinstall "Development Tools"
sudo yum -y install git nodejs vim htop
```

The localtime is set to UTC in the Vagrantfile, this can easily be changed. E.g. to change to GMT replace the following line:
```
sudo sudo ln -s /usr/share/zoneinfo/UTC /etc/localtime
```
With
```
sudo sudo ln -s /usr/share/zoneinfo/Europe/London /etc/localtime
```
If an alternative timezone is required there are a number of guides online of how this is done


### Running

Once this repository has been cloned and any changes you want to make have been made to the Vagrantfile (it is possible to run as is). Then simply run the following to bring up the Vagrant box:
```
vagrant up
```
Depending on the performance of your machine it will take between 5 - 15 minutes to download the base box and then install the additional packages. Once running use:
```
vagrant ssh
```
To ssh into the running box.

### Other
Any issues, questions or recommendations can be raised via the issue tracker


