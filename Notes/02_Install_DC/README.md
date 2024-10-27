# 02 Installing the Domain Controller

1) use 'sconfig' to :
    - Change hostname
    - Change IP to static 
    - Change DNS server to own IP

2) Install the Active Directory Windows Feature


# Shell Commands

1) Install-WindowsFeature AD-Domain-Services -IncludeManagementTools

2) Configure ADD Controller
    - import-Module ADDSDeployment
    - install-ADDSForest
    - Input 
        - DomainName: skogs.com
        - Password: ***********

# Change static IP

**Commands**
- Get-NetIPAddress -IPAddress '0.0.0.0' (Returns index of interface hosting the given IP)
- Get-NetIPInterface -InterfaceIndex # | Set-NetIPInterface -Dhcp D (Disable DHCP)

# Connecting to Domain Controller

- New-PSSession -ComputerName 192.168.13.155 -Credential (Get-Credential)

# Joinging computer to Domain


- Get-DnsClientServerAddress

`InterfaceAlias               Interface Address ServerAddresses`
`                             Index     Family`
`--------------               --------- ------- ---------------`
`Ethernet0                            4 IPv4    {127.0.0.1}`
`Ethernet0                            4 IPv6    {::1}`
`Loopback Pseudo-Interface 1          1 IPv4    {}`
`Loopback Pseudo-Interface 1          1 IPv6    {fec0:0:0:ffff::1, fec0:0:0:ffff::2, fec0:0:0:ffff::3}`

- Set-DnsClientServerAddress -interfaceindex 4 -ServerAddresses 192.168.13.155

`InterfaceAlias               Interface Address ServerAddresses`
`                             Index     Family`
`--------------               --------- ------- ---------------`
`Ethernet0                            4 IPv4    {192.168.13.155}`
`Ethernet0                            4 IPv6    {::1}`
`Loopback Pseudo-Interface 1          1 IPv4    {}`
`Loopback Pseudo-Interface 1          1 IPv6    {fec0:0:0:ffff::1, fec0:0:0:ffff::2, fec0:0:0:ffff::3}`

- add-computer -domainname skogs.com -credential Skogs\Administrator -restart -force