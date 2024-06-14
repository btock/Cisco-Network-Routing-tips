# Static Routing

Estas definen una ruta explícita entre dos dispositivos de red. A diferencia de los protocolos de routing dinámico, las rutas estáticas no se actualizan automáticamente y se deben reconfigurar de forma manual si se modifica la topología de la red

![static routing](https://github.com/btock/Cisco-Network-Routing-tips/assets/14008255/74c6c149-db63-44d5-b71e-663f03698669)

***
## Router 1 Configuration
***
```
Router>
Router>ena
Router#config t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#interface fa0/0
Router(config-if)#ip address 10.0.0.1 255.0.0.0
Router(config-if)#no shutdown
Router(config-if)#interface fa0/1
Router(config-if)#ip address 19.1.1.2 255.255.255.252
Router(config-if)#no shutdown
Router(config-if)#
%LINK-5-CHANGED: Interface FastEthernet0/0, changed state to up

%LINK-5-CHANGED: Interface FastEthernet0/1, changed state to up

Router(config-if)#
```
### Router 1 IP route Configuration
comand: Router(config)# ip route "destination_network" "subnet_mask" "ip_address_of_next_hop_neighbot"
```
Router(config)#ip route 192.168.1.0 255.255.255.0 19.1.1.1
Router(config)#ip route 172.16.0.0 255.255.0.0 19.1.1.1
Router(config)#
```
## Router 0 Configuration
***
```
Router#config t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#interface fa0/0
Router(config-if)#ip address 192.168.1.1 255.255.255.0
Router(config-if)#no shutdown
Router(config-if)#interface fa0/1
Router(config-if)#ip address 172.16.0.1 255.255.0.0
Router(config-if)#no shutdown
%LINK-5-CHANGED: Interface FastEthernet0/0, changed state to up

Router(config-if)#
%LINK-5-CHANGED: Interface FastEthernet0/1, changed state to up

Router(config-if)#exit
Router(config)#
```
### Router 1 IP route Configuration
```
Router(config)#ip route 10.0.0.0 255.0.0.0 19.1.1.2
Router(config)#
```
***
## Routing tables router 0 & 1
***
### Route 0
```
Router>
Router>sh ip route
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route

Gateway of last resort is not set

S    10.0.0.0/8 [1/0] via 19.1.1.2
     19.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C       19.0.0.0/8 is directly connected, FastEthernet1/0
L       19.1.1.1/32 is directly connected, FastEthernet1/0
     172.16.0.0/16 is variably subnetted, 2 subnets, 2 masks
C       172.16.0.0/16 is directly connected, FastEthernet0/1
L       172.16.0.1/32 is directly connected, FastEthernet0/1
     192.168.1.0/24 is variably subnetted, 2 subnets, 2 masks
C       192.168.1.0/24 is directly connected, FastEthernet0/0
L       192.168.1.1/32 is directly connected, FastEthernet0/0
```
### Route 1
```
Router>
Router>sh ip route
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route

Gateway of last resort is not set

     10.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C       10.0.0.0/8 is directly connected, FastEthernet0/0
L       10.0.0.1/32 is directly connected, FastEthernet0/0
     19.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C       19.1.1.0/30 is directly connected, FastEthernet0/1
L       19.1.1.2/32 is directly connected, FastEthernet0/1
S    172.16.0.0/16 [1/0] via 19.1.1.1
S    192.168.1.0/24 [1/0] via 19.1.1.1
```
## Connectivity test
***
