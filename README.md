# Práctica A: Servidor DHCP y NAT en Debian con Vagrant

Proyecto en **Windows 11** con **Vagrant** y **VirtualBox** para desplegar un servidor DHCP (`isc-dhcp-server`) y router NAT en Debian Bullseye que da servicio IP y salida a Internet a una red interna.

---

### 📐 Topología y Roles
* **`dhcp` (Servidor)**: Conectado a la red pública (`eth0`) y a la red interna `intnet` (`eth1`: `192.168.57.10/24`)[cite: 39, 40].
* **`c1` (Cliente Dinámico)**: Conectado a `intnet`, obtiene IP dinámica en el rango `192.168.57.20` – `192.168.57.50`[cite: 39, 41].
* **`printer` (Cliente Reserva)**: Conectado a `intnet` con MAC `08:00:27:11:22:33`, recibe la IP fija `192.168.57.111`[cite: 39, 44].

---

### ⚙️ Archivos de Configuración

* **`/etc/default/isc-dhcp-server`**: `INTERFACESv4="eth1"`[cite: 14]
* **`/etc/dhcp/dhcpd.conf`**:
  ```text
  default-lease-time 86400; max-lease-time 691200;
  option domain-name "christian.test"; option domain-name-servers 10.0.0.2, 4.4.4.4;
  authoritative;

  subnet 192.168.57.0 netmask 255.255.255.0 {
    range 192.168.57.20 192.168.57.50;
    option routers 192.168.57.10;
  }

  host printer {
    hardware ethernet 08:00:27:11:22:33;
    fixed-address 192.168.57.111;
    default-lease-time 7200;
  }
