---
title: Navigateur de Xamarin.Essentials ouvrir
description: La classe du navigateur permet à une application ouvrir un lien web dans le navigateur par défaut système optimisé ou un navigateur externe.
ms.assetid: BABF40CC-8BEE-43FD-BE12-6301DF27DD33
author: jamesmontemagno
ms.author: jamont
ms.date: 05/04/2018
ms.openlocfilehash: 2a95d0b89b78ce8b0ddfdc94d86c284a6f8b2bbe
ms.sourcegitcommit: 4db5f5c93f79f273d8fc462de2f405458b62fc02
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2018
---
# <a name="xamarinessentials-browser"></a>Xamarin.Essentials navigateur

![Version préliminaire de NuGet](~/media/shared/pre-release.png)

Le **navigateur** classe permet à une application ouvrir un lien web dans le navigateur par défaut système optimisé ou un navigateur externe.

## <a name="using-browser"></a>À l’aide du navigateur

Ajoutez une référence à Xamarin.Essentials dans votre classe :

```csharp
using Xamarin.Essentials;
```

Les fonctionnalités du navigateur fonctionnent en appelant le `OpenAsync` méthode avec la `Uri` et `BrowserLaunchType`.

```csharp

public class BrowserTest
{
    public async Task OpenBrowser(Uri uri)
    {
        await Browser.OpenAsync(uri, BrowserLaunchType.SystemPreferred);
    }
}
```

## <a name="platform-implementation-specifics"></a>Caractéristiques d’implémentation de plate-forme

# <a name="androidtabandroid"></a>[Android](#tab/android)

Le Type de lancement détermine comment le navigateur est lancé :

## <a name="system-preferred"></a>Système par défaut

[Chrome personnalisé onglets](https://developer.chrome.com/multidevice/android/customtabs) sera tentée à utiliser l’Uri de la charge et de conserver la reconnaissance de navigation.

## <a name="external"></a>Ressource externe

Un `Intent` permet de demander l’Uri est ouvert via le navigateur normal de systèmes.

# <a name="iostabios"></a>[iOS](#tab/ios)

## <a name="system-preferred"></a>Système par défaut

[SFSafariViewController](https://developer.xamarin.com/api/type/SafariServices.SFSafariViewController/) est utilisé pour charger l’Uri et de conserver la reconnaissance de navigation.

## <a name="external"></a>Ressource externe

La norme `OpenUrl` sur l’application principale est utilisé pour lancer le navigateur par défaut en dehors de l’application.

# <a name="uwptabuwp"></a>[UWP](#tab/uwp)

Navigateur par défaut de l’utilisateur sera toujours exécuté, quel que soit le `BrowserLaunchType`.

--------------

## <a name="api"></a>API

- [Code source du navigateur](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/Browser)
- [Documentation du navigateur API](xref:Xamarin.Essentials.Browser)
