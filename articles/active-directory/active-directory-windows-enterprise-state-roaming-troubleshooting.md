---
title: Problembehandlung bei Enterprise State Roaming-Einstellungen in Azure Active Directory | Microsoft-Dokumentation
description: "Enthält Antworten auf einige Fragen, die für IT-Administratoren in Bezug auf die Synchronisierung von Einstellungen und App-Daten ggf. interessant sind."
services: active-directory
keywords: "Enterprise State Roaming-Einstellungen, Windows-Cloud, Häufig gestellte Fragen zu Enterprise State Roaming"
documentationcenter: 
author: femila
manager: swadhwa
editor: 
ms.assetid: f45d0515-99f7-42ad-94d8-307bc0d07be5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: femila
translationtype: Human Translation
ms.sourcegitcommit: 58a583a761a400d8fa0488fbc4fbfec35ec62c41
ms.openlocfilehash: ebdf73ad8a7a2f2690a404676e0c81ee01e77357


---
#<a name="troubleshooting-enterprise-state-roaming-settings-in-azure-active-directory"></a>Problembehandlung bei Enterprise State Roaming-Einstellungen in Azure Active Directory

Dieses Thema enthält Informationen zur Behandlung und Diagnose von Problemen mit Enterprise State Roaming sowie eine Liste der bekannten Probleme.

## <a name="preliminary-steps-for-troubleshooting"></a>Vorbereitende Schritte zur Problembehandlung 
Bevor Sie mit der Problembehandlung beginnen, stellen Sie sicher, dass der Benutzer und das Gerät ordnungsgemäß konfiguriert wurden und dass alle Anforderungen von Enterprise State Roaming vom Gerät und dem Benutzer erfüllt werden. 

1. Windows 10 ist mit den neuesten Updates und mindestens Version 1511 (Betriebssystembuild 10586 oder höher) auf dem Gerät installiert. 
2. Das Gerät gehört Azure AD oder einer Domäne an und ist bei Azure AD registriert.
3. Im Azure Active Directory-Portal ist **Enterprise State Roaming** für das Verzeichnis unter **Konfigurieren** > **Geräte** > **Benutzer können Einstellungen und App-Daten des Unternehmens synchronisieren** aktiviert. Entweder werden alle Benutzer ausgewählt, oder der Benutzer wird für die Synchronisierung über die ausgewählte Option aktiviert und in die Sicherheitsgruppe aufgenommen.
4. Dem Benutzer ist ein Azure Active Directory Premium-Abonnement zugewiesen.  
5. Das Gerät wurde neu gestartet, und der Benutzer hat sich angemeldet, nachdem Enterprise State Roaming aktiviert wurde.

## <a name="information-to-include-when-you-need-help"></a>Erforderliche Informationen beim Anfordern von Hilfe
Wenn Ihr Problem mithilfe der folgenden Anleitungen nicht gelöst wird, können Sie sich an einen unserer Supportmitarbeiter wenden. Hierbei sollten Sie die folgenden Informationen bereithalten:

- **Allgemeine Beschreibung des Fehlers**: Werden dem Benutzer Fehlermeldungen angezeigt? Wenn keine Fehlermeldung angezeigt wird, beschreiben Sie das beobachtete unerwartete Verhalten so genau wie möglich. Welche Funktionen sind für die Synchronisierung aktiviert, und was möchte der Benutzer synchronisieren? Werden mehrere Funktionen nicht synchronisiert, oder nur eine?
- **Betroffene Benutzer:** Funktioniert die Synchronisierung für einen oder mehrere Benutzer bzw. funktioniert sie nicht? Wie viele Geräte sind pro Benutzer betroffen? Werden alle nicht synchronisiert, oder werden einige synchronisiert und einige nicht?
- **Informationen zum Benutzer**: Welche Identität verwendet der Benutzer, um sich beim Gerät anzumelden? Wie meldet sich der Benutzer beim Gerät an? Ist er Mitglied einer ausgewählten Sicherheitsgruppe, die synchronisieren darf? 
- **Informationen zum Gerät**: Gehört dieses Gerät Azure AD oder einer Domäne an? Welche Builds sind auf dem Gerät installiert? Welches sind die neuesten Updates?
- **Datum/Uhrzeit/Zeitzone**: Wann genau (Tag und Uhrzeit) haben Sie den Fehler beobachtet (geben Sie auch die Zeitzone an)?
- Diese Informationen helfen uns dabei, Ihr Problem so schnell wie möglich zu beheben.

## <a name="troubleshooting-and-diagnosing-issues"></a>Problembehandlung und Diagnose von Problemen
Dieser Abschnitt enthält Vorschläge zum Beheben und Diagnostizieren von Problemen im Zusammenhang mit Enterprise State Roaming.

