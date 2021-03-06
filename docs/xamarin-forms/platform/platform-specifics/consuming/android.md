---
title: Caractéristiques de plate-forme Android
description: Caractéristiques de la plateforme vous permettent de vous permet d’utiliser la fonctionnalité est disponible uniquement sur une plateforme spécifique, sans avoir à implémenter des convertisseurs personnalisés ou les effets. Cet article montre comment consommer les spécificités de plate-forme Android qui sont intégrées dans Xamarin.Forms.
ms.prod: xamarin
ms.assetid: C5D4AA65-9BAA-4008-8A1E-36CDB78A435D
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 05/23/2018
ms.openlocfilehash: 8d7ec3f2f64fdb8be903fd13bd72bcf545265a3d
ms.sourcegitcommit: 4f646dc5c51db975b2936169547d625c78a22b30
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2018
---
# <a name="android-platform-specifics"></a>Caractéristiques de plate-forme Android

_Caractéristiques de la plateforme vous permettent de vous permet d’utiliser la fonctionnalité est disponible uniquement sur une plateforme spécifique, sans avoir à implémenter des convertisseurs personnalisés ou les effets. Cet article montre comment consommer les spécificités de plate-forme Android qui sont intégrées dans Xamarin.Forms._

Sur Android, Xamarin.Forms contient les spécifications de plateforme suivantes :

