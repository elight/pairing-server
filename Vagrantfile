# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    Vagrant.require_plugin "vagrant-rackspace"
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "dummy"
  config.vm.provider :rackspace do |rs|
    rs.username = ENV['RAX_USERNAME']
    rs.api_key  = ENV['RAX_API_KEY']
    rs.flavor   = /1 GB Performance/
    rs.image    = /Ubuntu/
    rs.server_name = "pairing2"
    rs.rackspace_region   = "IAD"
  end


  config.vm.provision "shell", inline: <<-SHELL
     sudo apt-get update
     sudo apt-get upgrade -y
     sudo add-apt-repository ppa:cassou/emacs
     sudo apt-get update
     sudo apt-get install emacs24
     sudo apt-get -y install build-essential ruby1.9.1 ruby1.9.1-dev libopenssl-ruby1.9.1 git libpq-dev curl
     sudo gem install bundler
     cd ~
     git clone git@github.com:elight/.emacs.d.git
     cd .emacs.d
     curl -fsSkL https://raw.github.com/cask/cask/master/go > cask_install.py
     python cask_install.py
     rm cask_install.py
     cd ~/.emacs.d
     cask
  SHELL
end
