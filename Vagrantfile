# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
Vagrant.configure("2") do |config|

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "centos/7"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine.
  config.vm.network "forwarded_port", guest: 8000, host: 8000

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Share an additional folder to the guest VM.
  # The first argument is the path on the host to the actual folder.
  # The second argument is the path on the guest to mount the folder. 
  #config.vm.synced_folder "./share"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  config.vm.provider "virtualbox" do |vb|
    vb.cpus = 1
    vb.memory = 4096
  end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available.
  config.vm.provision "shell", privileged: false, inline: <<-SHELL

    # install MISC
    echo -e "\n### install MISC ###"
    sudo yum install -y vim git wget zip unzip

    # install dotfiles
    echo -e "\n### install dotfiles ###"
    git clone https://github.com/doHub1/dotfiles.git
    cd dotfiles
    bash install.sh

    # install RUBY
    # Referenced "https://qiita.com/tisk_jdb/items/61025d32862555846865"
    echo -e "\n### install RUBY ###"
    cd
    sudo yum -y install git gcc openssl-devel readline-devel
    git clone git://github.com/sstephenson/rbenv.git .rbenv
    echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
    echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
    git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
    rbenv install 2.6.5
    rbenv global 2.6.5
    source .bash_profile
    ruby -v
    gem -v

  SHELL

end







