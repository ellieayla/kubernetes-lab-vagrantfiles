VAGRANTFILE_API_VERSION = "2"

nodes = [
  { hostname: 'controller-0', ip: '10.240.0.10', lanip: '192.168.1.200' },
  { hostname: 'controller-1', ip: '10.240.0.11', lanip: '192.168.1.201' },
  { hostname: 'controller-2', ip: '10.240.0.12', lanip: '192.168.1.202' },
  { hostname: 'worker-0', ip: '10.240.0.20', lanip: '192.168.1.210' },
  { hostname: 'worker-1', ip: '10.240.0.21', lanip: '192.168.1.211' },
  { hostname: 'worker-2', ip: '10.240.0.22', lanip: '192.168.1.212' }
]

#jumpbox = { hostname: 'jumpbox', ip: '10.240.0.254', lanip: '192.168.1.11'}

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  nodes.each do |node|
    config.vm.define node[:hostname] do |node_config|
      node_config.vm.hostname = node[:hostname]
      node_config.vm.network 'private_network', ip: node[:ip], netmask: '255.255.255.0'  # /24
      node_config.vm.network 'private_network', ip: node[:lanip], netmark: '255.255.255.0'
    end
  end  

  #config.vm.define "jumpbox" do |node|
  #  node.vm.hostname = jumpbox[:hostname]
  #  node.vm.network 'private_network', ip: jumpbox[:ip], netmask: '255.255.255.0' # /24
  #  node.vm.network "private_network", ip: jumpbox[:lanip], netmark: '255.255.255.0'
  #  #node.vm.box = 'generic/ubuntu1604'
  #end

  # Applicable to all configs defined above
  config.vm.synced_folder('.', '/vagrant', type: 'nfs', disabled: true) # to disable sync
  config.vm.box = 'generic/ubuntu1604'
  
  # Depends on plugin installation: vagrant plugin install vagrant-vmware-esxi
  config.vm.provider :vmware_esxi do |esxi|
    #
    #   Provider settings
    #
    esxi.esxi_hostname = '192.168.1.25'
    esxi.esxi_username = 'mgmt'
    esxi.esxi_password = 'somethingsecret'
    esxi.esxi_virtual_network = ['VM Network']
    esxi.guest_memsize = '2048'
    esxi.guest_numvcpus = '2'
    esxi.guest_username = 'ubuntu'
  end
  
  config.vm.post_up_message = 'SSH to nodes with username/password "vagrant"'
end