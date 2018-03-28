---
title: "Conectarse a Adobe Analytics en Power BI Desktop (versión preliminar)"
description: "Use y conéctese fácilmente a Adobe Analytics en Power BI Desktop"
services: powerbi
documentationcenter: 
author: davidiseminger
manager: kfile
backup: 
editor: 
tags: 
qualityfocus: no
qualitydate: 
ms.service: powerbi
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/09/2018
ms.author: davidi
LocalizationGroup: Connect to data
ms.openlocfilehash: efd6d066e2f98f86248730917c2f4aa0c8a39983
ms.sourcegitcommit: 4217430c3419046c3a90819c34f133ec7905b6e7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2018
---
# <a name="connect-to-adobe-analytics-in-power-bi-desktop-preview"></a>Conectarse a Adobe Analytics en Power BI Desktop (versión preliminar)
En **Power BI Desktop** puede conectarse a **Adobe Analytics** y usar los datos subyacentes igual que cualquier otro origen de datos en Power BI Desktop. 

![Obtener datos de Adobe Analytics](media/desktop-connect-adobe-analytics/connect-adobe-analytics_01.png)

## <a name="enable-the-adobe-analytics-connector-preview"></a>Habilitar la versión preliminar del conector de Adobe Analytics 
Como el conector de **Adobe Analytics** está en versión preliminar, debe habilitar la característica de versión preliminar para que el conector esté disponible en la ventana **Obtener datos**. Para habilitar la versión preliminar del conector, seleccione **Archivo > Opciones y configuración > Opciones > Características de versión preliminar** en Power BI Desktop y, después, marque la casilla situada junto a **Marcadores**. 

![Habilitar la versión preliminar del conector de Adobe Analytics en Opciones](media/desktop-connect-adobe-analytics/connect-adobe-analytics_02.png)

Deberá reiniciar **Power BI Desktop** después de realizar la selección para habilitar la versión preliminar del conector de Adobe Analytics.

## <a name="connect-to-adobe-analytics-data"></a>Conectarse a los datos de Adobe Analytics
Para conectarse a datos de **Adobe Analytics**, seleccione **Obtener datos** en la cinta **Inicio** de Power BI Desktop. Seleccione **Servicios en línea** en las categorías de la izquierda y verá **Conector de Adobe Analytics**.

![Obtener datos de Adobe Analytics](media/desktop-connect-adobe-analytics/connect-adobe-analytics_01.png)

En la ventana de **Adobe Analytics** que aparecerá, haga clic en el botón **Iniciar sesión** y proporcione sus credenciales para iniciar sesión en su cuenta de Adobe Analytics. Aparecerá la ventana de inicio de sesión de Adobe, como se muestra en la siguiente imagen.

![Iniciar sesión en Adobe Analytics](media/desktop-connect-adobe-analytics/connect-adobe-analytics_03.png)

Cuando se le pida, escriba su nombre de usuario y contraseña. Una vez establecida la conexión, puede seleccionar varias dimensiones y medidas y obtener una vista previa de ellas en el cuadro de diálogo **Navegador** de Power BI para crear una salida tabular. También puede proporcionar los parámetros de entrada necesarios para los elementos seleccionados. 

![Seleccionar datos con el navegador](media/desktop-connect-adobe-analytics/connect-adobe-analytics_04.png)

Puede **Cargar** la tabla seleccionada, que muestra la tabla completa en **Power BI Desktop**, o bien puede **Editar** la consulta, que abre **Editor de consultas** para que pueda filtrar y refinar el conjunto de datos que desea utilizar y, a continuación, cargar ese conjunto de datos refinado en **Power BI Desktop**.

![Cargar o editar datos en el navegador](media/desktop-connect-adobe-analytics/connect-adobe-analytics_05.png)


## <a name="next-steps"></a>Pasos siguientes
Hay todo tipo de datos a los que puede conectarse con Power BI Desktop. Para obtener más información sobre orígenes de datos, consulte los siguientes recursos:

* [Introducción a Power BI Desktop](desktop-getting-started.md)
* [Orígenes de datos en Power BI Desktop](desktop-data-sources.md)
* [Combinar datos y darles forma con Power BI Desktop](desktop-shape-and-combine-data.md)
* [Connect to Excel workbooks in Power BI Desktop (Conectarse a libros de Excel en Power BI Desktop)](desktop-connect-excel.md)   
* [Especificar datos directamente en Power BI Desktop](desktop-enter-data-directly-into-desktop.md)   
