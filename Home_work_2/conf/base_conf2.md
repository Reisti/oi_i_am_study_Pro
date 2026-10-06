R27#show running-config  
version 15.5  
service timestamps debug datetime msec  
service timestamps log datetime msec  
no service password-encryption  
!  
hostname R27  
!  
boot-start-marker  
boot-end-marker  
!  
!  
enable secret 5 $1$jnS.$8H1T/z1IfYZ3DZQF.epFk.  
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
ip domain name R27.local  
ip cef  
no ipv6 cef  
!  
multilink bundle-name authenticated  
!  
cts logging verbose  
!  
username admin secret 5 $1$XNhz$a.wA/6kAxlUf/5vAcslZW1  
!  
redundancy  
!  
ip ssh version 2  
!  
interface Loopback0  
 ip address 10.21.37.17 255.255.255.255  
!  
interface Ethernet0/0  
 no ip address  
!  
interface Ethernet0/0.23  
 encapsulation dot1Q 23  
 ip address 10.21.7.17 255.255.255.128  
!  
router ospf 1  
 router-id 10.21.37.17  
 network 10.21.7.0 0.0.0.127 area 0  
 network 10.21.37.17 0.0.0.0 area 0  
!  
ip forward-protocol nd  
!  
!  
no ip http server  
no ip http secure-server  
ip route 0.0.0.0 0.0.0.0 10.21.37.15  
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
end    