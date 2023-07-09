Vagrant.configure("2") do |config|
  
  config.vm.provider :libvirt do |libvirt|
    libvirt.driver = "kvm"
  end
  config.winrm.max_tries = 300 
  config.winrm.retry_delay = 2 #seconds. This is the defaul value and just here for documentation.


  # Windows VM configuration
  config.vm.define "windows" do |windows|
    windows.vm.box = "peru/windows-server-2019-standard-x64-eval"
    windows.vm.hostname = "windows"
    windows.vm.provider :libvirt do |libvirt|
      libvirt.memory = 2048
      libvirt.cpus = 2
    end
    windows.vm.network :private_network, ip: "192.168.33.20"
    windows.vm.network :forwarded_port, guest: 3389, host: 13389 # Port forwarding for port 80
    windows.vm.communicator = "winrm"
    windows.vm.guest = :windows
    #windows.vm.winrm_username = "vagrant"
    #windows.vm.winrm_password = "vagrant"
  end

  # Ubuntu VM configuration
  config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.box = "generic/ubuntu2204"
    ubuntu.vm.hostname = "ubuntu"
    ubuntu.vm.provider :libvirt do |libvirt|
      libvirt.memory = 2048
      libvirt.cpus = 2
    end
    ubuntu.vm.provision "shell", path: "guacamole_install.sh"
    ubuntu.vm.network :private_network, ip: "192.168.33.10"
    ubuntu.vm.network :forwarded_port, guest: 8080, host: 8080 # Port forwarding for port 80
  end

end
