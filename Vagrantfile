# -*- mode: ruby -*-

# Default box
box_name = "debian.jessie64.libvirt.box"

nodes = [
  { :hostname => "node-1", :ip => "192.168.0.1", :memory => 2048, :cpus => 2 },
]


Vagrant.configure("2") do |config|

  # Nodes configs
  nodes.each_with_index do |node, i|
    config.vm.box_check_update = false
    config.vm.define "node-#{ i+1 }" do |nodeconfig|

      # Default box-name (cause I have only it)
      nodeconfig.vm.box = box_name

      # Hostname: slave-N
      nodeconfig.vm.hostname = "node-#{ i+1 }"

      # IP-address: 192.168.1.{N+2}, started at 192.168.1.2
      nodeconfig.vm.network :private_network, ip: "192.168.1.#{ i+2 }"
      # nodeconfig.vm.provision "shell", inline: $distcc_install
      # nodeconfig.vm.provision "file", source: "./compile", destination: "~/compile"
      nodeconfig.vm.provider :libvirt do |vb|
        vb.memory = node[:memory]
        vb.cpus   = node[:cpus]
      end
    end
  end
end
