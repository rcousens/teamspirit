# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "team-spirit-f21"
  config.vm.box_url = "build/virtualbox/vagrant/team-spirit-f21-x86_64.box"

  config.vm.network "forwarded_port", guest: 80, host:9980
  config.vm.network "forwarded_port", guest: 5432, host:9932
  
  config.vm.synced_folder "salt/roots/salt", "/srv/salt"
  config.vm.synced_folder "salt/roots/pillar", "/srv/pillar"
  config.vm.synced_folder "app", "/srv/www/ts.dev", type: "rsync", rsync__args: ["--verbose", "--archive", "--delete", "-z", "--copy-links", "-F"]

  config.vm.provider "virtualbox" do |v|
  	v.gui = true
  end
  
  config.vm.provision :salt do |salt|    
    salt.always_install = false
    salt.colorize = true
    salt.install_args = "v2015.2"
    salt.install_type = "git"    
    salt.log_level = "info"
    salt.minion_config = "salt/minion"
    salt.run_highstate = true
    salt.verbose = true
  end
end
