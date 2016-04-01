# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

servers=[
  {
    :hostname => "puppet-server",
    :box => "own-ubuntu",
    :ram => 1024,
    :cpu => 2,
    :setup => "setup-server.sh",
    :ip => "192.168.0.2"
  },
  {
    :hostname => "puppet-client1",
    :box => "own-ubuntu",
    :ram => 1024,
    :cpu => 2,
    :setup => "setup.sh",
    :ip => "192.168.0.3"
  },
  {
    :hostname => "puppet-client2",
    :box => "own-ubuntu",
    :ram => 1024,
    :cpu => 2,
    :setup => "setup.sh",
    :ip => "192.168.0.4"
  }

]

Vagrant.configure(2) do |config|
    servers.each do |machine|
        config.vm.define machine[:hostname] do |node|
            node.vm.box = machine[:box]
            node.vm.hostname = machine[:hostname]
	    node.vm.network "private_network", ip: machine[:ip]
            node.ssh.private_key_path = "/home/kornel/.ssh/vagrant/id_rsa"
	    node.vm.provision :shell, :path => machine[:setup]
#	    node.puppet_install.puppet_version = :latest
            node.vm.provider "virtualbox" do |vb|
                vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
	    end
	end
    end
end

