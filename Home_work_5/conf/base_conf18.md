
R18#show running-config    
Building configuration...    
    
Current configuration : 2017 bytes    
!    
! Last configuration change at 14:04:10 UTC Sun Nov 8 2026    
!    
version 15.5    
service timestamps debug datetime msec    
service timestamps log datetime msec    
no service password-encryption    
!    
hostname R18    
!    
boot-start-marker    
boot-end-marker    
!    
enable secret 5 $1$5tUn$jvIR2rEu11Fol0oyvIRyn0    
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
ip domain name R18.local    
ip cef    
no ipv6 cef    
!    
multilink bundle-name authenticated    
!    
cts logging verbose    
!    
username admin secret 5 $1$5Hgo$OPcWuy0wBPDtp0HKftPEr0    
!    
redundancy    
!    
ip ssh version 2    
!    
interface Loopback0    
 ip address 10.21.37.10 255.255.255.255    
!    
interface Ethernet0/0    
 no ip address    
!    
interface Ethernet0/0.22    
 encapsulation dot1Q 22    
 ip address 10.21.14.130 255.255.255.248    
!    
interface Ethernet0/1    
 no ip address    
!    
interface Ethernet0/1.23    
 encapsulation dot1Q 23    
 ip address 10.21.14.67 255.255.255.248    
!    
interface Ethernet0/2    
 no ip address    
!    
interface Ethernet0/2.24    
 encapsulation dot1Q 24    
 ip address 10.21.16.14 255.255.255.248    
!    
interface Ethernet0/3    
 no ip address    
!    
interface Ethernet0/3.21    
 encapsulation dot1Q 21    
 ip address 10.21.16.45 255.255.255.248    
!    
router eigrp SPB    
 !    
 address-family ipv4 unicast autonomous-system 2042    
  !    
  af-interface default    
   passive-interface    
  exit-af-interface    
  !    
  af-interface Ethernet0/0.22    
   no passive-interface    
  exit-af-interface    
  !    
  af-interface Ethernet0/1.23    
   no passive-interface    
  exit-af-interface    
  !    
  topology base    
  exit-af-topology    
  network 10.21.14.0 0.0.0.255    
  network 10.21.37.10 0.0.0.0    
  eigrp router-id 10.21.37.10    
 exit-address-family    
!    
ip forward-protocol nd    
!    
no ip http server    
no ip http secure-server    
!    
control-plane    
!    
banner motd ^C !!!Adeptus !!! ^C    
!    
line con 0    
 logging synchronous    
line aux 0    
line vty 0 4    
 login local    
 transport input ssh    
!    
end    
