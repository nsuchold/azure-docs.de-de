---
title: 'Azure Active Directory B2C: Registrierung einer Anwendung | Microsoft Docs'
description: Registrieren Ihrer Anwendung bei Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/06/2016
ms.author: swkrish
translationtype: Human Translation
ms.sourcegitcommit: fd22e9596feecbc12e577a4abfb47552e1b6e520
ms.openlocfilehash: da8f083cb7bca59501df080036e789a0fb75731e


---
# <a name="azure-active-directory-b2c-register-your-application"></a>Azure Active Directory B2C: Registrieren der Anwendung
## <a name="prerequisite"></a>Voraussetzung
Zum Erstellen einer Anwendung, die Registrierungen und Anmeldungen von Kunden akzeptiert, müssen Sie die Anwendung zunächst bei einem Azure Active Directory B2C-Mandanten registrieren. Erstellen Sie einen eigenen Mandanten mithilfe der unter [Erstellen eines Azure AD B2C-Mandanten](active-directory-b2c-get-started.md)beschriebenen Schritte. Nachdem Sie alle Schritte in diesem Artikel ausgeführt haben, ist das Blatt „B2C-Funktionen“ an Ihr Startmenü angeheftet.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="navigate-to-the-b2c-features-blade"></a>Navigieren zum Blatt „B2C-Funktionen“
Wenn das Blatt „B2C-Funktionen“ an Ihr Startmenü angeheftet ist, sehen Sie das Blatt, sobald Sie sich als globaler Administrator des B2C-Mandanten beim [Azure-Portal](https://portal.azure.com/) anmelden.

Sie können auf das Blatt auch zugreifen, indem Sie im [Azure-Portal](https://portal.azure.com/) im linken Navigationsbereich auf **Weitere Dienste** klicken und dann nach **Azure AD B2C** suchen.

> [!IMPORTANT]
> Sie müssen als globaler Administrator des B2C-Mandanten festgelegt sein, um auf das Blade mit den B2C-Features zugreifen zu können. Globale Administratoren anderer Mandanten oder Benutzer von Mandanten haben keinen Zugriff.  Mit dem Mandantenumschalter in der oberen rechten Ecke des Azure-Portals können Sie zu Ihrem B2C-Mandanten wechseln.
> 
> 

## <a name="register-an-application"></a>Registrieren einer Anwendung
1. Klicken Sie auf dem Blatt „B2C-Funktionen“ im Azure-Portal auf **Anwendungen**.
2. Klicken Sie oben auf dem Blatt auf **+Hinzufügen** .
3. Geben Sie einen **Namen** für die Anwendung ein, der die Funktion der Anwendung für Kunden beschreibt. Sie könnten z. B. „Contoso B2C-App“ eingeben.
4. Wenn Sie eine webbasierte Anwendung entwickeln, stellen Sie den Schalter **Web-App/Web-API** einschließen auf **Ja**. Die **Antwort-URLs** sind Endpunkte, an denen Azure AD B2C von Ihrer Anwendung angeforderte Token zurückgibt. Geben Sie z. B. Folgendes ein: `https://localhost:44316/`. Falls Ihre Webanwendung auch eine durch Azure AD B2C geschützte Web-API aufruft, wird darüber hinaus die Erstellung eines geheimen **Anwendungsschlüssels** empfohlen. Klicken Sie dazu auf die Schaltfläche **Schlüssel generieren**.
   
   > [!NOTE]
   > **Geheime Anwendungsschlüssel** sind wichtige Sicherheitsanmeldeinformationen, die entsprechend geschützt werden müssen.
   > 
   > 
5. Wenn Sie eine mobile Anwendung entwickeln, stellen Sie den Schalter **Nativen Client einschließen** auf **Ja**. Notieren Sie sich den standardmäßigen **Umleitungs-URI** , der automatisch für Sie erstellt wurde.
6. Klicken Sie auf **Erstellen** , um Ihre Anwendung zu registrieren.
7. Klicken Sie auf die soeben erstellte Anwendung, und notieren Sie sich die global eindeutige **Anwendungsclient-ID** zur späteren Verwendung in Ihrem Code.

> [!IMPORTANT]
> Über das Blatt „B2C-Funktionen“ erstellte Anwendungen müssen am gleichen Ort verwaltet werden. Mit PowerShell oder über ein anderes Portal bearbeitete B2C-Anwendungen werden nicht mehr unterstützt und können voraussichtlich nicht mehr mit Azure Active Directory B2C verwendet werden.
> 
> 

## <a name="build-a-quick-start-application"></a>Erstellen einer Schnellstart-App
Nachdem Sie nun über eine bei Azure AD B2C registrierte Anwendung verfügen, können Sie zum Einstieg eines der Schnellstarttutorials ausführen. Hier sind einige Vorschläge:

[!INCLUDE [active-directory-v2-quickstart-table](../../includes/active-directory-b2c-quickstart-table.md)]




<!--HONumber=Feb17_HO1-->


