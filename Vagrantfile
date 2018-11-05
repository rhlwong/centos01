$samplescript = <<-SCRIPT
yum install -y docker
systemctl enable docker
systemctl start docker
SCRIPT
#
Vagrant.configure(2) do |config|
                   
  config.vm.define "DockerLab02" do |dockerLab02|
    dockerLab02.vm.box = "centos/7"
    dockerLab02.vm.hostname = "DockerLab02"
    dockerLab02.vm.network "private_network", type: "dhcp",
      virtualbox__vboxnet2: true,
      auto_config: false
  
    dockerLab02.vm.provision "shell", inline: $samplescript
#    dockerLab02.vm.synced_folder "src/", "/var/www/html", owner:"sysadmin", group:"sysadmin"
    dockerLab02.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
    end
    dockerLab02.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = "1"
    end
  end
end
