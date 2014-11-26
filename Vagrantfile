# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'

dir = File.dirname(File.expand_path(__FILE__))

configValues = YAML.load_file("#{dir}/config.yaml")
data         = configValues['config']

def which(cmd)
    exts = ENV['PATHEXT'] ? ENV['PATHEXT'].split(';') : ['']
    ENV['PATH'].split(File::PATH_SEPARATOR).each do |path|
        exts.each { |ext|
            exe = File.join(path, "#{cmd}#{ext}")
            return exe if File.executable? exe
        }
    end
    return nil
end

Vagrant.configure("2") do |config|

    config.vm.provider :virtualbox do |v|
        v.name = "#{data['name']}"
        v.customize ["modifyvm", :id, "--memory", "#{data['memory']}"]
    end

    config.vm.box = "ubuntu/trusty64"
    
    config.vm.network :private_network, ip: "#{data['private_network']}"
    config.ssh.forward_agent = true

    # Ansible provisioning
    if which('ansible-playbook')
        config.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible/playbook.yml"
            ansible.inventory_path = "ansible/inventories/dev"
            ansible.limit = 'all'
        end
    end

    config.vm.network :forwarded_port, guest: 22, host: "#{data['forwarded_port']}"

    config.vm.synced_folder "#{data['synced_folder']['source']}", "#{data['synced_folder']['destination']}", type: "nfs"
end
