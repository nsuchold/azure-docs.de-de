---
title: "Verwaltete Azure Premium- und Standard-Datenträger – Übersicht | Microsoft-Dokumentation"
description: "Enthält eine Übersicht über Azure Managed Disks. Hiermit werden bei Verwendung von Azure-VMs die Speicherkonten für Sie verwaltet."
services: storage
documentationcenter: na
author: ramankumarlive
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: ramankum
translationtype: Human Translation
ms.sourcegitcommit: 58c395a45115c9db0027cffe96d20863c928a63d
ms.openlocfilehash: 74ec73388af06dbf5682c5aa1c84b153dfc4a744


---

# <a name="azure-managed-disks-overview"></a>Azure Managed Disks – Übersicht

Azure Managed Disks vereinfacht die Datenträgerverwaltung für Azure IaaS-VMs, indem die [Speicherkonten](storage-introduction.md) verwaltet werden, die den VM-Datenträgern zugeordnet sind. Sie müssen nur die Art ([Premium](storage-premium-storage.md) oder [Standard](storage-standard-storage.md)) und die benötigte Größe des Datenträgers angeben. Azure erstellt und verwaltet ihn dann für Sie.

>[!NOTE]
> Für Managed Disks muss Port 8443 verfügbar sein. Wenn Sie diesen Port blockieren möchten, müssen Sie nicht verwaltete Datenträger verwenden.
>

## <a name="benefits-of-managed-disks"></a>Vorteile von verwalteten Datenträgern

Hier werden einige Vorteile beschrieben, in deren Genuss Sie bei der Verwendung von verwalteten Datenträgern (Managed Disks) kommen.

### <a name="simple-and-scalable-vm-deployment"></a>Einfache und skalierbare VM-Bereitstellung

Managed Disks verwaltet die Speicherung für Sie im Hintergrund. Bisher mussten Sie Speicherkonten für die Datenträger (VHD-Dateien) Ihrer Azure-VMs erstellen. Beim zentralen Hochskalieren mussten Sie sicherstellen, dass zusätzliche Speicherkonten erstellt wurden, um den IOPS-Speichergrenzwert für Ihre Datenträger nicht zu überschreiten. Wenn Managed Disks die Verwaltung des Speichers übernimmt, gelten für Sie die Speicherkonto-Grenzwerte (z.B. 20.000 IOPS/Konto) nicht mehr. Außerdem ist es nicht mehr erforderlich, Ihre benutzerdefinierten Images (VHD-Dateien) in mehrere Speicherkonten zu kopieren. Sie können sie an einem zentralen Ort verwalten – ein Speicherkonto pro Azure-Region – und nutzen, um Hunderte von VMs unter einem Abonnement zu erstellen.

Mit Managed Disks können Sie für ein Abonnement bis zu 10.000 VM-**Datenträger** erstellen – und für ein Abonnement somit Tausende von **VMs**. Außerdem wird mit diesem Feature die Skalierbarkeit von [VM-Skalierungsgruppen (VMSS)](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) weiter erhöht, sodass Sie per Marketplace-Image bis zu&1;.000 VMs in einer VMSS erstellen können.

### <a name="better-reliability-for-availability-sets"></a>Bessere Zuverlässigkeit für Verfügbarkeitsgruppen

Managed Disks ermöglicht eine bessere Zuverlässigkeit für Verfügbarkeitsgruppen, indem sichergestellt wird, dass die Datenträger von VMs in einer Verfügbarkeitsgruppe ausreichend voneinander isoliert sind, um einzelne Fehlerquellen zu vermeiden. Hierzu werden die Datenträger automatisch in verschiedenen Speicherskalierungseinheiten („Stamps“) angeordnet. Wenn ein Stamp aufgrund eines Hardware- oder Softwarefehlers ausfällt, treten nur für die VM-Instanzen mit Datenträgern auf diesen Stamps Fehler auf. Angenommen, Sie führen eine Anwendung auf fünf VMs aus, und die VMs sind in einer Verfügbarkeitsgruppe enthalten. Die Datenträger für diese VMs werden nicht alle auf demselben Stamp gespeichert, damit die anderen Instanzen der Anwendung weiter ausgeführt werden, wenn ein Stamp ausfällt.

### <a name="better-security"></a>Höhere Sicherheit

