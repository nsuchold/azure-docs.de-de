---
title: "Häufige Fehler bei der Migration von einer klassischen Bereitstellung zu einer Azure Resource Manager-Bereitstellung | Microsoft-Dokumentation"
description: "In diesem Artikel werden die Fehler aufgeführt und beschrieben, die bei der Migration von IaaS-Ressourcen von der Azure-Dienstverwaltung zum Azure Resource Manager-Stapel am häufigsten auftreten."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5bc03a1b-eb1c-438c-83d9-f0e9d61f1b6a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/13/2016
ms.author: kasing
translationtype: Human Translation
ms.sourcegitcommit: daa311fcfd1ef06cf36e9443150fc967f0f39708
ms.openlocfilehash: 052505260c0998c8528146c4985400126d094f0d


---
# <a name="common-errors-during-classic-to-azure-resource-manager-migration"></a>Häufige Fehler bei der Migration von einer klassischen Bereitstellung zu einer Azure Resource Manager-Bereitstellung
In diesem Artikel werden die Fehler aufgeführt und beschrieben, die bei der Migration von IaaS-Ressourcen vom klassischen Azure-Bereitstellungsmodell zum Azure Resource Manager-Stapel am häufigsten auftreten.

## <a name="list-of-errors"></a>Liste der Fehler
| Fehlerzeichenfolge | Lösung |
| --- | --- |
| Interner Serverfehler |Dies ist in einigen Fällen ein vorübergehender Fehler, der nach einem erneuten Versuch nicht mehr auftritt. Wenn der Fehler weiterhin auftritt, [wenden Sie sich an den Azure-Support](../azure-supportability/how-to-create-azure-support-request.md), da in diesem Fall eine Untersuchung der Plattformprotokolle erforderlich ist. <br><br> **HINWEIS**: Sobald der Incident vom Supportteam aufgenommen wurde, versuchen Sie nicht, das Problem selbst zu lösen, da dies unerwartete Folgen für Ihre Umgebung nach sich ziehen könnte. |
| Die Migration von Bereitstellung "{deployment-name}" im HostedService "{hosted-service-name}" wird nicht unterstützt, da es sich um eine PaaS-Bereitstellung (Web/Worker) handelt. |Dies passiert, wenn eine Bereitstellung eine Web- oder Workerrolle enthält. Da die Migration nur für virtuelle Computer unterstützt wird, entfernen Sie die Web- oder Workerrolle aus der Bereitstellung, und wiederholen Sie die Migration. |
| Bei der Bereitstellung von Vorlage "{template-name}" ist ein Fehler aufgetreten. CorrelationId={guid} |Im Back-End des Migrationsdienst verwenden wir Azure Resource Manager-Vorlagen, um Ressourcen im Azure Resource Manager-Stapel zu erstellen. Da Vorlagen idempotent sind, können Sie den Migrationsvorgang üblicherweise sicher wiederholen, um diesen Fehler zu beheben. Wenn der Fehler weiterhin auftritt, [wenden Sie sich an den Azure-Support](../azure-supportability/how-to-create-azure-support-request.md), und geben Sie die CorrelationId an. <br><br> **HINWEIS**: Sobald der Incident vom Supportteam aufgenommen wurde, versuchen Sie nicht, das Problem selbst zu lösen, da dies unerwartete Folgen für Ihre Umgebung nach sich ziehen könnte. |
| Das virtuelle Netzwerk "{virtual-network-name}" ist nicht vorhanden. |Dieser Fehler kann auftreten, wenn Sie das virtuelle Netzwerk im neuen Azure-Portal erstellt haben. Der tatsächliche Name des virtuellen Netzwerk folgt dem Muster „Gruppe * <VNET name>“. |
| Der virtuelle Computer "{vm-name}" im HostedService "{hosted-service-name}" enthält die Erweiterung "{extension-name}", die in Azure Resource Manager nicht unterstützt wird. Es empfiehlt sich, sie vom virtuellen Computer zu deinstallieren, bevor Sie die Migration fortsetzen. |XML-Erweiterungen wie „BGInfo 1.*“ werden in Azure Resource Manager nicht unterstützt. Daher können diese Erweiterungen nicht migriert werden. Wenn die Installation dieser Erweiterungen auf dem virtuellen Computer beibehalten wird, werden sie vor dem Abschließen der Migration automatisch deinstalliert. |
| Die VM "{vm-name}" im HostedService {hosted-service-name} enthält die Erweiterung "VMSnapshot/VMSnapshotLinux", für die eine Migration derzeit nicht unterstützt wird. Deinstallieren Sie sie von der VM, und fügen Sie sie nach Abschluss der Migration über Azure Resource Manager wieder hinzu. |Dies ist das Szenario, in dem der virtuelle Computer für Azure Backup konfiguriert ist. Da dies zurzeit ein nicht unterstütztes Szenario ist, befolgen Sie die Problemumgehung unter https://aka.ms/vmbackupmigration. |
| Die VM "{vm-name}" im HostedService "{hosted-service-name}" enthält die Erweiterung "{extension-name}", deren Status nicht von der VM gemeldet wird. Daher kann diese VM nicht migriert werden. Stellen Sie sicher, dass der Erweiterungsstatus gemeldet wird, oder deinstallieren Sie die Erweiterung von der VM, und wiederholen Sie die Migration. <br><br> Die VM "{vm-name}" im HostedService "{hosted-service-name}" enthält die Erweiterung "{extension-name}", die den Handlerstatus "{handler-status}" meldet. Daher kann die VM nicht migriert werden. Stellen Sie sicher, dass der Erweiterungshandlerstatus "{handler-status}" gemeldet wird, oder deinstallieren Sie die Erweiterung von der VM, und wiederholen Sie die Migration. <br><br> Der VM-Agent für die VM "{vm-name}" im HostedService "{hosted-service-name}" meldet für den Agent den Gesamtstatus "Nicht bereit". Daher wird die VM möglicherweise nicht migriert, wenn sie über eine migrierbare Erweiterung verfügt. Stellen Sie sicher, dass der VM-Agent den Gesamtstatus des Agents als "Bereit" meldet. Informationen hierzu finden Sie unter https://aka.ms/classiciaasmigrationfaqs. |Gast-Agent- und VM-Erweiterungen in Azure benötigen ausgehenden Internetzugriff auf das Speicherkonto des virtuellen Computers, um ihren Status aufzufüllen. Häufige Fehlerursachen für den Statusfehler sind folgende: <li> Eine Netzwerksicherheitsgruppe blockiert den ausgehenden Zugriff auf das Internet. <li> Im virtuellen Netzwerk sind lokale DNS-Server vorhanden, und die DNS-Verbindung wurde unterbrochen. <br><br> Wenn weiterhin nicht unterstützte Status angezeigt werden, können Sie die Erweiterungen deinstallieren, um diese Prüfung zu überspringen und mit der Migration fortzufahren. |
| Die Migration von Bereitstellung "{deployment-name}" im HostedService "{hosted-service-name}" wird nicht unterstützt, da die Bereitstellung mehrere Verfügbarkeitsgruppen aufweist. |Zurzeit können nur gehostete Dienste mit höchstens einer Verfügbarkeitsgruppe migriert werden. Um dieses Problem zu umgehen, verschieben Sie die zusätzlichen Verfügbarkeitsgruppen und virtuellen Computer in diesen Verfügbarkeitsgruppen in einen anderen gehosteten Dienst. |
| Die Migration von Bereitstellung "{deployment-name}" im HostedService "{hosted-service-name}" wird nicht unterstützt, da die Bereitstellung über virtuelle Computer verfügt, die nicht Teil der Verfügbarkeitsgruppe sind, obwohl der HostedService einen virtuellen Computer enthält. |Um dieses Problem zu umgehen, verschieben Sie entweder alle virtuellen Computer in eine einzige Verfügbarkeitsgruppe, oder entfernen Sie alle virtuellen Computer aus der Verfügbarkeitsgruppe im gehosteten Dienst. |
| Das Speicherkonto / der HostedService / das virtuelle Netzwerk {virtual-network-name} wird gerade migriert und kann daher nicht geändert werden. |Dieser Fehler tritt auf, wenn der Vorgang zur Vorbereitung der Migration für die Ressource abgeschlossen ist und ein Vorgang ausgelöst wird, der die Ressource ändern würde. Aufgrund der Sperre auf der Verwaltungsebene nach dem Vorbereitungsvorgang werden alle Änderungen an der Ressource blockiert. Um die Verwaltungsebene zu entsperren, können Sie den Vorgang zum Commit der Migration ausführen, um die Migration abzuschließen, oder Sie führen den Vorgang zum Abbrechen der Migration aus, um ein Rollback des Vorbereitungsvorgangs auszuführen. |
| Die Migration ist für den HostedService "{hosted-service-name}" nicht zulässig, da die darin enthaltene VM "{vm-name}" den Zustand "RoleStateUnknown" aufweist. Die Migration ist nur dann zulässig, wenn sich die VM in einem der folgenden Zustände befindet: Wird ausgeführt, Beendet, Beendet (Zuordnung aufgehoben). |Für den virtuellen Computer findet möglicherweise gerade eine Statusübergang statt. Dies geschieht üblicherweise während eines Updatevorgangs auf dem HostedService, z.B. während eines Neustarts, der Installation einer Erweiterung usw. Es empfiehlt sich, den Updatevorgang des HostedService abzuschließen, bevor Sie versuchen, die Migration durchzuführen. |
| Die Bereitstellung „{deployment-name}“ im HostedService „{hosted-service-name}“ enthält den virtuellen Computer „{vm-name}“ mit dem Datenträger „{data-disk-name}“, dessen physische Blobgröße ({size-of-the-vhd-blob-backing-the-data-disk} Bytes) nicht der logischen VM-Datenträgergröße ({size-of-the-data-disk-specified-in-the-vm-api} Bytes) entspricht. Die Migration wird ohne Angabe einer Größe für den Datenträger für den virtuellen Azure Resource Manager-Computer fortgesetzt. Wenn Sie die Größe des Datenträgers korrigieren möchten, bevor die Migration fortgesetzt wird, besuchen Sie „https://aka.ms/vmdiskresize“. | Dieser Fehler kann auftreten, wenn Sie die VHD-Blobgröße angepasst haben, ohne die Größe im VM-API-Modell zu aktualisieren. Ausführliche Schritte zur Behebung finden Sie [weiter unten](#vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-the-vm-data-disk-logical-size-bytes).|

