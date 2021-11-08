
Vagrant.configure("2") do |config|

 config.vm.box = "ubuntu/xenial64"
# creating a virtual machine ubuntu 

# assign private ip to our VM
 config.vm.network "private_network", ip: "192.168.10.100" 

# ensure to install hostsupdater plugin on our localhost
 config.hostsupdater.aliases = ["development.local"]

end
