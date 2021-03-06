---
title: Docker-Containercluster in der Azure-Cloud | Microsoft-Dokumentation
description: "Azure Container Service bietet eine Möglichkeit zur Vereinfachung der Erstellung, Konfiguration und Verwaltung eines Clusters virtueller Computer, die für die Ausführung von Anwendungen in Containern vorkonfiguriert sind."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Container, Microservices, Mesos, Azure
ms.assetid: 52da4163-1182-4b2e-be00-4951e5c1da16
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: rogardle
translationtype: Human Translation
ms.sourcegitcommit: 2a381431acb6436ddd8e13c69b05423a33cd4fa6
ms.openlocfilehash: a11b133794f7aedfa6740757fd8c1e89da665744
ms.lasthandoff: 02/22/2017


---
# <a name="azure-container-service-introduction"></a>Einführung in Azure Container Service
Azure Container Service (ACS) vereinfacht Ihnen das Erstellen, Konfigurieren und Verwalten eines Clusters virtueller Computer, die für die Ausführung von Anwendungen in Containern vorkonfiguriert sind. Der Dienst verwendet eine optimierte Konfiguration gängiger Tools für Open-Source-Planung und Orchestrierung. So können Sie Ihre vorhandenen Kenntnisse nutzen, bzw. auf einen großen und wachsenden Pool von Communityfachkenntnissen zur Bereitstellung und Verwaltung von containerbasierten Anwendungen in Microsoft Azure zurückgreifen.

![Azure Container Service bietet eine Möglichkeit, Anwendungen, die in Containern ausgeführt werden, auf mehreren Hosts in Azure zu verwalten.](./media/acs-intro/acs-cluster-new.png)

Azure Container Service nutzt das Docker-Containerformat, um sicherzustellen, dass Ihre Anwendungscontainer vollständig portierbar sind. Der Dienst unterstützt außerdem Marathon und DC/OS, Docker Swarm oder Kubernetes, sodass Sie diese Anwendungen auf Tausende und sogar Zehntausende von Containern skalieren können.

Mit dem Azure Container Service können Sie die Unternehmensfunktionen von Azure nutzen, während gleichzeitig die Anwendungsportierbarkeit erhalten bleibt, auch auf den Orchestrierungsebenen.

## <a name="using-azure-container-service"></a>Verwenden von Azure Container Service
Mit dem Azure Container Service verfolgen wir das Ziel, mit Open Source-Tools und -Technologien, die heutzutage bei unseren Kunden beliebt sind, eine Umgebung für das Containerhosting bereitzustellen. Zu diesem Zweck machen wir die Standard-API-Endpunkte für den von Ihnen ausgewählten Orchestrator (DC/OS, Docker Swarm oder Kubernetes) verfügbar. Mithilfe dieser Endpunkte können Sie jede Software nutzen, die mit diesen Endpunkten kommunizieren kann. Im Fall des Docker Swarm-Endpunkts können Sie z. B. die Docker-Befehlszeilenschnittstelle (Command-Line Interface, CLI) verwenden. Für DC/OS können Sie beispielsweise die DCOS-CLI wählen. Für Kubernetes können Sie `kubectl` wählen.

## <a name="creating-a-docker-cluster-by-using-azure-container-service"></a>Erstellen eines Docker-Clusters mit Azure Container Service
Stellen Sie zum Verwenden von Azure Container Service zunächst einen Azure Container Service-Cluster über das Portal bereit (suchen Sie auf dem Marketplace nach **Azure Container Service**). Verwenden Sie hierzu entweder eine Azure Resource Manager-Vorlage ([Docker Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm), [DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos) oder [Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)) oder [Azure CLI 2.0](container-service-create-acs-cluster-cli.md). Die bereitgestellten Schnellstartvorlagen können auch so geändert werden, dass sie eine zusätzliche oder erweiterte Azure-Konfiguration enthalten. Weitere Informationen finden Sie unter [Bereitstellen eines Azure Container Service-Clusters](container-service-deployment.md).

## <a name="deploying-an-application"></a>Bereitstellen einer Anwendung
Azure Container Service ermöglicht die Auswahl von Docker Swarm, DC/OS oder Kubernetes zur Orchestrierung. Wie Sie Ihre Anwendung bereitstellen, hängt davon ab, welchen Orchestrator Sie wählen.

