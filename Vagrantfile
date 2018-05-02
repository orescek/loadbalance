ENV["LC_ALL"] = "en_US.UTF-8"

DOMAIN = ".vat.si"
VAGARNT_DIST = "ubuntu/xenial64"

Vagrant.configure(2) do |config|
  config.ssh.forward_agent=true
  config.vm.define "ha", primary: true do |ha|
    
    ha.vm.box =  VAGARNT_DIST
    ha.vm.network "private_network", ip:"192.168.101.10"
    ha.vm.network "forwarded_port", guest: 8080, host: 8080, auto_correct: false
    ha.vm.hostname = "ha" + DOMAIN
    ha.vm.provision "shell" do |s|
      s.path = "run.sh"
    end
      
    ha.vm.provision "ansible" do |ansible|
      ansible.inventory_path="ansible/provision/inventory"
      ansible.playbook = "ansible/haproxy.yml"  
    end
  end
  
    
  config.vm.define "m1", primary: true do |m1|
    
    m1.vm.box =  VAGARNT_DIST
    m1.vm.network "private_network", ip:"192.168.101.12"
    m1.vm.hostname = "m1" + DOMAIN
    m1.vm.provision "shell" do |s|
      s.path = "run.sh"
    end
      
     m1.vm.provision "ansible" do |ansible|
      ansible.inventory_path="ansible/provision/inventory"
      ansible.playbook = "ansible/machine.yml"  
     end
  end


  config.vm.define "m2", primary: true do |m2|
    
    m2.vm.box =  VAGARNT_DIST
    m2.vm.network "private_network", ip:"192.168.101.13"
    m2.vm.hostname = "m2" + DOMAIN
    m2.vm.provision "shell" do |s|
      s.path = "run.sh"
    end
      
     m2.vm.provision "ansible" do |ansible|
      ansible.inventory_path="ansible/provision/inventory"
      ansible.playbook = "ansible/machine.yml"  
     end
  end

end
