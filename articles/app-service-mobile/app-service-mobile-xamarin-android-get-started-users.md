---
title: "Erste Schritte mit der Authentifizierung für mobile Apps in Xamarin Android"
description: "Erfahren Sie, wie Sie mobile Apps zum Authentifizieren Ihrer Xamarin Android-App über eine Vielzahl von Identitätsanbietern nutzen können, darunter AAD, Google, Facebook, Twitter und Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: adrianhall
manager: erikre
editor: 
ms.assetid: 570fc12b-46a9-4722-b2e0-0d1c45fb2152
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: adrianha
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 4c0ba82ca010f1ee571424fa3d650718e5acdd8b
ms.lasthandoff: 11/17/2016


---
# <a name="add-authentication-to-your-xamarinandroid-app"></a>Hinzufügen der Authentifizierung zu Ihrer Xamarin.Android-App
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

In diesem Thema wird die Authentifizierung von Benutzern einer mobilen App über Ihre Clientanwendung veranschaulicht. In diesem Lernprogramm fügen Sie eine Authentifizierung zu dem Schnellstartprojekt hinzu. Sie verwenden dazu einen Identitätsanbieter, der von Azure Mobile Apps unterstützt wird. Nach der erfolgreichen Authentifizierung und Autorisierung in Mobile Apps wird die Benutzer-ID angezeigt.

Dieses Lernprogramm baut auf dem Mobile App-Schnellstart auf. Sie müssen außerdem zunächst das Lernprogramm [Erstellen einer Xamarin.Android-App]abschließen. Wenn Sie das heruntergeladene Schnellstart-Serverprojekt nicht verwenden, müssen Sie Ihrem Projekt das Authentifizierungs-Erweiterungspaket hinzufügen. Weitere Informationen zu Servererweiterungspaketen finden Sie unter [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)(in englischer Sprache).

## <a name="a-nameregisteraregister-your-app-for-authentication-and-configure-app-services"></a><a name="register"></a>Registrieren Ihrer App für die Authentifizierung und Konfigurieren von App Services
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="a-namepermissionsarestrict-permissions-to-authenticated-users"></a><a name="permissions"></a>Einschränken von Berechtigungen für authentifizierte Benutzer
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Führen Sie das Clientprojekt in Visual Studio oder Xamarin Studio auf einem Gerät oder Emulator aus. Stellen Sie sicher, dass ein Ausnahmefehler mit dem Statuscode 401 (Nicht autorisiert) angezeigt wird, nachdem die App gestartet wurde. Dies liegt daran, dass die App versucht, als nicht authentifizierter Benutzer auf Ihr Mobile App-Back-End zuzugreifen. Die Tabelle *TodoItem* erfordert jetzt eine Authentifizierung.

Als Nächstes aktualisieren Sie die Client-App, um Ressourcen vom mobilen App-Back-End mit einem authentifizierten Benutzer zu aktualisieren.

## <a name="a-nameadd-authenticationaadd-authentication-to-the-app"></a><a name="add-authentication"></a>Hinzufügen von Authentifizierung zur App
Die App wird so aktualisiert, dass Benutzer auf die Schaltfläche **Anmelden** tippen und sich authentifizieren müssen, bevor Daten angezeigt werden.

1. Fügen Sie der **TodoActivity** -Klasse den folgenden Code hinzu:
   
        // Define a authenticated user.
        private MobileServiceUser user;
        private async Task<bool> Authenticate()
        {
                var success = false;
                try
                {
                    // Sign in with Facebook login using a server-managed flow.
                    user = await client.LoginAsync(this,
                        MobileServiceAuthenticationProvider.Facebook);
                    CreateAndShowDialog(string.Format("you are now logged in - {0}",
                        user.UserId), "Logged in!");
   
                    success = true;
                }
                catch (Exception ex)
                {
                    CreateAndShowDialog(ex, "Authentication failed");
                }
                return success;
        }
   
        [Java.Interop.Export()]
        public async void LoginUser(View view)
        {
            // Load data only after authentication succeeds.
            if (await Authenticate())
            {
                //Hide the button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load the data.
                OnRefreshItemsSelected();
            }
        }
   
    Dies erstellt eine neue Methode zum Authentifizieren eines Benutzers und einen Methodenhandler für die neue Schaltfläche **Anmelden** . Der Benutzer wird im Codebeispiel oben mithilfe eines Facebook-Logins authentifiziert. Ein Dialogfeld wird verwendet, um die Benutzer-ID nach der Authentifizierung anzuzeigen.
   
   > [!NOTE]
   > Falls Sie einen anderen Identitätsanbieter als Facebook verwenden, ändern Sie den an **LoginAsync** übergebenen Wert in einen der folgenden Werte: *MicrosoftAccount*, *Twitter*, *Google* oder *WindowsAzureActiveDirectory*.
   > 
   > 
2. Löschen Sie in der **OnCreate** -Methode die folgende Codezeile, oder kommentieren Sie sie aus:
   
        OnRefreshItemsSelected ();
3. Fügen Sie in der Datei „Activity_To_Do.axml“ die folgende Definition der Schaltfläche *LoginUser* vor der vorhandenen Schaltfläche *AddItem* hinzu:
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. Fügen Sie das folgende Element in die Ressourcendatei „Strings.xml“ ein:
   
        <string name="login_button_text">Sign in</string>
5. Führen Sie das Clientprojekt in Visual Studio oder Xamarin Studio auf einem Gerät oder Emulator aus, und melden Sie sich mit dem ausgewählten Identitätsanbieter an.
   
       When you are successfully logged-in, the app will display your login ID and the list of todo items, and you can make updates to the data.

<!-- URLs. -->
[Erstellen einer Xamarin.Android-App]: app-service-mobile-xamarin-android-get-started.md