### <a name="using-dcos"></a>Verwenden von DC/OS
DC/OS ist ein verteiltes Betriebssystem und basiert auf dem Apache Mesos-Kernel für verteilte Systeme. Apache Mesos stammt von der Apache Software Foundation. Zu seinen Benutzern und Mitwirkenden zählen einige der [größten Namen im IT-Bereich](http://mesos.apache.org/documentation/latest/powered-by-mesos/).

![Für DC/OS konfigurierter Azure Container Service mit angezeigten Agents und Mastern.](media/acs-intro/dcos.png)

Die Features von DC/OS und Apache Mesos können sich sehen lassen:

* Bewährte Skalierbarkeit
* Fehlertolerant replizierte Master und Slaves mit Apache ZooKeeper
* Unterstützung von Containern im Docker-Format
* Native Isolierung zwischen Aufgaben mit Linux-Containern
* Zeitplanung von mehreren Ressourcen (Arbeitsspeicher, CPU, Datenträger und Ports)
* Java-, Python- und C++-APIs zur Entwicklung neuer paralleler Anwendungen
* Eine Webbenutzeroberfläche zum Anzeigen von Clusterzuständen

Unter dem Azure-Containerdienst beinhaltet DC/OS standardmäßig die Marathon-Orchestrierungsplattform für die Workloadplanung. Zur DC/OS-Bereitstellung von ACS gehört aber das Mesosphere Universe mit Diensten, die Ihrem Dienst hinzugefügt werden können. Zu den Universe-Diensten gehören Spark, Hadoop, Cassandra und noch viele weitere Dienste.

![DC/OS Universe in Azure Container Service](media/dcos/universe.png)

#### <a name="using-marathon"></a>Verwenden von Marathon
Marathon ist ein clusterweites Initialisierungs- und Steuerungssystem für Dienste in cgroups – oder, im Fall von Azure Container Service, in Containern im Docker-Format. Marathon verfügt über eine Webbenutzeroberfläche, über die Sie Ihre Anwendungen bereitstellen können. Der Zugriff erfolgt über eine URL, die in etwa wie folgt aussieht: `http://DNS_PREFIX.REGION.cloudapp.azure.com`. „DNS\_PREFIX“ und „REGION“ werden erst zum Zeitpunkt der Bereitstellung definiert. Natürlich können Sie auch Ihren eigenen DNS-Namen angeben. Weitere Informationen zum Ausführen eines Containers über die Marathon-Webbenutzeroberfläche finden Sie unter [Verwalten eines Azure Container Service-DC/OS-Clusters über die Marathon-Webbenutzeroberfläche](container-service-mesos-marathon-ui.md).

![Liste der Marathon-Anwendungen](media/dcos/marathon-applications-list.png)

Sie können auch die REST-APIs für die Kommunikation mit Marathon verwenden. Es gibt eine Reihe von Clientbibliotheken, die für jedes Tool verfügbar sind. Sie decken zahlreiche Sprachen ab – und natürlich können Sie das HTTP-Protokoll in einer beliebigen Sprache verwenden. Darüber hinaus bieten viele beliebte DevOps-Tools Unterstützung für Marathon. Dies bietet maximale Flexibilität für Ihr Arbeitsteam, wenn es in einem Azure Container Service-Cluster arbeitet. Weitere Informationen zum Ausführen eines Containers über die Marathon-REST-API finden Sie unter [DC/OS-Containerverwaltung über die Marathon-REST-API](container-service-mesos-marathon-rest.md).

### <a name="using-docker-swarm"></a>Verwenden von Docker Swarm
Docker Swarm bietet eine systemeigene Clusterfunktion für Docker. Da Docker die Standard-API von Docker Swarm bedient, kann jedes Tool, das bereits mit einem Docker-Daemon kommuniziert, Swarm verwenden, um transparent auf mehreren Hosts in Azure Container Service zu skalieren.

![Konfiguration von Azure Container Service für die Verwendung von Swarm](media/acs-intro/acs-swarm2.png)

Unterstützte Tools für die Verwaltung von Containern auf einem Swarm-Cluster sind u. a. folgende:

* Dokku
* Docker CLI und Docker Compose
* Krane
* Jenkins

### <a name="using-kubernetes"></a>Verwenden von Kubernetes
Kubernetes ist ein beliebtes Open Source-Tool für die Containerorchestrierung in der Produktion. Kubernetes automatisiert die Bereitstellung, Skalierung und Verwaltung von Anwendungen in Containern. Als Open Source-Lösung, die von der Open Source-Community unterstützt wird, kann das Tool nahtlos in Azure Container Service ausgeführt und für die Bereitstellung einer großen Anzahl von Containern in Azure Container Service verwendet werden.

![Konfiguration von Azure Container Service für die Verwendung von Kubernetes](media/acs-intro/kubernetes.png)

Das Tool bietet zahlreiche Funktionen, darunter:
* Horizontale Skalierung
* Dienstermittlung und Lastenausgleich
* Geheimnis- und Konfigurationsverwaltung
* API-basierte automatisierte Rollouts und Rollbacks
* Selbstreparatur




## <a name="videos"></a>Videos
Erste Schritte mit dem Azure Container Service:  

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Container-Service-101/player]
>
>

Erstellen von Anwendungen mithilfe von Azure Container Service (Build 2016)

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/B822/player]
>
>

## <a name="next-steps"></a>Nächste Schritte

Stellen Sie einen Azure Container Service-Cluster über das [Portal](container-service-deployment.md) oder mithilfe von [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) bereit.
