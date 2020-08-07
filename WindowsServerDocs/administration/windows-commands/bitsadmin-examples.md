---
title: bitsadmin examples
description: In den Beispielen wird gezeigt, wie das bitadmin-Tool verwendet wird, um die gängigsten Aufgaben auszuführen.
ms.topic: article
ms.assetid: cb8f8374-ba6e-4a68-85a1-9a95b8215354
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/31/2018
ms.openlocfilehash: 5cf827ebc96c2caf114a9605482a33636689dc25
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894582"
---
# <a name="bitsadmin-examples"></a>bitsadmin examples

In den folgenden Beispielen wird gezeigt, wie Sie das `bitsadmin` Tool verwenden, um die gängigsten Aufgaben auszuführen.

## <a name="transfer-a-file"></a>Übertragen einer Datei

Fügen Sie zum Erstellen eines Auftragsdateien hinzu, aktivieren Sie den Auftrag in der Übertragungs Warteschlange, und führen Sie den Auftrag aus:

`bitsadmin /transfer myDownloadJob /download /priority normal https://downloadsrv/10mb.zip c:\\10mb.zip`

Der bizadmin zeigt weiterhin Statusinformationen im MS-DOS-Fenster an, bis die Übertragung abgeschlossen ist oder ein Fehler auftritt.

## <a name="create-a-download-job"></a>Erstellen eines Download Auftrags

So erstellen Sie einen Download Auftrag mit dem Namen *mydownloadjob*:

```
bitsadmin /create myDownloadJob
```

Bigsadmin gibt eine GUID zurück, die den Auftrag eindeutig identifiziert. Verwenden Sie die GUID oder den Auftrags Namen in nachfolgenden Aufrufen. Der folgende Text ist eine Beispielausgabe.

### <a name="sample-output"></a>Beispielausgabe

`created job {C775D194-090F-431F-B5FB-8334D00D1CB6}`

## <a name="add-files-to-the-download-job"></a>Hinzufügen von Dateien zum Download Auftrag

So fügen Sie dem Auftrag eine Datei hinzu:

```
bitsadmin /addfile myDownloadJob https://downloadsrv/10mb.zip c:\\10mb.zip
```

Wiederholen Sie diesen Befehl für jede Datei, die Sie hinzufügen möchten. Wenn für mehrere Aufträge *mydownloadjob* als Name verwendet wird, müssen Sie die GUID des Auftrags verwenden, um Sie für den Abschluss eindeutig zu identifizieren.

## <a name="activate-the-download-job"></a>Aktivieren des Download Auftrags

Nachdem Sie einen neuen Auftrag erstellt haben, hält Bits den Auftrag automatisch an. So aktivieren Sie den Auftrag in der Übertragungs Warteschlange:

```
bitsadmin /resume myDownloadJob
```

Wenn für mehrere Aufträge *mydownloadjob* als Name verwendet wird, müssen Sie die GUID des Auftrags verwenden, um Sie für den Abschluss eindeutig zu identifizieren.

## <a name="determine-the-progress-of-the-download-job"></a>Bestimmen des Fortschritts des Download Auftrags

Der Schalter **/Info** gibt den Status des Auftrags und die Anzahl der übertragenen Dateien und Bytes zurück. Wenn der Zustand als angezeigt wird `TRANSFERRED` , bedeutet dies, dass Bits alle Dateien im Auftrag erfolgreich übertragen hat. Sie können auch das **/verbose** -Argument hinzufügen, um vollständige Details zum Auftrag zu erhalten, und **/List** oder **/Monitor** , um alle Aufträge in der Übertragungs Warteschlange zu erhalten.

So geben Sie den Status des Auftrags zurück

```
bitsadmin /info myDownloadJob /verbose
```

Wenn für mehrere Aufträge *mydownloadjob* als Name verwendet wird, müssen Sie die GUID des Auftrags verwenden, um Sie für den Abschluss eindeutig zu identifizieren.

## <a name="complete-the-download-job"></a>Download Auftrag ausführen

So schließen Sie den Auftrag ab, nachdem sich der Status geändert hat in `TRANSFERRED` :

```
bitsadmin /complete myDownloadJob
```

Sie müssen den Schalter ausführen, `/complete` bevor die Dateien im Auftrag verfügbar werden. Wenn für mehrere Aufträge *mydownloadjob* als Name verwendet wird, müssen Sie die GUID des Auftrags verwenden, um Sie für den Abschluss eindeutig zu identifizieren.

## <a name="monitor-jobs-in-the-transfer-queue-using-the-list-switch"></a>Überwachen von Aufträgen in der Übertragungs Warteschlange mit dem Schalter/List

So geben Sie den Status des Auftrags und die Anzahl der Dateien und Bytes zurück, die für alle Aufträge in der Übertragungs Warteschlange übertragen wurden:

```
bitsadmin /list
```

### <a name="sample-output"></a>Beispielausgabe

```
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN

Listed 2 job(s).
```

## <a name="monitor-jobs-in-the-transfer-queue-using-the-monitor-switch"></a>Überwachen von Aufträgen in der Übertragungs Warteschlange mit dem Schalter/Monitor

So geben Sie den Status des Auftrags und die Anzahl der Dateien und Bytes zurück, die für alle Aufträge in der Übertragungs Warteschlange übertragen werden, und aktualisieren die Daten alle 5 Sekunden:

```
bitsadmin /monitor
```

> [!NOTE]
> Drücken Sie STRG + C, um die Aktualisierung zu verhindern.

### <a name="sample-output"></a>Beispielausgabe

```
MONITORING BACKGROUND COPY MANAGER(5 second refresh)
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN
{0B138008-304B-4264-B021-FD04455588FF} job3 TRANSFERRED 1 / 1 100379370 / 100379370
```

## <a name="monitor-jobs-in-the-transfer-queue-using-the-info-switch"></a>Überwachen von Aufträgen in der Übertragungs Warteschlange mit dem Schalter/Info

So geben Sie den Status des Auftrags und die Anzahl der übertragenen Dateien und Bytes zurück

```
bitsadmin /info
```

### <a name="sample-output"></a>Beispielausgabe

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

## <a name="delete-jobs-from-the-transfer-queue"></a>Löschen von Aufträgen aus der Übertragungs Warteschlange

Um alle Aufträge aus der Übertragungs Warteschlange zu entfernen, verwenden Sie den Schalter/Reset:

```
bitsadmin /reset
```

### <a name="sample-output"></a>Beispielausgabe

```
{DC61A20C-44AB-4768-B175-8000D02545B9} canceled.
{BB6E91F3-6EDA-4BB4-9E01-5C5CBB5411F8} canceled.
2 out of 2 jobs canceled.
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
