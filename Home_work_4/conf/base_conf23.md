
R12#show running-config   
Building configuration...  
  
Current configuration : 2026 bytes  
!  
version 15.5  
service timestamps debug datetime msec  
service timestamps log datetime msec  
no service password-encryption  
!  
hostname R12  
!  
boot-start-marker  
boot-end-marker  
!  
enable secret 5 $1$z4XV$uvbvyTosK6nnMoK.s0wxp/  
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
ip domain name r12.local  
ip cef  
no ipv6 cef  
!  
multilink bundle-name authenticated  
!  
cts logging verbose  
!  
username admin secret 5 $1$JG0e$8Ds1CSYWQeWpWkNWoyX7V/  
!  
redundancy  
!  
ip ssh version 2  
!  
interface Loopback0  
 ip address 10.21.37.2 255.255.255.255  
!  
interface Ethernet0/0  
 no ip address  
!  
interface Ethernet0/0.21  
 encapsulation dot1Q 21  
 ip address 10.21.13.241 255.255.255.252  
!  
interface Ethernet0/1  
 no ip address  
!  
interface Ethernet0/1.11  
 encapsulation dot1Q 11  
 ip address 10.21.13.193 255.255.255.224  
!  
interface Ethernet0/1.24  
 encapsulation dot1Q 24  
 ip address 10.21.13.129 255.255.255.192  
!  
interface Ethernet0/2  
 no ip address  
!  
interface Ethernet0/2.22  
 encapsulation dot1Q 22  
 ip address 10.21.13.1 255.255.255.192  
!  
interface Ethernet0/3  
 no ip address  
!  
interface Ethernet0/3.23  
 encapsulation dot1Q 23  
 ip address 10.21.13.65 255.255.255.192  
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
 router-id 10.21.37.2  
 network 10.21.13.0 0.0.0.63 area 10  
 network 10.21.13.64 0.0.0.63 area 10  
 network 10.21.13.128 0.0.0.63 area 10  
 network 10.21.13.192 0.0.0.31 area 10  
 network 10.21.13.240 0.0.0.3 area 10  
 network 10.21.37.2 0.0.0.0 area 10  
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