---
title: Einmaliges Anmelden mit Anwendungsproxy | Microsoft Docs
description: "Erläutert das Bereitstellen von einmaligem Anmelden mit Azure AD-Anwendungsproxy."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: ded0d9c9-45f6-47d7-bd0f-3f7fd99ab621
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: kgremban
translationtype: Human Translation
ms.sourcegitcommit: c308524e41047220fbad026edb6a87f196d89580
ms.openlocfilehash: 3f293996d2565c495f707f99a0bb75bb7c24054e

---

# <a name="single-sign-on-with-application-proxy"></a>Einmaliges Anmelden mit Anwendungsproxy
Die einmalige Anmeldung ist ein wichtiges Element von Azure AD-Anwendungsproxy. Sie bietet optimale Benutzerfreundlichkeit mit den folgenden Schritten:

1. Ein Benutzer meldet sich bei der Cloud an.  
2. Alle Sicherheitsüberprüfungen erfolgen in der Cloud (Vorauthentifizierung).  
3. Wenn die Anforderung an die lokale Anwendung gesendet wird, nimmt der Anwendungsproxyconnector die Identität des Benutzers an. Die Back-End-Anwendung geht von einem regulären Benutzer eines in eine Domäne eingebundenen Geräts aus.

![Diagramm zum Zugriffsverlauf vom Endbenutzer über den Anwendungsproxy zum Unternehmensnetzwerk](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_diagram.png)

Der Azure AD-Anwendungsproxy unterstützt Sie beim Bereitstellen des einmaligen Anmeldens (Single Sign-On, SSO) für Benutzer. Gehen Sie folgendermaßen vor, um Ihre Apps mit SSO zu veröffentlichen:

## <a name="sso-for-on-prem-iwa-apps-using-kcd-with-application-proxy"></a>Einmaliges Anmelden für lokale IWA-Apps unter Verwendung von KCD mit Anwendungsproxy
Sie können für Anwendungen, die die integrierte Windows-Authentifizierung (IWA) verwenden, einmaliges Anmelden wie folgt aktivieren: Erteilen Sie einem Anwendungsproxy-Connector in Active Directory die Berechtigung, die Identität von Benutzern anzunehmen und Token in deren Namen zu senden und zu empfangen.

### <a name="network-diagram"></a>Netzwerkdiagramm
Dieses Diagramm erläutert die Vorgänge, die bei einem Zugriff eines Benutzers auf eine lokale Anwendung, die IWA verwendet, ablaufen.

![Flussdiagramm für Microsoft AAD-Authentifizierung](./media/active-directory-application-proxy-sso-using-kcd/AuthDiagram.png)

1. Der Benutzer gibt die URL ein, um über den Anwendungsproxy auf die lokale Anwendung zuzugreifen.
2. Der Anwendungsproxy leitet die Anforderung zur Vorauthentifizierung an Azure AD-Authentifizierungsdienste weiter. Zu diesem Zeitpunkt wendet Azure AD alle gültigen Authentifizierungs- und Autorisierungsrichtlinien an, wie z. B. mehrstufige Authentifizierung. Nachdem der Benutzer überprüft wurde, erstellt Azure AD ein Token und sendet es an den Benutzer.
3. Der Benutzer übergibt das Token an den Anwendungsproxy.
4. Der Anwendungsproxy überprüft das Token und ruft den Benutzerprinzipalnamen (UPN) daraus ab. Dann sendet er die Anforderung, den UPN und den Dienstprinzipalnamen (SPN) über einen zweifach authentifizierten, sicheren Kanal an den Connector.
5. Der Connector führt eine KCD-Aushandlung mit dem lokalen AD aus und nimmt dabei die Identität des Benutzers an, um ein Kerberos-Token für die Anwendung zu erhalten.
6. Active Directory sendet das Kerberos-Token für die Anwendung an den Connector.
7. Der Connector sendet die ursprüngliche Anforderung an den Anwendungsserver und verwendet dabei das von AD empfangene Kerberos-Token.
8. Die Anwendung sendet die Antwort an den Connector, die dann an den Anwendungsproxydienst und schließlich an den Benutzer zurückgegeben wird.

### <a name="prerequisites"></a>Voraussetzungen
Vergewissern Sie sich vor Ihren ersten Schritten mit SSO für den Anwendungsproxy, dass Ihre Umgebung über folgende Einstellungen und Konfigurationen verfügt:

