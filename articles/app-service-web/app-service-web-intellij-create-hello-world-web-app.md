---
title: Erstellen einer einfachen Azure-Web-App in IntelliJ | Microsoft-Dokumentation
description: "In diesem Tutorial erfahren Sie, wie Sie mit dem Azure-Toolkit für IntelliJ eine „Hello World“-Web-App für Azure erstellen."
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm;asirveda
translationtype: Human Translation
ms.sourcegitcommit: 2687011c449715d2ce5f491c3da501f38035d631
ms.openlocfilehash: 9c7b708c2bd923733cd034116453fcca2ada949b


---
# <a name="create-a-basic-azure-web-app-in-intellij"></a>Erstellen einer einfachen Azure-Web-App in IntelliJ
Dieses Tutorial zeigt das Erstellen und Bereitstellen einer einfachen „Hello World“-Anwendung in Azure als Web-App mithilfe des [Azure-Toolkits für IntelliJ]. Zur Vereinfachung wird ein grundlegendes JSP-Beispiel verwendet, aber mit einer ähnlichen Vorgehensweise können Sie auch ein Java-Servlet in Azure bereitstellen.

Wenn Sie dieses Tutorial abgeschlossen haben, entspricht Ihre Anwendung bei der Anzeige in einem Webbrowser etwa der folgenden Abbildung:

![Beispielwebseite][01]

## <a name="prerequisites"></a>Voraussetzungen
* Ein Java Developer Kit (JDK), Version 1.8 oder höher.
* IntelliJ IDEA Ultimate Edition. Diese können unter <https://www.jetbrains.com/idea/download/index.html> heruntergeladen werden.
* Eine Verteilung eines Java-basierten Webservers oder Anwendungsservers, wie z.B. [Apache Tomcat] oder [Jetty].
* Ein Azure-Abonnement, das Sie unter <https://azure.microsoft.com/free/> oder <http://azure.microsoft.com/pricing/purchase-options/> erhalten.
* Das [Azure-Toolkits für IntelliJ]. Informationen zum Installieren des Azure-Toolkits finden Sie unter [Installieren des Azure-Toolkits für IntelliJ].

## <a name="to-create-a-hello-world-application"></a>So erstellen Sie eine Hello World-Anwendung
Zunächst beginnen wir mit der Erstellung eines Java-Projekts.

1. Starten Sie IntelliJ, klicken Sie im Menü **Datei** auf **Neu** und dann auf **Projekt**.
   
    ![Datei Neu Projekt][02]
2. Wählen Sie im Dialogfeld „Neues Projekt“ nacheinander **Java** und **Webanwendung** aus, und klicken Sie dann auf **Neu**, um ein Projekt-SDK hinzuzufügen.
   
    ![Dialogfeld "Neues Projekt"][03a]
   
3. Wählen Sie im Dialogfeld für die Auswahl des Stammverzeichnisses für JDK den Ordner aus, in dem Ihr JDK installiert ist, und klicken Sie dann auf **OK**. Klicken Sie im Dialogfeld „Neues Projekt“ auf **Weiter**, um fortzufahren.
   
    ![Festlegen des JDK-Stammverzeichnisses][03b]
4. Für die Zwecke dieses Tutorials benennen Sie das Projekt mit **Java-Web-App-On-Azure**, und klicken Sie dann auf **Fertig stellen**.
   
    ![Dialogfeld "Neues Projekt"][04]
5. Erweitern Sie in der Projektexplorer-Ansicht von IntelliJ **Java-Web-App-On-Azure**, erweitern Sie anschließend **web**, und doppelklicken Sie dann auf **index.jsp**.
   
    ![Öffnen der Indexseite][05c]
