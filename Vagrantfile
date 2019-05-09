Vagrant.configure("2") do |config|
  config.vm.define "redismaster" do |redismaster|
    # Box Settings
    redismaster.vm.box = "bento/ubuntu-16.04"
    redismaster.vm.hostname = "redismaster"

    # Provider Settings
    redismaster.vm.provider "virtualbox" do |vb|
      # Display the VirtualBox GUI when booting the machine
      vb.gui = false
      vb.name = "redismaster"
      # Customize the amount of memory on the VM:
      vb.memory = "2048"
    end
    redismaster.vm.network "private_network", ip: "192.168.32.232"
    redismaster.vm.provision "shell", path: "provision/bootstrap.sh", privileged: false
  end

  config.vm.define "redisslave1" do |redisslave1|
    # Box Settings
    redisslave1.vm.box = "bento/ubuntu-16.04"
    redisslave1.vm.hostname = "redisslave1"

    # Provider Settings
    redisslave1.vm.provider "virtualbox" do |vb|
      # Display the VirtualBox GUI when booting the machine
      vb.gui = false
      vb.name = "redisslave1"
      # Customize the amount of memory on the VM:
      vb.memory = "1024"
    end
    redisslave1.vm.network "private_network", ip: "192.168.32.233"
    redisslave1.vm.provision "shell", path: "provision/bootstrap.sh", privileged: false
  end

  config.vm.define "redisslave2" do |redisslave2|
    # Box Settings
    redisslave2.vm.box = "bento/ubuntu-16.04"
    redisslave2.vm.hostname = "redisslave2"

    # Provider Settings
    redisslave2.vm.provider "virtualbox" do |vb|
      # Display the VirtualBox GUI when booting the machine
      vb.gui = false
      vb.name = "redisslave2"
      # Customize the amount of memory on the VM:
      vb.memory = "1024"
    end
    redisslave2.vm.network "private_network", ip: "192.168.32.234"
    redisslave2.vm.provision "shell", path: "provision/bootstrap.sh", privileged: false
  end
end
