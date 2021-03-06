---
title: Par courrier électronique Xamarin.Essentials
description: La classe de messagerie permet à une application ouvrir l’application de messagerie par défaut avec une informations spécifiées, y compris l’objet, le corps et les destinataires (à, CC, Cci).
ms.assetid: 5FBB6FF0-0E7B-4C29-8F06-91642AF12629
author: jamesmontemagno
ms.author: jamont
ms.date: 05/04/2018
ms.openlocfilehash: 3fee30e31dc18665d59f944462959fd3f8166968
ms.sourcegitcommit: 4db5f5c93f79f273d8fc462de2f405458b62fc02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2018
---
# <a name="xamarinessentials-email"></a>Par courrier électronique Xamarin.Essentials

![Version préliminaire de NuGet](~/media/shared/pre-release.png)

Le **messagerie** classe permet à une application ouvrir l’application de messagerie par défaut avec une informations spécifiées, y compris l’objet, le corps et les destinataires (à, CC, Cci).

## <a name="using-email"></a>Courrier électronique

Ajoutez une référence à Xamarin.Essentials dans votre classe :

```csharp
using Xamarin.Essentials;
```

La fonctionnalité de courrier électronique fonctionne en appelant le `ComposeAsync` méthode un `EmailMessage` qui contient des informations sur l’adresse de messagerie :

```csharp
public class EmailTest
{
    public async Task SendEmail(string subject, string body, List<string> recipients)
    {
        try
        {
            var message = new EmailMessage
            {
                Subject = subject,
                Body = body,
                To = recipients,
                //Cc = ccRecipients,
                //Bcc = bccRecipients
            }
            await Email.ComposeAsync(message);
        }
        catch (FeatureNotSupportedException fbsEx)
        {
            // Sms is not supported on this device
        }
        catch (Exception ex)
        {
            // Some other exception occured
        }
    }
}
```

## <a name="api"></a>API

- [Code source de messagerie](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/Email)
- [Documentation de l’API de messagerie](xref:Xamarin.Essentials.Email)
