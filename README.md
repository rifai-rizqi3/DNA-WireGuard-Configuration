# Simple-WireGuard-configuration

# Install Wireguard on all Machines
https://www.wireguard.com/install/

# Menyalakan VPN Service
```
  $ systemctl enable wg-quick@wg0.service
``` 
# Menonaktifkan VPN Service

  $ systemctl disabled wg-quick@wg0.service
  
# Status VPN Service

  $ systemctl status wg-quick@wg0.service

# Generete All Keys

  $ wg genkey > server_privatekey <br>
  $ wg pubkey < server_privatekey > server_publickey_client1 <br>
  $ wg pubkey < server_privatekey > server_publickey_client2 <br>
  $ wg genkey | tee client1_privatekey | wg pubkey > client1_publickey <br>
  $ wg genkey | tee client2_privatekey | wg pubkey > client2_publickey <br>

# Start

  $ wg-quick up wg0

# Stop 

  $ wg-quick down wg0

# Remove Client

  $ sudo wg set wg0 peer $1 remove <br>
  
  contoh : sudo wg set wg0 peer 192.168.1.3 remove
  
# Ubah client ke QR Code

  $ qrencode -t utf8 < android2.conf

# Check status

  $ wg show <br>
  interface: wg0 <br>
    public key: <SERVER PUBLIC KEY> <br>
    private key: (hidden) <br>
    listening port: 52820 <br>
    fwmark: 0xca6c <br><br>

  peer: <CLIENT 1 PUBLIC KEY> <br>
    endpoint: ... <br>
    allowed ips: 192.168.1.2/32 <br>
    latest handshake: 4 seconds ago <br>
    transfer: 21.11 KiB received, 38.92 KiB sent <br><br>

  peer: <CLIENT 2 PUBLIC KEY> <br>
    endpoint: ... <br>
    allowed ips: 192.168.1.3/32 <br>
    latest handshake: 9 seconds ago <br>
    transfer: 911.10 KiB received, 2.57 MiB sent <br>
  
# Adding Client (Sisi Client)
  
  [Interface] <br>
  ##PrivateKey Client <br>
  PrivateKey = AGQ842obGBgmDYJm2T4N0YLG1eEdUQB+Ci6CTK2Z4Eo= <br>
  ##IP Addres yang kosong di client <br>
  Address = 192.168.1.16/24 <br>
  DNS = 8.8.8.8,8.8.4.4 <br><br>

  [Peer] <br>
  #Public Key Server  <br>
  PublicKey = 96hfqF6QeUiTTjNaTu/mMg6FiqV4ZAzHxQStNdVb3DA= <br>
  AllowedIPs = 0.0.0.0/0, ::/0 <br>
  ##IP SERVER & PORT SERVER <br>
  Endpoint = 167.71.223.20:52820
  
 # Adding IP dan Public Key Client di Server
 
  $ wg set wg0 peer (Public Key Client) allowed-ips (IP yang kosong untuk Client) <br>

   contoh : wg set wg0 peer 9S9s5dEmRQDWK80kGSJA8Qc6m21dWrAM2HbJW3WR6SA= allowed-ips 192.168.1.16
   
 # Save Configuration
 
  $ sudo wg-quick save wg0
 
 
