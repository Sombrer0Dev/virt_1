VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/jammy64"

  # Shared NFS folder from host
  config.vm.synced_folder "./shared", "/mnt/shared", type: "nfs"

  # Define 4 machines
  (1..4).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.hostname = "node#{i}"
      node.vm.provider "virtualbox" do |vb|
        vb.name = "debian-node#{i}"
        vb.memory = 512
        vb.cpus = 1
      end

      # File provisioner to copy a file from host to guest
      node.vm.provision "file", source: "./example.txt", destination: "/home/vagrant/example.txt"

      # Optional shell provisioner to confirm file presence (for debug)
      node.vm.provision "shell", inline: <<-SHELL
        echo "Provisioning node#{i}..."
        ls -l /home/vagrant/example.txt
        ls -ld /mnt/shared
      SHELL
    end
  end
end
