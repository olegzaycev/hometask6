Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.provider "virtualbox" do |v|
    v.customize ["storagectl", :id, "--name", "SATA", "--add", "sata" ]

    Disks = [1,2,3,4]
    Disks.each do |hd|
        file_to_disk = "mydisk#{hd}.vmdk"    
        unless File.exist?(file_to_disk)
            v.customize [ "createmedium", "disk", "--filename", file_to_disk, "--format", "vmdk", "--size", 300]
        end
        v.customize [ "storageattach", :id, "--storagectl", "SATA", "--port", "#{hd}", "--device", "0", "--type", "hdd", "--medium", file_to_disk]
    end
  end
  
  config.vm.provision "shell", path: "provision.sh"
end