# all switches

en
conf t
enable secret class
no ip domain-lookup
line console 0
password cisco
login
line vty 0 15
password cisco
login
end
copy running-config startup-config

# Switch 1
conf t
vtp mode server
vtp domain Lab5
vtp password cisco
exit
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
