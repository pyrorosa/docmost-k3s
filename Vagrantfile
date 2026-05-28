Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2204"
  config.ssh.insert_key = false

  config.vm.provider :libvirt do |libvirt|
    libvirt.memory = 4096
    libvirt.cpus = 2
    libvirt.disk_bus = "virtio"
    libvirt.nested = true
    libvirt.management_network_address = "192.168.123.0/24"
  end

  config.vm.define "k3s-runner" do |node|
    node.vm.hostname = "k3s-runner"
    node.vm.network :private_network, ip: "192.168.123.215"
    node.vm.synced_folder ".", "/vagrant", disabled: true

    node.vm.provision "shell", inline: <<-SHELL
      set -e
      apt-get update
      apt-get upgrade -y
      apt-get install -y curl wget git rsync openssh-server python3
    SHELL
  end
end