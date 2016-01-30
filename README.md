# SQLAlwaysOnInAzureVM
Create SQL Always On in Azure VM by JSON Template and DSC

A AD will be created, AD name will be asked as parameter

Following accounts will be created:
1. AD Administrator: password will be asked as parameter
2. SQL Service Account: user name as [ADName]\s-SQLSVC; password will be asked as parameter
3. SQL Agent Account: user name as [ADName]\s-SQLAgent; password will be asked as parameter
4. Computer defaul administrator will be created, user name and password will be asked as parameter

JSON Parameters:
AD administrator password
SQL Service account password
SQL Agener Service account password
Default computer Administrator user name
Default computer administrator passowrd
Windows Server 2012 R2 image SKU
Sql Server 2014 image SKU
AD DC VM computer name prefix
SQL Always On VM computer name prefix


The basic running process:
1. Create 1 VNET, 2 Subnet - AD Subnet; DB Subnet
2. Create PIPs and NICs, every VM wil have 1 NIC, and every NIC will have a PIP, PIP dns name will be auto created as "sqlaoazuredemo" + "[VMNamePrefix][VMNumber]" (No dns name oversize checking in this demo)
2. Create all VMs: 
    2.1 2 VMs as AD DC in one availability set in AD Subnet; use windows server 2012 r2 image;
    2.2 2 VMs as SQL Always On Group in one availability set in DB Subnet; use sql server 2014 enterprise image;
    2.3 1 File Share Witness in DB Subnet; use windows server 2012 r2 image;
3. Create ILB as SQL always on listener
4. Use DSC Create AD
5. Use DSC Create Windows Cluster for SQL Always On VMs
6. Use DSC Create SQL Always On
