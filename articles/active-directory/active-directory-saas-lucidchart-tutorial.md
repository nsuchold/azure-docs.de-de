---
title: 'Tutorial: Azure Active Directory-Integration mit Lucidchart | Microsoft Docs'
description: "Erfahren Sie, wie Sie Lucidchart mit Azure Active Directory verwenden können, um einmaliges Anmelden, automatisierte Bereitstellung und vieles mehr zu ermöglichen."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/29/2016
ms.author: jeedes
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 8386497b457f63ba0b62f50301ce3948ce060b97


---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a>Tutorial: Azure Active Directory-Integration mit Lucidchart
In diesem Tutorial wird die Integration von Azure und Lucidchart erläutert.  
Das in diesem Lernprogramm verwendete Szenario setzt voraus, dass Sie bereits über die folgenden Elemente verfügen:

* Ein gültiges Azure-Abonnement
* Ein Lucidchart-Software-Abonnement, für das das einmalige Anmelden aktiviert ist.

Nach Abschluss dieses Tutorials können sich die Azure AD-Benutzer, die Sie Lucidchart zugewiesen haben, mittels einmaligen Anmeldens auf Ihrer Lucidchart-Unternehmenswebsite bei der Anwendung anmelden (durch den Dienstanbieter initiierte Anmeldung). Alternativ können sie den Zugriffsbereich nutzen (siehe [Einführung in den Zugriffsbereich](active-directory-saas-access-panel-introduction.md)).

Das in diesem Tutorial beschriebene Szenario besteht aus den folgenden Bausteinen:

1. Aktivieren der Anwendungsintegration für Lucidchart
2. Konfigurieren der einmaligen Anmeldung
3. Konfigurieren der Benutzerbereitstellung
4. Zuweisen von Benutzern

![Szenario](./media/active-directory-saas-lucidchart-tutorial/IC791183.png "Scenario")

## <a name="enabling-the-application-integration-for-lucidchart"></a>Aktivieren der Anwendungsintegration für Lucidchart
In diesem Abschnitt wird beschrieben, wie Sie die Anwendungsintegration für Lucidchart aktivieren.

### <a name="to-enable-the-application-integration-for-lucidchart-perform-the-following-steps"></a>So aktivieren Sie die Anwendungsintegration für Lucidchart
1. Klicken Sie im klassischen Azure-Portal im linken Navigationsbereich auf **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-lucidchart-tutorial/IC700993.png "Active Directory")
2. Wählen Sie in der Liste **Verzeichnis** das Verzeichnis aus, für das Sie die Verzeichnisintegration aktivieren möchten.
3. Klicken Sie zum Öffnen der Anwendungsansicht in der oberen Menüleiste der Verzeichnisansicht auf **Anwendungen** .
   
   ![Anwendungen](./media/active-directory-saas-lucidchart-tutorial/IC700994.png "Applications")
4. Klicken Sie unten auf der Seite auf **Hinzufügen** .
   
   ![Anwendung hinzufügen](./media/active-directory-saas-lucidchart-tutorial/IC749321.png "Add application")
5. Klicken Sie im Dialogfeld **Was möchten Sie tun?** auf **Anwendung aus dem Katalog hinzufügen**.
   
   ![Anwendung aus dem Katalog hinzufügen](./media/active-directory-saas-lucidchart-tutorial/IC749322.png "Add an application from gallerry")
6. Geben Sie im **Suchfeld** als Suchbegriff **Lucidchart** ein.
   
   ![Anwendungskatalog](./media/active-directory-saas-lucidchart-tutorial/IC791184.png "Application Gallery")
7. Wählen Sie im Ergebnisbereich **Lucidchart** aus, und klicken Sie dann auf **Abschließen**, um die Anwendung hinzuzufügen.
   
   ![Lucidchart](./media/active-directory-saas-lucidchart-tutorial/IC791185.png "Lucidchart")
   
   ## <a name="configuring-single-sign-on"></a>Konfigurieren der einmaligen Anmeldung

In diesem Abschnitt wird erläutert, wie Sie es Benutzern mithilfe einer Verbundanmeldung auf Basis des SAML-Protokolls ermöglichen, sich mit ihrem Azure AD-Konto bei Lucidchart zu authentifizieren.

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a>So konfigurieren Sie einmaliges Anmelden
1. Klicken Sie im klassischen Azure-Portal auf der Anwendungsintegrationsseite für **Lucidchart** auf **Einmaliges Anmelden konfigurieren**, um das Dialogfeld **Einmaliges Anmelden konfigurieren** zu öffnen.
   
   ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-lucidchart-tutorial/IC791186.png "Configure Single Sign-On")
2. Wählen Sie auf der Seite **Wie sollen sich Benutzer bei Lucidchart anmelden?** die Option **Microsoft Azure AD – einmaliges Anmelden** aus, und klicken Sie dann auf **Weiter**.
   
   ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-lucidchart-tutorial/IC791187.png "Configure Single Sign-On")
