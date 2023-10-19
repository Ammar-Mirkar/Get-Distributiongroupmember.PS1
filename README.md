# Get-Distributiongroupmember.PS1
#Distribution Group Membership Report
$Groups = Get-DistributionGroup 
$Groups | ForEach-Object {
$group = $_.Name
$members = ''
Get-DistributionGroupMember $group | ForEach-Object {
        If($members) {
              $members=$members + ";" + $_.Name
           } Else {
              $members=$_.Name
           }
  }
New-Object -TypeName PSObject -Property @{
      GroupName = $group
      Members = $members
     }
} | Export-CSV "C:\Distribution-Group-Members.csv" -NoTypeInformation -Encoding UTF8
