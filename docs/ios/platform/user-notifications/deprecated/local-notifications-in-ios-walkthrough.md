---
title: Procédure pas à pas - à l’aide de Notifications Local dans Xamarin.iOS
description: Dans cette section, nous examinerons l’utilisation de notifications locales dans une application Xamarin.iOS. Il va vous montrer les principes fondamentaux de la création et la publication d’une notification s’affiche une alerte lors de la réception par l’application.
ms.prod: xamarin
ms.assetid: 32B9C6F0-2BB3-4295-99CB-A75418969A62
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/18/2017
ms.openlocfilehash: bb133d16f12249cbd31e4fce2b227162b4b28333
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/04/2018
---
# <a name="walkthrough---using-local-notifications-in-xamarinios"></a>Procédure pas à pas - à l’aide de Notifications Local dans Xamarin.iOS

_Dans cette section, nous examinerons l’utilisation de notifications locales dans une application Xamarin.iOS. Il va vous montrer les principes fondamentaux de la création et la publication d’une notification s’affiche une alerte lors de la réception par l’application._

> [!IMPORTANT]
> Les informations contenues dans cette section relative à iOS 9 et antérieure, il est resté ici pour prendre en charge les anciennes versions d’iOS. Pour iOS 10 et versions ultérieures, consultez le [guide utilisateur Notification Framework](~/ios/platform/user-notifications/index.md) pour prendre en charge à la fois Local et distant Notification sur un appareil iOS.

## <a name="walkthrough"></a>Procédure pas à pas

Permettent de créer une application simple qui affiche les notifications locales en action. Cette application a un seul bouton sur elle. Lorsque nous cliquons sur le bouton, il crée une notification locale. Une fois la période de temps spécifié est écoulé, nous allons voir la notification s’affichent.


1. Dans Visual Studio pour Mac, créez une solution iOS vue unique et appelez-le `Notifications`.
1. Ouvrez le `Main.storyboard` de fichiers et faites glisser un bouton dans la vue. Nommez le bouton **bouton**et lui donner un titre **ajouter la Notification**. Vous pouvez également définir certaines [contraintes](~/ios/user-interface/designer/designer-auto-layout.md) sur le bouton à ce stade : 

    ![](local-notifications-in-ios-walkthrough-images/image3.png "Définition de certaines contraintes sur le bouton")
1. Modifier la `ViewController` classe et ajoutez le Gestionnaire d’événements suivant à la méthode ViewDidLoad :

    ```csharp
    button.TouchUpInside += (sender, e) =>
    {
        // create the notification
        var notification = new UILocalNotification();

        // set the fire date (the date time in which it will fire)
        notification.FireDate = NSDate.FromTimeIntervalSinceNow(60);

        // configure the alert
        notification.AlertAction = "View Alert";
        notification.AlertBody = "Your one minute alert has fired!";

        // modify the badge
        notification.ApplicationIconBadgeNumber = 1;

        // set the sound to be the default sound
        notification.SoundName = UILocalNotification.DefaultSoundName;

        // schedule it
        UIApplication.SharedApplication.ScheduleLocalNotification(notification);
    };
    ```

    Ce code crée une notification qui utilise un signal sonore, définit la valeur du badge icône sur 1 et affiche une alerte à l’utilisateur.

1. Ensuite modifier le fichier `AppDelegate.cs`, tout d’abord ajouter le code suivant à la `FinishedLaunching` (méthode). Nous avons vérifié pour voir si l’appareil est en cours d’exécution iOS 8, si nous sont donc **requis** pour demander l’autorisation de l’utilisateur de recevoir des notifications :

    ```csharp
    if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
            var notificationSettings = UIUserNotificationSettings.GetSettingsForTypes (
                UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound, null
            );

            application.RegisterUserNotificationSettings (notificationSettings);
        }
    ```

1. Toujours dans `AppDelegate.cs`, ajoutez la méthode suivante qui sera appelée lorsqu’une notification est reçue :

    ```csharp
    public override void ReceivedLocalNotification(UIApplication application, UILocalNotification notification)
            {
                // show an alert
                UIAlertController okayAlertController = UIAlertController.Create(notification.AlertAction, notification.AlertBody, UIAlertControllerStyle.Alert);
                okayAlertController.AddAction(UIAlertAction.Create("OK", UIAlertActionStyle.Default, null));

                Window.RootViewController.PresentViewController(okayAlertController, true, null);

                // reset our badge
                UIApplication.SharedApplication.ApplicationIconBadgeNumber = 0;
            }

    ```

1. Nous devons gérer le cas où la notification a été lancée en raison d’une notification locale. Modifier la méthode `FinishedLaunching` dans le `AppDelegate` pour inclure l’extrait de code suivant :


    ```csharp
    // check for a notification

    if (launchOptions != null)
    {
        // check for a local notification
        if (launchOptions.ContainsKey(UIApplication.LaunchOptionsLocalNotificationKey))
        {
            var localNotification = launchOptions[UIApplication.LaunchOptionsLocalNotificationKey] as UILocalNotification;
            if (localNotification != null)
            {
                UIAlertController okayAlertController = UIAlertController.Create(localNotification.AlertAction, localNotification.AlertBody, UIAlertControllerStyle.Alert);
                okayAlertController.AddAction(UIAlertAction.Create("OK", UIAlertActionStyle.Default, null));

                Window.RootViewController.PresentViewController(okayAlertController, true, null);

                // reset our badge
                UIApplication.SharedApplication.ApplicationIconBadgeNumber = 0;
            }
        }
    }

    ```

1. Enfin, exécutez l’application. Sur iOS 8, vous devrez autoriser les notifications. Cliquez sur **OK** puis cliquez sur le **ajouter la notification** bouton. Après un court instant, vous devez voir la boîte de dialogue alerte, comme indiqué dans les captures d’écran suivants :

    ![](local-notifications-in-ios-walkthrough-images/image0.png "Confirmer la possibilité d’envoyer des notifications") ![ ] (local-notifications-in-ios-walkthrough-images/image1.png "bouton de la Notification ajouter") ![ ] (local-notifications-in-ios-walkthrough-images/image2.png "la boîte de dialogue Alerte de notification")

## <a name="summary"></a>Récapitulatif

Cette procédure pas à pas vous a montré comment utiliser les différentes API pour créer et publier des notifications dans iOS. Il a également montré comment mettre à jour l’icône de l’application avec un badge pour fournir des commentaires spécifiques d’application à l’utilisateur.


## <a name="related-links"></a>Liens associés

- [Notifications locales (exemple)](https://developer.xamarin.com/samples/monotouch/LocalNotifications)
- [Local et le Guide de programmation des Notifications Push](https://developer.apple.com/library/prerelease/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/)
