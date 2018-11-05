$samplescript = <<-SCRIPT
yum install -y httpd
systemctl enable httpd
systemctl start httpd
SCRIPT
#
Vagrant.configure(2) do |config|
  config.vm.define "DockerLab02" do |DockerLab02|
    config.vm.box = "centos/7"
    config.vm.hostname = "DockerLab02"
    config.vm.network "private_network", type: "dhcp",
      virtualbox__vboxnet2: true,
      auto_config: false
  
    config.vm.provision "shell", inline: $samplescript
#    config.vm.synced_folder "src/", "/var/www/html", owner:"sysadmin", group:"sysadmin"
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
    end
    config.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = "1"
    end
  end
end
