VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/jammy64"

  # Define 4 VMs
  (1..4).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.hostname = "node#{i}"

      node.vm.provider "virtualbox" do |vb|
        vb.name = "ubuntu-node#{i}"
        vb.memory = 512
        vb.cpus = 1
      end

      # Use rsync instead of NFS or VirtualBox
      node.vm.synced_folder "./shared", "/mnt/shared", type: "rsync"

      # Copy a file using file provisioner
      node.vm.provision "file", source: "./copied.txt", destination: "/home/vagrant/copied.txt"

      # Optional: confirm everything worked
      node.vm.provision "shell", inline: <<-SHELL
        echo "Provisioned node#{i}"
        ls -l /home/vagrant/example.txt
        ls -ld /mnt/shared
      SHELL
    end
  end
end
