---
title: Numéroteur Xamarin.Essentials
description: La classe PhoneDialer permet à une application ouvrir un lien web dans le navigateur par défaut système optimisé ou un navigateur externe.
ms.assetid: E7457942-4D7B-4195-A2FF-417919B9537F
author: jamesmontemagno
ms.author: jamont
ms.date: 05/04/2018
ms.openlocfilehash: 112cc305457413ad057e390d46c5a765ea29514f
ms.sourcegitcommit: 3e05b135b6ff0d607bc2378c1b6e66d2eebbcc3e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/12/2018
---
# <a name="xamarinessentials-phone-dialer"></a>Numéroteur Xamarin.Essentials

![Version préliminaire de NuGet](~/media/shared/pre-release.png)

Le **PhoneDialer** classe permet à une application ouvrir un lien web dans le navigateur par défaut système optimisé ou un navigateur externe.

## <a name="using-phone-dialer"></a>À l’aide de Numéroteur téléphonique

Ajoutez une référence à Xamarin.Essentials dans votre classe :

```csharp
using Xamarin.Essentials;
```

La fonctionnalité Numéroteur téléphonique fonctionne en appelant le `Open` méthode avec un numéro de téléphone pour ouvrir le numéroteur avec. Lorsque `Open` est demandé à l’API tente automatiquement de mettre en forme le nombre en fonction de l’indicatif du pays, s’il est spécifié.

```csharp
public class PhoneDialerTest
{
    public async Task PlacePhoneCall(string number)
    {
        try
        {
            PhoneDialer.Open(number);
        }
        catch (ArgumentNullException anEx)
        {
            // Number was null or white space
        }
        catch (FeatureNotSupportedException ex)
        {
            // Phone Dialer is not supported on this device.
        }
        catch (Exception ex)
        {
            // Other error has occurred.
        }
    }
}
```

## <a name="api"></a>API

- [Numéroteur téléphonique code source](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/PhoneDialer)
- [Documentation de l’API de Numéroteur téléphonique](xref:Xamarin.Essentials.PhoneDialer)
