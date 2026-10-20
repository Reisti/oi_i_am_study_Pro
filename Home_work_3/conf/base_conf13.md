
R13#show running-config    
Building configuration...  
  
Current configuration : 2026 bytes  
!  
version 15.5  
service timestamps debug datetime msec  
service timestamps log datetime msec  
no service password-encryption  
!  
hostname R13  
!  
boot-start-marker  
boot-end-marker  
!  
enable secret 5 $1$VHM1$u0.2ytUqkQ.EYrTwvkHcu/  
!  
no aaa new-model  
!  
bsd-client server url https://cloudsso.cisco.com/as/token.oauth2  
mmi polling-interval 60  
no mmi auto-configure  
no mmi pvc  
mmi snmp-timeout 180  
!  
no ip domain lookup  
ip domain name R13.local  
ip cef  
no ipv6 cef  
!  
multilink bundle-name authenticated  
!  
cts logging verbose  
!  
username admin secret 5 $1$0KsD$PoUBWKGkR8jxC5yJmhdKc1  
!  
redundancy  
!  
ip ssh version 2  
!  
interface Loopback0  
 ip address 10.21.37.3 255.255.255.255  
!  
interface Ethernet0/0  
 no ip address  
!  
interface Ethernet0/0.24  
 encapsulation dot1Q 24  
 ip address 10.21.13.130 255.255.255.192  
!  
interface Ethernet0/1  
 no ip address  
!  
interface Ethernet0/1.11  
 encapsulation dot1Q 11  
 ip address 10.21.13.194 255.255.255.224  
!  
interface Ethernet0/1.21  
 encapsulation dot1Q 21  
 ip address 10.21.13.245 255.255.255.252  
!  
interface Ethernet0/2  
 no ip address  
!  
interface Ethernet0/2.22  
 encapsulation dot1Q 22  
 ip address 10.21.13.2 255.255.255.192  
!  
interface Ethernet0/3  
 no ip address  
!  
interface Ethernet0/3.23  
 encapsulation dot1Q 23  
 ip address 10.21.13.66 255.255.255.192  
!  
interface Ethernet1/0  
 no ip address  
 shutdown  
!  
interface Ethernet1/1  
 no ip address  
 shutdown  
!  
interface Ethernet1/2  
 no ip address  
 shutdown  
!  
interface Ethernet1/3  
 no ip address  
 shutdown  
!  
router ospf 1  
 router-id 10.21.37.3  
 network 10.21.13.0 0.0.0.63 area 10  
 network 10.21.13.64 0.0.0.63 area 10  
 network 10.21.13.128 0.0.0.63 area 10  
 network 10.21.13.192 0.0.0.31 area 10  
 network 10.21.13.244 0.0.0.3 area 10  
 network 10.21.37.3 0.0.0.0 area 10  
!  
ip forward-protocol nd  
!  
no ip http server  
no ip http secure-server  
!  
control-plane  
!  
line con 0  
 logging synchronous  
line aux 0  
line vty 0 4  
 login local  
 transport input ssh  
!  
end  