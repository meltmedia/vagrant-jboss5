# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "precise32"
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"

  config.vm.network :forwarded_port, guest: 8080, host: 8080

  config.vm.synced_folder "#{ENV['HOME']}/.m2/", "/usr/local/m2", id: "m2-repo"

  config.vm.provider :virtualbox do |vb|
  #   # Don't boot with headless mode
  #   vb.gui = true
  #
    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory", "2048", "--cpus", "2", "--ioapic", "on"]
  end



  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #
  config.vm.provision :chef_solo do |chef|
     chef.cookbooks_path = ["src/chef/cookbooks"]
     chef.add_recipe "apt"
     chef.add_recipe "vim"
     chef.add_recipe "maven"
     chef.add_recipe "activemq"
     chef.add_recipe "jboss5::server"

     chef.json = {
      "maven" =>  {
        "3" => {
          "url" => "http://apache.mirrors.tds.net/maven/maven-3/3.0.5/binaries/apache-maven-3.0.5-bin.tar.gz",
          "checksum" => "d98d766be9254222920c1d541efd466ae6502b82a39166c90d65ffd7ea357dd9"
        }, 
        "version" => 3
      }
    }
  end

end
