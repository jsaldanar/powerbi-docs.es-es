---
title: Personalización de objetos visuales en un informe
description: Cree su propia vista de un informe, sin modificarlo.
author: mihart
ms.author: mihart
ms.reviewer: mihart
ms.service: powerbi
ms.subservice: pbi-explore
ms.topic: how-to
ms.date: 10/13/2020
LocalizationGroup: Reports
ms.openlocfilehash: aa94908c8601052c9cb8ac7cd4a6c0e895afeff6
ms.sourcegitcommit: 653e18d7041d3dd1cf7a38010372366975a98eae
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2020
ms.locfileid: "96390159"
---
# <a name="personalize-visuals-in-a-report"></a>Personalización de objetos visuales en un informe

[!INCLUDE[consumer-appliesto-ynny](../includes/consumer-appliesto-ynny.md)]

Es difícil crear un solo objeto visual que satisfaga los requisitos de todos. Sin embargo, cuando un colega comparte un informe con usted, puede que desee realizar cambios en los objetos visuales, y no tener que pedirle que realice los cambios. 

Es posible que quiera cambiar lo que hay en el eje, modificar el tipo de objeto visual o agregar algo a la información sobre herramientas. Con la característica **Personalizar este objeto visual**, realice los cambios y, cuando tenga el objeto visual de la forma que desee, guárdelo como un [marcador](end-user-bookmarks.md) para tenerlo bien a mano. Ni siquiera necesita permiso de edición para el informe.

:::image type="content" source="media/end-user-personalize-visuals/power-bi-personalize.png" alt-text="Personalizar un objeto visual":::
 
## <a name="what-you-can-change"></a>Qué se puede cambiar

Esta característica ayuda a obtener información adicional a través de la exploración ad hoc de objetos visuales en un informe de Power BI. Estas son algunas de las modificaciones que puede realizar. Las opciones disponibles varían según el tipo de objeto visual. 

- Cambiar el tipo de visualización
- Intercambiar una medida o una dimensión
- Agregar o quitar una leyenda
- Comparar dos o más medidas
- Cambiar agregaciones, etc.

Esta característica no solo incorpora nuevas funcionalidades de exploración, sino que también permite capturar y compartir los cambios:

- Capturar los cambios
- Compartir los cambios
- Restablecer todos los cambios de un informe
- Restablecer todos los cambios de un objeto visual
- Borrar los cambios recientes

> [!IMPORTANT]
> La capacidad de personalizar un objeto visual debe habilitarla el *diseñador* del informe. Si no ve el icono **Personalizar este objeto visual** ![Personalize this visual icon](media/end-user-personalize-visuals/power-bi-personalize-visual-icon.png), el diseñador de informes no ha habilitado esta característica para el informe actual. Compruebe con el propietario del informe o con el administrador de Power BI que tiene habilitada la característica. Para mostrar la información de contacto del propietario del informe, seleccione el nombre del informe en la barra de menús de Power BI.

## <a name="personalize-visuals-in-the-power-bi-service"></a>Personalizar objetos visuales en el servicio Power BI

Al personalizar un objeto visual, puede explorar los datos de muchas maneras sin tener que salir de la [vista de lectura del informe](end-user-reading-view.md). En estos ejemplos se muestran las distintas formas en las que puede modificar una visualización para satisfacer sus necesidades. 

1. Abra un informe en la vista de lectura en el servicio Power BI.

2. En la barra de menús del objeto visual, seleccione el icono de **Personalizar este objeto visual** ![icono de Personalizar este objeto visual](media/end-user-personalize-visuals/power-bi-personalize-visual-icon.png). 

### <a name="change-the-visualization-type"></a>Cambiar el tipo de visualización

¿Cree que los datos se mostrarían mejor como un gráfico de columnas apiladas? Cambie el **tipo de visualización**.

:::image type="content" source="media/end-user-personalize-visuals/power-bi-personalize-change-visual-type.png" alt-text="Cambiar el tipo de visualización":::
 
### <a name="swap-out-a-measure-or-dimension"></a>Intercambiar una medida o una dimensión
Reemplace el campo que se está usando para el eje X seleccionando el campo que desee reemplazar y, a continuación, eligiendo otro.

:::image type="content" source="media/end-user-personalize-visuals/power-bi-personalize-change-axis.png" alt-text="Cambiar el eje":::
 
### <a name="add-or-remove-a-legend"></a>Agregar o quitar una leyenda
Al agregar una leyenda, puede codificar por colores un objeto visual según una categoría. En este ejemplo, la codificación de colores se basa en el nombre de la compañía. 

:::image type="content" source="media/end-user-personalize-visuals/power-bi-personalize-change-legend.png" alt-text="Agregar o quitar la leyenda":::

