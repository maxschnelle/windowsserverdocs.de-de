---
title: cleanmgr
description: Erfahren Sie, wie Sie die Befehlszeilenoptionen verwenden, um die Datenträgerbereinigung-Tool (Cleanmgr.exe) zum automatischen Bereinigen von bestimmte Dateien zu konfigurieren.
ms.prod: windows-server-threshold
ms.reviewer: cosmosdarwin
author: iangpgh
ms.author: jgerend
manager: daveba
ms.technology: storage-spaces
ms.date: 06/20/2019
ms.openlocfilehash: edcf878723653c3b51c8b5b29e9cd93106159446
ms.sourcegitcommit: 078304c4b92bb57eb85ba29634afc92cc028c644
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67301589"
---
# <a name="cleanmgr"></a>cleanmgr

> Gilt für: WindowsServer 2019, WindowsServer 2016, WindowsServer 2012, Windows Server 2008 R2, WindowsServer (Halbjährlicher Kanal)

Löscht nicht benötigte Dateien, die von der Festplatte des Computers an. Sie können Befehlszeilenoptionen verwenden, um anzugeben, dass temporäre Dateien, Internet-Dateien, heruntergeladenen Dateien und Recycle Bin-Dateien Cleanmgr bereinigt. Sie können dann die Aufgabe zu einem bestimmten Zeitpunkt ausgeführt werden soll, mit dem Tool für geplante Aufgaben planen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#examples).

## <a name="syntax"></a>Syntax

```
cleanmgr [/d <driveletter>] [/sageset:n]  [/sagerun:n] [/TUNEUP:n] [/LOWDISK] [/VERYLOWDISK]
```

## <a name="parameters"></a>Parameter

|      Parameter      |    Beschreibung     |
| ------------------- | ------------------ |
|  / d \<Driveletter >          | Gibt an, das Laufwerk, das Datenträgerbereinigung bereinigt werden sollen.<br>**Hinweis**: Die Option/d ist mit /sagerun:n nicht genutzt werden. |
| /sageset:n | Zeigt das Dialogfeld für die Bereinigung der Datenträgereinstellungen an, und erstellt einen Registrierungsschlüssel zum Speichern der Einstellungen, die Sie auswählen. Die `n` -Wert, der in der Registrierung gespeichert ist, können Sie Aufgaben zum Ausführen der Datenträgerbereinigung angeben. Die `n` Wert kann ganzzahligen Wert zwischen 0 und 65535 sein. Alle verfügbaren Optionen bei der Verwendung der Option/sageset geben an, um das Laufwerk, auf dem Windows installiert ist.  |
|  /sagerun:n  |  Führt die angegebenen Aufgaben, die auf der n-Wert zugewiesen werden, wenn Sie die Option \sageset verwenden. Alle Laufwerke auf dem Computer aufgelistet sind, und das ausgewählte Profil wird für jedes Laufwerk ausgeführt.           |
| /TUNEUP:n    | Führen Sie für den gleichen/sageset und sagerun `n` . |
| / LOWDISK     | Führen Sie mit den Standardeinstellungen. |
| / VERYLOWDISK | Führen Sie mit den Standardeinstellungen keine eingabeaufforderungen. |
| /?           | Anzeigen der Hilfe. |

## <a name="options"></a>Optionen

Die Optionen für die Dateien, die Sie für die Datenträgerbereinigung angeben können, mithilfe von/sageset und sagerun umfassen:

- **Temporäre Dateien von Setup** -Hierbei handelt es sich um Dateien, die durch ein Setupprogramm erstellt wurden, die nicht mehr ausgeführt wird.

- **Heruntergeladene Programmdateien** – heruntergeladene Programmdateien werden ActiveX-Steuerelemente und Java-Programme, die werden automatisch aus dem Internet heruntergeladen, wenn Sie bestimmte Seiten anzeigen. Diese Dateien werden vorübergehend im Ordner "Programme herunterladen" auf der Festplatte gespeichert. Diese Option enthält eine Schaltfläche "Dateien anzeigen", damit Sie die Dateien sehen können, vor der Datenträgerbereinigung entfernt. Die Schaltfläche öffnet C:\Winnt\Downloaded Ordner "Programme".

- **Temporäre Internetdateien** -die temporäre Internetdateien enthält Webseiten, die auf der Festplatte für die schnelle Anzeige gespeichert werden. Datenträgerbereinigung entfernt diese Seite, bleiben jedoch intakt die personalisierten Einstellungen für Webseiten. Diese Option schließt auch eine Schaltfläche "Dateien anzeigen", die im Ordner C:\Documents und Einstellungen\ Einstellungen\Temporary Internet Files\Content.IE5 geöffnet wird. 

