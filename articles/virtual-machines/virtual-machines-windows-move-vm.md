---
title: Verschieben einer Windows-VM-Ressource in Azure | Microsoft-Dokumentation
description: Verschieben Sie einen virtuellen Windows-Computer im Resource Manager-Bereitstellungsmodell in ein anderes Azure-Abonnement oder in eine andere Ressourcengruppe.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2016
ms.author: cynthn
translationtype: Human Translation
ms.sourcegitcommit: 6b80fa78fea505cd22bae2925ce1affbc1e48ab9
ms.openlocfilehash: cccbddd6993e3011e3e76bc84ffc212f3f8b1d55


---
# <a name="move-a-windows-vm-to-another-azure-subscription-or-resource-group"></a>Verschieben eines virtuellen Windows-Computers in ein anderes Azure-Abonnement oder in eine andere Ressourcengruppe
In diesem Artikel wird beschrieben, wie Sie einen virtuellen Windows-Computer zwischen Ressourcengruppen oder Abonnements verschieben. Das Verschieben zwischen Abonnements kann hilfreich sein, wenn Sie einen virtuellen Computer ursprünglich in einem persönlichen Abonnement erstellt haben und ihn nun in das Abonnement Ihres Unternehmens verschieben möchten, um weiterarbeiten zu können.

> [!NOTE]
> Im Rahmen der Verschiebung werden neue Ressourcen-IDs erstellt. Nachdem die VM verschoben wurde, müssen Sie Ihre Tools und Skripts aktualisieren, damit die neuen Ressourcen-IDs verwendet werden. 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-to-move-a-vm"></a>Verschieben eines virtuellen Computers mithilfe von PowerShell
Wenn Sie einen virtuellen Computer in eine andere Ressourcengruppe verschieben möchten, müssen Sie auch alle abhängigen Ressourcen verschieben. Für das Cmdlet „Move-AzureRMResource“ benötigen Sie Name und Art der Ressource. Beides können Sie mithilfe des Cmdlets „Find-AzureRMResource“ abrufen.

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


Zum Verschieben eines virtuellen Computers müssen mehrere Ressourcen verschoben werden. Wir können einfach separate Variablen für die einzelnen Ressourcen erstellen und sie anschließend auflisten. Dieses Beispiel umfasst die meisten der grundlegenden Ressourcen für einen virtuellen Computer und kann bei Bedarf mit weiteren Ressourcen ergänzt werden.

    $sourceRG = "<sourceResourceGroupName>"
    $destinationRG = "<destinationResourceGroupName>"

    $vm = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Compute/virtualMachines" -ResourceName "<vmName>"
    $storageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<storageAccountName>"
    $diagStorageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<diagnosticStorageAccountName>"
    $vNet = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/virtualNetworks" -ResourceName "<vNetName>"
    $nic = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkInterfaces" -ResourceName "<nicName>"
    $ip = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/publicIPAddresses" -ResourceName "<ipName>"
    $nsg = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkSecurityGroups" -ResourceName "<nsgName>"

    Move-AzureRmResource -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId

Schließen Sie den Parameter **-DestinationSubscriptionId** ein, um Ressourcen in ein anderes Abonnement zu verschieben. 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



Sie werden aufgefordert zu bestätigen, dass die angegebenen Ressourcen verschoben werden soll. Geben Sie **Y** ein, um zu bestätigen, dass die Ressourcen verschoben werden sollen.

## <a name="next-steps"></a>Nächste Schritte
Sie können viele verschiedene Arten von Ressourcen zwischen Ressourcengruppen und Abonnements verschieben. Weitere Informationen finden Sie unter [Verschieben von Ressourcen in eine neue Ressourcengruppe oder ein neues Abonnement](../azure-resource-manager/resource-group-move-resources.md).    




<!--HONumber=Jan17_HO4-->


