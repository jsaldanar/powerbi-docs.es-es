---
title: API de almacenamiento local en objetos visuales de Power BI
description: En el artículo se describe cómo usar la API de objetos visuales de Power BI para obtener acceso al almacenamiento local del explorador
author: KesemSharabi
ms.author: kesharab
ms.reviewer: rkarlin
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: reference
ms.date: 01/21/2019
ms.openlocfilehash: e2cb11ea9be85916e6b5557e7933f6a6b5a7159a
ms.sourcegitcommit: 7aa0136f93f88516f97ddd8031ccac5d07863b92
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "79380603"
---
# <a name="local-storage-api"></a>API de almacenamiento local

Cualquier objeto visual personalizado puede usar la API de almacenamiento local para solicitar al host que guarde o cargue datos desde el almacenamiento del dispositivo. Está aislada en el sentido de que hay una separación del almacenamiento entre los distintos tipos de objetos visuales.

## <a name="sample"></a>Ejemplo

Si el objeto visual personalizado debe aumentar un contador cada vez que se llama al método de actualización, pero el valor del contador también debe conservarse y no restablecerse cada vez que se inicia un objeto visual:

```typescript
export class Visual implements IVisual {
        // ...
        private updateCountName: string = 'updateCount';
        private updateCount: number;
        private storage: ILocalVisualStorageService;
        // ...

        constructor(options: VisualConstructorOptions) {
            // ...
            this.storage = options.host.storageService;
            // ...

            this.storage.get(this.updateCountName).then(count =>
            {
                this.updateCount = +count;
            })
            .catch(() =>
            {
                this.updateCount = 0;
                this.storage.set(this.updateCountName, this.updateCount.toString());
            });
            // ...
        }

        public update(options: VisualUpdateOptions) {
            // ...
            this.updateCount++;
            this.storage.set(this.updateCountName, this.updateCount.toString());
            // ...
        }
}
```

## <a name="known-limitations-and-issues"></a>Problemas y limitaciones conocidos

La API de almacenamiento local no está activada de forma predeterminada para los objetos visuales de Power BI. Si quiere activarla para un objeto visual de Power BI, envíe una solicitud al equipo de soporte técnico de objetos visuales de Power BI `pbicvsupport@microsoft.com`.  
**Tenga en cuenta que el objeto visual debe estar disponible en [AppSource](https://appsource.microsoft.com/en-us/marketplace/apps?product=power-bi-visuals) y estar [certificado](https://powerbi.microsoft.com/en-us/documentation/powerbi-custom-visuals-certified/).**
