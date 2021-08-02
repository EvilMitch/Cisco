# ROUTER
###### Encapsulation is the key to making subinterfaces on a router, these are essentially vlans. 
int g0/0.5
encapsulation dot1q 5
ip address 5.5.5.10 255.255.255.0
int g0/0.10
encapsulation dot1q 10
ip address 192.168.10.1 255.255.255.0
int g0/0.11
encapsulation dot1q 11
ip address 11.11.11.1 255.255.255.0
int g0/0.18
encapsulation dot1q 18
ip address 18.18.18.1 255.255.255.0
!

###### Make sure the main port isn't shut
int g0/0
no shut
exit
!

###### Set the username and password for local account, then configure the Console and VTY ports.
username user password cisco99
line con 0
logging synchronous
login local
line vty 0 15
logging synchronous
login local
transport input telnet ssh
!

 # SWITCH 

###### Simple trunking on the correct interfaces
int range fa0/1-3
switchport mode trunk
!

###### Vlan management with names
vlan 5
name Management
vlan 10
name Admin
vlan 11
name Staff
vlan 18
name Students
!


### Save Config
###### Do this once you've confirmed the changes you've made are working.
wr
!

###### Again with the configuring of VTY lines 
username user password cisco99
line vty 0 15
transport input ssh telnet
login local
password cisco99
logging synchronous
exit
!

###### Not necessary all the time, puts a password on Priv Exe
enable secret cisco99
service password-encryption
exit
!

###### Sometimes a vlan might not want to show up, so we just kind of go into it to generate it again
vlan5
exit
!

###### Port security to stop unauthorised devices from connecting
switchport port-security mac-address sticky
exit
!