## <a name="verify-sync-and-the-sync-your-settings-settings-page"></a>Überprüfen der Synchronisierung und die Seite „Einstellungen synchronisieren“ 

1. Melden Sie sich nach dem Einbinden Ihres Windows 10-PCs in eine Domäne, die Enterprise State Roaming zulässt, mit Ihrem Geschäftskonto an. Wechseln Sie zu **Einstellungen** > **Konten** > **Einstellungen synchronisieren**, und vergewissern Sie sich, dass die Synchronisierung und die einzelnen Einstellungen aktiviert sind und dass oben auf der Seite mit den Einstellungen angegeben ist, dass die Synchronisierung mit Ihrem Geschäftskonto durchgeführt wird. Überprüfen Sie unter **Einstellungen** > **Konten** > **Ihre Infos**, ob das gleiche Konto auch als Ihr Anmeldekonto verwendet wird. 
2. Stellen Sie sicher, dass die Synchronisierung über mehrere Computer hinweg funktioniert, indem Sie einige Änderungen auf dem ursprünglichen Computer vornehmen, z.B. die Taskleiste auf dem Bildschirm nach rechts oder oben verschieben. Beobachten Sie, wie die Änderung innerhalb von fünf Minuten an den zweiten Computer weitergegeben wird. 
 - Durch Sperren und Entsperren des Bildschirms (Windows-Taste+L) kann eine Synchronisierung ausgelöst werden.
 - Sie müssen auf beiden Computern dasselbe Anmeldekonto für die Synchronisierung verwenden, da das Enterprise State Roaming an das Benutzerkonto und nicht das Computerkonto gebunden ist.

**Mögliches Problem**: Auf der Seite mit den Einstellungen sind die Umschaltflächen ausgegraut, und anstelle eines Kontos wird der Text „Einige Windows-Funktionen sind nur verfügbar, wenn Sie ein Microsoft-Konto oder -Geschäftskonto verwenden“ wird angezeigt. Dieses Problem kann bei Geräten auftreten, die einer Domäne zugeordnet wurden und die in Azure AD registriert sind, aber die nicht erfolgreich bei Azure AD authentifiziert wurden. Eine mögliche Ursache ist, dass die Geräterichtlinie angewendet werden muss, aber diese Anwendung asynchron erfolgt und sich um einige Stunden verzögert. Um dieses Problem zu überprüfen, führen Sie die Schritte zum Überprüfen des Geräteregistrierungsstatus aus. So können Sie feststellen, ob dies der Fall ist.

### <a name="verify-the-device-registration-status"></a>Überprüfen des Geräteregistrierungsstatus
Für Enterprise State Roaming muss das Gerät bei Azure AD registriert sein. Zwar gelten diese Anweisungen nicht nur für Enterprise State Roaming, damit können Sie aber sicherstellen, dass der Windows 10-Client registriert ist, und den Fingerabdruck, die URL für Azure AD-Einstellungen, den NGC-Status und andere Informationen überprüfen.

1.  Öffnen Sie die Eingabeaufforderung ohne erhöhte Rechte. Öffnen Sie dazu das Dialogfeld „Ausführen“ (Windows-Taste+R), und geben Sie zum Öffnen der Eingabeaufforderung „cmd“ ein.
2.  Sobald die Eingabeaufforderung geöffnet ist, geben Sie *dsregcmd.exe /status* ein.
3.  Erwartete Ausgabe: Der Wert des Felds **AzureAdJoined**muss „YES“ sein, der Wert des Felds **WamDefaultSet** muss „YES“, und der Wert des Felds **WamDefaultGUID** muss eine GUID sein, die auf „(AzureAd)“ endet.

**Mögliches Problem**: **WamDefaultSet** und **AzureAdJoined** weisen „NO“ als Wert auf, das Gerät gehört der Domäne an und wurde bei Azure AD registriert, und das Gerät wird nicht synchronisiert. In diesem Fall muss das Gerät möglicherweise warten, bis die Richtlinie angewendet wird, oder die Authentifizierung für das Gerät schlägt beim Verbinden mit Azure AD fehl. Der Benutzer muss möglicherweise einige Stunden warten, bis die Richtlinie angewendet wird. Weitere mögliche Schritte zur Problembehandlung sind, erneut eine automatische Registrierung durch eine Abmeldung und erneute Anmeldung zu versuchen oder die Aufgabe in der Aufgabenplanung zu starten. In einigen Fällen kann das Problem behoben werden, indem *dsregcmd.exe /leave* in einem Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt wird, ein Neustart durchgeführt wird und die Registrierung erneut ausgeführt wird.


