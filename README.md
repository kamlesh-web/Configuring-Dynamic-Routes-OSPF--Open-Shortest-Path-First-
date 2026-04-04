## OSPF Network Topology

<img width="1366" height="768" alt="Coonfiguring OSPF Overview" src="https://github.com/user-attachments/assets/850709e8-a8ef-44ec-af82-511e9b3b9b64" />

---    
   
## Step by Step OSPF Configurations
    
    Router>
    Router>enable
    Router#
    Router#configure terminal
    Enter configuration commands, one per line.  End with CNTL/Z.
    Router(config)#
    Router(config)#hostname Router7
    Router7(config)#
    Router7(config)#enable secret CCNA
    Router7(config)#
    Router7(config)#interface loopback0
    
    Router7(config-if)#
    %LINK-3-UPDOWN: Interface Loopback0, changed state to down
    
    %LINEPROTO-5-UPDOWN: Line protocol on Interface Loopback0, changed state to up
    
    Router7(config-if)#ip address 7.7.7.7 255.255.255.255
    Router7(config-if)#
    Router7(config-if)#interface g0/0/0
    Router7(config-if)#
    Router7(config-if)#ip address 10.10.10.17 255.255.255.248
    Router7(config-if)#
    Router7(config-if)#no shutdown
    
    Router7(config-if)#
    %LINK-5-CHANGED: Interface GigabitEthernet0/0/0, changed state to up
    
    %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0, changed state to up
    
    Router7(config-if)#
    Router7(config-if)#interface g0/0/1
    Router7(config-if)#
    Router7(config-if)#ip address 192.168.4.254 255.255.255.0
    Router7(config-if)#
    Router7(config-if)#no shutdown
    
    Router7(config-if)#
    %LINK-5-CHANGED: Interface GigabitEthernet0/0/1, changed state to up
    
    %LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/1, changed state to up
    
    Router7(config-if)#exit
    Router7(config)#
    Router7(config)#router ospf 1
    Router7(config-router)#
    Router7(config-router)#network 10.10.10.0 0.0.0.31 area 2
    Router7(config-router)#
    04:23:05: %OSPF-5-ADJCHG: Process 1, Nbr 3.3.3.3 on GigabitEthernet0/0/0 from LOADING to FULL, Loading Done
    
    04:23:05: %OSPF-5-ADJCHG: Process 1, Nbr 6.6.6.6 on GigabitEthernet0/0/0 from LOADING to FULL, Loading Done
    Router7(config-router)#
    
    Router7(config-router)#
    Router7(config-router)#network 192.168.4.0 0.0.0.255 area 2
    Router7(config-router)#
    Router7(config-router)#auto-cost reference-bandwidth 100000
    % OSPF: Reference bandwidth is changed.
            Please ensure reference bandwidth is consistent across all routers.
    Router7(config-router)#
    Router7(config-router)#passive-interface g0/0/1
    Router7(config-router)#
    Router7(config-router)#do write
    Building configuration...
    [OK]
    Router7(config-router)#
    Router7(config-router)#end
    Router7#
    %SYS-5-CONFIG_I: Configured from console by console
    
    Router7#show ip ospf int br
    Interface     PID   Area                     IP Address/Mask          Cost  State  Nbrs F/C
    Gig0/0/1        1   2                    192.168.4.254/255.255.255.0   100   WAIT  0/0
    Gig0/0/0        1   2                    10.10.10.17/255.255.255.248   1000   BDR  0/0
    
    Router7#conf t
    Enter configuration commands, one per line.  End with CNTL/Z.
    Router7(config)#
    Router7(config)#router ospf 1
    Router7(config-router)#
    Router7(config-router)#end
    Router7#
    %SYS-5-CONFIG_I: Configured from console by console
    
    Router7#write
    Building configuration...
    [OK]
    Router7#
    Router7#show running-config | section ospf
    router ospf 1
     log-adjacency-changes
     passive-interface GigabitEthernet0/0/1
     auto-cost reference-bandwidth 100000
     network 10.10.10.0 0.0.0.31 area 2
     network 192.168.4.0 0.0.0.255 area 2
    Router7#
    Router7#
    Router7#show ip route
    Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
           D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
           N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
           E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
           i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
           * - candidate default, U - per-user static route, o - ODR
           P - periodic downloaded static route
    
    Gateway of last resort is 10.10.10.19 to network 0.0.0.0
    
         7.0.0.0/32 is subnetted, 1 subnets
    C       7.7.7.7/32 is directly connected, Loopback0
         10.0.0.0/8 is variably subnetted, 5 subnets, 3 masks
    O IA    10.10.10.0/29 [110/65966] via 10.10.10.19, 00:02:47, GigabitEthernet0/0/0
    O IA    10.10.10.8/30 [110/65866] via 10.10.10.19, 00:02:47, GigabitEthernet0/0/0
    O IA    10.10.10.12/30 [110/65766] via 10.10.10.19, 00:02:47, GigabitEthernet0/0/0
    C       10.10.10.16/29 is directly connected, GigabitEthernet0/0/0
    L       10.10.10.17/32 is directly connected, GigabitEthernet0/0/0
    O IA 192.168.1.0/24 [110/66066] via 10.10.10.19, 00:02:47, GigabitEthernet0/0/0
    O IA 192.168.2.0/24 [110/66066] via 10.10.10.19, 00:02:47, GigabitEthernet0/0/0
    O    192.168.3.0/24 [110/1100] via 10.10.10.18, 00:02:47, GigabitEthernet0/0/0
         192.168.4.0/24 is variably subnetted, 2 subnets, 2 masks
    C       192.168.4.0/24 is directly connected, GigabitEthernet0/0/1
    L       192.168.4.254/32 is directly connected, GigabitEthernet0/0/1
    O*E2 0.0.0.0/0 [110/1] via 10.10.10.19, 00:02:47, GigabitEthernet0/0/0
    
    Router7#
---
## OSPF Connectivity test
<img width="1366" height="768" alt="Coonfiguring OSPF PC2 Connectivity" src="https://github.com/user-attachments/assets/52f55821-cd67-4641-a07a-ab268c8fd2e9" />