## <a name="detailed-mitigations"></a>Ausführliche Behebungen

### <a name="vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-the-vm-data-disk-logical-size-bytes"></a>Virtueller Computer mit einem Datenträger, dessen physische Blobgröße in Bytes nicht der logischen VM-Datenträgergröße in Bytes entspricht.

Dieser Fall tritt ein, wenn die logische Größe des Datenträgers nicht auf die tatsächliche Größe der VHD-Blobgröße abgestimmt ist. Dies lässt sich problemlos mit den folgenden Befehlen überprüfen:

#### <a name="verifying-the-issue"></a>Überprüfen des Problems

```PowerShell
# Store the VM details in the VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

# Display the data disk properties
# NOTE the data disk LogicalDiskSizeInGB below which is 11GB. Also note the MediaLink Uri of the VHD blob as we'll use this in the next step
$vm.VM.DataVirtualHardDisks


HostCaching         : None
DiskLabel           : 
DiskName            : coreosvm-coreosvm-0-201611230636240687
Lun                 : 0
LogicalDiskSizeInGB : 11
MediaLink           : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
SourceMediaLink     : 
IOType              : Standard
ExtensionData       : 

# Now get the properties of the blob backing the data disk above
# NOTE the size of the blob is about 15 GB which is different from LogicalDiskSizeInGB above
$blob = Get-AzureStorageblob -Blob "coreosvm-dd1.vhd" -Container vhds 

$blob

ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudPageBlob
BlobType          : PageBlob
Length            : 16106127872
ContentType       : application/octet-stream
LastModified      : 11/23/2016 7:16:22 AM +00:00
SnapshotTime      : 
ContinuationToken : 
Context           : Microsoft.WindowsAzure.Commands.Common.Storage.AzureStorageContext
Name              : coreosvm-dd1.vhd
```

