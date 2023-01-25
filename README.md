# Simple-WireGuard-configuration

# Install Wireguard on all Machines
https://www.wireguard.com/install/

# Menyalakan VPN Service

  systemctl enable wg-quick@wg0.service
  
# Menonaktifkan VPN Service

  systemctl disabled wg-quick@wg0.service
  
# Status VPN Service

  systemctl status wg-quick@wg0.service

# Generete All Keys

$ wg genkey > server_privatekey
$ wg pubkey < server_privatekey > server_publickey_client1
$ wg pubkey < server_privatekey > server_publickey_client2
$ wg genkey | tee client1_privatekey | wg pubkey > client1_publickey
$ wg genkey | tee client2_privatekey | wg pubkey > client2_publickey

# Start

$ wg-quick up wg0

# Stop 

wg-quick down wg0

# Remove Client

  sudo wg set wg0 peer $1 remove
  
  contoh : sudo wg set wg0 peer 192.168.1.3 remove
  
# Ubah client ke QR Code

  qrencode -t utf8 < android2.conf

# Check status

$ wg show
interface: wg0
  public key: <SERVER PUBLIC KEY>
  private key: (hidden)
  listening port: 52820
  fwmark: 0xca6c

peer: <CLIENT 1 PUBLIC KEY>
  endpoint: ...
  allowed ips: 192.168.1.2/32
  latest handshake: 4 seconds ago
  transfer: 21.11 KiB received, 38.92 KiB sent

peer: <CLIENT 2 PUBLIC KEY>
  endpoint: ...
  allowed ips: 192.168.1.3/32
  latest handshake: 9 seconds ago
  transfer: 911.10 KiB received, 2.57 MiB sent
  
# Adding Client (Sisi Client)
  
  [Interface]
  ##PrivateKey Client
  PrivateKey = AGQ842obGBgmDYJm2T4N0YLG1eEdUQB+Ci6CTK2Z4Eo=
  ##IP Addres yang kosong di client
  Address = 192.168.1.16/24
  DNS = 8.8.8.8,8.8.4.4

  [Peer]
  #Public Key Server
  PublicKey = 96hfqF6QeUiTTjNaTu/mMg6FiqV4ZAzHxQStNdVb3DA=
  AllowedIPs = 0.0.0.0/0, ::/0
  ##IP SERVER & PORT SERVER
  Endpoint = 167.71.223.20:52820
  
 # Adding IP dan Public Key Client di Server
 
   wg set wg0 peer (Public Key Client) allowed-ips (IP yang kosong untuk Client)

   contoh : wg set wg0 peer 9S9s5dEmRQDWK80kGSJA8Qc6m21dWrAM2HbJW3WR6SA= allowed-ips 192.168.1.16
   
 # Save Configuration
 
    sudo wg-quick save wg0
 
 
