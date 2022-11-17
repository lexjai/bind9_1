# -- mode: ruby --
# vi: set ft=ruby :
BOX_IMAGE = "ubuntu/focal64"
DOMAIN = "aula104.local"
DNSIP = "192.168.1.12"
LAB = "bind9"

$dnsclient = <<-SHELL

  echo -e "nameserver $1\ndomain aula104.local">/etc/resolv.conf
SHELL


Vagrant.configure("2") do |config|
  # config general
  config.vm.box = BOX_IMAGE

  config.vm.provider "virtualbox" do |vb|
    vb.cpus = 1
    vb.memory = 1024
    vb.customize ["modifyvm", :id, "--groups", "/DNSLAB9"]
  end
 # nginx
  config.vm.define :dns do |guest|
    guest.vm.provider "virtualbox" do |vb, subconfig|
      vb.name = "nginx"
      subconfig.vm.hostname = "nginx.#{DOMAIN}"
      subconfig.vm.network :private_network, ip: DNSIP,  virtualboxintnet: LAB # ,  name: RED #
    end
    guest.vm.provision "shell", name: "nginx", path: "nginx.sh", args: DNSIP
  end



  # dns 
  config.vm.define :dns do |guest|
    guest.vm.provider "virtualbox" do |vb, subconfig| 
      vb.name = "dns"
      subconfig.vm.hostname = "dns.#{DOMAIN}"
      subconfig.vm.network :private_network, ip: DNSIP,  virtualboxintnet: LAB # ,  name: RED #
    end
    guest.vm.provision "shell", name: "dns-server", path: "enable-bind9.sh", args: DNSIP
  end


  # clients DHCP
  (1..1).each do |id|
    config.vm.define "client#{id}" do |guest|
      guest.vm.provider "virtualbox" do |vb, subconfig|
        vb.name = "client#{id}"
        subconfig.vm.hostname = "client#{id}.#{DOMAIN}"
console.loc(siccxp  )
        subconfig.vm.network :private_network, ip: "192.168.1.#{150+id}",  virtualboxintnet: LAB
      end
      guest.vm.provision "shell", name: "dns-client", inline: $dnsclient, args: DNSIP
      guest.vm.provision "shell", name: "testing", inline: <<-SHELL
        dig google.com +short
        dig -x 192.168.1.100 +short
        ping -a -c 1 apache1
        ping -a -c 1 apache2.aula104.local
        # curl apache1 --no-progress-meter 
        # curl apache2 --no-progress-meter 
        # curl nginx --no-progress-meter 
        ping -a -c 1 amazon.com
     
     

    Vagrantfile
    New
vagrant .congihure /0()
vagrant init obihann/nginx \
  --box-version 0.0.1
vagrant up

   ping -a -c 1 ns2
      SHELL
    end
  end

end