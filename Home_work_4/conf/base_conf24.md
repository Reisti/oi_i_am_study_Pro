R24#show running-config     
Building configuration...   
   
Current configuration : 1960 bytes   
!   
! Last configuration change at 16:23:05 UTC Thu Oct 22 2026   
!   
version 15.5   
service timestamps debug datetime msec   
service timestamps log datetime msec   
no service password-encryption   
!   
hostname R24   
!   
boot-start-marker   
boot-end-marker   
!   
enable secret 5 $1$puz3$Pi0c/1DB1wmHCz9HE4SST/   
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
ip domain name R24.local   
ip cef   
no ipv6 cef   
!   
multilink bundle-name authenticated   
!   
cts logging verbose   
!   
username admin secret 5 $1$yOJI$GFTR9KZV52ZCuImKH2qNX1   
!   
redundancy   
!   
ip ssh version 2   
!   
interface Loopback0   
 ip address 10.21.37.14 255.255.255.255   
 ip router isis TRIADA   
!   
interface Ethernet0/0   
 no ip address   
!   
interface Ethernet0/0.23   
 encapsulation dot1Q 23   
 ip address 10.21.12.9 255.255.255.252   
 ip router isis TRIADA   
!   
interface Ethernet0/1   
 no ip address   
!   
interface Ethernet0/1.22   
 encapsulation dot1Q 22   
 ip address 10.21.16.21 255.255.255.252   
 ip router isis TRIADA   
!   
interface Ethernet0/2   
 no ip address   
!   
interface Ethernet0/2.21   
 encapsulation dot1Q 21   
 ip address 10.21.16.9 255.255.255.252   
 ip router isis TRIADA   
!   
interface Ethernet0/3   
 no ip address   
!   
interface Ethernet0/3.24   
 encapsulation dot1Q 24   
 ip address 10.21.16.13 255.255.255.252   
 ip router isis TRIADA   
!   
router isis TRIADA   
 net 49.0024.0100.2103.7014.00   
 is-type level-2-only   
 metric-style wide   
 log-adjacency-changes   
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