Vagrant.configure("2") do |config|

  config.vm.define "box" do |box|
    box.vm.box = "centos/7"
    box.vm.hostname = 'node-redis'

    box.vm.network :private_network, ip: "192.168.56.101"

    #bbs.vm.synced_folder "/development/folder", "/home/vagrant/dev"

    box.vm.provision "shell", inline: $script

    box.ssh.forward_agent = true

    box.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "bbs"]
    end
  end

end

$script = <<SCRIPT
sudo curl --silent --location https://rpm.nodesource.com/setup_6.x | sudo bash -
sudo yum -y install epel-release
sudo yum -y --enablerepo=epel install jemalloc
# Install Redis RPM from: https://www.rpmfind.net/linux/rpm2html/search.php?query=redis
sudo rpm -Uvh ftp://195.220.108.108/linux/remi/enterprise/7/remi/x86_64/redis-3.2.1-1.el7.remi.x86_64.rpm
sudo rpm -Uhv http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el7.rf.x86_64.rpm
sudo yum -y groupinstall "Development Tools"
sudo yum -y install git nodejs vim htop wget
# Download Redis config file
sudo curl -o /etc/redis.conf https://gist.githubusercontent.com/stephencornelius/b32744ad3e6e9fadad1ab8485bf82e35/raw/4f636ec9c9724d7453d8d9943c4194b989b86aa4/redis.conf
sudo systemctl start redis.service
sudo systemctl enable redis.service
sudo rm /etc/localtime
sudo sudo ln -s /usr/share/zoneinfo/UTC /etc/localtime
SCRIPT
