---
title: biout admin-Beispiele
description: In den folgenden Beispielen wird gezeigt, wie Sie das bizadmin-Tool verwenden, um die gängigsten Aufgaben auszuführen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cb8f8374-ba6e-4a68-85a1-9a95b8215354
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/31/2018
ms.openlocfilehash: 96447410f76e4402c456b5ec402cc730480aedaf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850803"
---
# <a name="bitsadmin-examples"></a>biout admin-Beispiele

In den folgenden Beispielen wird gezeigt, wie Sie das `bitsadmin`-Tool verwenden, um die gängigsten Aufgaben auszuführen.

## <a name="transfer-a-file"></a>Übertragen einer Datei

Der **/Transfer** -Schalter ist eine Verknüpfung zum Ausführen der unten aufgeführten Aufgaben. Mit diesem Switch wird der Auftrag erstellt, die Dateien werden dem Auftrag hinzugefügt, der Auftrag wird in der Übertragungs Warteschlange aktiviert und der Auftrag abgeschlossen. Der bizadmin zeigt weiterhin Statusinformationen im MS-DOS-Fenster an, bis die Übertragung abgeschlossen ist oder ein Fehler auftritt.

`bitsadmin /transfer myDownloadJob /download /priority normal https://downloadsrv/10mb.zip c:\\10mb.zip`

## <a name="create-a-download-job"></a>Erstellen eines Download Auftrags

Verwenden Sie den Schalter **/Create** , um einen Download Auftrag mit dem Namen mydownloadjob zu erstellen.

### <a name="syntax"></a>Syntax

```
bitsadmin /create myDownloadJob
```

Bitsadmin gibt eine GUID zurück, die den Auftrag eindeutig identifiziert. Verwenden Sie die GUID oder den Auftrags Namen in nachfolgenden Aufrufen. Der folgende Text ist eine Beispielausgabe.

#### <a name="sample-output"></a>Beispielausgabe

`created job {C775D194-090F-431F-B5FB-8334D00D1CB6}`

## <a name="add-files-to-the-download-job"></a>Hinzufügen von Dateien zum Download Auftrag

Verwenden Sie den Schalter **/AddFile** , um dem Auftrag eine Datei hinzuzufügen. Wiederholen Sie diesen Befehl für jede Datei, die Sie hinzufügen möchten.

Wenn für mehrere Aufträge mydownloadjob als Name verwendet wird, müssen Sie mydownloadjob durch die GUID des Auftrags ersetzen, um den Auftrag eindeutig zu identifizieren.

### <a name="syntax"></a>Syntax

```
bitsadmin /addfile myDownloadJob https://downloadsrv/10mb.zip c:\\10mb.zip
```

## <a name="activate-the-download-job"></a>Aktivieren des Download Auftrags

Wenn Sie einen neuen Auftrag erstellen, hält Bits den Auftrag an. Verwenden Sie den Schalter **/Resume** , um den Auftrag in der Übertragungs Warteschlange zu aktivieren.

Wenn für mehrere Aufträge mydownloadjob als Name verwendet wird, müssen Sie mydownloadjob durch die GUID des Auftrags ersetzen, um den Auftrag eindeutig zu identifizieren.

### <a name="syntax"></a>Syntax

`bitsadmin /resume myDownloadJob`

## <a name="determine-the-progress-of-the-download-job"></a>Bestimmen des Fortschritts des Download Auftrags

Verwenden Sie den Schalter **/Info** , um den Status des Auftrags und die Anzahl der übertragenen Dateien und Bytes zurückzugeben. Wenn der Status übertragen wird, hat Bits erfolgreich alle Dateien im Auftrag übertragen.

- Verwenden Sie das **/verbose** -Argument, um ausführliche Informationen zum Auftrag zu erhalten.

- Verwenden Sie den Schalter " **/List** " oder " **/Monitor** ", um alle Aufträge in der Übertragungs Warteschlange zu erhalten.

Wenn für mehrere Aufträge mydownloadjob als Name verwendet wird, müssen Sie mydownloadjob durch die GUID des Auftrags ersetzen, um den Auftrag eindeutig zu identifizieren.

### <a name="syntax"></a>Syntax

