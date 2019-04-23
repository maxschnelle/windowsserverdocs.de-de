---
title: Beispiele für die Bitsadmin
description: Die folgenden Beispiele zeigen, wie Sie die Bitsadmin-Tool verwenden, um die am häufigsten verwendeten Aufgaben ausführen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb8f8374-ba6e-4a68-85a1-9a95b8215354
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/31/2018
ms.openlocfilehash: 4b9deb4fc7fbfccf569250e965274009764054f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849331"
---
# <a name="bitsadmin-examples"></a>Beispiele für die Bitsadmin

Die folgenden Beispiele zeigen, wie Sie mit der `bitsadmin` Tool, um die am häufigsten verwendeten Aufgaben ausführen.

## <a name="transfer-a-file"></a>Übertragen einer Datei

Die **/Übertragung** Switch ist eine Abkürzung für die unten aufgeführten Aufgaben ausführen. Dieser Schalter wird der Auftrag erstellt, fügt die Dateien für den Auftrag, den Auftrag in der Übertragungswarteschlange aktiviert und wird der Auftrag abgeschlossen. BITSAdmin weiterhin Statusinformationen im MS-DOS-Fenster angezeigt, bis die Übertragung abgeschlossen ist, oder ein Fehler auftritt.

**bitsadmin /transfer myDownloadJob /download /priority normal https://downloadsrv/10mb.zip c:\\10mb.zip**

## <a name="create-a-download-job"></a>Erstellen eines Auftrags herunterladen

Verwenden der **/ create** Schalter, um einen Downloadauftrag mit dem Namen MyDownloadJob zu erstellen.

**bitsadmin /create myDownloadJob**

BITSAdmin gibt eine GUID, die den Auftrag eindeutig identifiziert. Verwenden Sie den Namen GUID oder den Auftrag, bei nachfolgenden Aufrufen. Der folgende Text ist die Ausgabe des Beispiels.

``` syntax
Created job {C775D194-090F-431F-B5FB-8334D00D1CB6}.
```

Verwenden Sie als Nächstes die **an** Switch so den Downloadauftrag eine oder mehrere Dateien hinzu.

## <a name="add-files-to-the-download-job"></a>Hinzufügen von Dateien zum Downloadauftrag

Verwenden der **an** Switch zum Hinzufügen einer Datei für den Auftrag. Wiederholen Sie diesen Aufruf für jede Datei, die Sie hinzufügen möchten. Wenn mehrere Aufträge MyDownloadJob als ihren Namen verwenden, müssen Sie MyDownloadJob durch die Auftrags GUID zur eindeutigen Identifizierung des Auftrags ersetzen.

**Bitsadmin an MyDownloadJob https://downloadsrv/10mb.zip c:\\10mb.zip**

Um den Auftrag in der Übertragungswarteschlange zu aktivieren, verwenden die **/fortsetzen von** wechseln.

## <a name="activate-the-download-job"></a>Aktivieren des Download-Auftrags

Wenn Sie einen neuen Auftrag erstellen, hält BITS den Auftrag an. Um den Auftrag in der Übertragungswarteschlange zu aktivieren, verwenden die **/fortsetzen von** wechseln. Wenn mehrere Aufträge MyDownloadJob als ihren Namen verwenden, müssen Sie MyDownloadJob durch die Auftrags GUID zur eindeutigen Identifizierung des Auftrags ersetzen.

**Bitsadmin /resume myDownloadJob**

Um den Fortschritt des Auftrags zu ermitteln, verwenden die **/list**, **/Info**, oder **/Überwachen** wechseln.

## <a name="determine-the-progress-of-the-download-job"></a>Bestimmen Sie den Fortschritt des Auftrags herunterladen

Verwenden der **/Info** wechseln, um den Status eines Auftrags zu ermitteln. Wenn mehrere Aufträge MyDownloadJob als ihren Namen verwenden, müssen Sie MyDownloadJob durch die Auftrags GUID zur eindeutigen Identifizierung des Auftrags ersetzen.

**Bitsadmin/Info MyDownloadJob / verbose**

Die **/Info** Schalter gibt, den Status des Auftrags und die Anzahl der Dateien und übertragenen Bytes. Wenn der Status übertragen werden, BITS wurde erfolgreich übertragen alle Dateien im Auftrag. Die **/ verbose** -Argument erhalten Sie umfassende Details des Auftrags. Der folgende Text ist die Ausgabe des Beispiels.

``` syntax
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

Verwenden Sie zum Empfangen von Informationen für alle Aufträge in der Übertragungswarteschlange der **/list** oder **/Überwachen** wechseln.

## <a name="completing-the-download-job"></a>Den Auftrag abgeschlossen

Wenn der Status des Auftrags übertragen wird, BITS wurde erfolgreich übertragen alle Dateien im Auftrag. Die Dateien sind jedoch nicht verfügbar, bis Sie verwenden die **/ vollständige** wechseln. Wenn mehrere Aufträge MyDownloadJob als ihren Namen verwenden, müssen Sie MyDownloadJob durch die Auftrags GUID zur eindeutigen Identifizierung des Auftrags ersetzen.

**Bitsadmin / complete MyDownloadJob**

## <a name="monitoring-jobs-in-the-transfer-queue"></a>Überwachen von Aufträgen in der Übertragungswarteschlange

Verwenden der **/list**, **/Überwachen**, oder **/Info** zum Überwachen von Aufträgen in der Übertragungswarteschlange wechseln. Die **/list** -Switch bietet Informationen für alle Aufträge in der Warteschlange.

**bitsadmin /list**

Die **/list** Schalter gibt, den Status des Auftrags und die Anzahl der Dateien und für alle Aufträge in der Übertragungswarteschlange übertragenen Bytes. Der folgende Text ist die Ausgabe des Beispiels.

``` syntax
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN

Listed 2 job(s).
```

Verwenden der **/Überwachen** Switch um alle Aufträge in der Warteschlange zu überwachen. Die **/Überwachen** Switch aktualisiert die Daten alle 5 Sekunden. Geben Sie STRG + C, um die Aktualisierung zu beenden.

**bitsadmin /monitor**

Die **/Überwachen** Schalter gibt, den Status des Auftrags und die Anzahl der Dateien und für alle Aufträge in der Übertragungswarteschlange übertragenen Bytes. Der folgende Text ist die Ausgabe des Beispiels.

``` syntax
MONITORING BACKGROUND COPY MANAGER(5 second refresh)
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN
{0B138008-304B-4264-B021-FD04455588FF} job3 TRANSFERRED 1 / 1 100379370 / 100379370
```

## <a name="deleting-jobs-from-the-transfer-queue"></a>Löschen von Aufträgen aus der Übertragungswarteschlange

Verwenden der **/reset** Switch um alle Aufträge aus der Übertragungswarteschlange zu entfernen.

**bitsadmin /reset**

Der folgende Text ist die Ausgabe des Beispiels.

``` syntax
{DC61A20C-44AB-4768-B175-8000D02545B9} canceled.
{BB6E91F3-6EDA-4BB4-9E01-5C5CBB5411F8} canceled.
2 out of 2 jobs canceled.
```