* Ihre Apps (beispielsweise SharePoint-Web-Apps) sind für die Verwendung der integrierten Windows-Authentifizierung konfiguriert. Weitere Informationen finden Sie unter [Aktivieren der Unterstützung für die Kerberos-Authentifizierung](https://technet.microsoft.com/library/dd759186.aspx). Weitere Informationen zu SharePoint finden Sie unter [Planen der Kerberos-Authentifizierung in SharePoint 2013](https://technet.microsoft.com/library/ee806870.aspx).
* Alle Ihre Apps verfügen über Dienstprinzipalnamen.
* Der Server, auf dem der Connector ausgeführt wird, und der Server, auf dem die App ausgeführt wird, gehören einer Domäne an und sind Teil der gleichen Domäne bzw. der vertrauenswürdigen Domänen. Weitere Informationen zum Domänenbeitritt finden Sie unter [Hinzufügen eines Computers zu einer Domäne](https://technet.microsoft.com/library/dd807102.aspx).
* Der Server, auf dem der Connector ausgeführt wird, verfügt über Lesezugriff auf „TokenGroupsGlobalAndUniversal“ für Benutzer. Hierbei handelt es sich um eine Standardeinstellung, die unter Umständen im Rahmen einer Sicherheitshärtung für die Umgebung geändert wurde. Weitere hilfreiche Informationen zu dieser Einstellung finden Sie unter [KB2009157](https://support.microsoft.com/en-us/kb/2009157).

### <a name="active-directory-configuration"></a>Active Directory-Konfiguration
Die Active Directory-Konfiguration variiert in Abhängigkeit davon, ob Ihr Anwendungsproxy-Connector und der veröffentlichte Server sich in derselben Domäne befinden oder nicht.

#### <a name="connector-and-published-server-in-the-same-domain"></a>Connector und veröffentlichter Server in der gleichen Domäne
1. Wechseln Sie in Active Directory zu **Extras** > **Benutzer und Computer**.
2. Wählen Sie den Server aus, der den Connector ausführt.
.3. Klicken Sie mit der rechten Maustaste, und wählen Sie **Eigenschaften** > **Delegierung** aus.
4. Wählen Sie **Computer nur bei Delegierungen angegebener Dienste vertrauen**. Fügen Sie unter **Dienste, für die dieses Konto delegierte Anmeldeinformationen verwenden kann** den Wert für die Dienstprinzipalnamen-Identität (SPN) des Anwendungsservers hinzu.
5. Auf diese Weise kann der Anwendungsproxy-Connector die Identität von Benutzern in AD für die Anwendungen annehmen, die in der Liste definiert sind.

![Screenshot des Connector-SVR-Eigenschaftenfensters](./media/active-directory-application-proxy-sso-using-kcd/Properties.jpg)

#### <a name="connector-and-published-server-in-different-domains"></a>Connector und veröffentlichter Server in unterschiedlichen Domänen
1. Eine Liste der Voraussetzungen für das domänenübergreifende Arbeiten mit KCD finden Sie unter [Eingeschränkte Kerberos-Delegierung über Domänengrenzen hinweg](https://technet.microsoft.com/library/hh831477.aspx).
2. Verwenden Sie unter Windows 2012 R2 die Eigenschaft `principalsallowedtodelegateto` auf dem Connector-Server, um für den Anwendungsproxy das Delegieren für den Connector-Server zu aktivieren, wobei `sharepointserviceaccount` der veröffentlichte Server und `connectormachineaccount` der delegierende Server ist.

        $connector= Get-ADComputer -Identity connectormachineaccount -server dc.connectordomain.com

        Set-ADComputer -Identity sharepointserviceaccount -PrincipalsAllowedToDelegateToAccount $connector

        Get-ADComputer sharepointserviceaccount -Properties PrincipalsAllowedToDelegateToAccount

> [!NOTE]
> `sharepointserviceaccount` kann das SPS-Computerkonto oder ein Dienstkonto sein, unter dem der SPS-App-Pool ausgeführt wird.
>
>

### <a name="azure-classic-portal-configuration"></a>Konfiguration im klassischen Azure-Portal
1. Veröffentlichen Sie Ihre Anwendung entsprechend den Anweisungen unter [Veröffentlichen von Anwendungen mit einem Anwendungsproxy](active-directory-application-proxy-publish.md). Stellen Sie sicher, dass **Azure Active Directory** als **Präauthentifizierungsmethode** ausgewählt ist.
2. Wenn Ihre Anwendung in der Liste der Anwendungen angezeigt wird, wählen Sie sie aus und klicken auf **Konfigurieren**.
3. Legen Sie unter **Eigenschaften** die Option **Interne Authentifizierungsmethode** auf **Integrierte Windows-Authentifizierung** fest.  
   ![Erweiterte Anwendungskonfiguration](./media/active-directory-application-proxy-sso-using-kcd/cwap_auth2.png)  
4. Geben Sie den Wert für **Interner Anwendungs-SPN** des Anwendungsservers ein. In diesem Beispiel ist der SPN für die veröffentlichte Anwendung http/lob.contoso.com.  

> [!IMPORTANT]
> Stimmen Ihre lokale UPN und die UPN in Azure Active Directory nicht überein, müssen Sie die [delegierte Identität für die Anmeldung](#delegated-login-identity) konfigurieren, damit die Präauthentifizierung funktioniert.
>
>

|  |  |
| --- | --- |
| Interne Authentifizierungsmethode |Bei Verwendung von Azure AD für die Vorauthentifizierung können Sie eine interne Authentifizierungsmethode festlegen, um Ihren Benutzern das einmalige Anmelden (SSO) für diese Anwendung zu ermöglichen. <br><br> Wählen Sie **Integrierte Windows-Authentifizierung** (IWA) aus, wenn Ihre Anwendung IWA verwendet. Außerdem können Sie die eingeschränkte Kerberos-Delegierung (KCD) zum Aktivieren von SSO für diese Anwendung konfigurieren. Anwendungen, die IWA verwenden, müssen mithilfe von KCD konfiguriert werden. Ansonsten kann der Anwendungsproxy diese Anwendungen nicht veröffentlichen. <br><br> Wählen Sie **Keine** aus, wenn Ihre Anwendung IWA nicht verwendet. |
| Interner Anwendungs-SPN |Dies ist der Dienstprinzipalname (SPN) der internen Anwendung wie im lokalen Azure AD konfiguriert. Der SPN wird vom Anwendungsproxy-Connector verwendet, um Kerberos-Token für die Anwendung mithilfe der eingeschränkten Kerberos-Delegierung (KCD) abzurufen. |

## <a name="sso-for-non-windows-apps"></a>SSO für Nicht-Windows-Apps
Der Ablauf der Kerberos-Delegierung im Azure AD-Anwendungsproxy wird gestartet, wenn Azure AD den Benutzer in der Cloud authentifiziert. Sobald die Anforderung lokal ankommt, gibt der Azure AD-Anwendungsproxy-Connector durch Interaktion mit dem lokalen Active Directory ein Kerberos-Ticket für den Benutzer aus. Dieser Prozess wird als Kerberos Constrained Delegation (KCD) bezeichnet. In der nächsten Phase wird mit diesem Kerberos-Ticket eine Anforderung an die Back-End-Anwendung gesendet. Es gibt mehrere Protokolle, die definieren, wie solche Anforderungen gesendet werden. Die meisten Nicht-Windows-Server erwarten Negotiate/SPNego, das jetzt im Azure AD-Anwendungsproxy unterstützt wird.

![Nicht-Windows-SSO-Diagramm](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_nonwindows_diagram.png)

Weitere Informationen zu Kerberos finden Sie unter [All you want to know about Kerberos Constrained Delegation (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd) (Alles über die eingeschränkte Kerberos-Delegierung, KCD).

### <a name="delegated-login-identity"></a>delegierte Identität für die Anmeldung
Die Delegierte Identität für Anmeldung unterstützt zwei verschiedene Anmeldeszenarien:

* Nicht-Windows-Anwendungen erhalten in der Regel die Benutzeridentität in Form eines Benutzernamens oder SAM-Kontonamens anstelle einer E-Mail-Adresse ((username@domain)).
* Alternative Anmeldungskonfigurationen, bei denen sich die UPN in Azure AD und die UPN in Ihrem lokalen Active Directory unterscheiden.

Mit dem Anwendungsproxy können Sie wählen, welche Identität verwendet werden soll, um das Kerberos-Ticket erhalten. Diese Einstellung erfolgt pro Anwendung. Einige dieser Optionen eignen sich für Systeme, die kein E-Mail-Adressformat akzeptieren, andere sind auf eine alternative Anmeldung ausgelegt.

![Screenshot: Parameter „Delegierte Identität für Anmeldung“](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_upn.png)

Bei Verwendung der Delegierten Identität für Anmeldung ist der Wert unter Umständen nicht für alle Domänen oder Gesamtstrukturen in Ihrer Organisation eindeutig. Sie können dieses Problem umgehen, indem Sie die Anwendung zweimal mit zwei unterschiedlichen Connectorgruppen veröffentlichen. Da jede Anwendung einen anderen Benutzerkreis aufweist, lassen sich die Connectors mit einer unterschiedlichen Domäne verknüpfen.

## <a name="working-with-sso-when-on-premises-and-cloud-identities-are-not-identical"></a>Der Umgang mit SSO im lokalen Umfeld unterscheidet sich von dem mit Cloud-Identitäten.
Sofern nicht anderweitig konfiguriert, geht der Anwendungsproxy davon aus, dass Benutzer in der Cloud genau dieselbe Identität wie lokal besitzen. Für jede Anwendung lässt sich festlegen, welche Identität beim Ausführen der einmaligen Anmeldung verwendet wird.  

Diese Funktion ermöglicht vielen Organisationen mit unterschiedlichen lokalen Identitäten und Cloudidentitäten SSO aus der Cloud auf lokale Apps, ohne dass der Benutzer unterschiedliche Benutzernamen und Kennwörter eingeben muss. Hierzu gehören Organisationen mit folgenden Merkmalen:

* Sie besitzen intern mehrere Domänen ((joe@us.contoso.com,, joe@eu.contoso.com)) und eine einzelne Domäne in der Cloud ((joe@contoso.com)).
* Sie besitzen intern einen nicht routingfähigen Domänennamen ((joe@contoso.usa)) und einen zulässigen Namen in der Cloud.
* Sie verwenden intern keine Domänennamen (Joe).
* Sie verwenden lokal und in der Cloud unterschiedliche Aliase. Beispiel: joe-johns@contoso.com und joej@contoso.com  

Dies hilft auch bei Anwendungen, die keine Adressen in Form von E-Mail-Adressen akzeptieren – einem häufigen Szenario bei nicht auf Windows basierenden Back-End-Servern.

### <a name="setting-sso-for-different-cloud-and-on-prem-identities"></a>Festlegen von SSO für unterschiedliche lokale und cloudbasierte Identitäten
1. Konfigurieren Sie die Azure AD Connect-Einstellungen so, dass die E-Mail-Adresse die Hauptidentität ist. Dies erfolgt als Teil des Anpassungsvorgangs durch Änderung des **Benutzerprinzipalnamens** in den Synchronisierungseinstellungen. Diese Einstellungen bestimmen auch, wie sich Benutzer bei Office&365;, Windows&10;-Geräten und anderen Anwendungen anmelden, die Azure AD als Identitätsspeicher verwenden.  
   ![Screenshot: Benutzer identifizieren – Dropdownliste für Benutzerprinzipalname](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_connect_settings.png)  
2. Wählen Sie in den Anwendungskonfigurationseinstellungen für die zu modifizierende Anwendung die **Delegierte Identität für Anmeldung** aus:

   * Benutzerprinzipalname: joe@contoso.com  
   * Alternativer Benutzerprinzipalname: joed@contoso.local  
   * Benutzernamensteil des Benutzerprinzipalnamens: joe  
   * Benutzernamensteil des alternativen Benutzerprinzipalnamens: joed  
   * Lokaler SAM-Kontoname: je nach Konfiguration des lokalen Domänencontrollers

   ![Screenshot: Dropdownmenü „Delegierte Identität für Anmeldung“](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_upn.png)  

### <a name="troubleshooting-sso-for-different-identities"></a>Problembehandlung bei SSO für verschiedene Identitäten
Wenn im SSO-Prozess ein Fehler auftritt, wird dieser im Ereignisprotokoll des Connectorcomputers aufgeführt, wie unter [Problembehandlung](active-directory-application-proxy-troubleshoot.md)beschrieben.
In einigen Fällen wird die Anforderung jedoch erfolgreich an die Back-End-Anwendung gesendet, während die Anwendung mit verschiedenen anderen HTTP-Antworten reagiert. Die Problembehandlung beginnt in diesen Fällen zweckmäßigerweise mit der Untersuchung der Ereignisnummer 24029 auf dem Connectorcomputer im Sitzungsereignisprotokoll des Anwendungsproxys. Die Benutzeridentität, die für die Delegierung verwendet wurde, wird im Feld „Benutzer“ in den Ereignisdetails angezeigt. Wählen Sie zum Aktivieren des Sitzungsprotokolls im Menü „Ansicht“ der Ereignisanzeige die Option **Analytische und Debugprotokolle einblenden** aus.

## <a name="see-also"></a>Siehe auch
* [Veröffentlichen von Anwendungen mit dem Anwendungsproxy](active-directory-application-proxy-publish.md)
* [Problembehandlung von Anwendungsproxys](active-directory-application-proxy-troubleshoot.md)
* [Arbeiten mit Anwendungen, die Ansprüche unterstützen](active-directory-application-proxy-claims-aware-apps.md)
* [Aktivieren des bedingten Zugriffs](active-directory-application-proxy-conditional-access.md)

Aktuelle Neuigkeiten und Updates finden Sie im [Blog zum Anwendungsproxy](http://blogs.technet.com/b/applicationproxyblog/)

<!--Image references-->
[1]: ./media/active-directory-application-proxy-sso-using-kcd/AuthDiagram.png
[2]: ./media/active-directory-application-proxy-sso-using-kcd/Properties.jpg



<!--HONumber=Feb17_HO2-->


