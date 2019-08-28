# -*- mode: ruby -*-
# vim: set ft=ruby :
# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
:inetrouter => {
        :box_name => "centos/7",
        #:public => {:ip => '10.10.10.1', :adapter => 1},
        :net => [
                   {adapter: 2, auto_config: false, virtualbox__intnet: "central"},
                   {adapter: 3, auto_config: false, virtualbox__intnet: "central"}
                ]
  },
  :centralrouter => {
        :box_name => "centos/7",
        :net => [
                   {adapter: 2, auto_config: false, virtualbox__intnet: "central"},
                   {adapter: 3, auto_config: false, virtualbox__intnet: "central"},
                   {adapter: 4, auto_config: false, virtualbox__intnet: "office1"},
                ]
  },
  :testserver1 => {
    :box_name => "centos/7",
    :net => [
                  {adapter: 2, auto_config: false, virtualbox__intnet: "office1"},
                ]
  },
  :testserver2 => {
    :box_name => "centos/7",
    :net => [
                  {adapter: 2, auto_config: false, virtualbox__intnet: "office1"},
            ]
},
:testclient1 => {
    :box_name => "centos/7",
    :net => [
                  {adapter: 2, auto_config: false, virtualbox__intnet: "office1"},
            ]
  }, 
  :testclient2 => {
    :box_name => "centos/7",
    :net => [
                  {adapter: 2, auto_config: false, virtualbox__intnet: "office1"},
            ]
},
  
}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|
    # config.vm.provider :kvm do |kvm, ov        when "centralServer"
    config.vm.define boxname do |box|
      
        box.vm.box = boxconfig[:box_name]
        box.vm.host_name = boxname.to_s

        boxconfig[:net].each do |ipconf|
          box.vm.network "private_network", ipconf
        end
        
        if boxconfig.key?(:public)
          box.vm.network "public_network", boxconfig[:public]
        end

        box.vm.provision "shell", inline: <<-SHELL
          mkdir -p ~root/.ssh
                cp ~vagrant/.ssh/auth* ~root/.ssh
        SHELL
        
        case boxname.to_s
        when "inetrouter"
          box.vm.provision "ansible_local" do |ansible|
            ansible.playbook = "playbook.yml"
          end
        when "centralrouter"
          box.vm.provision "ansible_local" do |ansible|
            ansible.playbook = "playbook.yml"
          end
        when "testserver1"
          box.vm.provision "ansible_local" do |ansible|
            ansible.playbook = "playbook.yml"
          end
        when "testserver2"
          box.vm.provision "ansible_local" do |ansible|
            ansible.playbook = "playbook.yml"
          end
        when "testclient1"
          box.vm.provision "ansible_local" do |ansible|
            ansible.playbook = "playbook.yml"
          end
        when "testclient2"
          box.vm.provision "ansible_local" do |ansible|
            ansible.playbook = "playbook.yml"
        end
      end

  end
end
end  