6. Wenn in IntelliJ die Datei „index.jsp“ geöffnet wird, geben Sie den Text **Hello World!** ein, damit er dynamisch im vorhandenen `<body>`-Element angezeigt wird. Der aktualisierte `<body>` -Inhalt sollte in etwa wie folgt aussehen:
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. Speichern Sie die Datei „index.jsp“.

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a>So stellen Sie Ihre Anwendung in einem Azure-Web-App-Container bereit
Es gibt mehrere Möglichkeiten, eine Java-Webanwendung in Azure bereitzustellen. In diesem Tutorial wird eine der einfachsten beschrieben: Ihre Anwendung wird in einem Azure-Web-App-Container bereitgestellt – weder ein spezieller Projekttyp noch zusätzliche Tools sind erforderlich. Das JDK und die Webcontainersoftware werden von Azure für Sie bereitgestellt, sodass Sie weder ein eigenes JDK noch eigene Webcontainersoftware hochladen müssen; Sie benötigen lediglich Ihre Java Web-App. Darum dauert der Veröffentlichungsprozess für Ihre Anwendung nur Sekunden, nicht Minuten.

Vor der Veröffentlichung Ihrer Anwendung müssen Sie zuerst die Moduleinstellungen konfigurieren. Führen Sie dazu die folgenden Schritte aus:

1. Klicken Sie im Projektexplorer von IntelliJ mit der rechten Maustaste auf das Projekt **Java-Web-App-On-Azure** . Wenn das Kontextmenü angezeigt wird, klicken Sie auf **Moduleinstellungen öffnen**.

    ![Öffnen der Moduleinstellungen][05a]
2. Wenn das Dialogfeld „Projektstruktur“ angezeigt wird:

   a. Klicken Sie in der Liste der **Projekteinstellungen** auf **Artefakte**.
   b. Ändern Sie den Artefaktnamen im Feld **Name** so, dass er Leerzeichen oder Sonderzeichen enthält; dies ist erforderlich, da der Name im Uniform Resource Identifier (URI) verwendet wird.
   c. Ändern Sie den **Typ** in **Webanwendung: Archiv**.
   d. Klicken Sie auf **OK**, um das Dialogfeld mit der Projektstruktur zu schließen.

    ![Öffnen der Moduleinstellungen][05b]

Nachdem Sie die Moduleinstellungen konfiguriert haben, können Sie Ihre Anwendung mithilfe der folgenden Schritte in Azure veröffentlichen:

1. Klicken Sie im Projektexplorer von IntelliJ mit der rechten Maustaste auf das Projekt **Java-Web-App-On-Azure** . Wählen Sie im Kontextmenü **Azure** aus, und klicken Sie dann auf **Publish as Azure Web App...** (Als Azure-Web-App veröffentlichen).
   
    ![Kontextmenü zur Azure-Veröffentlichung][06]
2. Wenn Sie sich noch nicht über IntelliJ bei Azure angemeldet haben, werden Sie aufgefordert, sich bei Ihrem Azure-Konto anzumelden. (Wenn Sie über mehrere Azure-Konten verfügen, können einige der Eingabeaufforderungen während des Anmeldeprozesses mehrmals angezeigt werden, auch wenn sie scheinbar identisch sind. Befolgen Sie in diesem Fall weiterhin die Anweisungen zur Anmeldung.)
   
    ![Anmeldedialogfeld von Azure][07]
3. Nachdem Sie sich erfolgreich bei Ihrem Azure-Konto angemeldet haben, wird im Dialogfeld **Manage Subscriptions** (Abonnements verwalten) eine Liste der Abonnements angezeigt, die mit Ihren Anmeldeinformationen verknüpft sind. (Wenn mehrere Abonnements aufgeführt sind und Sie nur mit einer bestimmten Teilmenge davon arbeiten möchten, können Sie optional die Abonnements deaktivieren, die Sie nicht verwenden möchten.) Wenn Sie Ihre Abonnements ausgewählt haben, klicken Sie auf **Schließen**.
   
    ![Verwalten von Abonnements][08]
4. Wenn das Dialogfeld **Deploy to Azure Web App Container** (In Azure-Web-App-Container bereitstellen) angezeigt wird, werden alle Web-App-Container angezeigt, die Sie zuvor erstellt haben. Wenn Sie keine Container erstellt haben, ist die Liste leer.
   
    ![App-Container][09]
