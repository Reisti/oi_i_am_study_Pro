R16#show running-config   
Building configuration...   
   
Current configuration : 2700 bytes   
!   
version 15.5   
service timestamps debug datetime msec   
service timestamps log datetime msec   
no service password-encryption   
!   
hostname R16   
!   
boot-start-marker   
boot-end-marker   
!   
enable secret 5 $1$tKhE$El9wptaek3ej.D2CQZLoe0   
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
ip domain name R16.local   
ip cef   
no ipv6 cef   
!   
multilink bundle-name authenticated   
!   
cts logging verbose   
!   
username admin secret 5 $1$vUaJ$V/CE0c64uES9PEvFO/wUG0   
!   
redundancy   
!   
ip ssh version 2   
!   
interface Loopback0   
 ip address 10.21.37.8 255.255.255.255   
!   
interface Ethernet0/0   
 no ip address   
!   
interface Ethernet0/0.21   
 encapsulation dot1Q 21   
 ip address 10.21.14.1 255.255.255.248   
!   
interface Ethernet0/1   
 no ip address   
!   
interface Ethernet0/1.22   
 encapsulation dot1Q 22   
 ip address 10.21.14.129 255.255.255.248   
!   
interface Ethernet0/2   
 no ip address   
!   
interface Ethernet0/2.12   
 encapsulation dot1Q 12   
 ip address 10.21.144.33 255.255.255.192   
!   
interface Ethernet0/2.24   
 encapsulation dot1Q 24   
 ip address 10.21.14.193 255.255.255.248   
!   
interface Ethernet0/3   
 no ip address   
!   
interface Ethernet0/3.23   
 encapsulation dot1Q 23   
 ip address 10.21.14.65 255.255.255.248   
!   
router eigrp SPB   
 !   
 address-family ipv4 unicast autonomous-system 2042   
  !   
  af-interface default   
   passive-interface   
  exit-af-interface   
  !   
  af-interface Ethernet0/0.21   
   summary-address 10.21.14.0 255.255.255.0   
   summary-address 10.21.37.0 255.255.255.0   
   no passive-interface   
  exit-af-interface   
  !   
  af-interface Ethernet0/1.22   
   summary-address 10.21.14.0 255.255.255.0   
   summary-address 10.21.37.0 255.255.255.0   
   no passive-interface   
  exit-af-interface   
  !   
  af-interface Ethernet0/2.24   
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
  af-interface Ethernet0/3.23   
   summary-address 0.0.0.0 0.0.0.0   
   no passive-interface   
  exit-af-interface   
  !   
  topology base   
  exit-af-topology   
  network 10.21.14.0 0.0.0.255   
  network 10.21.37.8 0.0.0.0   
  network 10.21.144.0 0.0.0.255   
  eigrp router-id 10.21.37.8   
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