`bitsadmin /info myDownloadJob /verbose`

#### <a name="sample-output"></a>Beispielausgabe

```
GUID: {482FCAF0-74BF-469B-8929-5CCD028C9499} DISPLAY: myDownloadJob
TYPE: DOWNLOAD STATE: TRANSIENT_ERROR OWNER: domain\user
PRIORITY: NORMAL FILES: 0 / 1 BYTES: 0 / UNKNOWN
CREATION TIME: 12/17/2002 1:21:17 PM MODIFICATION TIME: 12/17/2002 1:21:30 PM
COMPLETION TIME: UNKNOWN
NOTIFY INTERFACE: UNREGISTERED NOTIFICATION FLAGS: 3
RETRY DELAY: 600 NO PROGRESS TIMEOUT: 1209600 ERROR COUNT: 0
PROXY USAGE: PRECONFIG PROXY LIST: NULL PROXY BYPASS LIST: NULL
ERROR FILE:    https://downloadsrv/10mb.zip -> c:\10mb.zip
ERROR CODE:    0x80072ee7 - The server name or address could not be resolved
ERROR CONTEXT: 0x00000005 - The error occurred while the remote file was being 
processed.
DESCRIPTION:
JOB FILES:
        0 / UNKNOWN WORKING https://downloadsrv/10mb.zip -> c:\10mb.zip
NOTIFICATION COMMAND LINE: none
```

## <a name="completing-the-download-job"></a>Abschließen des Download Auftrags

Wenn der Status des Auftrags übertragen wird, hat Bits erfolgreich alle Dateien im Auftrag übertragen. Die Dateien sind jedoch erst verfügbar, wenn Sie den Schalter **/Complete** verwenden.

Wenn für mehrere Aufträge mydownloadjob als Name verwendet wird, müssen Sie mydownloadjob durch die GUID des Auftrags ersetzen, um den Auftrag eindeutig zu identifizieren.

### <a name="syntax"></a>Syntax

`bitsadmin /complete myDownloadJob`

## <a name="monitoring-jobs-in-the-transfer-queue"></a>Überwachen von Aufträgen in der Übertragungs Warteschlange

Verwenden Sie den Schalter **/List**, **/Monitor**oder **/Info** , um Aufträge in der Übertragungs Warteschlange zu überwachen. Der **/List** -Schalter enthält Informationen zu allen Aufträgen in der Warteschlange.

## <a name="list-switch"></a>/List-Schalter

Der Schalter **/List** gibt den Status des Auftrags und die Anzahl der Dateien und Bytes zurück, die für alle Aufträge in der Übertragungs Warteschlange übertragen wurden.

### <a name="syntax"></a>Syntax

`bitsadmin /list`

#### <a name="sample-output-for-the-list-switch"></a>Beispielausgabe für den/List-Schalter

```
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN

Listed 2 job(s).
```

## <a name="monitor-switch"></a>/Monitor-Schalter

Der Schalter **/Monitor** gibt den Status des Auftrags und die Anzahl der Dateien und Bytes zurück, die für alle Aufträge in der Übertragungs Warteschlange übertragen werden, und aktualisiert die Daten alle 5 Sekunden. Drücken Sie STRG + C, um die Aktualisierung zu verhindern.

### <a name="syntax"></a>Syntax

`bitsadmin /monitor`

#### <a name="sample-output"></a>Beispielausgabe

```
MONITORING BACKGROUND COPY MANAGER(5 second refresh)
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN
{0B138008-304B-4264-B021-FD04455588FF} job3 TRANSFERRED 1 / 1 100379370 / 100379370
```

## <a name="deleting-jobs-from-the-transfer-queue"></a>Löschen von Aufträgen aus der Übertragungs Warteschlange

Verwenden Sie den Schalter **/Reset** , um alle Aufträge aus der Übertragungs Warteschlange zu entfernen.

### <a name="syntax"></a>Syntax

`bitsadmin /reset`

#### <a name="sample-output"></a>Beispielausgabe

```
{DC61A20C-44AB-4768-B175-8000D02545B9} canceled.
{BB6E91F3-6EDA-4BB4-9E01-5C5CBB5411F8} canceled.
2 out of 2 jobs canceled.
```
