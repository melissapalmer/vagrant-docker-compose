Vagrant.configure("2") do |config|
  
  config.vm.box = "ubuntu/xenial64"
  
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false
 
    # Customize the amount of memory on the VM:
    vb.memory = "1024"
    vb.cpus = "1"
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    
     vb.name = "docker_compose"
  end
  
  config.vm.network "forwarded_port", 
	guest: 8080, host: 8080
  config.vm.network "forwarded_port", 
	guest: 5433, host: 5433
	
  config.vm.network "public_network", bridge: "Intel(R) Dual Band Wireless-AC 7265"
  
  # Mount this folder as RO in the guest, since it contains secure stuff
  config.vm.synced_folder ".", "/vagrant", :mount_options => ["ro"]

  #To install, rebuild and run docker-compose on vagrant up
  config.vm.provision :docker 
  config.vm.provision :docker_compose, yml: "/vagrant/docker-compose.yml", rebuild: true, run: "always"
end