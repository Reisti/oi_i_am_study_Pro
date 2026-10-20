
R20#show running-config   
Building configuration...  
  
Current configuration : 1346 bytes  
!  
version 15.5  
service timestamps debug datetime msec  
service timestamps log datetime msec  
no service password-encryption  
!  
hostname R20  
!  
boot-start-marker  
boot-end-marker  
!  
enable secret 5 $1$oBo6$mK5XcRSS3nUYp0IsfnBTF/  
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
ip domain name R20.local  
ip cef    
no ipv6 cef  
!  
multilink bundle-name authenticated  
!  
cts logging verbose  
!  
username admin secret 5 $1$JRAk$Cw9cShZXwnv12wz2r9gO80  
!  
redundancy  
!  
ip ssh version 2  
!  
interface Loopback0  
 ip address 10.21.37.7 255.255.255.255  
!  
interface Ethernet0/0  
 no ip address  
!  
interface Ethernet0/0.102  
 encapsulation dot1Q 102  
 ip address 10.21.13.230 255.255.255.252  
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
 router-id 10.21.37.7  
 network 10.21.13.228 0.0.0.3 area 102  
 network 10.21.37.7 0.0.0.0 area 102  
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