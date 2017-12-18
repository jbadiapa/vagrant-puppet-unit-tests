# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "centos/7"

  config.vm.provider "virtualbox" do |v|
   v.memory = 2048
   v.cpus = 2
  end
  
  config.vm.provision "shell", inline: <<-SHELL
     yum install -y bundler git ruby
     yum install gcc-c++ patch readline readline-devel zlib zlib-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison iconv-devel sqlite-devel libyaml.x86_64 
     curl -L get.rvm.io > installer.sh
     sudo chmod 755 /home/vagrant/installer.sh
     sudo /home/vagrant/installer.sh
     sudo usermod -a -G rvm  vagrant
     su - 'vagrant' -c /bin/bash
     source /etc/profile.d/rvm.sh 
     su - 'vagrant' -c 'rvm install 2.1.8'
     su - 'vagrant' -c 'rvm use 2.1.8 --default'
     #ruby --version
     su - 'vagrant' -c 'gem install rake psych:2.2.4 rubygems-bundler'
     git clone https://github.com/openstack/puppet-tripleo.git
     su - 'vagrant' -c 'gem install bundler'
     cd puppet-tripleo
     sudo chown -R vagrant:vagrant /home/vagrant
  SHELL
  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    cd puppet-tripleo
    bundle install
    #bundle exec rake spec
  SHELL
  config.vm.define "puppet" do |puppet|
   puppet.vm.network "public_network", bridge: "enp0s31f6"
   puppet.vm.hostname = "puppet"
  end
end
