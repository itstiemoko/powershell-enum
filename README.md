# Powershell Active Directory Enumeration
Enumeration is the most important step when we perform a pentest or we want to audit our systems.
Using powershell commands instead of a external tools will help us to avoid triggering alerts on defense systems (AV,SIEM etc). As we say communicate with a Dog in his language and he won't bite you (okay nobody said that but you got the idea).

So here is a list of powershell commands for enumeration in Windows Active Directory environment. 

IMPORTANT : most of those commands are integrated to Active Directory module , you need to import first the module


```text
# Get Users in a specific Domain 
Get-ADUser -server Domaincontroller -Filter * -Properties *

#Get Users that can receive null password
Get-ADUser -server Domaincontroller -Filter {PasswordNotRequired -eq $true}

#Get all users that do not Require Preauthentication
Get-ADUser -Filter 'useraccountcontrol -band 4194304' -Properties useraccountcontrol | Format-Table name

# Get the list of all trusts within the current domain
Get-ADTrust -Filter *               

# Get the list of all trusts within the indicated domain
Get-ADTrust -Identity us.domain.corporation.local   

# Get Computers in a specific Domain 
Get-ADComputer -server Domaincontroller -Filter * -Properties *

# Get all active computer list in domain
# Get-ADComputer -Filter {enabled -eq $true} -properties *

# Get the default domain password policy from a specified domain
Get-ADDefaultDomainPasswordPolicy -Identity corp.local.com

# Get all groups that contain the word "admin" in the group name
Get-ADGroup -Filter 'Name -like "*admin*"' | select Name     

# Get all members of the "Domain Admins" group
Get-ADGroupMember -Identity "Domain Admins" -Recursive       

# Get group membership for a specific user
Get-ADPrincipalGroupMembership -Identity login001     

```