5. Wenn Sie zuvor keinen Azure-Web-App-Container erstellt haben, oder Sie Ihre Anwendung in einem neuen Container veröffentlichen möchten, führen Sie die folgenden Schritte aus. Wählen Sie andernfalls einen vorhandenen Web-App-Container aus, und fahren Sie mit Schritt 6 fort.
   
   1. Klicken Sie auf **+**
      
       ![App-Container hinzufügen][10]
   2. Das Dialogfeld **New Web App Container** (Neuer Web-App-Container) wird angezeigt, in dem Sie die nächsten Schritte ausführen.
      
       ![Neuer App-Container][11a]
   3. Geben Sie eine **DNS-Bezeichnung** für Ihren Web-App-Container ein; dies ist die Blatt-DNS-Bezeichnung der Host-URL für Ihre Webanwendung in Azure. Hinweis: Der Name muss verfügbar sein und den Azure-Web-App-Namenskonventionen entsprechen.
   4. Wählen Sie im Dropdownmenü **Web Container** (Webcontainer) die passende Software für Ihre Anwendung aus.
      
       Aktuell können Sie zwischen Tomcat 8, Tomcat 7 und Jetty 9 wählen. Azure stellt eine aktuelle Distribution der gewählten Software bereit und diese wird auf einer aktuellen Distribution von JDK 8 ausgeführt, die von Oracle erstellt und von Azure bereitgestellt wird.
   5. Wählen Sie im Dropdownmenü **Subscription** (Abonnement) das Abonnement aus, das Sie für diese Bereitstellung verwenden möchten.
   6. Wählen Sie im Dropdownmenü **Resource Group** (Ressourcengruppe) die Ressourcengruppe aus, der Sie Ihre Web-App zuordnen möchten. (Mithilfe von Azure-Ressourcengruppen können Sie verwandte Ressourcen gruppieren, um diese z.B. gemeinsam löschen zu können.)
      
       (Sie können eine vorhandene Ressourcengruppe auswählen (sofern vorhanden) und direkt mit Schritt g unten fortfahren oder die Schritte zum Erstellen einer neuen Ressourcengruppe ausführen:
      
      * Wählen Sie im Dropdownmenü **Ressourcengruppe** die Option **&lt;&lt;Neue Ressourcengruppe erstellen&gt;&gt;**.
      * Das Dialogfeld **New Resource Group** (Neue Ressourcengruppe) wird angezeigt:
        
          ![Neue Ressourcengruppe][12]
      * Geben Sie im Textfeld **Name** einen Namen für die neue Ressourcengruppe ein.
      * Wählen Sie im Dropdownmenü **Region** den entsprechenden Azure-Rechenzentrumsstandort für Ihre Ressourcengruppe aus.
      * Klicken Sie auf **OK**.
   7. Im Dropdownmenü **App Service Plan** (App Service-Plan) werden die App Service-Pläne aufgelistet, die der ausgewählten Ressourcengruppe zugeordnet sind. Ein App Service-Plan enthält verschiedene Informationen wie z.B. den Speicherort Ihrer Web-App, den Tarif und die Größe der Compute-Instanz. Da ein App Service-Plan für mehrere Web-Apps verwendet werden kann, wird er getrennt von einer bestimmten Web-App-Bereitstellung verwaltet.)
      
       Sie können einen vorhandenen App Service-Plan auswählen (sofern vorhanden) und direkt mit Schritt h unten fortfahren oder die folgenden Schritte ausführen, um einen neuen App Service-Plan zu erstellen:
      
      * Wählen Sie in der Dropdownliste **App Service-Plan** die Option **&lt;&lt;Neuen App Service-Plan erstellen&gt;&gt;**.
      * Das Dialogfeld **New App Service Plan** (Neuer App Service-Plan) wird angezeigt:
        
          ![Neuer App Service-Plan][13]
      * Geben Sie im Textfeld **Name** einen Namen für den neuen App Service-Plan ein.
      * Wählen Sie im Dropdownmenü **Location** (Standort) den entsprechenden Azure-Rechenzentrumsstandort für den Plan aus.
      * Wählen Sie im Dropdownmenü **Pricing Tier** (Tarif) die entsprechenden Preise für den Plan aus. Zu Testzwecken können Sie **Free**(Kostenlos) auswählen.
      * Wählen Sie im Dropdownmenü **Instance Size** (Instanzgröße) die entsprechende Instanzgröße für den Plan aus. Zu Testzwecken können Sie **Small**(Klein) wählen.
      * Klicken Sie auf **OK**.
   8. (Optional) Azure stellt standardmäßig automatisch eine aktuelle Distribution von Java 8 in Ihrem Web-App-Container als JVM bereit. Sie können jedoch eine andere JVM-Version und -Distribution auswählen. Führen Sie dazu die folgenden Schritte aus:
      
      * Klicken Sie im Dialogfeld **New Web App Container** (Neuer Web-App-Container) auf die Registerkarte **JDK**.
      * Folgende Optionen stehen zur Auswahl:
        
        * Bereitstellen des Standard-JDKs von Azure
        * Bereitstellen eines Drittanbieter-JDKs aus einer Dropdownliste mit zusätzlichen JDKs, die in Azure verfügbar sind
        * Bereitstellen eines benutzerdefinierten JDKs, das als ZIP-Datei verpackt und entweder öffentlich verfügbar sein oder sich in Ihrem Azure-Speicherkonto befinden muss
        
        ![New App Container (Neuer App-Container) Registerkarte „JDK“][11b]
   9. Wenn Sie alle oben genannten Schritte abgeschlossen haben, sollte das Dialogfeld „New Web App Container“ (Neuer Web-App-Container) folgender Abbildung ähneln:
      
       ![Neuer App-Container][14]
   10. Klicken Sie auf **OK** , um die Erstellung Ihres neuen Web-App-Containers abzuschließen.
       
        Warten Sie einige Sekunden, bis die Liste der Web-App-Container aktualisiert wurde. Ihr neu erstellter Web-App-Container sollte nun in der Liste angezeigt werden und markiert sein.
