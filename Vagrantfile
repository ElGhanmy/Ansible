Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: <<-SHELL
      apt-get update -y
      echo "192.168.56.10  ansible-master" >> /etc/hosts
      echo "192.168.56.11  worker-target01" >> /etc/hosts
      echo "192.168.56.12  worker-target02" >> /etc/hosts
  SHELL
  
  config.vm.define "ansible" do |ansible|
    ansible.vm.box = "bento/ubuntu-22.04"
    ansible.vm.hostname = "ansible-master"
    ansible.vm.network "private_network", ip: "192.168.56.10"
    ansible.vm.provider "virtualbox" do |vb|
        vb.memory = 4048
        vb.cpus = 2
      #  vb.gui = true
    end
    ansible.vm.provision "shell", inline: <<-SHELL
    sudo apt install ansible -y
SHELL
  end

  (1..3).each do |i|

  config.vm.define "target0#{i}" do |target|
    target.vm.box = "bento/ubuntu-22.04"
    target.vm.hostname = "worker-target0#{i}"
    target.vm.network "private_network", ip: "192.168.56.1#{i}"
    target.vm.provider "virtualbox" do |vb|
        vb.memory = 2048
        vb.cpus = 1
      #  vb.gui = true #Timed out while waiting for the machine to boot
    end
  end
  
  end
end

