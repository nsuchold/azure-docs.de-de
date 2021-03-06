---
title: 'Tutorial: Azure Active Directory-Integration mit Box | Microsoft Docs'
description: "Erfahren Sie, wie Sie Box mit Azure Active Directory verwenden können, um einmaliges Anmelden, automatisierte Bereitstellung und vieles mehr zu ermöglichen."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/29/2016
ms.author: jeedes
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: c8254f41006c36509af3626cb14825602e6a4adb


---
# <a name="tutorial-azure-active-directory-integration-with-box"></a>Tutorial: Azure Active Directory-Integration mit Box
In diesem Tutorial wird die Integration von Azure und Box erläutert.  
Das in diesem Lernprogramm verwendete Szenario setzt voraus, dass Sie bereits über die folgenden Elemente verfügen:

* Ein gültiges Azure-Abonnement
* Ein Testmandant bei Box

Nach Abschluss dieses Tutorials können sich die Azure AD-Benutzer, die Sie Box zugewiesen haben, mithilfe des einmaligen Anmeldens auf der Box-Unternehmenswebsite bei der Anwendung anmelden (durch den Dienstanbieter initiierte Anmeldung). Sie können aber auch den Zugriffsbereich nutzen (siehe [Einführung in den Zugriffsbereich](active-directory-saas-access-panel-introduction.md)).

Das in diesem Tutorial beschriebene Szenario besteht aus den folgenden Bausteinen:

1. Aktivieren der Anwendungsintegration für Box
2. Konfigurieren der einmaligen Anmeldung
3. Konfigurieren der Benutzer- und Gruppenbereitstellung
4. Zuweisen von Benutzern

![Szenario](./media/active-directory-saas-box-tutorial/IC769537.png "Scenario")

## <a name="enabling-the-application-integration-for-box"></a>Aktivieren der Anwendungsintegration für Box
In diesem Abschnitt wird beschrieben, wie Sie die Anwendungsintegration für Box aktivieren.

### <a name="to-enable-the-application-integration-for-box-perform-the-following-steps"></a>So aktivieren Sie die Anwendungsintegration für Box
1. Klicken Sie im klassischen Azure-Portal im linken Navigationsbereich auf **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-box-tutorial/IC700993.png "Active Directory")
2. Wählen Sie in der Liste **Verzeichnis** das Verzeichnis aus, für das Sie die Verzeichnisintegration aktivieren möchten.
3. Klicken Sie zum Öffnen der Anwendungsansicht in der oberen Menüleiste der Verzeichnisansicht auf **Anwendungen** .
   
   ![Anwendungen](./media/active-directory-saas-box-tutorial/IC700994.png "Applications")
4. Klicken Sie unten auf der Seite auf **Hinzufügen** .
   
   ![Anwendung hinzufügen](./media/active-directory-saas-box-tutorial/IC749321.png "Add application")
5. Klicken Sie im Dialogfeld **Was möchten Sie tun?** auf **Anwendung aus dem Katalog hinzufügen**.
   
   ![Anwendung aus dem Katalog hinzufügen](./media/active-directory-saas-box-tutorial/IC749322.png "Add an application from gallerry")
6. Geben Sie im **Suchfeld** als Suchbegriff **Box** ein.
   
   ![Anwendungskatalog](./media/active-directory-saas-box-tutorial/IC701023.png "Application gallery")
7. Wählen Sie im Ergebnisbereich **Box** aus, und klicken Sie dann auf **Abschließen**, um die Anwendung hinzuzufügen.
   
   ![Box](./media/active-directory-saas-box-tutorial/IC701024.png "Box")

## <a name="configuring-single-sign-on"></a>Konfigurieren der einmaligen Anmeldung
In diesem Abschnitt wird erläutert, wie Sie es Benutzern mithilfe einer Verbundanmeldung auf Basis des SAML-Protokolls ermöglichen, sich mit ihrem Azure AD-Konto bei Box zu authentifizieren. Im Rahmen dieses Verfahrens müssen Sie Metadaten auf Box.com hochladen.

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a>So konfigurieren Sie einmaliges Anmelden
1. Klicken Sie im klassischen Azure-Portal auf der Anwendungsintegrationsseite für **Box** auf **Einmaliges Anmelden konfigurieren**, um das Dialogfeld **Einmaliges Anmelden konfigurieren** zu öffnen.
   
   ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-box-tutorial/IC769538.png "Configure single sign-on")