6. Sie sind nun bereit für die erste Bereitstellung der Web-App in Azure. Klicken Sie auf **OK**, um Ihre Java-Anwendung im ausgewählten Web-App-Container bereitzustellen. Standardmäßig wird die Anwendung als Unterverzeichnis des Anwendungsservers bereitgestellt. Wenn sie als Stammanwendung bereitgestellt werden soll, aktivieren Sie das Kontrollkästchen **Deploy to root** (In Stamm bereitstellen), bevor Sie auf **OK** klicken.
   
    ![In Azure bereitstellen][15]
7. Als Nächstes sollte das **Azure-Aktivitätsprotokoll** mit dem Bereitstellungsstatus der Web-App angezeigt werden.
   
    ![Statusanzeige][16]
   
    Die Bereitstellung Ihrer Web-App in Azure sollte nur einige Sekunden dauern. Wenn Ihre Anwendung bereit ist, wird in der Spalte **Veröffentlicht** in the **Veröffentlicht** angezeigt. Wenn Sie auf den Link klicken, gelangen Sie zur Startseite der bereitgestellten Web-App. Sie können auch anhand der Schritte im folgenden Abschnitt zu Ihrer Web-App navigieren.

## <a name="browsing-to-your-web-app-on-azure"></a>Navigieren zur Web-App in Azure
Um in Azure zu Ihrer Web-App zu navigieren, können Sie die Ansicht **Azure Explorer** verwenden.

Wenn die Ansicht **Azure Explorer** noch nicht geöffnet ist, können Sie sie öffnen, indem Sie in IntelliJ auf das Menü **Ansicht**, auf **Toolfenster** und dann auf **Service Explorer** klicken. Wenn Sie sich nicht bereits angemeldet haben, werden sie dazu aufgefordert.

Wenn die Ansicht **Azure Explorer** angezeigt wird, navigieren Sie mit folgenden Schritten zu Ihrer Web-App: 

1. Erweitern Sie den Knoten **Azure** .
2. Erweitern Sie den Knoten **Web Apps** (Web-Apps). 
3. Klicken Sie mit der rechten Maustaste auf die gewünschte Web-App.
4. Wenn das Kontextmenü angezeigt wird, klicken Sie auf **Im Browser öffnen**.
   
    ![Durchsuchen von Web-App][17]

