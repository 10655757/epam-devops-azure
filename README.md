#epam-devops-azure

AZ-104-Lab03a

https://github.com/ArtakG/AZ-104-MicrosoftAzureAdministrator/blob/master/Instructions/Labs/LAB_03a-Manage_Azure_Resources_by_Using_the_Azure_Portal.md

1) create resource
2) create disk
3) change disk size
4) change disk type
5) move resources between resource groups
6) add resource lock

AZ-104-Lab03c

https://github.com/ArtakG/AZ-104-MicrosoftAzureAdministrator/blob/master/Instructions/Labs/LAB_03c-Manage_Azure_Resources_by_Using_Azure_PowerShell.md

1) create resource
$location = (Get-AzResourceGroup -Name az104-03a-rg1).Location
$rgName = 'az104-03c-rg1'
New-AzResourceGroup -Name $rgName -Location $location
Get-AzResourceGroup -Name $rgName

$diskConfig = New-AzDiskConfig `
 -Location $location `
 -CreateOption Empty `
 -DiskSizeGB 32 `
 -Sku Standard_LRS

2) create disk 
$diskName = 'az104-03c-disk1'

New-AzDisk `
 -ResourceGroupName $rgName `
 -DiskName $diskName `
 -Disk $diskConfig

3) change disk size
(Get-AzDisk -ResourceGroupName $rgName -Name $diskName).DiskSizeGB
New-AzDiskUpdateConfig -DiskSizeGB 64 | Update-AzDisk -ResourceGroupName $rgName -DiskName $diskName 
(Get-AzDisk -ResourceGroupName $rgName -Name $diskName).DiskSizeGB

4) change disk type
(Get-AzDisk -ResourceGroupName $rgName -Name $diskName).Sku
New-AzDiskUpdateConfig -Sku Premium_LRS | Update-AzDisk -ResourceGroupName $rgName -DiskName $diskName
(Get-AzDisk -ResourceGroupName $rgName -Name $diskName).Sku