### <a name="change-the-placement-of-fields"></a>Cambio de la ubicación de los campos

Al arrastrar y colocar, puede cambiar la posición de los campos dentro de la misma propiedad del objeto visual o incluso en distintas propiedades de objetos visuales. Por ejemplo, puede mover rápidamente un campo en la leyenda al eje de un objeto visual.

:::image type="content" source="media/end-user-personalize-visuals/personalize-drag-and-drop.png" alt-text="Captura de pantalla del arrastre de un campo en un objeto visual.":::

También puede cambiar rápidamente el orden de las columnas de una tabla o matriz.

:::image type="content" source="media/end-user-personalize-visuals/personalize-reorder-columns.png" alt-text="Captura de pantalla de la reordenación de columnas en una tabla.":::

### <a name="compare-two-or-more-different-measures"></a>Comparar dos o más medidas diferentes
Compare y contraste los valores de distintas medidas mediante el icono + para agregar varias medidas para un objeto visual. Para quitar una medida, seleccione **Más opciones (...)** y elija **Quitar campo**.

:::image type="content" source="media/end-user-personalize-visuals/power-bi-personalize-compare-measures.png" alt-text="Comparar medidas":::

### <a name="change-aggregations"></a>Cambiar agregaciones
Puede cambiar el modo en que se calcula una medida modificando la agregación en el panel **Personalizar**. Seleccione **Más opciones (...)** y elija la agregación que se va a usar.

:::image type="content" source="media/end-user-personalize-visuals/power-bi-personalize-change-aggregation.png" alt-text="Cambiar agregaciones":::

### <a name="capture-changes"></a>Capturar cambios 
Use marcadores personales para capturar los cambios, para que pueda volver a la vista personalizada. Seleccione **Marcadores** > **Marcadores personales** y asigne un nombre al marcador. 

:::image type="content" source="media/end-user-personalize-visuals/power-bi-personalize-bookmark.png" alt-text="Crear un marcador":::
 
También puede convertir el marcador en la vista predeterminada.

### <a name="share-changes"></a>Compartir cambios 
Si tiene permisos para leer y volver a compartir, cuando comparta el informe podrá elegir incluir los cambios.

:::image type="content" source="media/end-user-personalize-visuals/power-bi-personalize-share-changes.png" alt-text="Compartir cambios":::
 
### <a name="reset-all-your-changes-to-a-report"></a>Restablecer todos los cambios en un informe

En la esquina superior derecha del lienzo del informe, seleccione **Restablecer valores predeterminados**. Esta acción quitará todos los cambios de dicho informe y lo restablecerá a la última vista que guardó el autor del informe.

:::image type="content" source="media/end-user-personalize-visuals/power-bi-personalize-reset-all.png" alt-text="Restablecer todos los cambios":::
 
### <a name="reset-all-your-changes-to-a-visual"></a>Restablecer todos los cambios en un objeto visual

En la barra de menús del objeto visual, seleccione **Restablecer este objeto visual** para quitar todos los cambios de un determinado objeto visual y volver a establecerlo en la última vista que guardó el autor de ese objeto visual.

:::image type="content" source="media/end-user-personalize-visuals/power-bi-personalize-reset-visual.png" alt-text="Restablecer todos los cambios del objeto visual":::
 
### <a name="clear-recent-changes"></a>Borrar cambios recientes

Seleccione el icono de borrador para borrar todos los cambios recientes realizados desde que abrió el panel **Personalizar**.  

:::image type="content" source="media/end-user-personalize-visuals/power-bi-personalize-revert-changes.png" alt-text="Revertir cambios recientes":::

## <a name="limitations"></a>Limitaciones

Actualmente, la característica tiene algunas limitaciones que se deben tener en cuenta.

- **Personalizar este objeto visual** se puede desactivar para un informe entero o para un determinado objeto visual. Si no tiene una opción para personalizar un objeto visual, póngase en contacto con el administrador de Power BI o el propietario del informe. Para mostrar la información de contacto del propietario del informe, seleccione el nombre del informe en la barra de menús de Power BI.
- Las exploraciones de los usuarios no se conservan automáticamente. Debe guardar la vista como un marcador personal para capturar los cambios.
- Esta característica se admite en las aplicaciones móviles de Power BI para tabletas iOS y Android, así como en su versión para Windows; no se admite en las aplicaciones móviles de Power BI para teléfonos. Pero cualquier cambio en un objeto visual que guarde en un marcador personal mientras se encuentre en el servicio Power BI se respetará en todas las aplicaciones móviles de Power BI.

## <a name="next-steps"></a>Pasos siguientes
[Copiar un objeto visual del informe como una imagen estática](../visuals/power-bi-visualization-copy-paste.md)    
¿Tiene más preguntas? [Pruebe la comunidad de Power BI](https://community.powerbi.com/)
