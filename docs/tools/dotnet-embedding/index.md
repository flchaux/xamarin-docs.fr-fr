---
title: Incorporation .NET
description: 'Incorporation de .NET permet à votre Code .NET existant (c#, F #, etc.) à être consommés à partir d’autres langages de programmation'
ms.prod: xamarin
ms.assetid: 617C38CA-B921-4A76-8DFC-B0A3DF90E48A
author: topgenorth
ms.author: toopge
ms.date: 11/14/2017
ms.openlocfilehash: f6edf25faa00bc7c90a52b76a6e90168ccd85b32
ms.sourcegitcommit: 0a72c7dea020b965378b6314f558bf5360dbd066
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2018
---
# <a name="net-embedding"></a>Incorporation .NET

![Preview](~/media/shared/preview.png)

Incorporation de .NET permet à votre Code .NET existant (c#, F #, etc.) à partir d’autres langages de programmation et dans plusieurs environnements différents.

Cela signifie que si vous avez une bibliothèque .NET que vous souhaitez utiliser à partir de votre application iOS existante, vous pouvez le faire.   Ou, si vous souhaitez lier à une bibliothèque C++ native, vous pouvez également effectuer cette opération.   Ou utiliser du code .NET à partir de Java.

Incorporation de .NET est basée sur la [Embeddinator-4000](https://github.com/mono/Embeddinator-4000) projet open source.

## <a name="environments-and-languages"></a>Les environnements et les langues

L’outil est à la fois prenant en charge de l’environnement, qu'il utilise, ainsi que la langue qui est utilisées.   Par exemple, la plateforme iOS n’autorise pas la compilation juste-à-temps (JIT), afin de l’incorporation de .NET statiquement compilera votre code .NET en code natif qui peut être utilisé dans iOS.  Autres environnements n’autorisent pas la compilation JIT et dans ces environnements, nous accepter les compilation JIT.

Il prend en charge divers consommateurs de langage, il met en évidence de code .NET en tant que code IDIOMATIQUE dans le langage cible.   Voici la liste des langues prises en charge à l’heure actuelle :

- [**Objective-C** ](objective-c/index.md) – mappage .NET pour les API Objective-C IDIOMATIQUE
- [**Java** ](android/index.md) – mappage .NET à IDIOMATIQUE API Java
- [**C** ](get-started/c.md) – mappage .NET à orientée objet, comme les API C

D’autres langues seront ultérieurement.

## <a name="getting-started"></a>Prise en main

Pour commencer, vérifiez l’une de nos guides pour chacune des langues prises en charge actuellement :

- [**Objective-C** ](get-started/objective-c/index.md) – couvre macOS et iOS
- [**Java** ](get-started/java/index.md) – couvre macOS et Android
- [**C** ](get-started/c.md) – couvre le langage C sur les plateformes de bureau

## <a name="related-links"></a>Liens associés

- [Embeddinator-4000 sur GitHub](https://github.com/mono/Embeddinator-4000)
