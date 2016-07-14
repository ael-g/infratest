# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  $nsroot_private_ip = "192.168.10.254"

  ########## REGISTRAR NS ##########
  config.vm.define "nsroot" do |nsroot|
    nsroot.vm.box = "debian/jessie64"
    nsroot.vm.network "private_network", ip:$nsroot_private_ip 
    nsroot.vm.provision  "file", 
                          source:"nsroot/named.conf.local", 
                          destination:"/tmp/named.conf.local"
    nsroot.vm.provision  "file", 
                          source:"nsroot/db.one", 
                          destination:"/tmp/db.one"
    nsroot.vm.provision "shell",
      inline:"apt-get install -y bind9 && 
              mv /tmp/named.conf.local /etc/bind/ &&
              mv /tmp/db.one /etc/bind/ &&
              service bind9 restart
      "
  end


  ########## NAMESERVERS ##########
  config.vm.define "ns1" do |ns1|
    ns1.vm.box = "debian/jessie64"
    ns1.vm.network "private_network", ip: "192.168.10.10"
  end

  config.vm.define "ns2" do |ns2|
    ns2.vm.box = "debian/jessie64"
    ns2.vm.network "private_network", ip: "192.168.10.11"
  end


  ########## LOADBALANCERS ##########
  config.vm.define "lb1a" do |lb1a|
    lb1a.vm.box = "debian/jessie64"
    lb1a.vm.network "private_network", ip: "192.168.10.11"
  end

  config.vm.define "lb1b" do |lb1b|
    lb1b.vm.box = "debian/jessie64"
    lb1b.vm.network "private_network", ip: "192.168.10.11"
  end


  ########## BACKENDS ##########
  config.vm.define "back1a" do |back1a|
    back1a.vm.box = "debian/jessie64"
    back1a.vm.network "private_network", ip: "192.168.10.11"
  end

  config.vm.define "back1b" do |back1b|
    back1b.vm.box = "debian/jessie64"
    back1b.vm.network "private_network", ip: "192.168.10.11"
  end


  ########## CLIENTS ##########
  config.vm.define "client1" do |client1|
    client1.vm.box = "debian/jessie64"
    client1.vm.network "private_network", ip: "192.168.10.100"
    client1.vm.provision "shell",
      inline:"echo nameserver "+$nsroot_private_ip+" > /etc/resolv.conf"
  end
end
