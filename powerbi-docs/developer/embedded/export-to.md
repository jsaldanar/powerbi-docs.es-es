---
title: API para exportar informes de Power BI
description: Obtener información sobre cómo exportar un informe de Power BI insertado
author: KesemSharabi
ms.author: kesharab
ms.topic: how-to
ms.service: powerbi
ms.subservice: powerbi-developer
ms.date: 03/01/2020
ms.openlocfilehash: eb08eb2ed8ecead4e5a2437cafced6194f05acbe
ms.sourcegitcommit: a175faed9378a7d040a08ced3e46e54503334c07
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/18/2020
ms.locfileid: "79492316"
---
# <a name="export-report-to-file-preview"></a>Exportar informe a archivo (versión preliminar)

La API `exportToFile` permite exportar un informe de Power BI mediante una llamada REST. Se admiten los siguientes formatos de archivo:
* **PPTX** (PowerPoint)
* **PDF**
* **PNG**
    * Al exportar a un PNG, un informe de varias páginas se comprime en un archivo zip.
    * Cada archivo del archivo zip PNG representa una página del informe
    * Los nombres de página son los mismos que los valores devueltos de las API [Obtener páginas](https://docs.microsoft.com/rest/api/power-bi/reports/getpages) u [Obtener páginas en grupo](https://docs.microsoft.com/rest/api/power-bi/reports/getpagesingroup)

## <a name="usage-examples"></a>Ejemplos de uso

Puede usar la característica de exportación de varias maneras. Estos son algunos ejemplos:

* **Botón Enviar para imprimir**: en la aplicación, cree un botón que, al hacer clic en él, desencadene un trabajo de exportación. El trabajo puede exportar el informe visto como PDF o PPTX, y cuando la operación se complete, el usuario puede recibir el archivo como una descarga. Mediante marcadores, puede exportar el informe en un estado específico, incluidos filtros configurados, segmentaciones y configuraciones adicionales. Como la API es asincrónica, el archivo puede tardar un tiempo en estar disponible.

* **Datos adjuntos de correo electrónico**: envíe un correo electrónico automatizado a intervalos establecidos, con un informe PDF adjunto. Este escenario puede ser útil si desea automatizar el envío de un informe semanal a los ejecutivos.

## <a name="using-the-api"></a>Uso de la API

Antes de usar la API, compruebe que las siguientes [configuraciones de inquilinos del administrador](../../service-admin-portal.md#tenant-settings) estén habilitadas:
* **Exportación de informes como presentaciones de PowerPoint o documentos PDF**: habilitada de forma predeterminada.
* **Exportación de informes como archivos de imagen**: se requiere solo para PNG y está deshabilitada de forma predeterminada.

La API es asincrónica. Cuando se llama a la API [exportToFile](https://docs.microsoft.com/rest/api/power-bi/reports/exporttofile), se desencadena un trabajo de exportación. Después de activar un trabajo de exportación, use el [sondeo](https://docs.microsoft.com/rest/api/power-bi/reports/getexporttofilestatus) para realizar un seguimiento del trabajo, hasta que se complete.

Durante el sondeo, la API devuelve un número que representa la cantidad de trabajo completado. El trabajo en cada trabajo de exportación se calcula en función del número de páginas que tiene el informe. Todas las páginas tienen el mismo peso. Si, por ejemplo, está exportando un informe con diez páginas, y el sondeo devuelve setenta, significa que la API ha procesado siete de las diez páginas en el trabajo de exportación.

Cuando se completa la exportación, la llamada API de sondeo devuelve una [dirección URL de Power BI](https://docs.microsoft.com/rest/api/power-bi/reports/getfileofexporttofile) para obtener el archivo. La dirección URL estará disponible durante veinticuatro horas.

## <a name="supported-features"></a>Características admitidas

### <a name="selecting-which-pages-to-print"></a>Selección de páginas para imprimir

Especifique las páginas que desea imprimir conforme al valor devuelto de [Obtener páginas](https://docs.microsoft.com/rest/api/power-bi/reports/getpages) u [Obtener páginas en grupo](https://docs.microsoft.com/rest/api/power-bi/reports/getpagesingroup). También puede especificar el orden de las páginas que está exportando.

### <a name="bookmarks"></a>Marcadores

 Puede usar la API `exportToFile` para exportar mediante programación un informe en un estado específico, después de aplicarle filtros. Esto se hace usando las funcionalidades de [Marcadores](../../consumer/end-user-bookmarks.md). Para exportar un informe mediante marcadores, use la [API de JavaScript de marcadores](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Bookmarks).

 Por ejemplo, puede usar el método `capturedBookmark.state` del marcador para capturar los cambios que un usuario específico realizó en un informe y luego exportarlo en su estado actual.

Los [marcadores personales](../../consumer/end-user-bookmarks.md#personal-bookmarks) y los [filtros persistentes](https://powerbi.microsoft.com/blog/announcing-persistent-filters-in-the-service/) no se admiten.

### <a name="authentication"></a>Autenticación

Solo puede autenticarse utilizando un usuario (o usuario maestro). Actualmente, la [entidad de servicio](embed-service-principal.md) no se admite.

### <a name="row-level-security-rls"></a>Seguridad de nivel de fila (RLS)

Con la [seguridad de nivel de fila (RLS)](embedded-row-level-security.md), puede exportar un informe que muestra datos que solo son visibles para ciertos usuarios. Por ejemplo, si exporta un informe de ventas que está definido con roles regionales, puede filtrar dicho informe mediante programación para que solo se muestre una determinada región.

Para realizar la exportación mediante la seguridad de nivel de fila, debe tener los siguientes permisos:
* Permisos para escribir y volver a compartir para el conjunto de datos al que está conectado el informe
* Si el informe reside en un área de trabajo v1, debe ser el administrador de dicho espacio de trabajo
* Si el informe reside en un área de trabajo v2, debe ser un miembro o administrador de dicho espacio de trabajo

### <a name="data-protection"></a>Protección de datos

Los formatos PDF y PPTX admiten [etiquetas de sensibilidad](../../admin/service-security-data-protection-overview.md#sensitivity-labels-in-power-bi). Si exporta un informe con una etiqueta de sensibilidad a un archivo PDF o PPTX, el archivo exportado mostrará el informe con su etiqueta de sensibilidad.

### <a name="localization"></a>Localización

Al usar la API `exportToFile`, puede pasar su localización deseada. La configuración de localización afecta a la forma en que se muestra el informe, por ejemplo, cambiando el formato conforme a la localización seleccionada.

## <a name="concurrent-requests"></a>Solicitudes simultáneas

`exportToFile` admite solicitudes simultáneas de trabajos de exportación. En la tabla siguiente se muestra la cantidad de trabajos que puede ejecutar al mismo tiempo, dependiendo de la SKU en la que reside el informe. Las solicitudes concurrentes se refieren a páginas de informes. Por ejemplo, veinte páginas en una solicitud de exportación en una SKU A6 se procesarán simultáneamente. Esto llevará aproximadamente el mismo tiempo que enviar veinte solicitudes de exportación con una página cada una.

Un trabajo que supere su número de solicitudes simultáneas no se termina. Por ejemplo, si exporta tres páginas en una SKU A1, se ejecutará el primer trabajo y los dos últimos esperarán a los dos próximos ciclos de ejecución.

|SKU de Azure  |SKU de Office  |Número máximo de páginas de informe simultáneas  |
|-----------|------------|-----------|
|A1         |EM1         |1          |
|A2         |EM2         |2          |
|A3         |EM3         |3          |
|A4         |P1          |6          |
|A5         |P2          |12         |
|A6         |P3          |24         |

## <a name="limitations"></a>Limitaciones

* El informe que va a exportar debe estar en una capacidad Premium o Embedded.
* El conjunto de datos del informe que va a exportar debe estar en una capacidad Premium o Embedded.
* Para la versión preliminar pública, el número de páginas de informes de Power BI exportadas por hora está limitado a 50 por capacidad.
* Los informes exportados no pueden tener un tamaño superior a 250 MB.
* Al exportar a PNG, las etiquetas de sensibilidad no se admiten.
* La [entidad de servicio](embed-service-principal.md) no se admite.
* El número de páginas que se pueden incluir en un informe exportado es treinta. Si el informe incluye más páginas, la API devuelve un error y el trabajo de exportación se cancela.
* Los [marcadores personales](../../consumer/end-user-bookmarks.md#personal-bookmarks) y los [filtros persistentes](https://powerbi.microsoft.com/blog/announcing-persistent-filters-in-the-service/) no se admiten.
* Los informes paginados no se admiten actualmente.
* Los objetos visuales de Power BI que se enumeran a continuación no se admiten. Cuando se exporta un informe que contiene estos objetos visuales, las partes del informe que contienen dichos objetos visuales no se representarán y mostrarán un símbolo de error.
    * Objetos visuales de Power BI sin certificar
    * Objetos visuales de R
    * PowerApps
    * Objetos visuales de Python
    * Visio

## <a name="code-examples"></a>Ejemplos de código

Cuando crea un trabajo de exportación, hay tres pasos que se deben seguir:

1. Envío de una solicitud de exportación.
2. Sondeo.
3. Obtención del archivo.

En esta sección se proporcionan ejemplos para cada paso.

### <a name="step-1---sending-an-export-request"></a>Paso 1: Envío de una solicitud de exportación

El primer paso es enviar una solicitud de exportación. En este ejemplo, se envía una solicitud de exportación para una página específica.

```csharp
/////// Export sample ///////
private async Task<string> PostExportRequest(
    Guid reportId,
    Guid groupId,
    FileFormat format,
    IList<string> pageNames = null /* Get the page names from the GetPages API */)
        {
            var powerBIReportExportConfiguration = new PowerBIReportExportConfiguration
            {
                Settings = new ExportReportSettings
                {
                    Locale = "en-us",
                },

                // Note that page names differ from the page display names.
                // To get the page names use the GetPages API.
                Pages = pageNames?.Select(pn => new ExportReportPage(Name = pn)).ToList(),
            };

            var exportRequest = new ExportReportRequest
            {
                Format = format,
                PowerBIReportConfiguration = powerBIReportExportConfiguration,
            };

            var export = await Client.Reports.ExportToFileInGroupAsync(groupId, reportId, exportRequest);

            // Save the export ID, you'll need it for polling and getting the exported file
            return export.Id;
        }
```

### <a name="step-2---polling"></a>Paso 2: Sondeo

Después de enviar una solicitud de exportación, use el sondeo para identificar cuándo está listo el archivo de exportación que está esperando.

```csharp
private async Task<Export> PollExportRequest(
    Guid reportId,
    Guid groupId,
    string exportId /* Get from the ExportToAsync response */,
    int timeOutInMinutes,
    CancellationToken token)
    {
        Export exportStatus = null;
        DateTime startTime = DateTime.UtcNow;
        const int c_secToMillisec = 1000;
        do
        {
            if (DateTime.UtcNow.Subtract(startTime).TotalMinutes > timeOutInMinutes || token.IsCancellationRequested)
            {
                // Error handling for timeout and cancellations
                return null;
            }

            var httpMessage = await Client.Reports.GetExportToFileStatusInGroupWithHttpMessagesAsync(groupId, reportId, exportId);
            exportStatus = httpMessage.Body;

            // You can track the export progress using the PercentComplete that's part of the response
            SomeTextBox.Text = string.Format("{0} (Percent Complete : {1}%)", exportStatus.Status.ToString(), exportStatus.PercentComplete);

            if (exportStatus.Status == ExportState.Running || exportStatus.Status == ExportState.NotStarted)
            {
                // The recommended waiting time between polling requests can be found in the RetryAfter header
                // Note that this header is only populated when the status is either Running or NotStarted
                var retryAfter = httpMessage.Response.Headers.RetryAfter;
                var retryAfterInSec = retryAfter.Delta.Value.Seconds;
                await Task.Delay(retryAfterInSec * c_secToMillisec);
            }
        }
        // While not in a terminal state, keep polling
        while (exportStatus.Status != ExportState.Succeeded && exportStatus.Status != ExportState.Failed);

        return exportStatus;
    }
```

### <a name="step-3---getting-the-file"></a>Paso 3: Obtención del archivo

Una vez que el sondeo devuelve una dirección URL, use este ejemplo para obtener el archivo recibido.

```csharp
private readonly IDictionary<string, string> mediaTypeToSuffix = new Dictionary<string, string>
    {
        { "image/png", "png" },
        { "application/zip", "zip" },
        { "application/pdf", "pdf" },
        { "application/vnd.openxmlformats-officedocument.presentationml.presentation", "pptx" },
    };

private async Task<ExportedFile> GetExportedFile(
    Guid reportId,
    Guid groupId,
    Export export /* Get from the GetExportStatusAsync response */)
    {
        if (export.Status == ExportState.Succeeded)
        {
            var httpMessage = await Client.Reports.GetFileOfExportToFileInGroupWithHttpMessagesAsync(groupId, reportId, export.Id);
            var mediaType = httpMessage.Response.Content.Headers.ContentType.ToString().ToLower();

            if (!mediaTypeToSuffix.TryGetValue(mediaType, out string fileSuffix))
            {
                // Handle unexpected errors
            }
            else
            {
                return new ExportedFile
                {
                    FileStream = httpMessage.Body,
                    FileSuffix = fileSuffix,
                };
            }
        }

        return null;
    }

public class ExportedFile
{
    public Stream FileStream;
    public string FileSuffix;
}
```

### <a name="end-to-end-example"></a>Ejemplo de un extremo a otro

Este es un ejemplo de un extremo a extremo para exportar un informe. Este ejemplo incluye las siguientes etapas:
1. [Envío de la solicitud de exportación](#step-1---sending-an-export-request).
2. [Sondeo](#step-2---polling).
3. [Obtención del archivo](#step-3---getting-the-file).

```csharp
private async Task<ExportedFile> ExportPowerBIReport(
    Guid reportId,
    Guid groupId,
    FileFormat format,
    int pollingtimeOutInMinutes,
    CancellationToken token,
    IList<string> pageNames = null /* Get the page names from the GetPages API */)
        {
            try
            {
                var exportId = await PostExportRequest(reportId, groupId, format, pageNames);

                var export = await PollExportRequest(reportId, groupId, exportId, pollingtimeOutInMinutes, token);
                if (export == null || export.Status != ExportState.Succeeded)
                {
                    // Error, failure in exporting the report
                    return null;
                }

                return await GetExportedFile(reportId, groupId, export);
            }
            catch
            {
                // Error handling
                throw;
            }
        }
```

## <a name="next-steps"></a>Pasos siguientes

Revise cómo insertar contenido para sus clientes y su organización:

> [!div class="nextstepaction"]
>[Insertar para los clientes](embed-sample-for-customers.md)

> [!div class="nextstepaction"]
>[Insertar para la organización](embed-sample-for-your-organization.md)