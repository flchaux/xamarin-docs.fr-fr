---
title: L’incorporation de .NET dans Java
description: Comment utiliser une bibliothèque de Xamarin .NET dans un projet Android Native basée sur Java
ms.prod: xamarin
ms.assetid: A489EEF3-1008-4257-BF63-FE21D8C23821
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 03/28/2018
ms.openlocfilehash: 0ca855975db4b20fe80e98e2e818b8fde27f558c
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/04/2018
---
# <a name="embedding-net-in-java"></a>L’incorporation de .NET dans Java

Dans certains cas, vous souhaiterez ajouter une bibliothèque .NET de Xamarin à un projet Android natif existant. Pour ce faire, vous pouvez utiliser la [Embeddinator-4000](https://mono.github.io/Embeddinator-4000/) outil pour activer votre bibliothèque .NET dans une bibliothèque native qui peut être incorporée dans une application Android native basée sur Java.

 
## <a name="requirements"></a>Spécifications

Pour utiliser le Embeddinator-4000 avec Java sur Android, vous devez les éléments suivants :

-   **Android Studio** &ndash; [Android Studio 3.x](https://developer.android.com/studio/preview/index.html) ou version ultérieure doit être installé.

-   **Xamarin.Android** &ndash; [Xamarin.Android 7.5](https://www.visualstudio.com/xamarin/) ou version ultérieure doit être installé.

-   **Kit de développement Java** &ndash; [Java 1.8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) ou version ultérieure doit être installé.

-   **Mono** &ndash; [Mono 5.0](http://www.mono-project.com/download/) ou version ultérieure doit être installé.


# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Vous pouvez utiliser Visual Studio pour modifier et compiler votre code c#.

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio pour Mac](#tab/vsmac)

Vous pouvez utiliser Visual Studio pour Mac pour modifier et compiler votre code c#.

-----

 
## <a name="using-the-embeddinator-4000"></a>À l’aide de la Embeddinator-4000.

Pour utiliser une bibliothèque .NET dans un projet Android native, vous utilisez les étapes suivantes :

1.  Créez un projet de bibliothèque Android c#.

2.  Installez Embeddinator-4000 via NuGet.

3.  Exécutez Embeddinator sur l’assembly de bibliothèque Android.

4.  Utilisez le fichier AAR généré dans un projet Java dans Android Studio.

Ces étapes sont décrites en détail dans les [Embeddinator-4000](https://mono.github.io/Embeddinator-4000/getting-started-java-android.html) documentation.
