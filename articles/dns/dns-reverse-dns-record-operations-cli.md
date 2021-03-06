---
title: "Verwalten von Reverse-DNS-Einträgen für Ihre Azure-Dienste mit der Azure-CLI | Microsoft Docs"
description: "Mit der Azure-Befehlszeilenschnittstelle im Ressourcen-Manager Ihre Reverse-DNS-Einträge oder PTR-Einträge für Ihre Dienste verwalten"
services: DNS
documentationcenter: na
author: s-malone
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: c655707e-1156-4893-b163-0b228ffd25d2
ms.service: DNS
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/28/2016
ms.author: smalone
translationtype: Human Translation
ms.sourcegitcommit: 0f8bc125855bc5a5b67fde5b0b742c73b5da7610
ms.openlocfilehash: b7c91d7c13884a00bb06a7cfed55a59b357f7d18


---
# <a name="how-to-manage-reverse-dns-records-for-your-azure-services-using-the-azure-cli"></a>Gewusst wie: Verwalten von Reverse-DNS-Einträgen für Ihre Dienste mit der Azure-CLI

[!INCLUDE [dns-reverse-dns-record-operations-arm-selectors-include.md](../../includes/dns-reverse-dns-record-operations-arm-selectors-include.md)]


[!INCLUDE [dns-reverse-dns-record-operations-intro-include.md](../../includes/dns-reverse-dns-record-operations-intro-include.md)]


[!INCLUDE [azure-arm-classic-important-include](../../includes/learn-about-deployment-models-rm-include.md)]

Weitere Informationen zum klassischen Bereitstellungsmodell finden Sie unter [Mit Azure PowerShell Ihre Reverse-DNS-Einträge für Ihre Dienste verwalten](dns-reverse-dns-record-operations-classic-ps.md).

## <a name="validation-of-reverse-dns-records"></a>Überprüfung der Reverse-DNS-Einträge
Um sicherzustellen, dass kein Dritter Reverse-DNS-Einträge erstellen kann, die Ihren Domänen zugeordnet sind, erlaubt Azure die Erstellung von Reverse-DNS-Einträgen nur, wenn Folgendes zutrifft:

* Der ReverseFqdn-Wert entspricht dem vollqualifizierte Domänennamen (FQDN) der öffentlichen IP-Adressressource, für die er angegeben wurde, oder er entspricht dem FQDN einer beliebigen öffentlichen IP-Adresse innerhalb des gleichen Abonnements (lautet also beispielsweise „contosoapp1.northus.cloudapp.azure.com.“).
* Der ReverseFqdn-Wert wird vorwärts zum Namen oder zur IP-Adresse der öffentlichen IP-Adresse aufgelöst, für die er angegeben wurde, oder zu einem FQDN einer beliebigen öffentlichen IP-Adresse bzw. zu einer IP-Adresse innerhalb des gleichen Abonnements. „ReverseFqdn“ lautet also beispielsweise „app1.contoso.com“. Dies ist ein CName-Alias für „contosoapp1.northus.cloudapp.azure.com“.

Überprüfungen werden nur durchgeführt, wenn die Reverse-DNS-Eigenschaft für eine öffentliche IP-Adresse eingerichtet oder geändert wird. Es finden keine regelmäßigen Neuüberprüfungen statt.

## <a name="add-reverse-dns-to-existing-public-ip-addresses"></a>Hinzufügen von Reverse-DNS zu vorhandenen öffentlichen IP-Adressen
Sie können mit „azure network public-ip set“ einer vorhandenen öffentlichen IP-Adresse Reverse-DNS hinzufügen:

    azure network public-ip set -n PublicIp -g NRP-DemoRG-PS -f contosoapp1.westus.cloudapp.azure.com.

Wenn Sie Reverse-DNS einer vorhandenen öffentlichen IP-Adresse hinzufügen möchten, die noch keinen DNS-Namen besitzt, müssen Sie auch einen DNS-Namen angeben. Hierzu können Sie „azure network public-ip set“ verwenden:

    azure network public-ip set -n PublicIp -g NRP-DemoRG-PS -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.

## <a name="create-a-public-ip-address-with-reverse-dns"></a>Erstellen einer öffentlichen IP-Adresse mit Reverse-DNS
Sie können eine neue öffentliche IP-Adresse mit der angegebenen Reverse-DNS-Eigenschaft hinzufügen, indem Sie „azure network public-ip create“ ausführen:

    azure network public-ip create -n PublicIp3 -g NRP-DemoRG-PS -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.

## <a name="view-reverse-dns-for-existing-public-ip-addresses"></a>Anzeigen von Reverse-DNS für vorhandene öffentliche IP-Adressen
Mithilfe von „azure network public-ip show“ können Sie den konfigurierten Wert für eine vorhandene öffentliche IP-Adresse anzeigen:

    azure network public-ip show -n PublicIp3 -g NRP-DemoRG-PS

## <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a>Entfernen Sie eine Reverse-DNS aus vorhandenen öffentlichen IP-Adressen.
Mithilfe von „azure network public-ip set“ können Sie eine Reverse-DNS-Eigenschaft aus einer öffentlichen IP-Adresse entfernen. Dies erfolgt, indem der ReverseFqdn-Eigenschaftswert auf „leer“ gesetzt wird:

    azure network public-ip set -n PublicIp3 -g NRP-DemoRG-PS –f “”

[!INCLUDE [FAQ1](../../includes/dns-reverse-dns-record-operations-faq-host-own-arpa-zone-include.md)]

[!INCLUDE [FAQ2](../../includes/dns-reverse-dns-record-operations-faq-arm-include.md)]




<!--HONumber=Nov16_HO3-->


