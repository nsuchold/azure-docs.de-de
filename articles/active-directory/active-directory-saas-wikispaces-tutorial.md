---
title: 'Tutorial: Azure Active Directory-Integration mit Wikispaces | Microsoft Docs'
description: "Hier erfahren Sie, wie Sie Wikispaces mit Azure Active Directory verwenden können, um einmalige Anmeldung, automatisierte Bereitstellung und vieles mehr zu ermöglichen."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 665b95aa-f7f5-4406-9e2a-6fc299a1599c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/05/2016
ms.author: jeedes
translationtype: Human Translation
ms.sourcegitcommit: 1cef7ff21a8d076c89688f1fe75cebdb7c468199
ms.openlocfilehash: c7569177db0821b36e49439ec54224e1aeb9ad9d


---
# <a name="tutorial-azure-active-directory-integration-with-wikispaces"></a>Tutorial: Azure Active Directory-Integration mit Wikispaces
In diesem Tutorial wird die Integration von Azure und Wikispaces erläutert.  
Das in diesem Tutorial verwendete Szenario setzt voraus, dass Sie bereits über die folgenden Elemente verfügen:

* Ein gültiges Azure-Abonnement
* Ein Wikispaces-Abonnement, für das einmaliges Anmelden aktiviert ist

Nach Abschluss dieses Tutorials können sich die Wikispaces zugewiesenen Azure AD-Benutzer mittels einmaliger Anmeldung auf Ihrer Wikispaces-Unternehmenswebsite bei der Anwendung anmelden (durch den Dienstanbieter initiierte Anmeldung). Alternativ können sie den Zugriffsbereich nutzen (siehe [Einführung in den Zugriffsbereich](active-directory-saas-access-panel-introduction.md)).

Das in diesem Tutorial beschriebene Szenario besteht aus den folgenden Bausteinen:

1. Aktivieren der Anwendungsintegration für Wikispaces
2. Konfigurieren der einmaligen Anmeldung
3. Konfigurieren der Benutzerbereitstellung
4. Zuweisen von Benutzern

![Szenario](./media/active-directory-saas-wikispaces-tutorial/IC787182.png "Sceanrio")

## <a name="enabling-the-application-integration-for-wikispaces"></a>Aktivieren der Anwendungsintegration für Wikispaces
In diesem Abschnitt wird beschrieben, wie Sie die Anwendungsintegration für Wikispaces aktivieren.

### <a name="to-enable-the-application-integration-for-wikispaces-perform-the-following-steps"></a>So aktivieren Sie die Anwendungsintegration für Wikispaces:
1. Klicken Sie im klassischen Azure-Portal im linken Navigationsbereich auf **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-wikispaces-tutorial/IC700993.png "Active Directory")

2. Wählen Sie in der Liste **Verzeichnis** das Verzeichnis aus, für das Sie die Verzeichnisintegration aktivieren möchten.

3. Klicken Sie zum Öffnen der Anwendungsansicht in der oberen Menüleiste der Verzeichnisansicht auf **Anwendungen** .
   
    ![Anwendungen](./media/active-directory-saas-wikispaces-tutorial/IC700994.png "Applications")

4. Klicken Sie unten auf der Seite auf **Hinzufügen** .
   
    ![Anwendung hinzufügen](./media/active-directory-saas-wikispaces-tutorial/IC749321.png "Add application")

5. Klicken Sie im Dialogfeld **Was möchten Sie tun?** auf **Anwendung aus dem Katalog hinzufügen**.
   
    ![Anwendung aus dem Katalog hinzufügen](./media/active-directory-saas-wikispaces-tutorial/IC749322.png "Add an application from gallerry")

6. Geben Sie in das **Suchfeld** **Wikispaces** ein.
   
    ![Anwendungskatalog](./media/active-directory-saas-wikispaces-tutorial/IC787186.png "Application Gallery")

7. Wählen Sie im Ergebnisbereich **Wikispaces** aus, und klicken Sie dann auf **Abschließen**, um die Anwendung hinzuzufügen.
   
    ![Wikispaces](./media/active-directory-saas-wikispaces-tutorial/IC787187.png "Wikispaces")

## <a name="configuring-single-sign-on"></a>Konfigurieren der einmaligen Anmeldung
In diesem Abschnitt wird erläutert, wie Sie es Benutzern mithilfe einer Verbundanmeldung auf Basis des SAML-Protokolls ermöglichen, sich mit ihrem Azure AD-Konto bei Wikispaces zu authentifizieren.

### <a name="to-configure-single-sign-on-perform-the-following-steps"></a>So konfigurieren Sie einmaliges Anmelden
1. Klicken Sie im klassischen Azure-Portal auf der Anwendungsintegrationsseite für **Wikispaces** auf **Einmaliges Anmelden konfigurieren**, um das Dialogfeld **Einmaliges Anmelden konfigurieren** zu öffnen.
   
    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-wikispaces-tutorial/IC787188.png "Configure Single Sign-On")

