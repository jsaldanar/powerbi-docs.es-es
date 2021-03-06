---
author: davidiseminger
ms.service: powerbi
ms.topic: include
ms.date: 01/31/2020
ms.author: davidi
ms.openlocfilehash: 912b0213c328c623e7881f7f30fe7d67f6d889b3
ms.sourcegitcommit: 0e9e211082eca7fd939803e0cd9c6b114af2f90a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/13/2020
ms.locfileid: "83274655"
---
## <a name="limitations"></a>Limitaciones

Las limitaciones actuales para la seguridad de nivel de fila en los modelos en la nube son las siguientes:

* Si anteriormente definió roles y reglas en el servicio Power BI, debe volver a crearlos en Power BI Desktop.

* Solo puede definir RLS en los conjuntos de datos creados con Power BI Desktop. Si quiere habilitar RLS para conjuntos de datos creados con Excel, debe convertir primero los archivos en archivos de Power BI Desktop (PBIX). [Más información](../connect-data/desktop-import-excel-workbooks.md)

* Solo se admiten conexiones de importación y de DirectQuery. Las conexiones dinámicas con Analysis Services se controlan en el modelo local.

## <a name="known-issues"></a>Problemas conocidos

Hay un problema conocido en el que se produce un mensaje de error al intentar publicar un informe publicado anteriormente desde Power BI Desktop. El escenario es el siguiente:

1. Ana tiene un conjunto de datos publicado en el servicio Power BI y ha configurado RLS.

1. Ana actualiza el informe en Power BI Desktop y vuelve a publicarlo.

1. Ana recibe un error.

**Solución alternativa:** vuelva a publicar el archivo de Power BI Desktop desde el servicio Power BI hasta que se solucione este problema. Para ello, seleccione **Obtener datos** > **Archivos**.

