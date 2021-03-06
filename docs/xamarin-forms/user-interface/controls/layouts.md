---
title: Dispositions de Xamarin.Forms
description: Xamarin.Forms dispositions sont utilisées pour composer des contrôles d’interface utilisateur dans des structures visual.
ms.prod: xamarin
ms.assetid: F4180997-BA21-453A-9958-D1E2940DF050
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 05/21/2018
ms.openlocfilehash: ca48ad6fb7d5aae53f972f6e3b5257919d140a8d
ms.sourcegitcommit: 4f646dc5c51db975b2936169547d625c78a22b30
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2018
---
# <a name="xamarinforms-layouts"></a>Dispositions de Xamarin.Forms

_Xamarin.Forms dispositions sont utilisées pour composer des contrôles d’interface utilisateur dans des structures visual._

Le [ `Layout` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Layout) et [ `Layout<T>` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Layout%3CT%3E/) classes Xamarin.Forms sont spécialisées sous-types de vues qui agissent comme conteneurs pour les vues et autres mises en page. Le `Layout` dérive de la classe elle-même [ `View` ](views.md). Un `Layout` dérivé contient généralement une logique pour définir la position et la taille des éléments enfants dans les applications de Xamarin.Forms.

[![Types de mise en page Xamarin.Forms](layouts-images/layouts-sml.png "Xamarin.Forms disposition Types")](layouts-images/layouts.png#lightbox "Types de disposition de Xamarin.Forms")

Les classes qui dérivent de `Layout` peut être divisé en deux catégories :

## <a name="layouts-with-single-content"></a>Mises en page avec un contenu unique

Ces classes dérivent [ `Layout` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Layout/), qui définit [ `Padding` ](https://developer.xamarin.com/api/property/Xamarin.Forms.Layout.Padding/) et [ `IsClippedToBounds` ](https://developer.xamarin.com/api/property/Xamarin.Forms.Layout.IsClippedToBounds/) propriétés.

<a name="contentView" />

### <a name="contentview"></a>ContentView

|     |     |
| --- | --- |
| [`ContentView`](https://developer.xamarin.com/api/type/Xamarin.Forms.ContentView/) contient un seul enfant qui est défini avec la [ `Content` ](https://developer.xamarin.com/api/property/Xamarin.Forms.ContentView.Content/) propriété. Le `Content` propriété peut être définie sur any `View` dérivé, y compris d’autres `Layout` dérivés. `ContentView` est principalement utilisée comme un élément structurel et sert de classe de base à [ `Frame` ](#frame).<br /><br />[Documentation de l’API](https://developer.xamarin.com/api/type/Xamarin.Forms.ContentView/) | [![Exemple de ContentView](layouts-images/ContentView.png "ContentView exemple")](layouts-images/ContentView-Large.png#lightbox "ContentView exemple")<br />[Code c# pour cette page](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/ContentViewDemoPage.cs) / [page XAML](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/ContentViewDemoPage.xaml) |
|     |     |

<a named="frame" />

### <a name="frame"></a>Frame

|     |     |
| --- | --- |
| Le [ `Frame` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Frame/) dérive de la classe [ `ContentView` ](#contentView) et affiche un cadre rectangulaire autour de son enfant. `Frame` a une valeur par défaut [ `Padding` ](https://developer.xamarin.com/api/property/Xamarin.Forms.Layout.Padding/) valeur 20 et définit également [ `OutlineColor` ](https://developer.xamarin.com/api/property/Xamarin.Forms.Frame.OutlineColor/), [ `CornerRadius` ](https://developer.xamarin.com/api/property/Xamarin.Forms.Frame.CornerRadius/), et [ `HasShadow` ](https://developer.xamarin.com/api/property/Xamarin.Forms.Frame.HasShadow/)propriétés.<br /><br />[Documentation de l’API](https://developer.xamarin.com/api/type/Xamarin.Forms.Frame/) | [![Exemple de frame](layouts-images/Frame.png "Frame exemple")](layouts-images/Frame-Large.png#lightbox "Frame d’exemple")<br />[Code c# pour cette page](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/FrameDemoPage.cs) / [page XAML](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/FrameDemoPage.xaml) |
|     |     |

<a name="scrollView" />

### <a name="scrollview"></a>ScrollView

|     |     |
| --- | --- |
| [`ScrollView`](https://developer.xamarin.com/api/type/Xamarin.Forms.ScrollView/) est capable de faire défiler son contenu. Définir le [ `Content` ](https://developer.xamarin.com/api/property/Xamarin.Forms.ScrollView.Content/) propriété à une vue ou une disposition trop grande pour tenir sur l’écran. (Le contenu d’un `ScrollView` est très souvent un [ `StackLayout` ](#stackLayout).) Définir le [ `Orientation` ](https://developer.xamarin.com/api/property/Xamarin.Forms.ScrollView.Orientation/) propriété pour indiquer si le défilement doit être vertical, horizontal, ou les deux.<br /><br />[Documentation de l’API](https://developer.xamarin.com/api/type/Xamarin.Forms.ScrollView/) / [Guide](~/xamarin-forms/user-interface/layouts/scroll-view.md) / [exemple](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Layout/) | [![Exemple de ScrollView](layouts-images/ScrollView.png "ScrollView exemple")](layouts-images/ScrollView-Large.png#lightbox "ScrollView exemple")<br />[Code c# pour cette page](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/ScrollViewDemoPage.cs) / [page XAML](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/ScrollViewDemoPage.xaml) |
|     |     |

### <a name="templatedview"></a>TemplatedView

|     |     |
| --- | --- |
| [`TemplatedView`](https://developer.xamarin.com/api/type/Xamarin.Forms.TemplatedView/) Affiche le contenu avec un modèle de contrôle, et est la classe de base pour [ `ContentView` ](#contentView).<br /><br />[Documentation de l’API](https://developer.xamarin.com/api/type/Xamarin.Forms.TemplatedView/) / [Guide](~/xamarin-forms/app-fundamentals/templates/control-templates/index.md) | [![Exemple de TemplatedView](layouts-images/TemplatedView.png "TemplatedView exemple")](layouts-images/TemplatedView.png#lightbox "TemplatedView exemple") |
|     |     |

### <a name="contentpresenter"></a>ContentPresenter

|     |     |
| --- | --- |
| [`ContentPresenter`](https://developer.xamarin.com/api/type/Xamarin.Forms.ContentPresenter/) est un gestionnaire de disposition pour les vues basées sur un modèle, au sein d’un [ `ControlTemplate` ](https://developer.xamarin.com/api/type/Xamarin.Forms.ControlTemplate/) pour marquer où s’affiche le contenu qui doit être présentées.<br /><br />[Documentation de l’API](https://developer.xamarin.com/api/type/Xamarin.Forms.ContentPresenter/) / [Guide](~/xamarin-forms/app-fundamentals/templates/control-templates/index.md) | [![Exemple de ContentPresenter](layouts-images/ContentPresenter.png "ContentPresenter exemple")](layouts-images/ContentPresenter.png#lightbox "ContentPresenter exemple") |
|     |     |

## <a name="layouts-with-multiple-children"></a>Dispositions de plusieurs enfants

Ces classes dérivent [ `Layout<View>` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Layout%3CT%3E/).

<a name="stackLayout" />

### <a name="stacklayout"></a>StackLayout

|     |     |
| --- | --- |
| [`StackLayout`](https://developer.xamarin.com/api/type/Xamarin.Forms.StackLayout/) Positionne les éléments enfants dans une pile soit horizontalement ou verticalement en se basant sur le [ `Orientation` ](https://developer.xamarin.com/api/property/Xamarin.Forms.StackLayout.Orientation/) propriété. Le [ `Spacing` ](https://developer.xamarin.com/api/property/Xamarin.Forms.StackLayout.Spacing/) propriété régit l’espacement entre les enfants et a la valeur par défaut 6.<br /><br />[Documentation de l’API](https://developer.xamarin.com/api/type/Xamarin.Forms.StackLayout/) / [Guide](~/xamarin-forms/user-interface/layouts/stack-layout.md) / [exemple](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Layout/)| [![Exemple de StackLayout](layouts-images/StackLayout.png "StackLayout exemple")](layouts-images/StackLayout-Large.png#lightbox "StackLayout exemple")<br />[Code c# pour cette page](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/StackLayoutDemoPage.cs) / [page XAML](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/StackLayoutDemoPage.xaml) |
|     |     |

<a name="grid" />

### <a name="grid"></a>Grille

|     |     |
| --- | --- |
| [`Grid`](https://developer.xamarin.com/api/type/Xamarin.Forms.Grid/) Positionne ses éléments enfants dans une grille de lignes et de colonnes. Position d’un enfant est indiquée à l’aide de la [propriétés jointes](~/xamarin-forms/xaml/attached-properties.md) [ `Row` ](https://developer.xamarin.com/api/field/Xamarin.Forms.Grid.RowProperty/), [ `Column` ](https://developer.xamarin.com/api/field/Xamarin.Forms.Grid.ColumnProperty/), [ `RowSpan` ](https://developer.xamarin.com/api/field/Xamarin.Forms.Grid.RowSpanProperty/), et [ `ColumnSpan` ](https://developer.xamarin.com/api/field/Xamarin.Forms.Grid.ColumnSpanProperty/).<br /><br />[Documentation de l’API](https://developer.xamarin.com/api/type/Xamarin.Forms.Grid/) / [Guide](~/xamarin-forms/user-interface/layouts/grid.md) / [exemple](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Layout/) | [![Exemple de grille](layouts-images/Grid.png "exemple de grille")](layouts-images/Grid-Large.png#lightbox "exemple de grille")<br />[Code c# pour cette page](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/GridDemoPage.cs) / [page XAML](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/GridDemoPage.xaml) |
|     |     |

### <a name="absolutelayout"></a>DispositionAbsolue

|     |     |
| --- | --- |
| [`AbsoluteLayout`](https://developer.xamarin.com/api/type/Xamarin.Forms.AbsoluteLayout/) Positionne les éléments enfants à des emplacements spécifiques par rapport à son parent. Position d’un enfant est indiquée à l’aide de la [propriétés jointes](~/xamarin-forms/xaml/attached-properties.md) [ `LayoutBounds` ](https://developer.xamarin.com/api/field/Xamarin.Forms.AbsoluteLayout.LayoutBoundsProperty/) et [ `LayoutFlags` ](https://developer.xamarin.com/api/field/Xamarin.Forms.AbsoluteLayout.LayoutFlagsProperty/). Un `AbsoluteLayout` est utile pour animer les positions des vues.<br /><br />[Documentation de l’API](https://developer.xamarin.com/api/type/Xamarin.Forms.AbsoluteLayout/) / [Guide](~/xamarin-forms/user-interface/layouts/absolute-layout.md) / [exemple](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Layout/) | [![Exemple de DispositionAbsolue](layouts-images/AbsoluteLayout.png "DispositionAbsolue exemple")](layouts-images/AbsoluteLayout-Large.png#lightbox "DispositionAbsolue exemple")<br />[Code c# pour cette page](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/AbsoluteLayoutdDemoPage.cs) / [page XAML](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/AbsoluteLayoutDemoPage.xaml) avec [code-behind](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/AbsoluteLayoutDemoPage.xaml.cs) |
|     |     |

### <a name="relativelayout"></a>RelativeLayout

|     |     |
| --- | --- |
| [`RelativeLayout`](https://developer.xamarin.com/api/type/Xamarin.Forms.RelativeLayout/) Positionne les éléments enfants relatif à la `RelativeLayout` lui-même ou pour leurs frères. Position d’un enfant est indiquée à l’aide de la [propriétés jointes](~/xamarin-forms/xaml/attached-properties.md) qui sont définies sur les objets de type [ `Constraint` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Constraint/) et [ `BoundsConstraint` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Constraint/).<br /><br />[Documentation de l’API](https://developer.xamarin.com/api/type/Xamarin.Forms.RelativeLayout/) / [Guide](~/xamarin-forms/user-interface/layouts/relative-layout.md) / [exemple](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Layout/) | [![Exemple de RelativeLayout](layouts-images/RelativeLayout.png "RelativeLayout exemple")](layouts-images/RelativeLayout-Large.png#lightbox "RelativeLayout exemple")<br />[Code c# pour cette page](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/RelativeLayoutDemoPage.cs) / [page XAML](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/RelativeLayoutDemoPage.xaml) |
|     |     |

### <a name="flexlayout"></a>FlexLayout

|     |     |
| --- | --- |
| [`FlexLayout`](xref:Xamarin.Forms.FlexLayout) est basé sur le code CSS [Flexible Module de mise en page de boîte de](http://www.w3.org/TR/css-flexbox-1/), communément appelé _flex disposition_ ou _flex-box_. `FlexLayout` définit les cinq propriétés jointes pouvant être liées qui autorisent les enfants à être ni empilés, ni encapsulée avec de nombreuses options d’alignement et l’orientation et les six propriétés pouvant être liées.<br /><br />[Documentation de l’API](xref:Xamarin.Forms.FlexLayout) / [Guide](~/xamarin-forms/user-interface/layouts/flex-layout.md) / [exemple](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/FlexLayoutDemos/) | [![Exemple de FlexLayout](layouts-images/FlexLayout.png "FlexLayout exemple")](layouts-images/FlexLayout-Large.png#lightbox "FlexLayout exemple")<br />[Code c# pour cette page](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/CodeExamples/FlexLayoutDemoPage.cs) / [page XAML](https://github.com/xamarin/xamarin-forms-samples/blob/master/FormsGallery/FormsGallery/FormsGallery/XamlExamples/FlexLayoutDemoPage.xaml) |
|     |     |

## <a name="related-links"></a>Liens associés

- [Introduction à Xamarin.Forms](~/xamarin-forms/get-started/introduction-to-xamarin-forms.md)
- [Exemple de Xamarin.Forms FormsGallery](https://developer.xamarin.com/samples/FormsGallery/)
- [Exemples Xamarin.Forms](https://developer.xamarin.com/samples/xamarin-forms/all/)
- [Documentation de l’API de Xamarin.Forms](https://developer.xamarin.com/api/root/Xamarin.Forms/)