2. Wählen Sie auf der Seite **Wie sollen sich Benutzer bei Wikispaces anmelden?** die Option **Microsoft Azure AD – einmaliges Anmelden** aus, und klicken Sie dann auf **Weiter**.
   
    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-wikispaces-tutorial/IC787189.png "Configure Single Sign-On")

3. Geben Sie auf der Seite **App-URL konfigurieren** im Textfeld **Wikispaces-Anmelde-URL** die URL im Format „*http://company.wikispaces.net*“ ein, und klicken Sie dann auf **Weiter**.
   
    ![App-URL konfigurieren](./media/active-directory-saas-wikispaces-tutorial/IC787190.png "Configure App URL")

4. Klicken Sie auf der Seite **Einmaliges Anmelden konfigurieren für Wikispaces** auf **Metadaten herunterladen**, und speichern Sie die Metadatendatei auf Ihrem Computer.
   
   ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-wikispaces-tutorial/IC787191.png "Configure Single Sign-On")

5. Senden Sie die Metadatendatei an das Supportteam von  Wikispaces.
   
    > [!NOTE]
    > Das einmalige Anmelden muss vom Supportteam von Wikispaces konfiguriert werden. Sie erhalten eine Benachrichtigung, sobald die Konfiguration abgeschlossen ist.
    > 
    > 

6. Bestätigen Sie im klassischen Azure-Portal die Konfiguration der einmaligen Anmeldung, und klicken Sie dann auf **Abschließen**, um das Dialogfeld **Einmaliges Anmelden konfigurieren** zu schließen.
   
    ![Einmaliges Anmelden konfigurieren](./media/active-directory-saas-wikispaces-tutorial/IC787192.png "Configure Single Sign-On")

## <a name="configuring-user-provisioning"></a>Konfigurieren der Benutzerbereitstellung
Damit sich Azure AD-Benutzer bei Wikispaces anmelden können, müssen sie in Wikispaces bereitgestellt werden.  
Im Fall von Wikispaces ist die Bereitstellung eine manuelle Aufgabe.

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a>So stellen Sie Benutzerkonten bereit:
1. Melden Sie sich bei Ihrer **Wikispaces** -Unternehmenswebsite als Administrator an.

2. Wechseln Sie zu **Mitglieder**.
   
    ![Mitglieder](./media/active-directory-saas-wikispaces-tutorial/IC787193.png "Members")

3. Klicken Sie auf **Personen einladen**.
   
    ![Personen einladen](./media/active-directory-saas-wikispaces-tutorial/IC787194.png "Invite People")

4. Führen Sie im Abschnitt **Personen einladen** die folgenden Schritte aus:
   
    ![Invite People](./media/active-directory-saas-wikispaces-tutorial/IC787208.png "Invite People")
   
    a. Geben Sie **Benutzernamen oder E-Mail-Adresse** eines gültigen AAD-Benutzerkontos, das Sie bereitstellen möchten, in die entsprechenden Textfelder ein.
   
    b. Klicken Sie auf **Send**.  
      
    > [!NOTE]
    > Der Besitzer des Azure Active Directory-Kontos erhält eine E-Mail mit einem Link zur Bestätigung des Kontos, bevor es aktiv wird.
    > 
    > 

> [!NOTE]
> Sie können AAD-Benutzerkonten auch mithilfe anderer Tools zum Erstellen von Wikispaces-Benutzerkonten oder mithilfe der von Wikispaces bereitgestellten APIs erstellen.
> 
> 

## <a name="assigning-users"></a>Zuweisen von Benutzern
Um Ihre Konfiguration zu testen, müssen Sie den Azure AD-Benutzern, denen Sie die Verwendung Ihrer Anwendung ermöglichen möchten, Zugriff auf die Anwendung gewähren. Weisen Sie dazu der Anwendung Benutzer zu.

### <a name="to-assign-users-to-wikispaces-perform-the-following-steps"></a>So weisen Sie Wikispaces Benutzer zu:
1. Erstellen Sie im klassischen Azure-Portal ein Testkonto.

2. Klicken Sie auf der Anwendungsintegrationsseite für **Wikispaces** auf **Benutzer zuweisen**.
   
    ![Benutzer zuweisen](./media/active-directory-saas-wikispaces-tutorial/IC787195.png "Assign Users")

3. Wählen Sie den Testbenutzer aus, klicken Sie auf **Zuweisen** und anschließend auf **Ja**, um die Zuweisung zu bestätigen.
   
    ![Ja](./media/active-directory-saas-wikispaces-tutorial/IC767830.png "Yes")

Wenn Sie die SSO-Einstellungen testen möchten, öffnen Sie den Zugriffsbereich. Weitere Informationen zum Zugriffsbereich finden Sie unter [Einführung in den Zugriffsbereich](active-directory-saas-access-panel-introduction.md).




<!--HONumber=Dec16_HO1-->