#### <a name="mitigating-the-issue"></a>Beheben des Problems

```PowerShell
# Convert the blob size in bytes to GB into a variable which we'll use later
$newSize = [int]($blob.Length / 1GB)

# See the calculated size in GB
$newSize

15

# Store the disk name of the data disk as we'll use this to identify the disk to be updated
$diskName = $vm.VM.DataVirtualHardDisks[0].DiskName

# Identify the LUN of the data disk to remove
$lunToRemove = $vm.VM.DataVirtualHardDisks[0].Lun

# Now remove the data disk from the VM so that the disk isn't leased by the VM and it's size can be updated
Remove-AzureDataDisk -LUN $lunToRemove -VM $vm | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       213xx1-b44b-1v6n-23gg-591f2a13cd16   Succeeded  

# Verify we have the right disk that's going to be updated
Get-AzureDisk -DiskName $diskName

AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : 
Location             : East US
DiskSizeInGB         : 11
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 0c56a2b7-a325-123b-7043-74c27d5a61fd
OperationStatus      : Succeeded

# Now update the disk to the new size
Update-AzureDisk -DiskName $diskName -ResizedSizeInGB $newSize -Label $diskName

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureDisk     cv134b65-1b6n-8908-abuo-ce9e395ac3e7 Succeeded 

# Now verify that the "DiskSizeInGB" property of the disk matches the size of the blob 
Get-AzureDisk -DiskName $diskName


AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : coreosvm-coreosvm-0-201611230636240687
Location             : East US
DiskSizeInGB         : 15
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 1v53bde5-cv56-5621-9078-16b9c8a0bad2
OperationStatus      : Succeeded

# Now we'll add the disk back to the VM as a data disk. First we need to get an updated VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

Add-AzureDataDisk -Import -DiskName $diskName -LUN 0 -VM $vm -HostCaching ReadWrite | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       b0ad3d4c-4v68-45vb-xxc1-134fd010d0f8 Succeeded      
```

## <a name="next-steps"></a>Nächste Schritte
Hier finden Sie eine Liste von Artikeln zum Thema Migration, die den Vorgang erläutern.

* [Plattformgestützte Migration von IaaS-Ressourcen aus dem klassischen Bereitstellungsmodell zu Azure Resource Manager](virtual-machines-windows-migration-classic-resource-manager.md)
* [Migrieren von IaaS-Ressourcen vom klassischen Bereitstellungsmodell zu Azure Resource Manager mithilfe von PowerShell](virtual-machines-windows-ps-migration-classic-resource-manager.md)
* [Migrieren von IaaS-Ressourcen vom klassischen Bereitstellungsmodell zu Azure Resource Manager mithilfe der Befehlszeilenschnittstelle](virtual-machines-linux-cli-migration-classic-resource-manager.md)




<!--HONumber=Feb17_HO3-->