- Définition du mode de fonctionnement d’un clavier programmable. Pour plus d’informations, consultez [définition du Mode d’entrée clavier logicielle](#soft_input_mode).
- L’activation rapide de défilement dans une [ `ListView` ](https://developer.xamarin.com/api/type/Xamarin.Forms.ListView/) pour plus d’informations, consultez [permettant le défilement rapide dans un ListView](#fastscroll).
- Activer le glissement entre les pages dans un [ `TabbedPage` ](https://developer.xamarin.com/api/type/Xamarin.Forms.TabbedPage/). Pour plus d’informations, consultez [activation passant entre les Pages dans un TabbedPage](#enable_swipe_paging).
- Contrôle de l’ordre de plan des éléments visuels pour déterminer l’ordre de dessin. Pour plus d’informations, consultez [contrôle de l’élévation d’éléments visuels](#elevation).
- La désactivation de la [ `Disappearing` ](https://developer.xamarin.com/api/event/Xamarin.Forms.Page.Appearing/) et [ `Appearing` ](https://developer.xamarin.com/api/event/Xamarin.Forms.Page.Appearing/) page événements de cycle de vie sur Suspendre et reprendre respectivement, pour les applications qui utilisent AppCompat. Pour plus d’informations, consultez [la désactivation de la Disappearing et les événements de cycle de vie de Page qui apparaissent](#disable_lifecycle_events).
- Contrôle si un [ `WebView` ](xref:Xamarin.Forms.WebView) peut afficher un contenu mixte. Pour plus d’informations, consultez [activation du contenu mixte dans un WebView](#webview-mixed-content).
- Définition des options de l’éditeur pour le clavier logiciel pour la méthode d’entrée une [ `Entry` ](xref:Xamarin.Forms.Entry). Pour plus d’informations, consultez [Options d’éditeur de méthode d’entrée de paramètre entrée](#entry-imeoptions).

<a name="soft_input_mode" />

## <a name="setting-the-soft-keyboard-input-mode"></a>Définition du Mode d’entrée de clavier logiciel

Cette plateforme spécifique est utilisée pour définir le mode de fonctionnement pour une zone d’entrée de clavier logiciel et est utilisée en XAML en définissant le [ `Application.WindowSoftInputModeAdjust` ](https://developer.xamarin.com/api/field/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.Application.WindowSoftInputModeAdjustProperty/) à une valeur de propriété attachée la [ `WindowSoftInputModeAdjust` ](https://developer.xamarin.com/api/type/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.WindowSoftInputModeAdjust/) énumération :

```xaml
<Application ...
             xmlns:android="clr-namespace:Xamarin.Forms.PlatformConfiguration.AndroidSpecific;assembly=Xamarin.Forms.Core"
             android:Application.WindowSoftInputModeAdjust="Resize">
  ...
</Application>
```

Vous pouvez également être utilisée à partir de c# à l’aide de l’API fluent :

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.AndroidSpecific;
...

App.Current.On<Android>().UseWindowSoftInputModeAdjust(WindowSoftInputModeAdjust.Resize);
```

Le `Application.On<Android>` méthode spécifie que cette plate-forme spécifique sera exécuté uniquement sur Android. Le [ `Application.UseWindowSoftInputModeAdjust` ](https://developer.xamarin.com/api/member/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.Application.UseWindowSoftInputModeAdjust/p/Xamarin.Forms.IPlatformElementConfiguration{Xamarin.Forms.PlatformConfiguration.Android,Xamarin.Forms.Application}/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.WindowSoftInputModeAdjust/) (méthode), dans le [ `Xamarin.Forms.PlatformConfiguration.AndroidSpecific` ](https://developer.xamarin.com/api/namespace/Xamarin.Forms.PlatformConfiguration.AndroidSpecific/) espace de noms est utilisée pour définir le mode de fonctionnement de zone d’entrée clavier programmable, avec la [ `WindowSoftInputModeAdjust` ](https://developer.xamarin.com/api/type/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.WindowSoftInputModeAdjust/) énumération qui fournit deux valeurs : [ `Pan` ](https://developer.xamarin.com/api/field/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.WindowSoftInputModeAdjust.Pan/) et [ `Resize` ](https://developer.xamarin.com/api/field/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.WindowSoftInputModeAdjust.Resize/). Le `Pan` valeur utilise le [ `AdjustPan` ](https://developer.xamarin.com/api/field/Android.Views.SoftInput.AdjustPan/) option de réglage, qui ne se redimensionne la fenêtre quand un contrôle d’entrée a le focus. Au lieu de cela, le contenu de la fenêtre est panoramique afin que le focus actuel n’est pas masqué par le clavier logiciel. Le `Resize` valeur utilise le [ `AdjustResize` ](https://developer.xamarin.com/api/field/Android.Views.SoftInput.AdjustResize/) option de réglage, qui redimensionne la fenêtre lorsqu’un contrôle d’entrée a le focus, pour libérer de l’espace pour le clavier logiciel.

Le résultat est que le clavier logiciel d’entrée de zone de mode de fonctionnement peut être défini quand un contrôle d’entrée a le focus :

[![](android-images/pan-resize.png "Clavier logiciel fonctionne en Mode spécifique à la plateforme")](android-images/pan-resize-large.png#lightbox "Soft Keyboard Operating Mode Plaform-Specific")

<a name="fastscroll" />

## <a name="enabling-fast-scrolling-in-a-listview"></a>L’activation de défilement rapide dans un ListView

Cette plateforme spécifique est utilisée pour activer le défilement rapide des données dans un [ `ListView` ](https://developer.xamarin.com/api/type/Xamarin.Forms.ListView/). Elle est consommée en XAML en définissant le `ListView.IsFastScrollEnabled` propriété attachée un `boolean` valeur :

```xaml
<ContentPage ...
             xmlns:android="clr-namespace:Xamarin.Forms.PlatformConfiguration.AndroidSpecific;assembly=Xamarin.Forms.Core">
    <StackLayout Margin="20">
        ...
        <ListView ItemsSource="{Binding GroupedEmployees}"
                  GroupDisplayBinding="{Binding Key}"
                  IsGroupingEnabled="true"
                  android:ListView.IsFastScrollEnabled="true">
            ...
        </ListView>
    </StackLayout>
</ContentPage>
```

Vous pouvez également être utilisée à partir de c# à l’aide de l’API fluent :

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.AndroidSpecific;
...

var listView = new Xamarin.Forms.ListView { IsGroupingEnabled = true, ... };
listView.SetBinding(ItemsView<Cell>.ItemsSourceProperty, "GroupedEmployees");
listView.GroupDisplayBinding = new Binding("Key");
listView.On<Android>().SetIsFastScrollEnabled(true);
```

Le `ListView.On<Android>` méthode spécifie que cette plate-forme spécifique sera exécuté uniquement sur Android. Le `ListView.SetIsFastScrollEnabled` (méthode), dans le [ `Xamarin.Forms.PlatformConfiguration.AndroidSpecific` ](https://developer.xamarin.com/api/namespace/Xamarin.Forms.PlatformConfiguration.AndroidSpecific/) espace de noms est utilisé pour activer le défilement rapide des données dans un [ `ListView` ](https://developer.xamarin.com/api/type/Xamarin.Forms.ListView/). En outre, le `SetIsFastScrollEnabled` méthode peut être utilisée pour activer/désactiver le défilement rapide en appelant le `IsFastScrollEnabled` méthode à retourner si le défilement rapide est activé :

```csharp
listView.On<Android>().SetIsFastScrollEnabled(!listView.On<Android>().IsFastScrollEnabled());
```

Le résultat est que défilement rapide des données dans un [ `ListView` ](https://developer.xamarin.com/api/type/Xamarin.Forms.ListView/) peut être activé, ce qui modifie la taille du curseur de défilement :

[![](android-images/fastscroll.png "ListView FastScroll spécifique à la plateforme")](android-images/fastscroll-large.png#lightbox "ListView FastScroll Plaform-Specific")

<a name="enable_swipe_paging" />

## <a name="enabling-swiping-between-pages-in-a-tabbedpage"></a>Activer le glissement entre les Pages dans un TabbedPage

Cette plateforme spécifique est utilisée pour activer le glissement avec un mouvement du doigt horizontal entre les pages dans un [ `TabbedPage` ](https://developer.xamarin.com/api/type/Xamarin.Forms.TabbedPage/). Elle est consommée en XAML en définissant le [ `TabbedPage.IsSwipePagingEnabled` ](https://developer.xamarin.com/api/field/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.TabbedPage.IsSwipePagingEnabledProperty/) propriété attachée un `boolean` valeur :

```xaml
<TabbedPage ...
            xmlns:android="clr-namespace:Xamarin.Forms.PlatformConfiguration.AndroidSpecific;assembly=Xamarin.Forms.Core"
            android:TabbedPage.OffscreenPageLimit="2"
            android:TabbedPage.IsSwipePagingEnabled="true">
    ...
</TabbedPage>
```

Vous pouvez également être utilisée à partir de c# à l’aide de l’API fluent :

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.AndroidSpecific;
...

On<Android>().SetOffscreenPageLimit(2)
             .SetIsSwipePagingEnabled(true);
```

Le `TabbedPage.On<Android>` méthode spécifie que cette plate-forme spécifique sera exécuté uniquement sur Android. Le [ `TabbedPage.SetIsSwipePagingEnabled` ](https://developer.xamarin.com/api/member/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.TabbedPage.SetIsSwipePagingEnabled/p/Xamarin.Forms.BindableObject/System.Boolean/) (méthode), dans le [ `Xamarin.Forms.PlatformConfiguration.AndroidSpecific` ](https://developer.xamarin.com/api/namespace/Xamarin.Forms.PlatformConfiguration.AndroidSpecific/) espace de noms est utilisée pour activer le glissement entre les pages dans un [ `TabbedPage` ](https://developer.xamarin.com/api/type/Xamarin.Forms.TabbedPage/). En outre, le `TabbedPage` classe dans le `Xamarin.Forms.PlatformConfiguration.AndroidSpecific` espace de noms comporte également un [ `EnableSwipePaging` ](https://developer.xamarin.com/api/member/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.TabbedPage.EnableSwipePaging/p/Xamarin.Forms.IPlatformElementConfiguration%7BXamarin.Forms.PlatformConfiguration.Android,Xamarin.Forms.TabbedPage%7D/) méthode qui permet cette spécifique à la plateforme, et un [ `DisableSwipePaging` ](https://developer.xamarin.com/api/member/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.TabbedPage.DisableSwipePaging/p/Xamarin.Forms.IPlatformElementConfiguration%7BXamarin.Forms.PlatformConfiguration.Android,Xamarin.Forms.TabbedPage%7D/) méthode désactive Cette plateforme spécifique. Le [ `TabbedPage.OffscreenPageLimit` ](https://developer.xamarin.com/api/field/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.TabbedPage.OffscreenPageLimitProperty/) propriété attachée, et [ `SetOffscreenPageLimit` ](https://developer.xamarin.com/api/member/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.TabbedPage.SetOffscreenPageLimit/p/Xamarin.Forms.BindableObject/System.Int32/) (méthode), sont utilisées pour définir le nombre de pages doit être conservé dans un état d’inactivité de chaque côté de la page actuelle.

Le résultat est que la pagination de balayage via les pages affichées par un [ `TabbedPage` ](https://developer.xamarin.com/api/type/Xamarin.Forms.TabbedPage/) est activé :

![](android-images/tabbedpage-swipe.png)

<a name="elevation" />

## <a name="controlling-the-elevation-of-visual-elements"></a>Contrôle de l’élévation d’éléments visuels

Cette plateforme spécifique est utilisé pour contrôler l’élévation, ou ordre de plan, des éléments visuels sur les applications qui ciblent API 21 ou version ultérieure. L’élévation d’un élément visuel détermine son ordre de dessin, avec des éléments visuels avec des valeurs Z supérieures OCCLUSION des éléments visuels avec des valeurs Z inférieure. Elle est consommée en XAML en définissant le `VisualElement.Elevation` propriété attachée un `boolean` valeur :

```xaml
<ContentPage ...
             xmlns:android="clr-namespace:Xamarin.Forms.PlatformConfiguration.AndroidSpecific;assembly=Xamarin.Forms.Core"
             Title="Elevation">
    <StackLayout>
        <Grid>
            <Button Text="Button Beneath BoxView" />
            <BoxView Color="Red" Opacity="0.2" HeightRequest="50" />
        </Grid>        
        <Grid Margin="0,20,0,0">
            <Button Text="Button Above BoxView - Click Me" android:VisualElement.Elevation="10"/>
            <BoxView Color="Red" Opacity="0.2" HeightRequest="50" />
        </Grid>
    </StackLayout>
</ContentPage>
```

Vous pouvez également être utilisée à partir de c# à l’aide de l’API fluent :

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.AndroidSpecific;
...

public class AndroidElevationPageCS : ContentPage
{
    public AndroidElevationPageCS()
    {
        ...
        var aboveButton = new Button { Text = "Button Above BoxView - Click Me" };
        aboveButton.On<Android>().SetElevation(10);

        Content = new StackLayout
        {
            Children =
            {
                new Grid
                {
                    Children =
                    {
                        new Button { Text = "Button Beneath BoxView" },
                        new BoxView { Color = Color.Red, Opacity = 0.2, HeightRequest = 50 }
                    }
                },
                new Grid
                {
                    Margin = new Thickness(0,20,0,0),
                    Children =
                    {
                        aboveButton,
                        new BoxView { Color = Color.Red, Opacity = 0.2, HeightRequest = 50 }
                    }
                }
            }
        };
    }
}
```

Le `Button.On<Android>` méthode spécifie que cette plate-forme spécifique sera exécuté uniquement sur Android. Le `VisualElement.SetElevation` (méthode), dans le [ `Xamarin.Forms.PlatformConfiguration.AndroidSpecific` ](https://developer.xamarin.com/api/namespace/Xamarin.Forms.PlatformConfiguration.AndroidSpecific/) espace de noms est utilisée pour définir l’élévation de l’élément visuel autorisant des valeurs null `float`. En outre, le `VisualElement.GetElevation` méthode peut être utilisée pour récupérer la valeur de l’élévation d’un élément visuel.

Le résultat est que l’élévation des éléments visuels peut être contrôlée afin que les éléments visuels avec des valeurs Z supérieures occlude des éléments visuels avec des valeurs Z inférieure. Par conséquent, dans cet exemple la seconde [ `Button` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Button/) est rendu au-dessus de la [ `BoxView` ](https://developer.xamarin.com/api/type/Xamarin.Forms.BoxView/) , car il possède une valeur plus élevée de l’élévation :

![](android-images/elevation.png)

<a name="disable_lifecycle_events" />

## <a name="disabling-the-disappearing-and-appearing-page-lifecycle-events"></a>Désactiver les événements de cycle de vie de Page disparition et affichage

Cette plateforme spécifique est utilisée pour désactiver la [ `Disappearing` ](https://developer.xamarin.com/api/event/Xamarin.Forms.Page.Appearing/) et [ `Appearing` ](https://developer.xamarin.com/api/event/Xamarin.Forms.Page.Appearing/) les événements de page dans l’application suspendre et reprendre la respectivement, pour les applications qui utilisent AppCompat. En outre, il inclut la possibilité de contrôler si le clavier logiciel s’affiche à la reprise, s’il a été affiché sur pause, pourvu que le mode de fonctionnement du clavier souple est défini comme [ `WindowSoftInputModeAdjust.Resize` ](https://developer.xamarin.com/api/field/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.WindowSoftInputModeAdjust.Resize/).

> [!NOTE]
> Notez que ces événements sont activés par défaut pour conserver le comportement existant pour les applications qui s’appuient sur les événements. La désactivation de ces événements rend le cycle des événements AppCompat de correspondre le cycle des événements pré-AppCompat.

Cette plateforme spécifiques peuvent être utilisées dans XAML en définissant le [ `Application.SendDisappearingEventOnPause` ](https://developer.xamarin.com/api/field/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat.Application.SendDisappearingEventOnPauseProperty/), [ `Application.SendAppearingEventOnResume` ](https://developer.xamarin.com/api/field/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat.Application.SendAppearingEventOnResumeProperty/), et [ `Application.ShouldPreserveKeyboardOnResume` ](https://developer.xamarin.com/api/field/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat.Application.ShouldPreserveKeyboardOnResumeProperty/) propriétés jointes à `boolean` valeurs :

```xaml
<Application ...
             xmlns:android="clr-namespace:Xamarin.Forms.PlatformConfiguration.AndroidSpecific;assembly=Xamarin.Forms.Core"             xmlns:androidAppCompat="clr-namespace:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat;assembly=Xamarin.Forms.Core"
             android:Application.WindowSoftInputModeAdjust="Resize"
             androidAppCompat:Application.SendDisappearingEventOnPause="false"
             androidAppCompat:Application.SendAppearingEventOnResume="false"
             androidAppCompat:Application.ShouldPreserveKeyboardOnResume="true">
  ...
</Application>
```

Vous pouvez également être utilisée à partir de c# à l’aide de l’API fluent :

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.AndroidSpecific;
using Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat;
...

Xamarin.Forms.Application.Current.On<Android>()
     .UseWindowSoftInputModeAdjust(WindowSoftInputModeAdjust.Resize)
     .SendDisappearingEventOnPause(false)
     .SendAppearingEventOnResume(false)
     .ShouldPreserveKeyboardOnResume(true);
```

Le `Application.Current.On<Android>` méthode spécifie que cette plate-forme spécifique sera exécuté uniquement sur Android. Le [ `Application.SendDisappearingEventOnPause` ](https://developer.xamarin.com/api/member/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat.Application.SendDisappearingEventOnPause/p/Xamarin.Forms.IPlatformElementConfiguration{Xamarin.Forms.PlatformConfiguration.Android,Xamarin.Forms.Application}/System.Boolean/) (méthode), dans le [ `Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat` ](https://developer.xamarin.com/api/namespace/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat/) espace de noms est utilisé pour activer ou désactiver le déclenchement de l’événement le [ `Disappearing` ](https://developer.xamarin.com/api/event/Xamarin.Forms.Page.Appearing/) les événements de page, lorsque l’application passe à l’arrière-plan. Le [ `Application.SendAppearingEventOnResume` ](https://developer.xamarin.com/api/member/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat.Application.SendAppearingEventOnResume/p/Xamarin.Forms.IPlatformElementConfiguration{Xamarin.Forms.PlatformConfiguration.Android,Xamarin.Forms.Application}/System.Boolean/) méthode est utilisée pour activer ou désactiver le déclenchement de l’événement le [ `Appearing` ](https://developer.xamarin.com/api/event/Xamarin.Forms.Page.Appearing/) des événements de page, lorsque l’application reprend à partir de l’arrière-plan. Le [ `Application.ShouldPreserveKeyboardOnResume` ](https://developer.xamarin.com/api/member/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat.Application.ShouldPreserveKeyboardOnResume/p/Xamarin.Forms.IPlatformElementConfiguration{Xamarin.Forms.PlatformConfiguration.Android,Xamarin.Forms.Application}/System.Boolean/) sert de méthode contrôle si le clavier logiciel s’affiche à la reprise, si elle était affichée sur pause, fourni que le mode de fonctionnement du clavier conditionnels a la valeur [ `WindowSoftInputModeAdjust.Resize` ](https://developer.xamarin.com/api/field/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.WindowSoftInputModeAdjust.Resize/).

Le résultat est que le [ `Disappearing` ](https://developer.xamarin.com/api/event/Xamarin.Forms.Page.Appearing/) et [ `Appearing` ](https://developer.xamarin.com/api/event/Xamarin.Forms.Page.Appearing/) les événements de page ne sont pas être déclenchés sur pause de l’application et reprendre respectivement, et que si le clavier logiciel a été affichée lorsque l’application a été suspendu, il affichera également lorsque l’application reprend :

[![](android-images/keyboard-on-resume.png "Cycle de vie des événements spécifiques à une plateforme")](android-images/keyboard-on-resume-large.png#lightbox "cycle de vie des événements spécifiques à la plateforme")

<a name="webview-mixed-content" />

## <a name="enabling-mixed-content-in-a-webview"></a>L’activation de contenu mixte dans un affichage Web

Ce contrôle spécifique à la plateforme si un [ `WebView` ](xref:Xamarin.Forms.WebView) peut afficher un contenu mixte dans les applications qui ciblent les API 21 ou supérieur. Contenu mixte est initialement chargé via une connexion HTTPS, mais qui charge des ressources (telles que des images, audio, vidéo, feuilles de style, scripts) via une connexion HTTP. Elle est consommée en XAML en définissant le [ `WebView.MixedContentMode` ](x:ref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.WebView.MixedContentModeProperty) à une valeur de propriété attachée la [ `MixedContentHandling` ](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.MixedContentHandling) énumération :

```xaml
<ContentPage ...
             xmlns:android="clr-namespace:Xamarin.Forms.PlatformConfiguration.AndroidSpecific;assembly=Xamarin.Forms.Core">
    <WebView ... android:WebView.MixedContentMode="AlwaysAllow" />
</ContentPage>
```

Vous pouvez également être utilisée à partir de c# à l’aide de l’API fluent :

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.AndroidSpecific;
...

webView.On<Android>().SetMixedContentMode(MixedContentHandling.AlwaysAllow);
```

Le `WebView.On<Android>` méthode spécifie que cette plate-forme spécifique sera exécuté uniquement sur Android. Le [ `WebView.SetMixedContentMode` ](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.WebView.SetMixedContentMode(Xamarin.Forms.IPlatformElementConfiguration{Xamarin.Forms.PlatformConfiguration.Android,Xamarin.Forms.WebView},Xamarin.Forms.PlatformConfiguration.AndroidSpecific.MixedContentHandling)) (méthode), dans le [ `Xamarin.Forms.PlatformConfiguration.AndroidSpecific` ](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific) espace de noms est utilisée pour déterminer si un contenu mixte peut être affiché, avec la [ `MixedContentHandling` ](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.MixedContentHandling) énumération en fournissant trois valeurs possibles :

- [`AlwaysAllow`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.MixedContentHandling.AlwaysAllow) – Indique que le [ `WebView` ](xref:Xamarin.Forms.WebView) permettra une origine HTTPS charger le contenu à partir d’une origine HTTP.
- [`NeverAllow`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.MixedContentHandling.NeverAllow) – Indique que le [ `WebView` ](xref:Xamarin.Forms.WebView) n’autorise pas une origine HTTPS charger le contenu à partir d’une origine HTTP.
- [`CompatibilityMode`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.MixedContentHandling.CompatibilityMode) – Indique que le [ `WebView` ](xref:Xamarin.Forms.WebView) tentera d’être compatible avec l’approche de la dernière version du navigateur web appareil. Un contenu HTTP peut être chargée par une origine HTTPS et d’autres types de contenu seront bloqués. Les types de contenu qui sont bloqués ou autorisés peuvent changer à chaque version de système d’exploitation.

Le résultat qui est spécifié [ `MixedContentHandling` ](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.MixedContentHandling) valeur est appliquée à la [ `WebView` ](xref:Xamarin.Forms.WebView), qui contrôle si le contenu mixte peut s’afficher :

[![WebView mixte de gestion de contenu spécifique à la plateforme](android-images/webview-mixedcontent.png "WebView mixte de gestion de contenu spécifique à la plateforme")](android-images/webview-mixedcontent-large.png#lightbox "WebView mixte de gestion de contenu spécifique à la plateforme")

<a name="entry-imeoptions" />

## <a name="setting-entry-input-method-editor-options"></a>Options de l’entrée de paramètre d’éditeur de méthode

Cette plate-forme spécifique définit la méthode d’entrée des options de l’éditeur pour le clavier logiciel pour un [ `Entry` ](xref:Xamarin.Forms.Entry). Cela inclut la définition de bouton d’action de l’utilisateur dans le coin inférieur du clavier logiciel et les interactions avec le `Entry`. Elle est consommée en XAML en définissant le [ `Entry.ImeOptions` ](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.Entry.ImeOptionsProperty) à une valeur de propriété attachée la [ `ImeFlags` ](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.ImeFlags) énumération :

```xaml
<ContentPage ...
             xmlns:android="clr-namespace:Xamarin.Forms.PlatformConfiguration.AndroidSpecific;assembly=Xamarin.Forms.Core">
    <StackLayout ...>
        <Entry ... android:Entry.ImeOptions="Send" />
        ...
    </StackLayout>
</ContentPage>
```

Vous pouvez également être utilisée à partir de c# à l’aide de l’API fluent :

```csharp
using Xamarin.Forms.PlatformConfiguration;
using Xamarin.Forms.PlatformConfiguration.AndroidSpecific;
...

entry.On<Android>().SetImeOptions(ImeFlags.Send);
```

Le `Entry.On<Android>` méthode spécifie que cette plate-forme spécifique sera exécuté uniquement sur Android. Le [ `Entry.SetImeOptions` ](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.Entry.SetImeOptions(Xamarin.Forms.IPlatformElementConfiguration{Xamarin.Forms.PlatformConfiguration.Android,Xamarin.Forms.Entry},Xamarin.Forms.PlatformConfiguration.AndroidSpecific.ImeFlags)) (méthode), dans le [ `Xamarin.Forms.PlatformConfiguration.AndroidSpecific` ](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific) espace de noms est utilisé pour définir l’option d’action de méthode d’entrée pour le clavier logiciel pour le [ `Entry` ](xref:Xamarin.Forms.Entry), avec la [ `ImeFlags` ](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.ImeFlags) énumération fournissant les valeurs suivantes :

- [`Default`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.ImeFlags.Default) : indique qu’aucune action spécifique de clé est requise et que le contrôle sous-jacent génère ses propres si c’est possible.
- [`None`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.ImeFlags.None) : indique qu’aucune clé d’action ne sera disponible.
- [`Go`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.ImeFlags.Go) : indique que la clé d’action effectue une opération « go », en prenant l’utilisateur à la cible du texte tapé.
- [`Search`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.ImeFlags.Search) : indique que la clé d’action effectue une opération de « recherche », en prenant l’utilisateur pour les résultats de recherche pour le texte qu’ils ont entrées.
- [`Send`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.ImeFlags.Send) : indique que la clé d’action effectue une opération « Envoyer », de fournir le texte à sa cible.
- [`Next`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.ImeFlags.Next) : indique que la clé d’action effectue une opération « suivante », en prenant l’utilisateur dans le champ suivant qui accepte le texte.
- [`Done`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.ImeFlags.Done) : indique que la clé d’action effectue une opération « terminée », en fermant le clavier logiciel.
- [`Previous`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.ImeFlags.Previous) : indique que la clé d’action effectue une opération « précédente », l’utilisateur être redirigé vers le champ précédent qui accepte le texte.
- [`ImeMaskAction`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.ImeFlags.ImeMaskAction) – le masque pour sélectionner les options d’action.
- [`NoPersonalizedLearning`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.ImeFlags.NoPersonalizedLearning) – Indique que le vérificateur d’orthographe sera en savoir plus à partir de l’utilisateur, ni suggérer selon ce que l’utilisateur a précédemment tapé.
- [`NoFullscreen`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.ImeFlags.NoFullscreen) – Indique que l’interface utilisateur ne doit pas s’en plein écran.
- [`NoExtractUi`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.ImeFlags.NoExtractUi) : indique qu’aucune interface utilisateur ne doivent être affichée pour le texte extrait.
- [`NoAccessoryAction`](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.ImeFlags.NoAccessoryAction) : indique qu’aucune interface utilisateur ne s’affichera pour les actions personnalisées.

Le résultat qui est spécifié [ `ImeFlags` ](xref:Xamarin.Forms.PlatformConfiguration.AndroidSpecific.ImeFlags) valeur est appliquée pour le clavier logiciel pour le [ `Entry` ](xref:Xamarin.Forms.Entry), qui définit la méthode d’entrée, options de l’éditeur :

[![Méthode éditeur spécifique à la plateforme d’entrée l’entrée](android-images/entry-imeoptions.png "méthode éditeur spécifique à la plateforme d’entrée l’entrée")](android-images/entry-imeoptions-large.png#lightbox "entrée d’entrée de méthode éditeur spécifique à la plateforme")

## <a name="summary"></a>Récapitulatif

Cet article vous a montré comment consommer les spécificités de plate-forme Android qui sont intégrées dans Xamarin.Forms. Caractéristiques de la plateforme vous permettent de vous permet d’utiliser la fonctionnalité est disponible uniquement sur une plateforme spécifique, sans avoir à implémenter des convertisseurs personnalisés ou les effets.

## <a name="related-links"></a>Liens associés

- [Création de caractéristiques de la plateforme](~/xamarin-forms/platform/platform-specifics/creating.md)
- [PlatformSpecifics (exemple)](https://developer.xamarin.com/samples/xamarin-forms/userinterface/platformspecifics/)
- [AndroidSpecific](https://developer.xamarin.com/api/namespace/Xamarin.Forms.PlatformConfiguration.AndroidSpecific/)
- [AndroidSpecific.AppCompat](https://developer.xamarin.com/api/namespace/Xamarin.Forms.PlatformConfiguration.AndroidSpecific.AppCompat/)
