R28#show running-config  
Building configuration...  
  
Current configuration : 2653 bytes  
!  
version 15.5  
service timestamps debug datetime msec  
service timestamps log datetime msec  
no service password-encryption  
!  
hostname R28  
!  
boot-start-marker  
boot-end-marker  
!  
!  
enable secret 5 $1$9.7c$/UqDxWLDVFnD/Sm23TcED/  
!  
no aaa new-model  
!  
!  
!  
bsd-client server url https://cloudsso.cisco.com/as/token.oauth2  
mmi polling-interval 60  
no mmi auto-configure  
no mmi pvc  
mmi snmp-timeout 180  
!  
no ip domain lookup  
ip domain name R28.local  
ip cef  
no ipv6 cef  
!  
multilink bundle-name authenticated  
!  
cts logging verbose  
!  
!  
username admin secret 5 $1$jToS$KZuqxAJSCf3HTcxswFLvn1  
!  
redundancy  
!  
!  
track 1 ip sla 1 reachability  
!  
track 2 ip sla 2 reachability  
!  
interface Loopback0  
 ip address 10.21.37.12 255.255.255.255  
!  
interface Ethernet0/0  
 no ip address  
!  
interface Ethernet0/0.23  
 encapsulation dot1Q 23  
 ip address 10.21.7.12 255.255.255.128  
!  
interface Ethernet0/1  
 no ip address  
!  
interface Ethernet0/1.21  
 encapsulation dot1Q 21  
 ip address 10.21.73.12 255.255.255.128  
!  
interface Ethernet0/2  
 no ip address  
!  
interface Ethernet0/2.13  
 encapsulation dot1Q 13  
 ip address 10.2.4.1 255.255.255.128  
 ip policy route-map CHU  
!  
interface Ethernet0/2.37  
 encapsulation dot1Q 37  
 ip address 10.37.21.12 255.255.255.128  
!  
interface Ethernet0/2.777  
 encapsulation dot1Q 777 native  
!  
router ospf 1  
 router-id 10.21.37.12  
 network 10.21.3.0 0.0.0.127 area 0  
 network 10.21.7.0 0.0.0.127 area 0  
 network 10.21.37.12 0.0.0.0 area 0  
 network 10.21.73.0 0.0.0.127 area 0 
 network 10.37.21.0 0.0.0.127 area 0  
!  
ip forward-protocol nd  
!  
!  
no ip http server  
no ip http secure-server  
!  
ip access-list standard USER_CHU  
 permit 10.2.4.0 0.0.0.127  
!  
ip sla 1  
 icmp-echo 10.21.73.15 source-interface Ethernet0/1.21  
 threshold 1000  
 timeout 1000  
 frequency 5  
ip sla schedule 1 life forever start-time now   
ip sla 2  
 icmp-echo 10.21.7.16 source-interface Ethernet0/0.23  
 threshold 1000  
 timeout 1000  
 frequency 5  
ip sla schedule 2 life forever start-time now  
!  
route-map CHU permit 10  
 match ip address USER_CHU  
 match track  1  
 set ip next-hop 10.21.73.15  
!  
route-map CHU permit 20  
 description "main vlan23"  
 match ip address USER_CHU  
 set ip next-hop 10.21.7.16  
!  
route-map CHU permit 30  
 description "main other"  
!  
control-plane  
!  
line con 0  
 logging synchronous
 login local
line aux 0
 login local
line vty 0 4
 login local
 transport input ssh
!
!
end
