# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  $nsroot_private_ip = "192.168.10.254"

  config.vm.define "nsroot" do |nsroot|
    nsroot.vm.box = "debian/jessie64"
    nsroot.vm.network "private_network", ip:$nsroot_private_ip 
    nsroot.vm.provision  "file", 
                          source:"nsroot/named.conf.local", 
                          destination:"/tmp/named.conf.local"
    nsroot.vm.provision  "file", 
                          source:"nsroot/db.omb.one", 
                          destination:"/tmp/db.omb.one"
    nsroot.vm.provision "shell",
      inline:"apt-get install -y bind9 && 
              mv /tmp/named.conf.local /etc/bind/ &&
              mv /tmp/db.omb.one /etc/bind/ &&
              service bind9 restart
      "
  end

  config.vm.define "ns1" do |ns1|
    ns1.vm.box = "debian/jessie64"
    ns1.vm.network "private_network", ip: "192.168.10.10"
  end

  config.vm.define "ns2" do |ns2|
    ns2.vm.box = "debian/jessie64"
    ns2.vm.network "private_network", ip: "192.168.10.11"
  end

  config.vm.define "client1" do |client1|
    client1.vm.box = "debian/jessie64"
    client1.vm.network "private_network", ip: "192.168.10.100"
    client1.vm.provision "shell",
      inline:"echo nameserver "+$nsroot_private_ip+" > /etc/resolv.conf"
  end
end