2. Wählen Sie auf der Seite **Wie sollen sich Benutzer bei Box anmelden?** die Option **Microsoft Azure AD – einmaliges Anmelden** aus, und klicken Sie dann auf **Weiter**.
   
   ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-box-tutorial/IC769539.png "Configure single sign-on")
3. Geben Sie auf der Seite **App-URL konfigurieren** im Textfeld für die **Box-Mandanten-URL** die URL Ihres Box-Mandanten ein (z.B. https://<mydomainname>.box.com), und klicken Sie auf **Weiter**.
   
   ![App-URL konfigurieren](./media/active-directory-saas-box-tutorial/IC669826.png "Configure app URL")
4. Klicken Sie auf der Seite **Einmaliges Anmelden konfigurieren für Box** auf **Metadaten herunterladen**, und speichern Sie die Datendatei lokal auf Ihrem Computer.
   
   ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-box-tutorial/IC669824.png "Configure single sign-on")
5. Leiten Sie die Metadatendatei an das Supportteam von Box weiter. Das Supportteam muss ein einmaliges Anmelden für Sie konfigurieren.
6. Bestätigen Sie die Konfiguration des einmaligen Anmeldens, und klicken Sie dann auf **Abschließen**, um das Dialogfeld **Einmaliges Anmelden konfigurieren** zu schließen.
   
   ![Configure single sign-on](./media/active-directory-saas-box-tutorial/IC769540.png "Configure single sign-on")
   
   ## <a name="configuring-user-provisioning"></a>Konfigurieren der Benutzerbereitstellung

In diesem Abschnitt wird erläutert, wie Sie die Bereitstellung von Active Directory-Benutzerkonten für Box aktivieren.

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a>So konfigurieren Sie einmaliges Anmelden
1. Klicken Sie im klassischen Azure-Portal auf der Anwendungsintegrationsseite für **Box** auf **Benutzerbereitstellung konfigurieren**, um das Dialogfeld **Benutzerbereitstellung konfigurieren** zu öffnen. 
   
    ![Automatische Benutzerbereitstellung aktivieren](./media/active-directory-saas-box-tutorial/IC769541.png "Enable automatic user provisioning")
2. Klicken Sie auf der Dialogfeldseite **Benutzerbereitstellung aktivieren für Box** auf **Benutzerbereitstellung aktivieren**. 
   
    ![Automatische Benutzerbereitstellung aktivieren](./media/active-directory-saas-box-tutorial/IC769544.png "Enable automatic user provisioning")
3. Stellen Sie auf der Seite **Anmelden, um Zugriff auf Box zu gewähren** die erforderlichen Anmeldeinformationen bereit, und klicken Sie dann auf **Autorisieren**. 
   
    ![Automatische Benutzerbereitstellung aktivieren](./media/active-directory-saas-box-tutorial/IC769546.png "Enable automatic user provisioning")
4. Klicken Sie auf **Zugriff gewähren auf Box** , um diesen Vorgang zu autorisieren und zum klassischen Azure-Portal zurückzukehren. 
   
    ![Automatische Benutzerbereitstellung aktivieren](./media/active-directory-saas-box-tutorial/IC769549.png "Enable automatic user provisioning")
5. Auf der Seite **Bereitstellungsoptionen** können Sie mit den Kontrollkästchen **Bereitzustellende Objekttypen** auswählen, ob neben Benutzerobjekten auch Gruppenobjekte in Box bereitgestellt werden.  Weitere Informationen finden Sie weiter unter im Abschnitt „Zuweisen von Benutzern und Gruppen“.
6. Klicken Sie zum Abschließen der Konfiguration auf die Schaltfläche „Abschließen“. 
   
    ![Automatische Benutzerbereitstellung aktivieren](./media/active-directory-saas-box-tutorial/IC769551.png "Enable automatic user provisioning")

## <a name="assigning-a-test-user"></a>Zuweisen eines Testbenutzers
Um Ihre Konfiguration zu testen, müssen Sie den Azure AD-Benutzern, denen Sie die Verwendung Ihrer Anwendung ermöglichen möchten, Zugriff auf die Anwendung gewähren. Weisen Sie dazu der Anwendung Benutzer zu.

