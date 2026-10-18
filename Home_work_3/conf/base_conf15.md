
R15#show running-config    
Building configuration...  
  
Current configuration : 1965 bytes  
!  
! Last configuration change at 19:12:03 UTC Sun Oct 18 2026  
!  
version 15.5  
service timestamps debug datetime msec  
service timestamps log datetime msec  
no service password-encryption  
!  
hostname R15  
!  
boot-start-marker  
boot-end-marker  
!  
enable secret 5 $1$07ej$M7GHFv3h7TbZbkRVLsj130  
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
ip domain name R15.local  
ip cef  
no ipv6 cef  
!  
multilink bundle-name authenticated  
!  
cts logging verbose  
!  
username admin secret 5 $1$R7nM$nEcdmMTmYBG.plYFZUT3N1  
!  
redundancy  
!  
ip ssh version 2  
!  
interface Loopback1  
 ip address 10.21.37.5 255.255.255.255  
!  
interface Ethernet0/0  
 no ip address  
!  
interface Ethernet0/0.22  
 encapsulation dot1Q 22  
 ip address 10.21.3.5 255.255.255.128  
!  
interface Ethernet0/1  
 no ip address  
!  
interface Ethernet0/1.23  
 encapsulation dot1Q 23  
 ip address 10.21.7.5 255.255.255.128  
!  
interface Ethernet0/2  
 no ip address  
!  
interface Ethernet0/2.21  
 encapsulation dot1Q 21  
 ip address 10.21.73.5 255.255.255.128  
!  
interface Ethernet0/3  
 no ip address  
!  
interface Ethernet0/3.102  
 encapsulation dot1Q 102  
 ip address 10.21.102.5 255.255.255.128  
!  
router ospf 1  
 router-id 10.21.37.5  
 area 102 filter-list prefix BLOCK_AREA101 out  
 network 10.21.3.0 0.0.0.127 area 10  
 network 10.21.7.0 0.0.0.127 area 10  
 network 10.21.37.5 0.0.0.0 area 0  
 network 10.21.73.0 0.0.0.127 area 0  
 network 10.21.102.0 0.0.0.127 area 102  
 default-information originate always metric 10  
!  
ip forward-protocol nd  
!  
no ip http server  
no ip http secure-server  
!  
ip prefix-list BLOCK_AREA101 seq 5 deny 10.21.37.6/32  
ip prefix-list BLOCK_AREA101 seq 10 permit 0.0.0.0/0 le 32  
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

