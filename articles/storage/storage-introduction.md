---
title: "Einführung in Azure Storage | Microsoft-Dokumentation"
description: "Eine Übersicht über Azure Storage, dem Onlinedatenspeicher von Microsoft in der Cloud. Hier erfahren Sie, wie Sie in Ihren Anwendungen die beste verfügbare Cloudspeicherlösung verwenden."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/24/2017
ms.author: marsma
translationtype: Human Translation
ms.sourcegitcommit: f4b26aa9a4dd110eafb8f9f8d658cc0f530136ec
ms.openlocfilehash: 4548d83525dba6024d1892950e3acbc6b857977a
ms.lasthandoff: 02/27/2017


---
# <a name="introduction-to-microsoft-azure-storage"></a>Einführung in Microsoft Azure Storage

## <a name="overview"></a>Übersicht
Azure Storage ist eine Cloudspeicherlösung für moderne Anwendungen, die eine Kombination aus Dauerhaftigkeit, Verfügbarkeit und Skalierbarkeit benötigen, um die Anforderungen ihrer Kunden zu erfüllen. In diesem Artikel finden Entwickler, IT-Experten und Entscheidungsträger Antworten auf folgende Fragen:

* Was ist Azure Storage, und wie können Sie in Ihren Cloud-, Mobil-, Server- und Desktopanwendungen davon profitieren?
* Welche Arten von Daten (Blob-/Objektdaten, NoSQL-Tabellendaten, Warteschlangennachrichten und Dateifreigaben) können mithilfe der Azure Storage-Dienste gespeichert werden?
* Wie wird der Zugriff auf Ihre Daten in Azure Storage verwaltet?
* Wie wird die Dauerhaftigkeit Ihrer Azure Storage-Daten mittels Redundanz und Replikation gewährleistet?
* Welche Schritte sind zum Erstellen einer ersten Azure Storage-Anwendung erforderlich?

Informationen zum Einrichten und Starten von Azure Storage finden Sie unter [Erste Schritte mit Azure Storage – Einstieg in fünf Minuten](storage-getting-started-guide.md).

