---
title: Déployer des cases à cocher désactivée dans le Gestionnaire de Configuration
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: aaf675cd-d885-4dac-9754-77dbcaea3be9
author: asb3993
ms.author: amburns
ms.date: 12/02/2016
ms.openlocfilehash: ab825ba4d28ca8768e5c633fc3779828638a498d
ms.sourcegitcommit: 0a72c7dea020b965378b6314f558bf5360dbd066
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2018
---
# <a name="deploy-checkboxes-disabled-in-configuration-manager"></a>Déployer des cases à cocher désactivée dans le Gestionnaire de Configuration

Depuis Xamarin 3.5, Xamarin.iOS projets déployés automatiquement chaque fois que vous appuyez sur la **Démarrer** bouton de barre d’outils ou le choix le **Déboguer > Démarrer le débogage** élément de menu. Vous devez toujours définir le projet d’application Xamarin.iOS souhaité comme le **projet de démarrage** avant avant d’exécuter des deux commandes.

Pour cette raison, le **déployer** cases à cocher sont désactivées intentionnellement dans le Gestionnaire de Configuration Visual Studio pour les projets de Xamarin.iOS :

![](deploy-checkboxes-images/configuration.png "Gestionnaire de Configuration Visual Studio affichant la case à cocher « Déployer » désactivée pour un projet de Xamarin.iOS dans Xamarin 3.5")

Cette modification élimine une erreur peut apparaître dans les versions antérieures de Xamarin (version 3.3 et versions antérieure) lorsque le projet d’application Xamarin.iOS n’a pas été défini à déployer :

![](deploy-checkboxes-images/error.png "Message d’erreur : le projet iPhoneApp1 doit être déployé avant de pouvoir être démarré. Vérifiez que le projet est sélectionné pour être déployé dans le Gestionnaire de Configuration de Solution.")
