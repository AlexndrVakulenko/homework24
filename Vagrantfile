Vagrant.configure(2) do |config|
  config.vm.box = "centos/7"

 	config.vm.provision "shell", inline: <<-SHELL
	#      mkdir -p ~root/.ssh
  #        cp ~vagrant/.ssh/auth* ~root/.ssh
    repo_file=/etc/yum.repos.d/CentOS-Base.repo
    cp ${repo_file} ~/CentOS-Base.repo.backup
    sudo sed -i s/#baseurl/baseurl/ ${repo_file}
    sudo sed -i s/mirrorlist.centos.org/vault.centos.org/ ${repo_file}
    sudo sed -i s/mirror.centos.org/vault.centos.org/ ${repo_file}
    sudo yum clean all
    yum install -y  bind bind-utils ntp vim mc
  SHELL

  config.vm.provider "virtualbox" do |v|
	  v.memory = 256
  end

  config.vm.define "ns01" do |ns01|
    ns01.vm.network "private_network", ip: "192.168.50.10", virtualbox__intnet: "dns"
    ns01.vm.hostname = "ns01"
    ns01.vm.synced_folder ".", "/vagrant", disabled: true
  end

  config.vm.define "ns02" do |ns02|
    ns02.vm.network "private_network", ip: "192.168.50.11", virtualbox__intnet: "dns"
    ns02.vm.hostname = "ns02"
    ns02.vm.synced_folder ".", "/vagrant", disabled: true
  end

  config.vm.define "client" do |client|
    client.vm.network "private_network", ip: "192.168.50.15", virtualbox__intnet: "dns"
    client.vm.hostname = "client"
    client.vm.synced_folder ".", "/vagrant", disabled: true
  end

    config.vm.define "client2" do |client2|
    client2.vm.network "private_network", ip: "192.168.50.16", virtualbox__intnet: "dns"
    client2.vm.hostname = "client2"
    client2.vm.synced_folder ".", "/vagrant", disabled: true
  end 
  
end
