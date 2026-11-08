R32#show running-config     
Building configuration...    
    
Current configuration : 1805 bytes    
!    
! Last configuration change at 14:24:06 UTC Sun Nov 8 2026    
!    
version 15.5    
service timestamps debug datetime msec    
service timestamps log datetime msec    
no service password-encryption    
!    
hostname R32    
!    
boot-start-marker    
boot-end-marker    
!    
enable secret 5 $1$CyWV$vewzr0prvNvGvrnHMQLXQ/    
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
ip domain name R32.local    
ip cef    
no ipv6 cef    
!    
multilink bundle-name authenticated    
!    
cts logging verbose    
!    
username admin secret 5 $1$E6BB$tVnTeQX.xGrpcTZoulbxe0    
!    
redundancy    
!    
ip ssh version 2    
!    
interface Loopback0    
 ip address 10.21.37.11 255.255.255.255    
!    
interface Ethernet0/0    
 no ip address    
!    
interface Ethernet0/0.23    
 encapsulation dot1Q 23    
 ip address 10.21.14.68 255.255.255.248    
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
router eigrp SPB    
 !    
 address-family ipv4 unicast autonomous-system 2042    
  !    
  af-interface default    
   passive-interface    
  exit-af-interface    
  !    
  af-interface Ethernet0/0.23    
   no passive-interface    
  exit-af-interface    
  !    
  topology base    
   distribute-list prefix ONLY-DEFAULT in Ethernet0/0.23    
  exit-af-topology    
  network 10.21.14.64 0.0.0.7    
  network 10.21.37.11 0.0.0.0    
  eigrp router-id 10.21.37.11    
 exit-address-family    
!    
ip forward-protocol nd    
!    
no ip http server    
no ip http secure-server    
!    
ip prefix-list ONLY-DEFAUKT seq 5 permit 0.0.0.0/0    
!    
control-plane    
!    
banner motd ^C !!! Adeptus !!! ^C    
!    
line con 0    
 logging synchronous    
line aux 0    
line vty 0 4    
 login local    
 transport input ssh    
!    
end    