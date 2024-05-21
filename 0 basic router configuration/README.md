# Router configuration

## Router Base configuration (Router1) 

- hostname
  * Router1
- MOTD
  * this is bto's company switch, kindly Stay out!
- enable secret password
  * pass= ciscotest
- secure vty 0-4
  * pass= ciscotest
- domain name
  * beto.com
- no ip domain lookup
  * disable device address translation
- usuario y contraseña
  * user= beto
  * pass= ciscotest
- ssh version 2
- Secure console port
  * pass= ciscotest
- Service password encryption
  * encrypts all passwords

```
Router>ena
Router#config t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#hostname Router1
Router1(config)#banner motd #this is bto's company switch, kindly Stay out!#
Router1(config)#enable password ciscotest
Router1(config)#line vty 0 4
Router1(config-line)#login
% Login disabled on line 2, until 'password' is set
% Login disabled on line 3, until 'password' is set
% Login disabled on line 4, until 'password' is set
% Login disabled on line 5, until 'password' is set
% Login disabled on line 6, until 'password' is set
Router1(config-line)#password ciscotest
Router1(config-line)#exit
Router1(config)#ip domain name beto.com
Router1(config)#no ip domain-lookup
Router1(config)#username beto password ciscotest
Router1(config)#crypto key generate rsa
The name for the keys will be: Router1.beto.com
Choose the size of the key modulus in the range of 360 to 4096 for your
  General Purpose Keys. Choosing a key modulus greater than 512 may take
  a few minutes.

How many bits in the modulus [512]: 1024
% Generating 1024 bit RSA keys, keys will be non-exportable...[OK]

Router1(config)#ip ssh version 2
*Mar 1 0:31:7.142: %SSH-5-ENABLED: SSH 1.99 has been enabled
Router1(config)#line console 0
Router1(config-line)#password ciscotest
Router1(config-line)#login
Router1(config-line)#exit
Router1(config)#service password-encryption
Router1(config)#
```
***
# Loopback
***
logic interface in the router, could be used to test and manage a router device, ensures that at least one interface is available
```
router(config)# interface loopback (number)
router(config)#ip address 19.20.168.10 255.255.255.0 (could be any ip address)
```
***

