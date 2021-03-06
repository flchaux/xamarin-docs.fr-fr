---
title: Modèles de données
description: Un DataTemplate est utilisé pour spécifier l’apparence des données sur les contrôles pris en charge et généralement lié aux données à afficher.
ms.prod: xamarin
ms.assetid: 838F4BDB-B719-457F-8633-27E9B267A2A0
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 09/11/2017
ms.openlocfilehash: 14de42acd1bde00df146a9fe5d772366735ed295
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/04/2018
---
# <a name="data-templates"></a>Modèles de données

_Un DataTemplate est utilisé pour spécifier l’apparence des données sur les contrôles pris en charge et généralement lié aux données à afficher._

## <a name="introductionintroductionmd"></a>[Introduction](introduction.md)

Xamarin.Forms des modèles de données permettent de définir la présentation des données sur les contrôles pris en charge. Cet article fournit une introduction aux modèles de données, examiner les raisons pour lesquelles ils sont nécessaires.

## <a name="creating-a-datatemplatecreatingmd"></a>[Création d’un DataTemplate](creating.md)

Modèles de données peuvent être créés en ligne, dans un [ `ResourceDictionary` ](https://developer.xamarin.com/api/type/Xamarin.Forms.ResourceDictionary/), ou d’un type personnalisé ou un type de cellule Xamarin.Forms approprié. Un modèle inline doit être utilisé s’il est inutile de réutiliser le modèle de données ailleurs. Vous pouvez également un modèle de données peut être réutilisé en le définissant comme un type personnalisé, ou comme ressource au niveau du contrôle, au niveau des pages, ou au niveau de l’application.

## <a name="creating-a-datatemplateselectorselectormd"></a>[Création d’un DataTemplateSelector](selector.md)

A [ `DataTemplateSelector` ](https://developer.xamarin.com/api/type/Xamarin.Forms.DataTemplateSelector/) peut être utilisé pour choisir un [ `DataTemplate` ](https://developer.xamarin.com/api/type/Xamarin.Forms.DataTemplate/) lors de l’exécution en fonction de la valeur d’une propriété liée aux données. Cela permet à plusieurs `DataTemplate` instances à appliquer le même type d’objet, pour personnaliser l’apparence d’objets particuliers. Cet article explique comment créer et utiliser un `DataTemplateSelector`.


## <a name="related-links"></a>Liens associés

- [Modèles de données (exemple)](https://developer.xamarin.com/samples/xamarin-forms/templates/datatemplates/)