## <a name="updating-your-web-app"></a>Aktualisieren Ihrer Web-App
Das Aktualisieren einer vorhandenen, ausgeführten Azure-Web-App ist ein schneller und einfacher Prozess, und Ihnen stehen zwei Optionen für die Aktualisierung zur Verfügung:

* Sie können die Bereitstellung einer vorhandenen Java-Web-App aktualisieren.
* Sie können eine weitere Java-Anwendung in dem gleichen Web-App-Container veröffentlichen.

In beiden Fällen ist der Prozess identisch und dauert nur wenige Sekunden:

1. Klicken Sie im Projektexplorer von IntelliJ mit der rechten Maustaste auf die Java-Anwendung, die Sie aktualisieren oder einem vorhandenen Web-App-Container hinzufügen möchten.
2. Wählen Sie im Kontextmenü **Azure** und dann **Publish as Azure Web App...** (Als Azure-Web-App veröffentlichen) aus.
3. Da Sie sich bereits zuvor angemeldet haben, sehen Sie eine Liste Ihrer vorhandenen Web-App-Container. Wählen Sie den Container aus, in dem Sie Ihre Java-Anwendung veröffentlichen oder erneut veröffentlichen möchten, und klicken Sie auf **OK**.

Wenige Sekunden später wird Ihre aktualisierte Bereitstellung in der Ansicht **Azure Activity Log** (Azure-Aktivitätsprotokoll) als **Published** (Veröffentlicht) angezeigt, und Sie können die aktualisierte Anwendung in einem Webbrowser überprüfen.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Starten, Beenden oder Neustarten einer vorhandenen Web-App
Um einen vorhandenen Azure-Web-App-Container zu starten oder zu beenden (einschließlich aller darin bereitgestellten Java-Anwendungen), können Sie die Ansicht **Azure Explorer** verwenden.

Wenn die Ansicht **Azure Explorer** noch nicht geöffnet ist, können Sie sie öffnen, indem Sie in IntelliJ auf das Menü **Ansicht**, auf **Toolfenster** und dann auf **Service Explorer** klicken. Wenn Sie sich nicht bereits angemeldet haben, werden sie dazu aufgefordert.

Wenn die Ansicht **Azure Explorer** angezeigt wird, starten oder beenden Sie Ihre Web-App mit folgenden Schritten: 

1. Erweitern Sie den Knoten **Azure** .
2. Erweitern Sie den Knoten **Web Apps** (Web-Apps). 
3. Klicken Sie mit der rechten Maustaste auf die gewünschte Web-App.
4. Wenn das Kontextmenü angezeigt wird, klicken Sie auf **Starten**, **Beenden** oder **Neu starten**. Beachten Sie, dass die Menüoptionen kontextabhängig sind. Sie können nur eine ausgeführte Web-App beenden oder eine Web-App starten, die zurzeit nicht ausgeführt wird.
   
    ![Beenden von Web-App][18]

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zu den Azure-Toolkits für Java-IDEs finden Sie unter den folgenden Links:

* [Azure-Toolkit für Eclipse]
  * [Installation des Azure Toolkit für Eclipse]
  * [Erstellen einer „Hello World“-Web-App für Azure in Eclipse]
  * [Neuerungen im Azure-Toolkit für Eclipse]
* [Azure-Toolkits für IntelliJ]
  * [Installieren des Azure-Toolkits für IntelliJ]
  * *Erstellen einer „Hello World“-Web-App für Azure in IntelliJ (dieser Artikel)*
  * [Neuerungen im Azure-Toolkit für IntelliJ]

<a name="see-also"></a>

## <a name="see-also"></a>Weitere Informationen
Weitere Informationen zum Verwenden von Azure mit Java finden Sie im [Azure Java Developer Center].

Weitere Informationen zum Erstellen von Azure-Web-Apps finden Sie unter [Web-Apps – Übersicht].

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure-Toolkit für Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure-Toolkits für IntelliJ]: ../azure-toolkit-for-intellij.md
[Erstellen einer „Hello World“-Web-App für Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Installation des Azure Toolkit für Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Installieren des Azure-Toolkits für IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Neuerungen im Azure-Toolkit für Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[Neuerungen im Azure-Toolkit für IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Web-Apps – Übersicht]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png



<!--HONumber=Feb17_HO2-->


