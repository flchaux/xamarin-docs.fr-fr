---
title: La vérification de l’Orientation de périphérique
description: Permet de DependencyService accès orientation du périphérique à partir de code partagé
ms.prod: xamarin
ms.assetid: 5F60975F-47DB-4361-B97C-2290D6F77D2F
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 08/09/2016
ms.openlocfilehash: 09cd92b436be97f5490ac74890e4b0723bcd5701
ms.sourcegitcommit: 1561c8022c3585655229a869d9ef3510bf83f00a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2018
---
# <a name="checking-device-orientation"></a>La vérification de l’Orientation de périphérique

Cet article vous aidera à utiliser [ `DependencyService` ](https://developer.xamarin.com/api/type/Xamarin.Forms.DependencyService/) pour vérifier l’orientation du périphérique à partir du code partagé à l’aide des API natives sur chaque plateforme. Cette procédure pas à pas est basée sur le serveur existant `DeviceOrientation` plug-in par Ali Özgür. Consultez le [référentiel GitHub](https://github.com/aliozgur/Xamarin.Plugins/tree/master/DeviceOrientation) pour plus d’informations.

- **[Création de l’Interface](#Creating_the_Interface)**  &ndash; comprendre comment l’interface est créée dans le code partagé.
- **[iOS implémentation](#iOS_Implementation)**  &ndash; apprendre à implémenter l’interface en code natif pour iOS.
- **[Implémentation Android](#Android_Implementation)**  &ndash; apprendre à implémenter l’interface en code natif pour Android.
- **[Implémentation de la plateforme Windows universelle](#WindowsImplementation)**  &ndash; apprendre à implémenter l’interface en code natif pour la plateforme Windows universelle (UWP).
- **[Mise en œuvre dans le Code partagé](#Implementing_in_Shared_Code)**  &ndash; apprendre à utiliser `DependencyService` pour appeler l’implémentation native à partir de code partagé.

L’application à l’aide `DependencyService` aura la structure suivante :

![](device-orientation-images/orientation-diagram.png "Structure de l’Application DependencyService")

> [!NOTE]
> Il est possible de détecter si l’appareil est en orientation portrait ou paysage dans le code partagé, comme illustré dans [appareil Orientation]/guides/xamarin-forms/user-interface/layouts/device-orientation/#changes-in-orientation). La méthode décrite dans cet article utilise des fonctionnalités natives pour obtenir plus d’informations, notamment si l’appareil est inversé.

<a name="Creating_the_Interface" />

## <a name="creating-the-interface"></a>Création de l'interface utilisateur

Tout d’abord, créez une interface dans le code partagé qui exprime la fonctionnalité que vous souhaitez mettre en œuvre. Pour cet exemple, l’interface contient une méthode unique :

```csharp
namespace DependencyServiceSample.Abstractions
{
    public enum DeviceOrientations
    {
        Undefined,
        Landscape,
        Portrait
    }

    public interface IDeviceOrientation
    {
        DeviceOrientations GetOrientation();
    }
}
```

Codage de cette interface dans le code partagé permettent à l’application de Xamarin.Forms accéder à l’orientation du périphérique API sur chaque plateforme.

> [!NOTE]
> Classes implémentant l’interface doivent avoir un constructeur sans paramètre pour travailler avec les `DependencyService`.

<a name="iOS_Implementation" />

## <a name="ios-implementation"></a>Implémentation d’iOS

L’Interface doit être implémentée dans chaque projet d’application de plateforme spécifique. Notez que la classe a un constructeur sans paramètre afin que la `DependencyService` peut créer des instances :

```csharp
using UIKit;
using Foundation;

namespace DependencyServiceSample.iOS
{
    public class DeviceOrientationImplementation : IDeviceOrientation
    {
        public DeviceOrientationImplementation(){ }

        public DeviceOrientations GetOrientation()
        {
            var currentOrientation = UIApplication.SharedApplication.StatusBarOrientation;
            bool isPortrait = currentOrientation == UIInterfaceOrientation.Portrait
                || currentOrientation == UIInterfaceOrientation.PortraitUpsideDown;

            return isPortrait ? DeviceOrientations.Portrait: DeviceOrientations.Landscape;
        }
    }
}
```

Enfin, ajoutez ceci `[assembly]` attribut au-dessus de la classe (et en dehors des espaces de noms qui ont été définies), y compris tout `using` instructions :

```csharp
using UIKit;
using Foundation;
using DependencyServiceSample.iOS; //enables registration outside of namespace

[assembly: Xamarin.Forms.Dependency (typeof (DeviceOrientationImplementation))]
namespace DependencyServiceSample.iOS {
    ...
```

Cet attribut enregistre la classe en tant qu’implémentation de la `IDeviceOrientation` Interface, ce qui signifie que `DependencyService.Get<IDeviceOrientation>` peut être utilisé dans le code partagé pour créer une instance de celui-ci.

<a name="Android_Implementation" />

## <a name="android-implementation"></a>Implémentation Android

Le code suivant implémente `IDeviceOrientation` sur Android :

```csharp
using DependencyServiceSample.Droid;
using Android.Hardware;

namespace DependencyServiceSample.Droid
{
    public class DeviceOrientationImplementation : IDeviceOrientation
    {
        public DeviceOrientationImplementation() { }

        public static void Init() { }

        public DeviceOrientations GetOrientation()
        {
            IWindowManager windowManager = Android.App.Application.Context.GetSystemService(Context.WindowService).JavaCast<IWindowManager>();

            var rotation = windowManager.DefaultDisplay.Rotation;
            bool isLandscape = rotation == SurfaceOrientation.Rotation90 || rotation == SurfaceOrientation.Rotation270;
            return isLandscape ? DeviceOrientations.Landscape : DeviceOrientations.Portrait;
        }
    }
}
```

Ajoutez ceci `[assembly]` attribut au-dessus de la classe (et en dehors des espaces de noms qui ont été définies), y compris tout `using` instructions :

```csharp
using DependencyServiceSample.Droid; //enables registration outside of namespace
using Android.Hardware;

[assembly: Xamarin.Forms.Dependency (typeof (DeviceOrientationImplementation))]
namespace DependencyServiceSample.Droid {
    ...
```

Cet attribut enregistre la classe en tant qu’implémentation de la `IDeviceOrientaiton` Interface, ce qui signifie que `DependencyService.Get<IDeviceOrientation>` peut être utilisé dans le code partagé peut créer une instance de celui-ci.

<a name="WindowsImplementation" />

## <a name="universal-windows-platform-implementation"></a>Mise en œuvre de la plateforme Windows universelle

Le code suivant implémente la `IDeviceOrientation` interface sur la plateforme Windows universelle :

```csharp
namespace DependencyServiceSample.WindowsPhone
{
    public class DeviceOrientationImplementation : IDeviceOrientation
    {
        public DeviceOrientationImplementation() { }

        public DeviceOrientations GetOrientation()
        {
            var orientation = Windows.UI.ViewManagement.ApplicationView.GetForCurrentView().Orientation;
            if (orientation == Windows.UI.ViewManagement.ApplicationViewOrientation.Landscape) {
                return DeviceOrientations.Landscape;
            }
            else {
                return DeviceOrientations.Portrait;
            }
        }
    }
}
```

Ajouter le `[assembly]` attribut au-dessus de la classe (et en dehors des espaces de noms qui ont été définies), y compris tout `using` instructions :

```csharp
using DependencyServiceSample.WindowsPhone; //enables registration outside of namespace

[assembly: Dependency(typeof(DeviceOrientationImplementation))]
namespace DependencyServiceSample.WindowsPhone {
    ...
```

Cet attribut enregistre la classe en tant qu’implémentation de la `DeviceOrientationImplementation` Interface, ce qui signifie que `DependencyService.Get<IDeviceOrientation>` peut être utilisé dans le code partagé peut créer une instance de celui-ci.

<a name="Implementing_in_Shared_Code" />

## <a name="implementing-in-shared-code"></a>Mise en œuvre dans le Code partagé

Maintenant nous pouvons écrire et tester le code partagé qui accède à la `IDeviceOrientation` interface. Cette page simple inclut un bouton qui met à jour son propre texte selon l’orientation du périphérique. Elle utilise le `DependencyService` pour obtenir une instance de la `IDeviceOrientation` interface &ndash; lors de l’exécution, cette instance correspond à l’implémentation spécifique à la plateforme qui a un accès complet pour le Kit de développement natif :

```csharp
public MainPage ()
{
    var orient = new Button {
        Text = "Get Orientation",
        VerticalOptions = LayoutOptions.CenterAndExpand,
        HorizontalOptions = LayoutOptions.CenterAndExpand,
    };
    orient.Clicked += (sender, e) => {
       var orientation = DependencyService.Get<IDeviceOrientation>().GetOrientation();
       switch(orientation){
           case DeviceOrientations.Undefined:
                orient.Text = "Undefined";
                break;
           case DeviceOrientations.Landscape:
                orient.Text = "Landscape";
                break;
           case DeviceOrientations.Portrait:
                orient.Text = "Portrait";
                break;
       }
    };
    Content = orient;
}
```

Cette application en cours d’exécution sur les plateformes Windows, Android ou iOS et en appuyant sur le bouton entraînera le texte du bouton mise à jour avec l’orientation du périphérique.

![](device-orientation-images/orientation.png "Exemple de l’Orientation de périphérique")


## <a name="related-links"></a>Liens associés

- [À l’aide de DependencyService (exemple)](https://developer.xamarin.com/samples/UsingDependencyService)
- [DependencyService (exemple)](https://developer.xamarin.com/samples/DependencyService/DependencyServiceSample/)
- [Exemples Xamarin.Forms](https://github.com/xamarin/xamarin-forms-samples)
