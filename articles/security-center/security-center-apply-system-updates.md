---
title: Anwenden von Systemupdates in Azure Security Center | Microsoft Docs
description: In diesem Dokument erfahren Sie, wie Sie die Azure Security Center-Empfehlungen **Systemupdates anwenden** und **Neustart nach Systemupdates** implementieren.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
translationtype: Human Translation
ms.sourcegitcommit: 53f4898f31ef19a39e1448235ed14c8fc7df7b3b
ms.openlocfilehash: 50cdea437db5387813c6a3905d14b6904d2aba34


---
# <a name="apply-system-updates-in-azure-security-center"></a>Anwenden von Systemupdates in Azure Security Center
Azure Security Center überprüft virtuelle Windows- und Linux-Computer (Virtual Machines, VMs) täglich auf fehlende Betriebssystemupdates. Security Center ruft eine Liste mit verfügbaren Sicherheitsupdates und wichtigen Updates von Windows Update oder WSUS (Windows Server Update Services) ab – je nachdem, welcher Dienst für einen virtuellen Windows-Computer konfiguriert ist.  Darüber hinaus prüft Security Center auch die neuesten Updates für Linux-Systeme. Falls auf Ihrem virtuellen Computer ein Systemupdate fehlt, empfiehlt Security Center die Anwendung von Systemupdates.

> [!NOTE]
> Der Dienst wird anhand einer Beispielbereitstellung vorgestellt.  Es ist keine schrittweise Anleitung.
>
>

## <a name="implement-the-recommendation"></a>Implementieren der Empfehlung
1. Wählen Sie auf dem Blatt **Empfehlungen** die Option **Systemupdates** anwenden aus.

   ![Systemupdates anwenden][1]
2. Das Blatt **Systemupdates anwenden** wird geöffnet und zeigt eine Liste mit virtuellen Computern an, bei denen Systemupdates fehlen. Wählen Sie einen virtuellen Computer aus.

   ![Auswählen eines virtuellen Computers][2]
3. Ein Blatt mit einer Liste fehlender Updates für den virtuellen Computer wird angezeigt. Wählen Sie ein Systemupdate aus. In diesem Beispiel wählen wir „KB3156016“ aus.

   ![Fehlende Sicherheitsupdates][3]

4. Führen Sie die auf dem Blatt **Sicherheitsupdate** angegebenen Schritte aus, um das fehlende Update anzuwenden.

   ![Sicherheitsupdate][4]

## <a name="reboot-after-system-updates"></a>Neustart nach Systemupdates
1. Kehren Sie zum Blatt **Empfehlungen** zurück. Nach dem Anwenden von Systemupdates wird ein neuer Eintrag namens **Neustart nach Systemupdates**generiert. Dieser Eintrag informiert Sie darüber, dass der virtuelle Computer neu gestartet werden muss, um das Anwenden der Systemupdates abzuschließen.

   ![Neustart nach Systemupdates][5]
2. Wählen Sie **Neustart nach Systemupdates**aus. Daraufhin wird das Blatt **Ein Neustart zum Abschließen der Systemupdates steht aus.** mit einer Liste virtueller Computer angezeigt, die neu gestartet werden müssen, um das Anwenden von Systemupdates abzuschließen.

   ![Neustart ausstehend][6]

Starten Sie den virtuellen Computer über Azure neu, um den Prozess abzuschließen.

## <a name="see-also"></a>Weitere Informationen
Weitere Informationen zu Security Center finden Sie in den folgenden Quellen:

* [Festlegen von Sicherheitsrichtlinien in Azure Security Center:](security-center-policies.md) Erfahren Sie, wie Sie Sicherheitsrichtlinien für Ihre Azure-Abonnements und -Ressourcengruppen konfigurieren.
* [Verwalten von Sicherheitsempfehlungen in Azure Security Center:](security-center-recommendations.md) Hier erfahren Sie, wie Empfehlungen Ihnen beim Schutz der Azure-Ressourcen helfen.
* [Überwachen der Sicherheitsintegrität in Azure Security Center:](security-center-monitoring.md) Erfahren Sie, wie Sie die Integrität Ihrer Azure-Ressourcen überwachen.
* [Verwalten von und Reagieren auf Sicherheitswarnungen in Azure Security Center:](security-center-managing-and-responding-alerts.md) Erfahren Sie, wie Sie Sicherheitswarnungen verwalten und darauf reagieren.
* [Überwachen von Partnerlösungen mit Azure Security Center:](security-center-partner-solutions.md) Erfahren Sie, wie der Integritätsstatus Ihrer Partnerlösungen überwacht wird.
* [Azure Security Center – Häufig gestellte Fragen:](security-center-faq.md) Hier finden Sie häufig gestellte Fragen zur Verwendung des Diensts.
* [Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/) (Blog zur Azure-Sicherheit): Hier finden Sie Blogbeiträge zur Sicherheit und Compliance von Azure.

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png



<!--HONumber=Feb17_HO1-->