### <a name="to-assign-users-to-box-perform-the-following-steps"></a>So weisen Sie Box Benutzer zu
1. Erstellen Sie im klassischen Azure-Portal ein Testkonto.
2. Klicken Sie auf der Anwendungsintegrationsseite für **Box** auf **Benutzer zuweisen**. 
   
    ![Benutzer zuweisen](./media/active-directory-saas-box-tutorial/IC769552.png "Assign users")
3. Wählen Sie den Testbenutzer aus, klicken Sie auf **Zuweisen** und anschließend auf **Ja**, um die Zuweisung zu bestätigen. 
   
   ![Ja](./media/active-directory-saas-box-tutorial/IC767830.png "Yes")

Nach 10 Minuten können Sie überprüfen, ob das Konto mit Box synchronisiert wurde.

Als ersten Überprüfungsschritt können Sie den Bereitstellungsstatus überprüfen, indem Sie im klassischen Azure-Portal auf der Anwendungsintegrationsseite für Box auf „Dashboard“ klicken.

![Dashboard](./media/active-directory-saas-box-tutorial/IC769553.png "Dashboard")

Ein erfolgreich abgeschlossener Benutzerbereitstellungszyklus wird durch einen entsprechenden Status angezeigt:

![Integrationsstatus](./media/active-directory-saas-box-tutorial/IC769555.png "Integration status")

In Ihrem Box-Mandanten werden synchronisierte Benutzer in der **Verwaltungskonsole** unter **Verwaltete Benutzer** aufgelistet.

![Integrationsstatus](./media/active-directory-saas-box-tutorial/IC769556.png "Integration status")

## <a name="assigning-users-and-groups"></a>Zuweisen von Benutzern und Gruppen
Auf der Registerkarte **Box > Benutzer und Gruppen** im klassischen Azure-Portal können Sie angeben, welchen Benutzern und Gruppen Zugriff auf Box gewährt werden soll. Durch die Zuweisung eines Benutzers oder einer Gruppe geschieht Folgendes:

* Azure AD ermöglicht es dem zugewiesenen Benutzer (entweder durch direkte Zuweisung oder durch eine Gruppenmitgliedschaft), sich bei Box zu authentifizieren. Wenn ein Benutzer nicht zugewiesen ist, lässt Azure AD eine Anmeldung bei Box nicht zu und gibt auf der Azure AD-Anmeldeseite einen Fehler zurück.
* Eine App-Kachel für Box wird dem [Anwendungsstartprogramm](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)des Benutzers hinzugefügt.
* Wenn die automatische Bereitstellung aktiviert ist, werden die zugewiesenen Benutzer und/oder Gruppen der Bereitstellungswarteschlange hinzugefügt, damit sie automatisch bereitgestellt werden.
  
  * Wenn nur Benutzerobjekte zur Bereitstellung konfiguriert wurden, werden alle direkt zugewiesenen Benutzer in der Bereitstellungswarteschlange platziert. Zudem werden alle Benutzer, die Mitglieder von zugewiesenen Gruppen sind, in die Bereitstellungswarteschlange aufgenommen. 
  * Wenn Gruppenobjekte zur Bereitstellung konfiguriert wurden, werden alle zugewiesenen Gruppenobjekte in Box bereitgestellt. Darüber hinaus werden auch alle Benutzer bereitgestellt, die Mitglieder dieser Gruppen sind. Die Gruppen- und Benutzermitgliedschaften bleiben erhalten, nachdem sie an Box übertragen wurden.

Auf der Registerkarte **Attribute > Einmaliges Anmelden** können Sie konfigurieren, welche Benutzerattribute (oder Ansprüche) in Box während der SAML-basierten Authentifizierung angezeigt werden. Auf der Registerkarte **Attribute > Bereitstellung** können Sie konfigurieren, wie Benutzer- und Gruppenattribute während der Bereitstellung von Azure AD an Box übertragen werden. Weitere Informationen finden Sie in den unten aufgeführten Ressourcen.

## <a name="additional-resources"></a>Zusätzliche Ressourcen
* [Anpassen ausgestellter Ansprüche im SAML-Token](active-directory-saml-claims-customization.md)
* [Bereitstellung: Anpassen von Attributzuordnungen](active-directory-saas-customizing-attribute-mappings.md)
* [Liste der Tutorials zur Integration von SaaS-Apps in Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](active-directory-appssoaccess-whatis.md)




<!--HONumber=Nov16_HO3-->