Sie können die [Rollenbasierte Zugriffssteuerung in Azure (RBAC)](../active-directory/role-based-access-control-what-is.md) verwenden, um die spezifischen Berechtigungen für einen verwalteten Datenträger einem oder mehreren Benutzern zuzuweisen. Managed Disks bietet viele verschiedene Vorgänge, z.B. Lesen, Schreiben (Erstellen/Aktualisieren), Löschen, Exportieren und Abrufen eines [SAS-URI (Shared Access Signature)](storage-dotnet-shared-access-signature-part-1.md) für den Datenträger. Sie haben die Möglichkeit, Personen nur Zugriff auf die Vorgänge zu gewähren, die sie jeweils benötigen, um ihre Aufgaben zu erledigen. Wenn Sie es für eine Person beispielsweise nicht zulassen möchten, dass sie einen verwalteten Datenträger auf ein Speicherkonto kopiert, können Sie festlegen, dass der Zugriff auf die Exportaktion für diesen verwalteten Datenträger nicht gewährt wird. Wenn Sie nicht möchten, dass eine Person einen SAS-URI zum Kopieren eines verwalteten Datenträgers verwendet, können Sie auch festlegen, dass diese Berechtigung für den verwalteten Datenträger nicht gewährt wird.

## <a name="pricing-and-billing"></a>Preise und Abrechnung 

Bei der Verwendung von Managed Disks gelten die folgenden Abrechnungsaspekte:

* Speichertyp

* Datenträgergröße

* Anzahl von Transaktionen

* Ausgehende Datenübertragungen

* Managed Disk-Momentaufnahmen (vollständige Datenträgerkopie)

Wir sehen uns die einzelnen Aspekte nun genauer an.

**Speichertyp:** Managed Disks verfügt über zwei Leistungsstufen: [Premium](storage-premium-storage.md) (SSD-basiert) und [Standard](storage-standard-storage.md) (HDD-basiert). Die Abrechnung für einen verwalteten Datenträger richtet sich danach, welchen Speichertyp Sie für den Datenträger ausgewählt haben.


**Datenträgergröße**: Die Abrechnung für verwaltete Datenträger richtet sich nach der bereitgestellten Datenträgergröße. Azure ordnet die bereitgestellte Größe (aufgerundet) der nächstgelegenen Managed Disks-Option zu. Dies ist in den Tabellen unten angegeben. Jeder verwaltete Datenträger wird einer der unterstützten bereitgestellten Größen zugeordnet und entsprechend abgerechnet. Wenn Sie beispielsweise einen verwalteten Standard-Datenträger erstellen und eine bereitgestellte Größe von 200 GB angeben, wird die Abrechnung gemäß den Preisen für den Datenträgertyp S20 durchgeführt.

Hier sind die Datenträgergrößen aufgeführt, die für einen verwalteten Premium-Datenträger verfügbar sind:

| **Datenträgertyp<br>Premium – verwaltet**  | **P10** | **P20** | **P30**        |
|------------------|---------|---------|----------------|
| Datenträgergröße        | 128 GB  | 512 GB  | 1024 GB (1 TB) |

Hier sind die Datenträgergrößen aufgeführt, die für einen verwalteten Standard-Datenträger verfügbar sind: 

| **Datenträgertyp<br>Standard – verwaltet** | **S4**  | **S6**  | **S10**        | **S20** | **S30**        |
|------------------|---------|---------|----------------|---------|----------------|
| Datenträgergröße        | 32 GB   | 64 GB   | 128 GB  | 512 GB  | 1024 GB (1 TB) |

**Anzahl von Transaktionen**: Ihnen wird die Anzahl von Transaktionen berechnet, die Sie für einen verwalteten Standard-Datenträger durchführen. Für einen verwalteten Premium-Datenträger fallen keine Kosten für Transaktionen an.

