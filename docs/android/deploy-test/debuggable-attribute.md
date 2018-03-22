---
title: "Attribut débogable"
ms.topic: article
ms.prod: xamarin
ms.assetid: 1ABF90F1-6A70-45AE-9271-D90DC42807D0
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 02/05/2018
ms.openlocfilehash: 65037029d01d499421fd825f72347ae1bebd9966
ms.sourcegitcommit: 0fdb243b46cf21be47584900805cadcd077121bf
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/12/2018
---
# <a name="debuggable-attribute"></a>Attribut débogable



Pour permettre le débogage, Android prend en charge Java Debug Wire Protocol (JDWP). Cette technologie permet à des outils tels qu’ADB de communiquer avec une machine virtuelle Java. JDWP est important pendant le développement, mais il doit être désactivé avant la publication de l’application.

JDWP peut être la valeur de l’attribut `android:debuggable` dans une application Android. Xamarin.Android offre les possibilités suivantes pour définir cet attribut :

1.  Création d’un fichier `AndroidManifext.xml` et définition de l’attribut `android:debuggable` dans ce dernier.
1.  Inclusion de `ApplicationAttribute` dans un fichier `.CS`  comme suit : `[assembly: Application(Debuggable=false)]`.


Si `AndroidManifest.xml` et `ApplicationAttribute` sont tous deux présents, le contenu de `AndroidManifest.xml` est prioritaire devant ce qui est spécifié par le `ApplicationAttribute`.

Si ni `AndroidManifest.xml` ni `ApplicationAttribute` ne sont présents, la valeur par défaut de l’attribut `android:debuggable` dépend de la génération ou non de symboles de débogage. S’il y a des symboles de débogage, Xamarin.Android définira l’attribut `android:debuggable` sur `true`.

Notez que la valeur des attributs `android:debuggable` ne dépend PAS nécessairement de la configuration de build. Il est possible que l’attribut `android:debuggable` des versions release soit défini sur true.


## <a name="related-links"></a>Liens associés

- [Applications débogables sur le marché Android](http://labs.mwrinfosecurity.com/blog/2011/07/07/debuggable-apps-in-android-market/)