- **Alte Chkdsk-Dateien** – Wenn Chkdsk überprüft einen Datenträger für Fehler, Chkdsk möglicherweise verlorene Dateifragmente als Dateien im Stammordner auf dem Datenträger speichern. Diese Dateien sind nicht erforderlich.

- **Papierkorb** -der Papierkorb enthält Dateien, die Sie vom Computer gelöscht haben. Diese Dateien werden nicht dauerhaft entfernt werden, bis Sie den Papierkorb leeren. Diese Option enthält eine Schaltfläche für Dateien anzeigen, die den Papierkorb geöffnet wird. **Hinweis**: Ein Papierkorb kann in mehr als einem Laufwerk, z. B. nicht nur in %SystemRoot% angezeigt werden.

- **Temporäre Dateien** -Programme mitunter temporären Informationen speichern, in einen Ordner "Temp". Beim Beenden des Programms in der Regel dieser Informationen gelöscht. Sie können problemlos temporäre Dateien löschen, die nicht innerhalb der letzten Woche geändert wurden.

- **Temporäre Offlinedateien** -temporäre Offlinedateien sind lokale Kopien der zuletzt geöffneten Netzwerkdateien. Diese Dateien werden automatisch zwischengespeichert werden, damit, dass Sie sie verwenden können, nachdem Sie aus dem Netzwerk trennen. Eine Schaltfläche "Dateien anzeigen" wird geöffnet, den Ordner Offlinedateien.

- **Offlinedateien** -Offlinedateien werden lokale Kopien von Netzwerk-Dateien, die Sie explizit offline zur Verfügung haben, damit Sie sie verwenden können, nachdem Sie aus dem Netzwerk trennen möchten. Eine Schaltfläche "Dateien anzeigen" wird geöffnet, den Ordner Offlinedateien.

- **Alte Dateien komprimieren** -Windows kann Dateien komprimieren, die Sie nicht vor kurzem verwendet haben. Komprimieren von Dateien Speicherplatz auf dem Datenträger gespeichert, aber Sie können die Dateien weiterhin verwenden. Es werden keine Dateien gelöscht. Da die Dateien mit unterschiedlichen Raten komprimiert werden, ist die angezeigte Menge des Speicherplatzes, die Sie erhalten werden ungefährer Wert. Eine Schaltfläche "Optionen" ermöglicht Ihnen die Angabe der Anzahl der Tage, die gewartet wird, bevor die Datenträgerbereinigung eine nicht verwendete Datei komprimiert.

- **Katalogdateien für den Inhaltsindex** -der Indexdienst-beschleunigt und verbessert Dateisuchen mithilfe einer der Dateien, die auf dem Datenträger sind. Diese Katalogdateien bleiben von einer früheren Indizierungsvorgang und können ohne weiteres gelöscht werden. **Hinweis**: Katalogdatei kann in mehr als einem Laufwerk, z. B. nicht nur in % SystemRoot% angezeigt.

**Beachten Sie** bei Angabe von bereinigen das Laufwerk, das die Windows-Installation enthält alle der folgenden Optionen stehen auf der Registerkarte "Datenträgerbereinigung". Wenn Sie einem anderen Laufwerk angeben, sind nur den Papierkorb, und die Katalog-Dateien für Inhalte Indexoptionen auf der Registerkarte "Datenträgerbereinigung" verfügbar. 

## <a name="examples"></a>Beispiele

Zum Ausführen der Datenträgerbereinigung-app, damit Sie das Dialogfeld verwenden können zum Angeben von Optionen für die Verwendung später Speichern der Einstellungen in den Satz **1**, geben Sie Folgendes ein:

```
cleanmgr /sageset:1
```

Zum Ausführen der Datenträgerbereinigung und die Optionen, die Sie angegeben haben, mit dem Cleanmgr /sageset:1 Befehl einschließen möchten, geben Sie Folgendes ein:

```
cleanmgr /sagerun:1
```

Auszuführende ```cleanmgr /sageset:1``` und ```cleanmgr /sagerun:1``` zusammen geben:

```
cleanmgr /tuneup:1
```

## <a name="additional-references"></a>Weitere Verweise

[Freigeben von Speicherplatz auf dem Laufwerk in Windows 10](https://support.microsoft.com/en-us/help/12425/windows-10-free-up-drive-space)