**Mögliches Problem**: Das Feld für **AzureAdSettingsUrl** leer ist, und das Gerät wird nicht synchronisiert. Möglicherweise hat sich der Benutzer zuletzt am Gerät angemeldet, bevor Enterprise State Roaming im Azure Active Directory-Portal aktiviert wurde. Bitten Sie den IT-Administrator, im Portal „Benutzer können Einstellungen und App-Daten des Unternehmens synchronisieren“ zu deaktivieren und erneut zu aktivieren. Starten Sie dann das Gerät neu, und fordern Sie den Benutzer auf, sich anzumelden. 

## <a name="enterprise-state-roaming-and-multi-factor-authentication"></a>Enterprise State Roaming und Multi-Factor Authentication 
In bestimmten Fällen werden Daten von Enterprise State Roaming nicht synchronisiert, wenn die Multi-Factor Authentication (MFA) konfiguriert ist. Weitere Informationen zu diesen Symptomen finden Sie im Supportdokument [KB3193683](https://support.microsoft.com/kb/3193683). 

**Mögliches Problem**: Wenn Ihr Windows 10-Gerät so konfiguriert ist, dass für die Anmeldung beim Azure Active Directory-Portal die Multi-Factor Authentication erforderlich ist, werden die Einstellungen möglicherweise nicht synchronisiert, wenn Sie sich mit einem Kennwort bei dem Gerät anmelden. Diese Art der MFA-Konfiguration dient dem Schutz eines Azure-Administratorkontos. Administratoren können die Synchronisierung möglicherweise trotzdem durchführen, indem sie sich mit ihrer Microsoft Passport for Work-PIN bei ihrem Windows 10-Gerät anmelden oder indem sie die Multi-Factor Authentication durchführen, während sie auf andere Azure-Dienste wie Office 365 zugreifen.

**Mögliches Problem**: Bei der Synchronisierung kann ein Fehler auftreten, wenn der Administrator die Richtlinie für bedingten Zugriff mit Multi-Factor Authentication über die Azure Active Directory-Verbunddienste konfiguriert hat und das Zugriffstoken auf dem Gerät abläuft. Stellen Sie sicher, dass Sie die Microsoft Passport for Work-PIN zum An- und Abmelden verwenden, oder führen Sie die Multi-Factor Authentication durch, während Sie auf andere Azure-Dienste wie Office 365 zugreifen.

###<a name="event-viewer"></a>Ereignisanzeige
Für eine erweiterte Problembehandlung kann die Ereignisanzeige verwendet werden, um nach bestimmten Fehlern suchen. Diese sind in der folgenden Tabelle dokumentiert. Die Ereignisse finden Sie unter Ereignisanzeige > Anwendungs- und Dienstprotokolle > **Microsoft** > **Windows** > **SettingSync** und bei identitätsbezogenen Problemen mit der Synchronisierung unter **Microsoft** > **Windows** > **Azure AD**.


## <a name="known-issues"></a>Bekannte Probleme

### <a name="sync-does-not-work-on-devices-that-have-apps-side-loaded-using-mdm-software"></a>Die Synchronisierung funktioniert nicht auf Geräten, auf denen Apps mit MDM-Software quergeladen wurden

Betrifft Geräte mit dem Windows 10 Anniversary Update (Version 1607). In der Ereignisanzeige unter den SettingSync-Azure-Protokollen wird häufig die Ereignis-ID 6013 mit Fehler 80070259 angezeigt.

**Empfohlene Maßnahme**  
Stellen Sie sicher, dass auf dem Windows 10-v1607-Client das kumulative Update vom 23. August 2016 installiert ist ([KB3176934](https://support.microsoft.com/kb/3176934), Betriebssystembuild 14393.82). 

---

### <a name="internet-explorer-favorites-do-not-sync"></a>Internet Explorer-Favoriten werden nicht synchronisiert

Betrifft Geräte unter Windows 10 mit dem November-Update (Version 1511).

**Empfohlene Maßnahme**  
Stellen Sie sicher, dass auf dem Windows 10-v1511-Client das kumulative Update vom Juli 2016 installiert ist ([KB3172985](https://support.microsoft.com/kb/3172985), Betriebssystembuild 10586.494).

---

### <a name="theme-is-not-syncing-as-well-as-data-protected-with-windows-information-protection"></a>Das Design sowie mit Windows Information Protection geschützten Daten werden nicht synchronisiert 

Um Datenlecks zu verhindern, werden mit [Windows Information Protection](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip) geschützte Daten auf Geräten mit Windows 10 Anniversary Update nicht über Enterprise State Roaming synchronisiert.



**Empfohlene Maßnahme**  
Keine Dieses Problem wird im Rahmen von zukünftigen Updates für Windows voraussichtlich behoben.

---

### <a name="date-time-and-region-settings-do-not-sync-on-domain-joined-device"></a>Einstellungen für Datum, Uhrzeit und Region werden auf einem Gerät, das einer Domäne angehört, nicht synchronisiert 
  
Bei Geräten, die einer Domäne angehören, werden die Einstellungen für Datum, Uhrzeit und Region nicht synchronisiert: automatische Zeit. Durch das Verwenden der automatischen Zeit können die anderen Einstellungen für Datum, Uhrzeit und Region außer Kraft gesetzt werden, und dies kann dazu führen, dass diese Einstellungen nicht synchronisiert werden. 

**Empfohlene Maßnahme**  
Keine 

---

### <a name="uac-prompts-when-syncing-passwords"></a>Aufforderungen der Benutzerkontensteuerung beim Synchronisieren von Kennwörtern

Betrifft Geräte unter Windows 10 mit dem November-Update (Version 1511) und einer drahtlosen Netzwerkkarte, die so konfiguriert ist, dass Kennwörter synchronisiert werden.

**Empfohlene Maßnahme**  
Stellen Sie sicher, dass auf dem Windows 10-v1511-Client das kumulative Update installiert ist ([KB3140743](https://support.microsoft.com/kb/3140743), Betriebssystembuild 10586.494).

---

### <a name="sync-does-not-work-on-devices-that-use-smart-card-for-login"></a>Die Synchronisierung funktioniert nicht auf Geräten, die eine Smartcard für die Anmeldung verwenden
Wenn Sie versuchen, sich mit einer Smartcard oder einer virtuellen Smartcard bei Ihrem Windows-Gerät anzumelden, funktioniert die Synchronisierung der Einstellungen nicht mehr.     

**Empfohlene Maßnahme**  
Keine Dieses Problem wird im Rahmen von zukünftigen Updates für Windows voraussichtlich behoben.

---

### <a name="domain-joined-device-is-not-syncing-after-leaving-corporate-network"></a>Ein zu einer Domäne gehörendes Gerät wird nach dem Verlassen des Unternehmensnetzwerks nicht synchronisiert     
Bei zu einer Domäne gehörenden Geräte, die in Azure AD registriert sind, können Synchronisierungsfehler auftreten, wenn sich das Gerät längere Zeit außerhalb Ihrer Geschäftsräume befindet, und die Domänenauthentifizierung kann nicht abgeschlossen werden.

**Empfohlene Maßnahme**  
Verbinden Sie das Gerät mit einem Unternehmensnetzwerk, sodass die Synchronisierung fortgesetzt werden kann.

---

### <a name="event-id-6065-80070533-this-user-cant-sign-in-because-this-account-is-currently-disabled"></a>Ereignis-ID 6065: 80070533: Der Benutzer kann sich nicht anmelden, da das Konto momentan deaktiviert ist  
In der Ereignisanzeige unter „SettingSync/Debugprotokolle“ kann dieser Fehler angezeigt werden, wenn dem Mandanten nicht automatisch Azure RMS bereitgestellt wurde. 

**Empfohlene Maßnahme**  
Führen Sie die Schritte unter [KB3193791](https://support.microsoft.com/kb/3193791) aus. 

---

### <a name="event-id-1098-error-0xcaa5001c-token-broker-operation-failed"></a>Ereignis-ID 1098: Fehler: 0xCAA5001C: Fehler beim Tokenmaklervorgang  
In der Ereignisanzeige unter „AAD/Betriebsprotokolle“ kann dieser Fehler angezeigt werden (Ereignis 1104: Aufruf des AAD-Cloud-AP-Plug-Ins – Fehler beim Abrufen des Tokens: 0xC000005F). Dieses Problem tritt auf, wenn Berechtigungen oder Besitzattribute fehlen.  

**Empfohlene Maßnahme**  
Führen Sie die Schritte unter [KB3196528](https://support.microsoft.com/kb/3196528) aus.  



## <a name="next-steps"></a>Nächste Schritte

- Verwenden Sie das Forum [User Voice](https://feedback.azure.com/forums/169401-azure-active-directory/category/158658-enterprise-state-roaming), um Feedback zu geben und Vorschläge zur Verbesserung von Enterprise State Roaming zu machen.

- Weitere Informationen finden Sie in der [Übersicht über Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md). 

## <a name="related-topics"></a>Verwandte Themen
* [Übersicht über Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [Aktivieren von Enterprise State Roaming in Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md)
* [Roaming von Einstellungen und Daten – Häufig gestellte Fragen](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Gruppenrichtlinien- und MDM-Einstellungen für Einstellungssynchronisierung](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Windows 10-Roamingeinstellungen – Referenz](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)



<!--HONumber=Jan17_HO2-->