3. Geben Sie auf der Seite **App-URL konfigurieren** im Textfeld für die **Lucidchart-Anmelde-URL** die von Ihren Benutzern für die Anmeldung bei Ihrer Lucidchart-Anwendung verwendete URL ein (z.B. *https://chart2.office.lucidchart.com/saml/sso/azure*), und klicken Sie dann auf **Weiter**.
   
   ![App-URL konfigurieren](./media/active-directory-saas-lucidchart-tutorial/IC791188.png "Configure App URL")
4. Klicken Sie auf der Seite **Einmaliges Anmelden konfigurieren für Lucidchart** auf **Metadaten herunterladen**, und speichern Sie die Metadatendatei lokal auf Ihrem Computer.
   
   ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-lucidchart-tutorial/IC791189.png "Configure Single Sign-On")
5. Melden Sie sich in einem anderen Webbrowserfenster bei der Lucidchart-Unternehmenswebsite als Administrator an.
6. Klicken Sie im oberen Menü auf **Team**.
   
   ![Team](./media/active-directory-saas-lucidchart-tutorial/IC791190.png "Team")
7. Klicken Sie auf **Anwendung \> SAML verwalten**.
   
   ![SAML verwalten](./media/active-directory-saas-lucidchart-tutorial/IC791191.png "Manage SAML")
8. Führen Sie auf der Dialogseite **SAML-Authentifizierungseinstellungen** die folgenden Schritte aus:
   
   1. Wählen Sie **SAML-Authentifizierung aktivieren** aus, und klicken Sie dann auf **Optional**.
      ![SAML-Authentifizierungseinstellungen](./media/active-directory-saas-lucidchart-tutorial/IC791192.png "SAML Authentication Settings")
   2. Geben Sie im Textfeld **Domäne** Ihre Domäne ein, und klicken Sie auf **Zertifikat ändern**.
      ![Zertifikat ändern](./media/active-directory-saas-lucidchart-tutorial/IC791193.png "Change Certificate")
   3. Öffnen Sie die heruntergeladene Metadatendatei, kopieren Sie den Inhalt, und fügen Sie ihn in das Textfeld **Metadaten hochladen** ein.
      ![Metadaten hochladen](./media/active-directory-saas-lucidchart-tutorial/IC791194.png "Upload Metadata")
   4. Wählen Sie **Automatisch neue Benutzer zum Team hinzufügen** aus, und klicken Sie auf **Änderungen speichern**.
      ![Save Changes](./media/active-directory-saas-lucidchart-tutorial/IC791195.png "Save Changes")
9. Bestätigen Sie die Konfiguration des einmaligen Anmeldens, und klicken Sie dann auf **Abschließen**, um das Dialogfeld **Einmaliges Anmelden konfigurieren** zu schließen.
   
   ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-lucidchart-tutorial/IC791196.png "Configure Single Sign-On")
   
   ## <a name="configuring-user-provisioning"></a>Konfigurieren der Benutzerbereitstellung

Für das Konfigurieren der Benutzerbereitstellung in Lucidchart steht kein Aktionselement zur Verfügung.  
Wenn sich ein zugewiesener Benutzer über den Zugriffsbereich bei Lucidchart anmelden möchte, überprüft Lucidchart, ob der Benutzer vorhanden ist.  
Ist noch kein Benutzerkonto verfügbar, wird es von Lucidchart automatisch erstellt.

## <a name="assigning-users"></a>Zuweisen von Benutzern
Um Ihre Konfiguration zu testen, müssen Sie den Azure AD-Benutzern, denen Sie die Verwendung Ihrer Anwendung ermöglichen möchten, Zugriff auf die Anwendung gewähren. Weisen Sie dazu der Anwendung Benutzer zu.

### <a name="to-assign-users-to-lucidchart-perform-the-following-steps"></a>So weisen Sie Lucidchart Benutzer zu:
1. Erstellen Sie im klassischen Azure-Portal ein Testkonto.
2. Klicken Sie auf der Anwendungsintegrationsseite für **Lucidchart** auf **Benutzer zuweisen**.
   
   ![Benutzer zuweisen](./media/active-directory-saas-lucidchart-tutorial/IC791197.png "Assign Users")
3. Wählen Sie den Testbenutzer aus, klicken Sie auf **Zuweisen** und anschließend auf **Ja**, um die Zuweisung zu bestätigen.
   
   ![Ja](./media/active-directory-saas-lucidchart-tutorial/IC767830.png "Yes")

Wenn Sie die SSO-Einstellungen testen möchten, öffnen Sie den Zugriffsbereich. Weitere Informationen zum Zugriffsbereich finden Sie unter [Einführung in den Zugriffsbereich](active-directory-saas-access-panel-introduction.md).




<!--HONumber=Nov16_HO3-->


