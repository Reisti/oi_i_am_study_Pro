R17#show running-config     
Building configuration...     
     
Current configuration : 2556 bytes     
!     
! Last configuration change at 14:18:57 UTC Sun Nov 8 2026     
!     
version 15.5     
service timestamps debug datetime msec     
service timestamps log datetime msec     
no service password-encryption     
!     
hostname R17     
!     
boot-start-marker     
boot-end-marker     
!     
enable secret 5 $1$3o.a$LtgV7GkSRoIS7ONgXtJ6i0     
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
ip domain name R17.local     
ip cef     
no ipv6 cef     
!     
multilink bundle-name authenticated     
!     
cts logging verbose     
!     
username admin secret 5 $1$uUMS$h/nG9ljkoJeQ2LYODaa410     
!     
redundancy     
!     
ip ssh version 2     
!     
interface Loopback0     
 ip address 10.21.37.9 255.255.255.255     
!     
interface Ethernet0/0     
 no ip address     
!     
interface Ethernet0/0.24     
 encapsulation dot1Q 24     
 ip address 10.21.14.194 255.255.255.248     
!     
interface Ethernet0/1     
 no ip address     
!     
interface Ethernet0/1.23     
 encapsulation dot1Q 23     
 ip address 10.21.14.66 255.255.255.248     
!     
interface Ethernet0/2     
 no ip address     
!     
interface Ethernet0/2.12     
 encapsulation dot1Q 12     
 ip address 10.21.144.34 255.255.255.192     
!     
interface Ethernet0/2.21     
 encapsulation dot1Q 21     
 ip address 10.21.14.2 255.255.255.248     
!     
interface Ethernet0/3     
 no ip address     
!     
router eigrp SPB     
 !     
 address-family ipv4 unicast autonomous-system 2042     
  !     
  af-interface default     
   passive-interface     
  exit-af-interface     
  !     
  af-interface Ethernet0/0.24     
   summary-address 10.21.14.0 255.255.255.0     
   summary-address 10.21.37.0 255.255.255.0     
   no passive-interface     
  exit-af-interface     
  !     
  af-interface Ethernet0/1.23     
   summary-address 10.21.14.0 255.255.255.0     
   summary-address 10.21.37.0 255.255.255.0     
   no passive-interface     
  exit-af-interface     
  !     
  af-interface Ethernet0/2.12     
   summary-address 10.21.37.0 255.255.255.0     
   summary-address 10.21.144.0 255.255.255.0     
   no passive-interface     
  exit-af-interface     
  !     
  af-interface Ethernet0/2.21     
   summary-address 10.21.14.0 255.255.255.0     
   summary-address 10.21.37.0 255.255.255.0     
   no passive-interface     
  exit-af-interface     
  !     
  topology base     
  exit-af-topology     
  network 10.21.14.0 0.0.0.255     
  network 10.21.37.9 0.0.0.0     
  network 10.21.144.0 0.0.0.255     
  eigrp router-id 10.21.37.9     
 exit-address-family     
!     
ip forward-protocol nd     
!     
no ip http server     
no ip http secure-server     
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