Informationen zu Tools, Bibliotheken und weiteren Ressourcen für die Arbeit mit Azure Storage finden Sie weiter unten unter [Nächste Schritte](#next-steps) .

## <a name="what-is-azure-storage"></a>Was ist Azure Storage?
Cloud Computing ermöglicht neue Szenarien für Anwendungen, die skalierbaren, langlebigen und hochverfügbaren Speicher für ihre Daten benötigen. Genau zu diesem Zweck wurde Azure Storage entwickelt. Mit Azure Storage können Entwickler nicht nur umfangreiche Anwendungen für neue Szenarien entwickeln, es bildet auch die Speichergrundlage für Azure Virtual Machines – ein weiterer Beleg für dessen Robustheit.

Dank der äußerst flexiblen Skalierbarkeit von Azure Storage können Sie Hunderte Terabytes an Daten speichern und verarbeiten, um den Big Data-Anforderungen von Anwendungen in den Bereichen Wissenschaft, Finanzanalyse und Medien gerecht zu werden. Sie können aber ebenso gut die geringen Datenmengen der Website eines kleinen Unternehmens speichern. In jedem Fall bezahlen Sie nur für die Daten, die Sie tatsächlich speichern. Azure Storage speichert derzeit mehrere Billionen einzigartiger Kundenobjekte und verarbeitet im Schnitt mehrere Millionen Anforderungen pro Sekunde.

Azure Storage ist elastisch: Sie können Anwendungen für ein breites globales Publikum entwickeln und nach Bedarf skalieren – sowohl im Hinblick auf die gespeicherten Daten als auch auf die dafür ausgeführten Anforderungen. Dabei zahlen Sie nur für das, was Sie tatsächlich nutzen.

Azure Storage verwendet ein automatisches Partitionierungssystem, das auf der Grundlage des Datenverkehrs einen automatischen Lastenausgleich Ihrer Daten durchführt. Das bedeutet, dass Azure Storage immer automatisch die nötigen Ressourcen zuordnet, um die wachsenden Anforderungen Ihrer Anwendung zu erfüllen.

Azure Storage ist weltweit und von jeder Art von Anwendung erreichbar – ganz gleich, ob die Anwendung in der Cloud, auf dem Desktop, auf einem lokalen Server oder auf einem mobilen Gerät oder Tablet ausgeführt wird. Sie können Azure Storage in mobilen Szenarien verwenden, in denen eine Anwendung einen Teil der Daten auf einem Gerät speichert und sie mit einem umfassenden Dataset in der Cloud synchronisiert.

Azure Storage unterstützt Clients mit verschiedensten Betriebssystemen (unter anderem Windows und Linux) und einer Vielzahl von Programmiersprachen (darunter .NET, Java, Node.js, Python, Ruby, PHP und C++ sowie mobile Programmiersprachen), um eine problemlose Entwicklung zu ermöglichen. Darüber hinaus macht Azure Storage Datenressourcen über einfache REST-APIs verfügbar. Diese können auf jedem Client verwendet werden, der Daten per HTTP/HTTPS senden und empfangen kann.

Azure Storage Premium bietet eine leistungsstarke Datenträgerunterstützung mit niedriger Latenz für E/A-intensive Workloads unter Azure Virtual Machines. Mit Azure Storage Premium können Sie mehrere persistente Datenträger an einen virtuellen Computer anfügen und diese gemäß Ihren Leistungsanforderungen konfigurieren. Jeder Datenträger basiert auf einer SSD-Festplatte in Azure Storage Premium, um eine bestmögliche E/A-Leistung zu erzielen. Weitere Informationen finden Sie unter [Storage Premium: Hochleistungsspeicher für Workloads virtueller Azure-Computer](storage-premium-storage.md) .

## <a name="introducing-the-azure-storage-services"></a>Einführung in die Azure Storage-Dienste
Azure Storage umfasst vier Dienste: Blob Storage, Table Storage, Queue Storage und File Storage.

* Blob Storage dient zum Speichern unstrukturierter Objektdaten. Bei einem Blob kann es sich um einen beliebigen Text- oder Binärdatentyp handeln – also beispielsweise um ein Dokument, eine Mediendatei oder einen Anwendungs-Installer. Blob Storage wird auch als Objektspeicher bezeichnet.
* Table Storage dient zum Speichern strukturierter Datasets. Table Storage ist ein Schlüssel-/Attribut-basierter NoSQL-Datenspeicher, der eine rasche Entwicklung und schnellen Zugriff auf große Datenmengen erlaubt.
* Queue Storage bietet zuverlässiges Messaging für die Workflowverarbeitung und für die Kommunikation zwischen Komponenten von Clouddiensten.
* File Storage bietet einen gemeinsam genutzten Speicher für Legacyanwendungen unter Verwendung des standardmäßigen SMB-Protokolls. Virtuelle Azure-Computer und Clouddienste können Dateidaten in verschiedenen Anwendungskomponenten über eingebundene Freigaben teilen, und lokale Anwendungen können über die REST-API des Dateidiensts auf Dateidaten in einer Freigabe zugreifen.

Ein Azure-Speicherkonto ist ein sicheres Konto, mit dem Sie auf Dienste in Azure Storage zugreifen können. Ihr Speicherkonto stellt den eindeutigen Namespace für Ihre Speicherressourcen bereit. Die folgende Abbildung zeigt die Beziehungen zwischen den Azure-Speicherressourcen in einem Speicherkonto:

![Azure Storage-Ressourcen](./media/storage-introduction/storage-concepts.png)

[!INCLUDE [storage-account-types-include](../../includes/storage-account-types-include.md)]

[!INCLUDE [storage-versions-include](../../includes/storage-versions-include.md)]

## <a name="blob-storage"></a>Blob-Speicher
Blob Storage ist eine kostengünstige und skalierbare Lösung für Benutzer, die große Mengen an unstrukturierten Objektdaten in der Cloud speichern möchten. Mit Blob Storage lassen sich unter anderem folgende Inhalte speichern:

* Dokumente
* Daten aus sozialen Netzwerken (etwa Fotos, Videos, Musik und Blogs)
* Sicherungskopien von Dateien, Computern, Datenbanken und Geräten
* Bilder und Texte für Webanwendungen
* Konfigurationsdaten für Cloudanwendungen
* Big Data wie Protokolle und andere umfangreiche Datasets

Jedes Blob ist in einem Container organisiert. Container sind auch eine praktische Möglichkeit, um Gruppen von Objekten Sicherheitsrichtlinien zuzuordnen. Ein Speicherkonto kann eine beliebige Anzahl von Containern enthalten, und ein Container kann eine beliebige Anzahl von Blobs enthalten. Die Speicherkapazität eines Speicherkontos beträgt maximal 500 TB.

Blob Storage bietet drei Arten von Blobs: Blockblobs, Anfügeblobs und Seitenblobs (Festplatten).

* Blockblobs sind für das Streamen und Speichern von Cloudobjekten optimiert und eine gute Wahl für die Speicherung von Dokumenten, Mediendateien, Sicherungskopien und Ähnlichem.
* Anfügeblobs ähneln Blockblobs, sind aber für Anfügevorgänge optimiert. Zum Aktualisieren eines Anfügeblobs muss an dessen Ende ein neuer Block hinzugefügt werden. Somit eignen sich Anfügeblobs sehr gut für Szenarien wie die Protokollierung, da hier neue Daten nur am Ende des Blobs geschrieben werden müssen.
* Seitenblobs sind für die Darstellung von IaaS-Festplatten und für die Unterstützung zufallsgesteuerter Schreibzugriffe optimiert und können bis zu 1 TB groß sein. Bei einer mit dem Netzwerk für virtuelle Azure-Computer verbundenen IaaS-Festplatte handelt es sich um eine als Seitenblob gespeicherte virtuelle Festplatte.

Wenn sich die Daten besonders umfangreicher Datasets aufgrund von Netzwerkbeschränkungen nicht sinnvoll über eine Kabelverbindung in Blob Storage hochladen bzw. daraus herunterladen lassen, können Sie eine Festplatte an Microsoft schicken und Ihre Daten direkt in das Rechenzentrum importieren bzw. aus dem Rechenzentrum exportieren lassen. Weitere Informationen finden Sie unter [Verwenden des Microsoft Azure Import/Export-Diensts zum Übertragen von Daten in den Blobspeicher](storage-import-export-service.md).

## <a name="table-storage"></a>Table Storage
Moderne Anwendungen sind im Vergleich zu früheren Softwaregenerationen häufig auf Datenspeicher mit höherer Skalierbarkeit und Flexibilität angewiesen. Table Storage bietet eine hoch verfügbare und äußerst flexibel skalierbare Speicherung, sodass sich Ihre Anwendung automatisch auf die Anforderungen der Benutzer einstellen kann. Table Storage ist ein Schlüssel-/Attribut-basierter NoSQL-Speicher von Microsoft und unterscheidet sich durch das schemalose Design von herkömmlichen relationalen Datenbanken. Mit einem schemalosen Datenspeicher können Sie Ihre Daten problemlos an die sich verändernden Anforderungen Ihrer Anwendung anpassen. Die hohe Benutzerfreundlichkeit von Table Storage ermöglicht Entwicklern eine rasche Anwendungserstellung. Der Datenzugriff ist für alle Arten von Anwendungen schnell und kostengünstig.  Table Storage ist in der Regel erheblich günstiger als herkömmliche SQL-Lösungen für ähnliche Datenmengen.

Bei Table Storage handelt es sich um einen Schlüssel-/Attribut-basierten Speicher. Das bedeutet, dass jeder Wert in einer Tabelle mit einem typisierten Eigenschaftennamen gespeichert wird. Der Eigenschaftenname kann für Filter und Auswahlkriterien verwendet werden. Eine Sammlung mit Eigenschaften und deren Werte bilden eine Entität. Da der Tabellenspeicher schemalos ist, können zwei Entitäten in der gleichen Tabelle unterschiedliche Sammlungen von Eigenschaften enthalten, und diese Eigenschaften können jeweils einen anderen Typ haben.

Mit Table Storage können Sie flexible Datasets wie Benutzerdaten für Webanwendungen, Adressbücher, Geräteinformationen und jegliche Art von Metadaten speichern, die Ihr Dienst erfordert.  Sie können eine beliebige Anzahl von Entitäten in einer Tabelle speichern, und ein Speicherkonto kann eine beliebige Anzahl von Tabellen enthalten (bis zur Speicherkapazitätsgrenze eines Speicherkontos).

Genau wie bei Blobs und Warteschlangen können Entwickler Table Storage unter Verwendung standardmäßiger REST-Protokolle aufrufen und verwalten. Table Storage unterstützt allerdings auch einen Teil des OData-Protokolls. Dies vereinfacht erweiterte Abfragefunktionen und ermöglicht die Verwendung der Formate JSON und AtomPub (XML-basiert).

Für moderne internetbasierte Anwendungen stellen NoSQL-Datenbanken wie Table Storage eine beliebte Alternative zu herkömmlichen relationalen Datenbanken dar.

## <a name="queue-storage"></a>Warteschlangenspeicher
Bei der Entwicklung skalierbarer Anwendungen werden häufig einzelne Anwendungskomponenten entkoppelt, um eine unabhängige Skalierung zu ermöglichen. Queue Storage bietet eine zuverlässige Messaginglösung für die asynchrone Kommunikation zwischen Anwendungskomponenten – ganz gleich, ob diese in der Cloud, auf dem Desktop, auf einem lokalen Server oder auf einem mobilen Gerät ausgeführt werden. Queue Storage unterstützt auch die Verwaltung asynchroner Aufgaben und den Aufbau von Prozessworkflows.

Ein Speicherkonto kann eine beliebige Anzahl von Warteschlangen enthalten. Eine Warteschlange kann eine beliebige Anzahl von Nachrichten enthalten (bis zur Kapazitätsgrenze des Speicherkontos). Einzelne Nachrichten können bis zu 64 KB groß sein.

## <a name="file-storage"></a>File Storage
Azure File Storage bietet cloudbasierte SMB-Dateifreigaben, mit denen Sie ältere Anwendungen, die auf Dateifreigaben angewiesen sind, schnell und ohne kostspielige Neuentwicklungen nach Azure migrieren können. Mit Azure File Storage können Anwendungen, die auf virtuellen Azure-Computern oder in Clouddiensten ausgeführt werden, eine Dateifreigabe in der Cloud nach dem gleichen Prinzip einbinden wie eine Desktopanwendung, die eine typische SMB-Freigabe einbindet. Die File Storage-Freigaben können dann von beliebig vielen Anwendungskomponenten gleichzeitig eingebunden und genutzt werden.

Da es sich bei File Storage-Freigaben um gewöhnliche SMB-Freigaben handelt, können Anwendungen in Azure über die E/A-APIs des Systems auf die Freigaben zugreifen. Entwickler können daher bei der Migration vorhandener Anwendungen auf ihren vorhandenen Code sowie auf bereits angeeignetes Know-how zurückgreifen. IT-Experten können PowerShell-Cmdlets verwenden, um File Storage-Freigaben im Rahmen der Verwaltung von Azure-Anwendungen zu erstellen, einzubinden und zu verwalten.

Genau wie die anderen Azure Storage-Dienste stellt auch File Storage eine REST-API für den Zugriff auf Daten in Freigaben bereit. Lokale Anwendungen können die REST-API von File Storage aufrufen, um auf Daten in Dateifreigaben zuzugreifen. Auf diese Weise können Unternehmen einen Teil ihrer älteren Anwendungen nach Azure migrieren und andere Anwendungen weiterhin intern ausführen. Die Einbindung von Dateifreigaben ist nur für Anwendungen möglich, die in Azure ausgeführt werden. Lokale Anwendungen müssen über die REST-API auf die Dateifreigaben zugreifen.

Verteilte Anwendungen können File Storage für die Speicherung und Weitergabe von Anwendungsdaten sowie für Entwicklungs- und Testtools verwenden. Eine Anwendung kann beispielsweise Konfigurationsdateien und Diagnosedaten wie Protokolle, Metriken und Absturzabbilder in einer File Storage-Freigabe speichern, um diese Daten anderen virtuellen Computern oder Rollen zur Verfügung zu stellen. Entwickler und Administratoren können Hilfsprogramme für die Erstellung oder Verwaltung einer Anwendung in einer File Storage-Freigabe speichern, die für alle Komponenten verfügbar ist, anstatt diese Hilfsprogramme einzeln auf allen virtuellen Computern oder Rolleninstanzen zu installieren.

## <a name="access-to-blob-table-queue-and-file-resources"></a>Zugreifen auf Blob-, Tabellen-, Warteschlangen- und Dateiressourcen
Standardmäßig kann nur der Besitzer eines Speicherkontos auf Ressourcen in diesem Konto zugreifen. Aus Sicherheitsgründen muss jede Anforderung für Ressourcen in Ihrem Konto authentifiziert werden. Die Authentifizierung beruht auf einem Modell mit gemeinsam verwendeten Schlüsseln. Blobs können auch für die Unterstützung anonymer Authentifizierungen konfiguriert werden.

Ihr Speicherkonto wird bei der Erstellung zwei privaten Zugriffsschlüsseln zugeordnet, die für die Authentifizierung verwendet werden. Die Verwendung von zwei Schlüsseln stellt sicher, dass Ihre Anwendung auch dann verfügbar bleibt, wenn Sie die Schlüssel im Rahmen der allgemeinen Sicherheitsverwaltung regelmäßig erneuern.

Wenn Sie anderen Benutzern kontrollierten Zugriff auf Ihre Speicherressourcen gewähren müssen, können Sie eine Shared Access Signature erstellen. Eine Shared Access Signature (SAS) ist ein Token, das an eine URL angefügt werden kann und delegierten Zugriff auf eine Speicherressource ermöglicht. Jeder Benutzer, der über dieses Token verfügt, kann während der Gültigkeitsdauer mit festgelegten Berechtigungen auf die Ressource zugreifen, auf die das Token verweist. Ab Version 05.04.2015 unterstützt Azure Storage zwei Arten von SAS: Dienst-SAS und Konto-SAS.

Die Dienst-SAS delegiert den Zugriff auf eine Ressource in nur einem der folgenden Speicherdienste: Blob Storage, Queue Storage, Table Storage oder File Storage.

Eine Konto-SAS delegiert den Zugriff auf Ressourcen in einem oder mehreren der Speicherdienste. Sie können den Zugriff auf Dienstebenenvorgänge delegieren, die nicht mit einer Dienst-SAS verfügbar sind. Sie können auch den Zugriff auf Lese-, Schreib- und Löschvorgänge in Blob-Containern, Tabellen, Warteschlangen und Dateifreigaben delegieren, die mit einer Dienst-SAS nicht zulässig sind.

Außerdem können Sie einen Container und die dazugehörigen Blobs (oder ein bestimmtes Blob) öffentlich verfügbar machen. Wenn Sie einen Container oder ein Blob als öffentliche Ressource konfigurieren, kann jeder Benutzer anonym und ohne Authentifizierung drauf zugreifen.  Mithilfe öffentlicher Container und Blobs können Sie Ressourcen wie Medien und Dokumente verfügbar machen, die auf Websites gehostet werden.  Zur Verringerung der Netzwerklatenz für ein globales Publikum können Sie von Websites verwendete Blobdaten in Azure CDN zwischenspeichern.

Weitere Informationen zu Shared Access Signatures finden Sie unter [Shared Access Signatures, Teil&1;: Grundlagen zum SAS-Modell](storage-dotnet-shared-access-signature-part-1.md) . Weitere Informationen zum sicheren Zugriff auf Ihr Speicherkonto finden Sie unter [Verwalten des anonymen Lesezugriffs auf Container und Blobs](storage-manage-access-to-resources.md) sowie unter [Authentication for the Azure Storage Services](https://msdn.microsoft.com/library/azure/dd179428.aspx) (Authentifizierung für die Azure Storage-Dienste).

## <a name="replication-for-durability-and-high-availability"></a>Replikation für Dauerhaftigkeit und hohe Verfügbarkeit
Die Daten in Ihrem Microsoft Azure-Speicherkonto werden stets repliziert, um Beständigkeit und hohe Verfügbarkeit sicherzustellen. Bei der Replikation werden Ihre Daten kopiert, und zwar entweder innerhalb desselben Rechenzentrums, oder in ein zweites Rechenzentrum. Dies hängt davon ab, welche Replikationsoption Sie wählen. Mit der Replikation werden Ihre Daten geschützt, und die Betriebszeit der Anwendung wird hoch gehalten, falls es zu vorübergehenden Hardwareausfällen kommt. Wenn Ihre Daten in einem zweiten Rechenzentrum repliziert werden, werden Ihre Daten außerdem vor einem Ausfall aufgrund einer Katastrophe am primären Standort geschützt.

Mit der Replikation wird sichergestellt, dass Ihr Speicherkonto auch bei Ausfällen die [Servicelevelvereinbarung (SLA) für Storage](https://azure.microsoft.com/support/legal/sla/storage/) erfüllt. Die Servicelevelvereinbarung enthält Informationen zu Azure Storage-Garantien in Bezug auf Dauerhaftigkeit und Verfügbarkeit.

Wenn Sie ein Speicherkonto erstellen, können Sie eine der folgenden Replikationsoptionen auswählen:

* **Lokal redundanter Speicher (LRS)** Lokal redundanter Speicher verwaltet drei Kopien Ihrer Daten. LRS wird innerhalb eines einzelnen Rechenzentrums dreimal in einer einzelnen Region repliziert. LRS schützt Ihre Daten vor normalen Hardwareausfällen, aber nicht vor dem Ausfall eines einzelnen Rechenzentrums.

    LRS wird zu günstigen Preisen angeboten. Für maximale Stabilität empfehlen wir, dass Sie georedundanten Speicher (nachfolgend beschrieben) verwenden.
* **Zonenredundanter Speicher (ZRS)** Zonenredundanter Speicher verwaltet drei Kopien Ihrer Daten. ZRS wird über zwei oder drei Standorte hinweg dreimal repliziert, entweder innerhalb einer einzelnen Region oder über zwei Regionen hinweg, wodurch eine höhere Stabilität als bei LRS entsteht. ZRS gewährleistet die Dauerhaftigkeit Ihrer Daten innerhalb einer einzelnen Region.

    ZRS bietet eine höhere Dauerhaftigkeit als LRS. Für maximale Dauerhaftigkeit empfehlen wir jedoch die Verwendung von georedundantem Speicher (siehe Beschreibung weiter unten).

  > [!NOTE]
  > ZRS ist derzeit nur für Blockblobs verfügbar und wird erst ab der Version 2014-02-14 unterstützt.
  >
  > Sobald Sie Ihr Speicherkonto erstellt und die ZRS ausgewählt haben, ist die Wahl eines anderen Replikationstyps nicht mehr möglich.
  >
  >
* **Georedundanter Speicher (GRS)**: GRS hält sechs Kopien Ihrer Daten vor. Mit GRS werden Ihre Daten dreimal innerhalb der primären Region und dreimal in einer sekundären Region repliziert, die hunderte Kilometer von der primären Region entfernt ist. Mit GRS werden Ihre Daten dreimal innerhalb der primären Region und dreimal in einer sekundären Region hunderte von Kilometern von der primären Region entfernt repliziert, wodurch höchste Stabilität erreicht wird. Im Falle eines Ausfalls in der primären Region führt Azure Storage ein Failover auf die sekundäre Region aus. Durch GRS wird die Dauerhaftigkeit Ihrer Daten in zwei separaten Regionen gewährleistet.

    Informationen zu den Kombinationen aus primären und sekundären Regionen finden Sie unter [Azure-Regionen](https://azure.microsoft.com/regions/).
* **Georedundanter Speicher mit Lesezugriff (RA-GRS)** Georedundanter Speicher mit Lesezugriff repliziert Ihre Daten an einen sekundären geografischen Standort und bietet außerdem Lesezugriff auf die Daten am sekundären Standort. Mithilfe von RA-GRS können Sie entweder vom primären oder vom sekundären Standort aus auf Ihre Daten zugreifen, falls einer der Standorte nicht mehr verfügbar ist. Bei der Erstellung Ihres Speicherkontos ist RA-GRS die Standardoption.

  > [!IMPORTANT]
  > Die Art der Datenreplikation kann nach der Speicherkontoerstellung geändert werden, sofern bei der Kontoerstellung nicht die ZRS-Option angegeben wurde. Beachten Sie jedoch, dass unter Umständen zusätzlich einmalige Datenübertragungskosten anfallen, wenn Sie von LRS zu GRS oder RA-GRS wechseln.
  >
  >

Weitere Details zu den Speicherreplikationsoptionen finden Sie unter [Azure-Speicherreplikation](storage-redundancy.md) .

Preisinformationen für die Speicherkontoreplikation finden Sie unter [Preise für Azure Storage](https://azure.microsoft.com/pricing/details/storage/). Darüber hinaus finden Sie unter [Azure-Regionen](https://azure.microsoft.com/regions/#services) weitere Informationen dazu, welche Dienste in den einzelnen Regionen verfügbar sind.

Architekturdetails zur Beständigkeit von Azure Storage finden Sie unter [SOSP Paper – Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)(SOSP-Dokument – Azure Storage: Ein hoch verfügbarer Cloud-Speicherdienst mit starker Konsistenz).

## <a name="transferring-data-to-and-from-azure-storage"></a>Übertragen von Daten in und aus Azure Storage
Über das Befehlszeilenprogramm AzCopy können Sie Blob-, Datei- und Tabellendaten innerhalb Ihres Speicherkontos oder zwischen Speicherkonten kopieren. Weitere Informationen finden Sie unter [Übertragen von Daten mit dem Befehlszeilenprogramm AzCopy](storage-use-azcopy.md) .

AzCopy baut auf der [Azure Storage Data Movement Library](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)auf, die derzeit als Vorschau verfügbar ist.

Mithilfe des Azure Import/Export-Diensts können Sie Blobdaten in Ihr Speicherkonto importieren oder Blobdaten aus Ihrem Speicherkonto exportieren, indem Sie eine Festplatte an das Azure-Rechenzentrum schicken. Weitere Informationen zu diesem Dienst finden Sie unter [Verwenden des Microsoft Azure Import/Export-Diensts zum Übertragen von Daten in den Blobspeicher](storage-import-export-service.md).

## <a name="pricing"></a>Preise
[!INCLUDE [storage-account-billing-include](../../includes/storage-account-billing-include.md)]

## <a name="storage-apis-libraries-and-tools"></a>Storage-APIs, -Bibliotheken und -Tools
Auf Azure Storage-Ressourcen kann über jede Sprache zugegriffen werden, die für HTTP/HTTPS-Anforderungen geeignet ist. Zusätzlich bietet Azure Storage Programmierbibliotheken für einige beliebte Sprachen. Diese Bibliotheken vereinfachen viele Aspekte der Arbeit mit Azure Storage und behandeln bestimmte Details wie synchrone und asynchrone Aufrufe, die Zusammenfassung von Vorgängen, die Ausnahmeverwaltung, automatische Wiederholungen nicht erfolgreicher Vorgänge, das Betriebsverhalten und Ähnliches. Bibliotheken sind aktuell für die folgenden Sprachen und Plattformen erhältlich. Weitere sind in Planung.

### <a name="azure-storage-data-services"></a>Azure Storage-Datendienste
* [REST-API für Speicherdienste](http://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Speicherclientbibliothek für .NET, Windows Phone und Windows-Runtime](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Speicherclientbibliothek für C++](https://github.com/Azure/azure-storage-cpp)
* [Speicherclientbibliothek für Java/Android](https://azure.microsoft.com/develop/java/)
* [Speicherclientbibliothek für Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Speicherclientbibliothek für PHP](https://azure.microsoft.com/develop/php/)
* [Speicherclientbibliothek für Ruby](https://azure.microsoft.com/develop/ruby/)
* [Speicherclientbibliothek für Python](https://azure.microsoft.com/develop/python/)
* [Storage-Cmdlets für PowerShell 1.0](https://msdn.microsoft.com/library/azure/mt269418.aspx)

### <a name="azure-storage-management-services"></a>Azure Storage-Verwaltungsdienste
* [Speicherressourcenanbieter – REST-API-Referenz](/rest/api/storagerp/)
* [Speicherressourcenanbieter – Clientbibliothek für .NET](/dotnet/api/microsoft.azure.management.storage)
* [Speicherressourcenanbieter – Cmdlets für PowerShell 1.0](/powershell/storage/)
* [Storage-Dienstverwaltung – REST-API (klassisch)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### <a name="azure-storage-data-movement-services"></a>Azure Storage-Datenverschiebungsdienste
* [Import/Export-Storage-Dienst – REST-API](storage-import-export-service.md)
* [Storage-Datenverschiebung – Clientbibliothek für .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### <a name="tools-and-utilities"></a>Tools und Hilfsprogramme
* [Azure-Speicher-Explorer](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [Azure Storage-Clienttools](storage-explorers.md)
* [Azure-SDKs und -Tools](https://azure.microsoft.com/tools/)
* [Azure-Speicheremulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azureps-cmdlets-docs)
* [Befehlszeilenprogramm AzCopy](http://aka.ms/downloadazcopy)

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zu Azure Storage finden Sie in den folgenden Ressourcen:

### <a name="documentation"></a>Dokumentation
* [Azure-Speicherdokumentation](https://azure.microsoft.com/documentation/services/storage/)
* [Erstellen Sie ein Speicherkonto](storage-create-storage-account.md)
* [Erste Schritte mit Azure Storage – Einstieg in fünf Minuten](storage-getting-started-guide.md)

### <a name="for-administrators"></a>Für Administratoren
* [Verwenden von Azure PowerShell mit Azure Storage](storage-powershell-guide-full.md)
* [Verwenden der Azure-Befehlszeilenschnittstelle mit Azure Storage](storage-azure-cli.md)

### <a name="for-net-developers"></a>Für .NET-Entwickler
* [Erste Schritte mit Azure Blob Storage mit .NET](storage-dotnet-how-to-use-blobs.md)
* [Erste Schritte mit Azure Table Storage mit .NET](storage-dotnet-how-to-use-tables.md)
* [Erste Schritte mit Azure Queue Storage mit .NET](storage-dotnet-how-to-use-queues.md)
* [Erste Schritte mit Azure File Storage unter Windows](storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Für Java-/Android-Entwickler
* [Gewusst wie: Verwenden von Blob Storage mit Java](storage-java-how-to-use-blob-storage.md)
* [Gewusst wie: Verwenden von Table Storage mit Java](storage-java-how-to-use-table-storage.md)
* [Gewusst wie: Verwenden von Queue Storage mit Java](storage-java-how-to-use-queue-storage.md)
* [Gewusst wie: Verwenden von File Storage mit Java](storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Für Node.js-Entwickler
* [Gewusst wie: Verwenden von Blob Storage mit Node.js](storage-nodejs-how-to-use-blob-storage.md)
* [Gewusst wie: Verwenden von Table Storage mit Node.js](storage-nodejs-how-to-use-table-storage.md)
* [Gewusst wie: Verwenden von Queue Storage mit Node.js](storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>Für PHP-Entwickler
* [Gewusst wie: Verwenden von Blob Storage mit PHP](storage-php-how-to-use-blobs.md)
* [Gewusst wie: Verwenden von Table Storage mit PHP](storage-php-how-to-use-table-storage.md)
* [Gewusst wie: Verwenden von Queue Storage mit PHP](storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Für Ruby-Entwickler
* [Gewusst wie: Verwenden von Blob Storage mit Ruby](storage-ruby-how-to-use-blob-storage.md)
* [Gewusst wie: Verwenden von Table Storage mit Ruby](storage-ruby-how-to-use-table-storage.md)
* [Gewusst wie: Verwenden von Queue Storage mit Ruby](storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Für Python-Entwickler
* [Gewusst wie: Verwenden von Blob Storage mit Python](storage-python-how-to-use-blob-storage.md)
* [Gewusst wie: Verwenden von Table Storage mit Python](storage-python-how-to-use-table-storage.md)
* [Gewusst wie: Verwenden von Queue Storage mit Python](storage-python-how-to-use-queue-storage.md)
* [Gewusst wie: Verwenden von Azure File Storage mit Python](storage-python-how-to-use-file-storage.md)

