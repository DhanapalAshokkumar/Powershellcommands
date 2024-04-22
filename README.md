# Powershellcommands
PowerShell AD Commands - To check who manages the AD Group (who/email)

Get-ADGroup -filter {Name -like "ADGroupname" } -Properties managedB
y |
>> ForEach-Object {
>> $managedBy = $_.managedBy;
>>
>> if ($managedBy -ne $null)
>> {
>>  $manager = (get-aduser -Identity $managedBy -Properties emailAddress);
>>  $managerName = $manager.Name;
>>  $managerEmail = $manager.emailAddress;
>> }
>> else
>> {
>>  $managerName = 'N/A';
>>  $managerEmail = 'N/A';
>> }
>>
>> Write-Output $_; } |
>> Select-Object @{n='Group Name';e={$_.Name}}, @{n='Managed By Name';e={$managerName}}, @{n='Managed By Email';e={$managerEmail}}
