Vagrant.configure("2") do |config|

  config.vm.define "promtail-loki-ch" do |server|
    server.vm.box = "geerlingguy/ubuntu2004"
	server.vm.hostname = "promtail-loki-ch"
    server.vm.network "public_network", ip: "192.168.0.45"
	server.vm.provider "virtualbox" do |vb|
    	vb.memory = "8192"
		vb.cpus = "8"
    	vb.name = "promtail-loki-ch"
	end
	#ansible.vm.provision "shell", path: "userdata/ansible-setup.sh"
  end
end
