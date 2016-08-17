# all switches

en
conf t
ip default-gateway 172.17.1.1
int vlan1
ip address 172.17.1.2 255.255.255.0
no ip address 10.0.0.1 255.255.255.0 secondary
exit


conf t
hostname switch1
ip domain-name website.be
crypto key generate rsa
2048
username switchadmin password cisco
enable secret class
no ip domain-lookup
line console 0
logging synchronous
login local
line vty 0 4
transport input ssh
login local
password cisco
exit
service password-encryption


copy running-config startup-config

# Switch 1
en
class
conf t
vtp mode server
vtp domain Lab5
vtp password cisco
int range fa0/1-5
switchport mode trunk
switchport trunk native vlan 99
no shutdown
exit
vlan 99
name management
vlan 10
name faculty-staff
vlan 20
name students
vlan 30
name guest
exit
int vlan99
ip address 172.17.99.11 255.255.255.0
exit
int range fa0/6-10
switchport access vlan 30
int range fa0/11-17
switchport access vlan 10
int range fa0/18-24
switchport access vlan 20
exit
spanning-tree vlan 99 priority 4096
exit

copy running-config startup-config

# Optional Switch 2

vtp mode client
vtp domain Lab5
vtp password cisco
end
int range fa0/1-5
switchport mode trunk
switchport trunk native vlan 99
no shut
int vlan99
ip address 172.17.99.12 255.255.255.0
end
copy running-config startup-config
