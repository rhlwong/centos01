$samplescript = <<-SCRIPT
yum install -y docker
yum install -y epel-release
yum -y update
yum -y install python2-pip
pip install docker-py
systemctl enable docker
systemctl start docker
SCRIPT
#
Vagrant.configure(2) do |config|
                   
  config.vm.define "DockerWeb01" do |dockerweb01|
    dockerweb01.vm.box = "centos/7"
    dockerweb01.vm.hostname = "DockerWeb01"
    dockerweb01.vm.network "private_network", ip: "192.168.57.110", auto_config: false
#    dockerweb01.vm.provision "shell", inline: $samplescript
    dockerweb01.vm.provision "ansible" do |ansible|
      ansible.playbook = "webplay.yml"
    end
    dockerweb01.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = "1"
    end
  end

  config.vm.define "DockerWeb02" do |dockerweb02|
    dockerweb02.vm.box = "centos/7"
    dockerweb02.vm.hostname = "DockerWeb02"
    dockerweb02.vm.network "private_network", ip: "192.168.57.111", auto_config: false
    dockerweb02.vm.provision "shell", inline: $samplescript
    dockerweb02.vm.provision "ansible" do |ansible|
      ansible.playbook = "webplay.yml"
    end
    dockerweb02.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = "1"
    end
  end

  config.vm.define "DockerDB01" do |dockerdb01|
    dockerdb01.vm.box = "centos/7"
    dockerdb01.vm.hostname = "DockerDB01"
    dockerdb01.vm.network "private_network", ip: "192.168.57.120",  auto_config: false
    dockerdb01.vm.provision "shell", inline: $samplescript
    dockerdb01.vm.provision "ansible" do |ansible|
      ansible.playbook = "dbplay.yml"
    end
    dockerdb01.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = "1"
    end
  end

end