**Ausgehende Datenübertragungen:**[Ausgehende Datenübertragungen](https://azure.microsoft.com/pricing/details/data-transfers/) (Daten, die von den Azure-Rechenzentren ausgehen) verursachen Kosten bei der Bandbreitenverwendung.

**Momentaufnahmen für verwaltete Datenträger (vollständige Datenträgerkopie)**: Bei einer verwalteten Momentaufnahme handelt es sich um eine schreibgeschützte Kopie eines verwalteten Datenträgers, der als verwalteter Standard-Datenträger gespeichert wird. Mit Momentaufnahmen können Sie Ihre verwalteten Datenträger jederzeit sichern. Diese Momentaufnahmen existieren unabhängig vom Quelldatenträger und können zum Erstellen von neuen verwalteten Datenträgern verwendet werden. Die Kosten für eine verwaltete Momentaufnahme sind die gleichen wie für einen verwalteten Standard-Datenträger. Wenn Sie beispielsweise eine Momentaufnahme eines verwalteten Premium-Datenträgers mit 128 GB erstellen, entsprechen die Kosten für die verwaltete Momentaufnahme den Kosten für einen verwalteten Standard-Datenträger mit 128 GB.

Für Managed Disks werden derzeit keine [inkrementellen Momentaufnahmen](storage-incremental-snapshots.md) unterstützt, aber dies ist bereits geplant.

Weitere Informationen dazu, wie Sie Momentaufnahmen mit Managed Disks erstellen, finden Sie unter diesen Ressourcen:

* [Erstellen einer Kopie einer als verwalteter Datenträger gespeicherten virtuellen Festplatte mithilfe von Momentaufnahmen unter Windows](../virtual-machines/virtual-machines-windows-snapshot-copy-managed-disk.md)
* [Erstellen einer Kopie einer als verwalteter Datenträger gespeicherten virtuellen Festplatte mithilfe von Momentaufnahmen unter Linux](../virtual-machines/linux/virtual-machines-linux-snapshot-copy-managed-disk.md)


Ausführliche Informationen zu Preisen für Managed Disks finden Sie unter [Managed Disks Preise](https://azure.microsoft.com/pricing/details/managed-disks).

## <a name="images"></a>Bilder

Für Managed Disks wird auch die Erstellung eines verwalteten benutzerdefinierten Image unterstützt. Sie können ein Image aus Ihrer benutzerdefinierten VHD in einem Speicherkonto oder direkt von einer ausgeführten VM erstellen. Hierbei werden in einem Image alle verwalteten Datenträger zusammengefasst, die einer ausgeführten VM zugeordnet sind, einschließlich der Datenträger für das Betriebssystem und für die Daten. Dies ermöglicht Ihnen die Erstellung von Hunderten von VMs mit Ihrem benutzerdefinierten Image, ohne dass Sie Speicherkonten kopieren oder verwalten müssen.

Informationen zur Erstellung von Images finden Sie in den folgenden Artikeln:
* [How to capture a managed image of a generalized VM in Azure](../virtual-machines/virtual-machines-windows-capture-image-resource.md) (Erstellen eines verwalteten Image eines generalisierten virtuellen Computers in Azure)
* [Erfassen eines virtuellen Linux-Computers, der in Azure ausgeführt wird](../virtual-machines/virtual-machines-linux-capture-image.md)

## <a name="images-versus-snapshots"></a>Vergleich von Images und Momentaufnahmen

Der Begriff „Image“ wird in Verbindung mit VMs bereits häufig verwendet, und jetzt kommen noch die „Momentaufnahmen“ hinzu. Es ist wichtig, dass Ihnen der Unterschied klar ist. Bei Managed Disks können Sie ein Image einer generalisierten VM erstellen, deren Zuordnung aufgehoben wurde. Dieses Image umfasst alle Datenträger, die an die VM angefügt sind. Sie können dieses Image verwenden, um eine neue VM mit allen Datenträgern zu erstellen.

Eine Momentaufnahme ist eine Kopie eines Datenträgers zum Zeitpunkt der Erstellung. Sie gilt nur für einen Datenträger. Wenn Sie eine VM mit nur einem Datenträger (Betriebssystem) verwenden, können Sie eine Momentaufnahme oder ein Image davon erstellen und dann entweder aus der Momentaufnahme oder dem Image eine VM erstellen.

Was passiert, wenn Sie eine VM mit fünf Stripesetdatenträgern verwenden? Sie können eine Momentaufnahme für jeden Datenträger erstellen, aber auf der VM liegen keine Informationen zum Zustand der Datenträger vor. Für die Momentaufnahmen sind nur Informationen zum jeweiligen Datenträger vorhanden. In diesem Fall müssen die Momentaufnahmen miteinander koordiniert werden, und dies wird derzeit nicht unterstützt. Falls Sie eine Kopie Ihrer VM erstellen möchten, müssen Sie also ein Image erstellen. Standardmäßig enthält das Image eine koordinierte Kopie aller fünf Datenträger.

## <a name="azure-backup-service-support"></a>Azure Backup-Dienst – Unterstützung 

Virtuelle Azure-Computer mit nicht verwalteten Datenträgern können mithilfe von Azure Backup gesichert werden. [Weitere Informationen](../backup/backup-azure-vms-first-look-arm.md)

Der Azure Backup-Dienst kann auch in Kombination mit Managed Disks verwendet werden, um einen Sicherungsauftrag mit zeitbasierten Sicherungen, unkomplizierter Wiederherstellung von virtuellen Computern und Aufbewahrungsrichtlinien für Sicherungen zu erstellen. Weitere Informationen hierzu finden Sie im Artikel zur [Verwendung des Azure Backup-Diensts für virtuelle Computer mit Managed Disks](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup). 

## <a name="managed-disks-and-storage-service-encryption-sse"></a>Managed Disks und Storage Service Encryption (SSE)

Für Azure Storage wird die automatische Verschlüsselung der Daten unterstützt, die in ein Speicherkonto geschrieben werden. Weitere Informationen finden Sie unter [Azure Storage Service Encryption für ruhende Daten](storage-service-encryption.md). Was passiert mit den Daten auf Ihren verwalteten Datenträgern? Derzeit ist es nicht möglich, Storage Service Encryption für Managed Disks zu aktivieren, aber dies wird in einer späteren Version der Fall sein. Bis dahin müssen Sie wissen, wie Sie eine VHD-Datei verwenden, die sich in einem verschlüsselten Speicherkonto befindet und selbst verschlüsselt wurde. 

Mit SSE werden Daten verschlüsselt, wenn sie in das Speicherkonto geschrieben werden. Wenn Sie eine VHD-Datei verwenden, die schon einmal per SSE verschlüsselt wurde, können Sie diese VHD-Datei nicht zum Erstellen einer VM nutzen, für die Managed Disks verwendet wird. Es ist zudem nicht möglich, einen verschlüsselten nicht verwalteten Datenträger in einen verwalteten Datenträger zu konvertieren. Falls Sie die Verschlüsselung für dieses Speicherkonto deaktivieren, wird die VHD-Datei auch nicht entschlüsselt. 

Zum Verwenden eines Datenträgers, der verschlüsselt wurde, müssen Sie zuerst die VHD-Datei in ein Speicherkonto kopieren, das noch nie verschlüsselt war. Anschließend können Sie eine VM mit Managed Disks erstellen und diese VHD-Datei während der Erstellung angeben oder die kopierte VHD-Datei mit Managed Disks an eine ausgeführte VM anfügen. 

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Managed Disks finden Sie in den folgenden Artikeln.

### <a name="get-started-with-managed-disks"></a>Erste Schritte mit verwalteten Datenträgern 

* [Erstellen eines virtuellen Computers mithilfe von Resource Manager und PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md)

* [Erstellen eines virtuellen Linux-Computers mithilfe der Azure-Befehlszeilenschnittstelle 2.0 (Vorschau)](../virtual-machines/virtual-machines-linux-quick-create-cli.md)

* [Attach a data disk to a Windows VM using PowerShell](../virtual-machines/virtual-machines-windows-attach-disk-ps.md) (Anfügen eines Datenträgers an einen virtuellen Windows-Computer mithilfe von PowerShell)

* [Hinzufügen eines verwalteten Datenträgers zu einem virtuellen Linux-Computer](../virtual-machines/virtual-machines-linux-quick-create-cli.md)

### <a name="compare-managed-disks-storage-options"></a>Vergleichen der Managed Disks-Speicheroptionen 

* [Storage Premium und Datenträger](storage-premium-storage.md)

* [Standard-Speicher und -Datenträger](storage-standard-storage.md)

### <a name="operational-guidance"></a>Leitfaden

* [Migrieren von AWS und anderen Plattformen zu Managed Disks in Azure](../virtual-machines/virtual-machines-windows-on-prem-to-azure.md)

* [Migrate Azure VMs to Managed Disks in Azure](../virtual-machines/virtual-machines-windows-migrate-to-managed-disks.md) (Migrieren von Azure-VMs zu Managed Disks in Azure)



<!--HONumber=Feb17_HO2-->


