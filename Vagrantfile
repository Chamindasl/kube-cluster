IMAGE_NAME = "ubuntu/bionic64"
N = 2

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    provisioner = Vagrant::Util::Platform.windows? ? :guest_ansible : :ansible

    config.vm.provider "virtualbox" do |v|
        v.memory = 1024
        v.cpus = 2
    end
      
    config.vm.define "km" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.network "private_network", ip: "192.168.50.10"
        master.vm.hostname = "km"
        master.vm.provision provisioner  do |ansible|
            ansible.playbook = "kubernetes-setup/master-playbook.yml"
            ansible.extra_vars = {
                node_ip: "192.168.50.10",
            }
        end
    end

    (1..N).each do |i|
        config.vm.define "kw#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "192.168.50.#{i * 10 + 10}"
            node.vm.hostname = "kw#{i}"
            node.vm.provision provisioner  do |ansible|
                ansible.playbook = "kubernetes-setup/woker-playbook.yml"
                ansible.extra_vars = {
                    node_ip: "192.168.50.#{i * 10 + 10}",
                }
            end
        end
	end
end

