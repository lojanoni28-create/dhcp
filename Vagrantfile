Vagrant.configure("2") do |config|
  # 1. SERVIDOR DHCP (dhcp)
  config.vm.define "server" do |srv|
    srv.vm.box = "debian/bullseye64"
    srv.vm.hostname = "dhcp"

    srv.vm.network "public_network", bridge: "Ethernet" #

    srv.vm.network "private_network",
      ip: "192.168.57.10",
      netmask: "255.255.255.0",
      virtualbox__intnet: "intnet" #[cite: 39, 40]
  end

  # 2. CLIENTE DINÁMICO (c1)
  config.vm.define "c1" do |client|
    client.vm.box = "debian/bullseye64"
    client.vm.hostname = "c1"

    client.vm.network "private_network",
      type: "dhcp",
      virtualbox__intnet: "intnet" #[cite: 39, 42]
  end

  # 3. CLIENTE RESERVA / IMPRESORA (printer)
  config.vm.define "printer" do |prn|
    prn.vm.box = "debian/bullseye64"
    prn.vm.hostname = "printer"

    prn.vm.network "private_network",
      mac: "080027112233",
      type: "dhcp",
      virtualbox__intnet: "intnet" #[cite: 39, 44]
  end
end