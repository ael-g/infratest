# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  $dnsroot_private_ip = "192.168.10.254"

  config.vm.define "dnsroot" do |dnsroot|
    dnsroot.vm.box = "debian/jessie64"
    dnsroot.vm.network "private_network", ip:$dnsroot_private_ip 
    dnsroot.vm.provision  "file", 
                          source:"dnsroot/named.conf.local", 
                          destination:"/tmp/named.conf.local"
    dnsroot.vm.provision  "file", 
                          source:"dnsroot/db.omb.one", 
                          destination:"/tmp/db.omb.one"
    dnsroot.vm.provision "shell",
      inline:"apt-get install -y bind9 && 
              mv /tmp/named.conf.local /etc/bind/ &&
              mv /tmp/db.omb.one /etc/bind/ &&
              service bind9 restart
      "
  end

  config.vm.define "dns1" do |dns1|
    dns1.vm.box = "debian/jessie64"
    dns1.vm.network "private_network", ip: "192.168.10.1"
  end

  config.vm.define "dns2" do |dns2|
    dns2.vm.box = "debian/jessie64"
    dns2.vm.network "private_network", ip: "192.168.10.2"
  end

  config.vm.define "client1" do |client1|
    client1.vm.box = "debian/jessie64"
    client1.vm.network "private_network", ip: "192.168.10.100"
    client1.vm.provision "shell",
      inline:"echo nameserver "+$dnsroot_private_ip+" > /etc/resolv.conf"
  end
end
