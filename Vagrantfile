nodes = [
  {
    :hostname => 'mgmt',
    :ram => 256,
    :ip => '10.0.0.10',
    :cpu_cap => 50,
    :cpu => 2,
    :gui => false,
    :box => 'ubuntu/trusty64',
  },
#  {
#    :hostname => 'httpd',
#    :ip => '10.0.0.20',
#    :ram => 1024,
#    :box => 'centos/7',
#    :cpu_cap => 50,
#    :ansible_provision => 'setup_ansible_script.yml',
#  },
]


Vagrant.configure("2") do |config|
  nodes.each do |node|
    config.vm.define node[:hostname] do |nodeconfig|
      if node.key?(:provision)
        nodeconfig.vm.provision "shell", path: node[:provision]
      end
      if node.key?(:ansible_provision)
        nodeconfig.vm.provision "ansible" do |ansible|
          ansible.playbook = node[:ansible_provision]
        end
      end
      if node.key?(:box_version)
        nodeconfig.vm.box_version = node[:box_version]
      end
      nodeconfig.vm.box = node[:box]
      nodeconfig.vm.hostname = node[:hostname] + ".box"
      nodeconfig.vm.network :private_network, ip: node[:ip]

      memory = node[:ram] ? node[:ram] : 256;
      cpu_cap = node[:cpu_cap] ? node[:cpu_cap] : 50;

      nodeconfig.vm.provider :virtualbox do |vb|
        vb.gui = node.fetch(:gui, false)
        vb.customize [
          "modifyvm", :id,
          "--cpuexecutioncap", cpu_cap.to_s,
          "--memory", memory.to_s,
          "--cpus", node.fetch(:cpu, 1),
        ]
      end
    end
  end
end
