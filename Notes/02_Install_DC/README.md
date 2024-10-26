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

