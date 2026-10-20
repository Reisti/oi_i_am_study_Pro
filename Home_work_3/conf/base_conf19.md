R19#show running-config   
Building configuration...  
  
Current configuration : 1372 bytes  
!  
version 15.5  
service timestamps debug datetime msec  
service timestamps log datetime msec  
no service password-encryption  
!  
hostname R19  
!  
boot-start-marker  
boot-end-marker  
!  
enable secret 5 $1$ah6k$683xiQGMC7up5ry5D2rSU/  
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
ip domain name R19.local  
ip cef  
no ipv6 cef  
!  
multilink bundle-name authenticated  
!  
cts logging verbose  
!  
username admin secret 5 $1$KJCi$FvXM8h8lNIG/3XFmNoy5i/  
!  
redundancy  
!  
ip ssh version 2  
!  
interface Loopback0  
 ip address 10.21.37.6 255.255.255.255  
!  
interface Ethernet0/0  
 no ip address  
!  
interface Ethernet0/0.101  
 encapsulation dot1Q 101  
 ip address 10.21.13.226 255.255.255.252  
!  
interface Ethernet0/1  
 no ip address  
 shutdown  
!  
interface Ethernet0/2  
 no ip address  
 shutdown  
!  
interface Ethernet0/3  
 no ip address  
 shutdown  
!  
router ospf 1  
 router-id 10.21.37.6  
 area 101 stub no-summary  
 network 10.21.13.224 0.0.0.3 area 101  
 network 10.21.37.6 0.0.0.0 area 101  
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