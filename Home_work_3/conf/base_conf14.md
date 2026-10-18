R14#show running-config    
Building configuration...  
  
Current configuration : 1920 bytes  
!  
! Last configuration change at 19:30:08 UTC Sun Oct 18 2026  
!  
version 15.5  
service timestamps debug datetime msec  
service timestamps log datetime msec  
no service password-encryption  
!  
hostname R14  
!  
boot-start-marker  
boot-end-marker  
!  
enable secret 5 $1$oYVA$kJzY/e2eF6mqNw/lvbQG8.  
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
ip domain name R14.local  
ip cef  
no ipv6 cef  
!  
multilink bundle-name authenticated  
!  
cts logging verbose  
!  
username admin secret 5 $1$Z5U7$fgM/OCyZdR/z1zGoF0bTe/  
!  
redundancy  
!  
ip ssh version 2  
!  
interface Loopback0  
 description Management Loopback Interface  
 ip address 10.21.37.4 255.255.255.255  
!  
interface Ethernet0/0  
 no ip address  
!  
interface Ethernet0/0.22  
 encapsulation dot1Q 22  
 ip address 10.21.3.4 255.255.255.128  
!  
interface Ethernet0/1  
 no ip address  
!  
interface Ethernet0/1.23  
 encapsulation dot1Q 23  
 ip address 10.21.7.4 255.255.255.128  
!  
interface Ethernet0/2  
 no ip address  
!  
interface Ethernet0/2.21  
 encapsulation dot1Q 21  
 ip address 10.21.73.4 255.255.255.128  
!  
interface Ethernet0/3  
 no ip address  
!  
interface Ethernet0/3.101  
 encapsulation dot1Q 101  
 ip address 10.21.101.4 255.255.255.128  
!  
router ospf 1  
 router-id 10.21.37.4  
 area 101 stub no-summary  
 network 10.21.3.0 0.0.0.127 area 10  
 network 10.21.7.0 0.0.0.127 area 10  
 network 10.21.37.4 0.0.0.0 area 0  
 network 10.21.73.0 0.0.0.127 area 0  
 network 10.21.101.0 0.0.0.127 area 101  
 default-information originate always metric 10  
!  
ip forward-protocol nd  
!  
no ip http server    
no ip http secure-server 255.0 10.21.73.18  
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
!  
end  
  