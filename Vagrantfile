# -*- mode: ruby -*-
# vi: set ft=ruby :

BOX_CHECK_UPDATE = false
SSH_INSERT_KEY = false
SSH_FORWARD_AGENT = true

NETWORK_PRIVATE_IP_PREFIX = "172.16.3."

# VirtualBox configuration options
VBOX_CONFIG = [
  { "--cpus" => "2" },
  { "--memory" => "256" },
  { "--natdnshostresolver1" => "on"}
]

boxes = [
  {
    :name => "centos-6",
    :box => "bento/centos-6.7",
    :vbox_config => VBOX_CONFIG,
    :private_ip => NETWORK_PRIVATE_IP_PREFIX + "10"
  },
  {
    :name => "centos-7",
    :box => "bento/centos-7.1",
    :vbox_config => VBOX_CONFIG,
    :private_ip => NETWORK_PRIVATE_IP_PREFIX + "11"
  },
  {
    :name => "ubuntu-12.04",
    :box => "bento/ubuntu-12.04",
    :vbox_config => VBOX_CONFIG,
    :private_ip => NETWORK_PRIVATE_IP_PREFIX + "12"
  },
  {
    :name => "ubuntu-14.04",
    :box => "bento/ubuntu-14.04",
    :vbox_config => VBOX_CONFIG,
    :private_ip => NETWORK_PRIVATE_IP_PREFIX + "13"
  }
]

Vagrant.configure(2) do |config|

  config.vm.box_check_update = BOX_CHECK_UPDATE
  config.ssh.insert_key = SSH_INSERT_KEY
  config.ssh.forward_agent = SSH_FORWARD_AGENT

  boxes.each do |box|
    config.vm.define box[:name] do |config|

      config.vm.box = box[:box]
      config.vm.hostname = box[:name]

      # VirtualBox customizations
      unless box[:vbox_config].nil?
        config.vm.provider "virtualbox" do |vb|
          box[:vbox_config].each do |hash|
            hash.each do |key, value|
                vb.customize ["modifyvm", :id, key, value]
            end
          end
        end
      end

      config.vm.network "private_network", ip: box[:private_ip]

      config.vm.provision "ansible" do |ansible|
        ansible.playbook = "playbook.yml"
      end

    end
  end

end
