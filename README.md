# vagrant


#### Конфигурирование нескольких машин

Вариант 1

ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'

Vagrant.configure("2") do |config|
 
  config.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory=256
      vb.cpus=1
      vb.check_guest_additions=false
  config.vm.box_check_update=false
  config.vm.box="ubuntu/trusty64"
 end

(1..$mach_quant).each do |i|
    config.vm.define "node#{i}" do |node|
        node.vm.network "public_network", ip: "192.168.1.#{24+i}"
        node.vm.hostname = "node#{i}"
    end
end
  
end

![image](https://github.com/user-attachments/assets/37cd480b-cb27-44bd-ac51-6c997d7ac653)


Вариант 2

ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.box_check_update = false


  config.vm.define "dev" do |dev|
      dev.vm.network  "public_network", ip: "192.168.1.160"
      dev.vm.hostname = "dev"  
      dev.vm.provider "virtualbox" do |vb|
         vb.memory = "4096"
      end
  end

  
 config.vm.define "db" do |db|
     db.vm.network "public_network", ip: "192.168.1.161"
     db.vm.hostname = "db"  
     db.vm.provider "virtualbox" do |vb|
         vb.memory = "1024"
     end
 end


 config.vm.define "ci" do |ci|
     ci.vm.network "public_network", ip: "192.168.1.162"
     ci.vm.hostname = "ci"  
     ci.vm.provider "virtualbox" do |vb|
         vb.memory = "2048"
     end
 end

 config.vm.define "lamp_node" do |lamp|
     lamp.vm.network "public_network", ip: "192.168.1.163"
     lamp.vm.hostname = "lamp_node"  
     lamp.vm.provider "virtualbox" do |vb|
         vb.memory = "512"
     end
 end

end

![image](https://github.com/user-attachments/assets/c70f7675-8481-4c97-8daf-870feeed5972)


#### Дополнительные материалы

https://help.ubuntu.ru/wiki/vagrant
