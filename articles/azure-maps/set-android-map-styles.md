---
title: Definir um estilo de mapa usando o Azure Maps SDK do Android | Mapas do Microsoft Azure
description: Neste artigo, você aprenderá sobre as funcionalidades relacionadas ao estilo do Microsoft Azure Maps para o SDK do Android.
author: farah-alyasari
ms.author: v-faalya
ms.date: 04/26/2019
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: philmea
ms.openlocfilehash: 96564a89a2b64203eef913b0d8300f0dafa332c5
ms.sourcegitcommit: 2823677304c10763c21bcb047df90f86339e476a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2020
ms.locfileid: "77209572"
---
# <a name="set-map-style-using-azure-maps-android-sdk"></a>Definir o estilo de mapa usando o Azure Maps SDK do Android

Este artigo mostra duas maneiras de definir estilos de mapa usando o SDK do Android do Azure Maps. O mapas do Azure tem seis estilos de mapas diferentes para escolher. Para obter mais informações sobre os estilos de mapa com suporte, consulte [estilos de mapa com suporte no mapas do Azure](./supported-map-styles.md).


## <a name="prerequisites"></a>Prerequisites

Para concluir o processo neste artigo, você precisa instalar o [Azure Maps SDK do Android](https://docs.microsoft.com/azure/azure-maps/how-to-use-android-map-control-library) para carregar um mapa.


## <a name="set-map-style-in-the-layout"></a>Definir o estilo de mapa no layout

Você pode definir um estilo de mapa no arquivo de layout para sua classe de atividade. Edite o **layout de > res > activity_main. xml**, portanto, é semelhante ao seguinte:

```XML
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    >

    <com.microsoft.azure.maps.mapcontrol.MapControl
        android:id="@+id/mapcontrol"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:mapcontrol_centerLat="47.602806"
        app:mapcontrol_centerLng="-122.329330"
        app:mapcontrol_zoom="12"
        app:mapcontrol_style="grayscale_dark"
        />

</FrameLayout>
```

O atributo `mapcontrol_style` acima define o estilo de mapa como **grayscale_dark**. 

<center>

estilo de ![-grayscale_dark](./media/set-android-map-styles/grayscale-dark.png)</center>

## <a name="set-map-style-in-the-activity-class"></a>Definir o estilo de mapa na classe de atividade

O estilo de mapa pode ser definido na classe de atividade. Copie o trecho de código a seguir para o método **OnCreate ()** da sua classe `MainActivity.java`. Esse código definirá o estilo de mapa como **satellite_road_labels**.

```Java
mapControl.onReady(map -> {
    //Set the camera of the map.
    map.setCamera(center(47.64, -122.33), zoom(14));

    //Set the style of the map.
    map.setStyle(style(MapStyle.SATELLITE));
});
```

<center>

estilo de ![-satélite-Road-Labels](./media/set-android-map-styles/satellite-road-labels.png)</center>