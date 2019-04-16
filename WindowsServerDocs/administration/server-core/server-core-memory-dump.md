---
title: Konfigurieren von Speicher Dump-Dateien für die Server Core-installation
description: Informationen Sie zum Konfigurieren von Speicher Dump-Dateien für die Server Core-Installationsoption von Windows Server
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: bd22378ec7ce5a1ff4e39546246e6e85ca859c45
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/01/2018
ms.locfileid: "1448051"
---
# <a name="configure-memory-dump-files-for-server-core-installation"></a>Konfigurieren von Speicher Dump-Dateien für die Server Core-installation

>Gilt für: Windows Server (Semi-Annual Channel) and Windows Server 2016

Verwenden Sie die folgenden Schritte aus, um ein Speicherabbild für Ihre Server Core-Installation zu konfigurieren. 

## <a name="step-1-disable-the-automatic-system-page-file-management"></a>Schritt 1: Deaktivieren der automatischen System Seite dateiverwaltung

Der erste Schritt besteht darin Ihr System Wiederherstellungsoptionen manuell konfigurieren. Dies ist erforderlich, um die verbleibenden Schritte auszuführen.

Führen Sie den folgenden Befehl aus: 

```
wmic computersystem set AutomaticManagedPagefile=False
```
 
## <a name="step-2-configure-the-destination-path-for-a-memory-dump"></a>Schritt 2: Konfigurieren Sie den Zielpfad für ein Speicherabbild

Sie müssen nicht die Auslagerungsdatei auf der Partition haben, auf dem das Betriebssystem installiert ist. Um die Seitendatei auf einer anderen Partition verschieben, müssen Sie einen neuen Registrierungseintrag mit dem Namen **DedicatedDumpFile**erstellen. Sie können die Größe der Auslagerungsdatei mit der Registrierungseintrag **DumpFileSize** definieren. Gehen Sie folgendermaßen vor, um die Registrierungseinträge DedicatedDumpFile und DumpFileSize zu erstellen: 

1. Führen Sie an der Befehlszeile den Befehl **regedit ein** , um den Registrierungs-Editor zu öffnen.
2. Suchen, und klicken Sie dann auf den folgenden Registrierungsunterschlüssel: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl
3. Klicken Sie auf **Bearbeiten > Neu > Zeichenfolgenwert**.
4. Benennen Sie den Wert **DedicatedDumpFile**, und drücken Sie die EINGABETASTE.
5. Mit der rechten Maustaste **DedicatedDumpFile**, und klicken Sie dann auf **Ändern**.
6. **Wertdaten** vom Typ **\ < Laufwerk\ >: \\\ < Dedicateddumpfile.sys\ >**, und klicken Sie dann auf **OK**.

   >[!NOTE] 
   > Ersetzen Sie \ < Laufwerk\ > mit einem Laufwerk mit genügend Datenträger Speicherplatz für die Auslagerungsdatei, und Ersetzen Sie \ < Dedicateddumpfile.dmp\ > durch den vollständigen Pfad zur Datei dedizierten.
 
7. Klicken Sie auf **Bearbeiten > Neu > DWORD-Wert**.
8. Geben Sie **DumpFileSize**, und drücken Sie die EINGABETASTE.
9. Mit der rechten Maustaste **DumpFileSize**, und klicken Sie dann auf **Ändern**.
10. Klicken Sie im Dialogfeld **DWORD-Wert bearbeiten**klicken Sie unter **Base**auf **Dezimal**.
11. **Wertdaten**Geben Sie den entsprechenden Wert ein, und klicken Sie dann auf **OK**.
   >[!NOTE]
   > Die Größe der Dumpdatei wird in Megabyte (MB).
12. Beenden Sie den Registrierungs-Editor.

Nachdem Sie den Speicherort der Partition von der Speicherabbild ermittelt haben, konfigurieren Sie im Zielpfad für Datei der Seite. Um den aktuellen Zielpfad für Datei der Seite anzuzeigen, führen Sie den folgenden Befehl ein:

```
wmic RECOVEROS get DebugFilePath
```

Das Standardziel für **DebugFilePath** ist % systemroot%\memory.dmp. Um die aktuelle Zielpfad zu ändern, führen Sie den folgenden Befehl ein:

```
wmic RECOVEROS set DebugFilePath = <FilePath>
```

Legen Sie \ < FilePath\ > im Zielpfad. Der folgende Befehl wird beispielsweise Arbeitsspeicher Dump Zielpfad auf C:\WINDOWS\MEMORY. DMP: 

```
wmic RECOVEROS set DebugFilePath = C:\WINDOWS\MEMORY.DMP
```
 
## <a name="step-3-set-the-type-of-memory-dump"></a>Schritt 3: Legen Sie den Typ der Speicherabbild

Bestimmen der Art der Speicherabbild für Ihren Server konfigurieren. Um den aktuellen Speicher Dump Typ anzuzeigen, führen Sie den folgenden Befehl ein:

```
wmic RECOVEROS get DebugInfoType
```

Um den aktuellen Speicher Dump-Typ zu ändern, führen Sie den folgenden Befehl aus: 

```
wmic RECOVEROS set DebugInfoType = <Value>
```

\ < Value\ > kann 0, 1, 2 oder 3, wie unten definiert.

- 0: Deaktivieren Sie das Entfernen der ein Speicherabbild.
- 1: vollständige Speicherabbild. Zeichnet gesamten Inhalt des Systemspeichers auf, wenn Ihr Computer unerwartet beendet wird. Ein vollständiges Speicherabbild enthalten möglicherweise Daten von Prozessen, die ausgeführt wurden, wenn das Speicherabbild erfasst wurden.
- 2: Kernelspeicherabbild (Standard). Zeichnet nur den Kernelspeicher auf. Dies beschleunigt die Informationen in einer Protokolldatei aufzeichnen, wenn Ihr Computer unerwartet beendet wird.
- 3: kleines Speicherabbild. Zeichnet den kleinsten Satz nützlicher Informationen, die dazu ermitteln beitragen kann, warum Sie Ihren Computer unerwartet beendet.

## <a name="step-4-configure-the-server-to-restart-automatically-after-generating-a-memory-dump"></a>Schritt 4: Konfigurieren des Servers automatisch neu starten, nachdem ein Speicherabbild generieren

In der Standardeinstellung der Server wird automatisch neu gestartet, nachdem ein Speicherabbild generiert wird. Um die aktuelle Konfiguration anzuzeigen, führen Sie den folgenden Befehl aus:

```
wmic RECOVEROS get AutoReboot
```

Wenn der Wert für **AutoReboot** auf true festgelegt ist, wird der Server automatisch neu gestartet, nachdem ein Speicherabbild generiert. Es ist keine Konfiguration erforderlich, und Sie mit dem nächsten Schritt fortfahren können.

Wenn der Wert für **AutoReboot** auf false festgelegt ist, wird der Server nicht automatisch neu gestartet. Führen Sie den folgenden Befehl aus, um den Wert zu ändern:

```
wmic RECOVEROS set AutoReboot = true
```
 
## <a name="step-5-configure-the-server-to-overwrite-the-existing-memory-dump-file"></a>Schritt 5: Konfigurieren des Servers, um die vorhandenen Kernelspeicherabbild-Datei überschreiben

Standardmäßig überschreibt der Server der vorhandenen Speicherabbild, wenn eine neue erstellt wird. Um festzustellen, ob bereits vorhandene Arbeitsspeicher Abbilddateien konfiguriert sind, überschrieben werden soll, führen Sie den folgenden Befehl aus:

```
wmic RECOVEROS get OverwriteExistingDebugFile
```

Wenn der Wert 1 ist, wird der Server die vorhandenen Kernelspeicherabbild-Datei überschrieben. Es ist keine Konfiguration erforderlich, und Sie können mit dem nächsten Schritt fortfahren.

Wenn der Wert 0 ist, wird nicht der Server die vorhandenen Kernelspeicherabbild-Datei überschreiben. Führen Sie den folgenden Befehl aus, um den Wert zu ändern: 

```
wmic RECOVEROS set OverwriteExistingDebugFile = 1
```
 
## <a name="step-6-set-an-administrative-alert"></a>Schritt 6: Festlegen einer administrativen Benachrichtigung

Bestimmen, ob eine administrative Warnung geeignet ist und **SendAdminAlert** entsprechend festgelegt. Um den aktuellen Wert für SendAdminAlert anzuzeigen, führen Sie den folgenden Befehl aus:

```
wmic RECOVEROS get SendAdminAlert
```

Die möglichen Werte für SendAdminAlert sind TRUE oder FALSE. Um den vorhandenen SendAdminAlert Wert auf "true" zu ändern, führen Sie den folgenden Befehl aus: 

```
wmic RECOVEROS set SendAdminAlert = true
```
 
## <a name="step-7-set-the-memory-dumps-page-file-size"></a>Schritt 7: Festlegen der Speicherabbild Größe der Auslagerungsdatei

Um die aktuelle Seite dateieinstellungen überprüfen möchten, führen Sie einen der folgenden Befehle aus:

   ```
   wmic.exe pagefile
   ```

   oder

   ```
   wmic.exe pagefile list /format:list
   ```

Führen Sie beispielsweise den folgenden Befehl aus, um die Anfangs- und maximale Größe der Auslagerungsdatei konfigurieren:

```
wmic pagefileset where name="c:\\pagefile.sys" set InitialSize=1000,MaximumSize=5000
```

## <a name="step-8-configure-the-server-to-generate-a-manual-memory-dump"></a>Schritt 8: Konfigurieren des Servers, ein manuelles Speicherabbild generieren

Sie können ein Speicherabbild manuell mithilfe der Tastatur PS/2 generieren. Dieses Feature ist standardmäßig deaktiviert, und es ist nicht verfügbar für Tastaturen (USB = Universal Serial Bus).

Schreibt die manuelle Speicher aktivieren, um mithilfe der Tastatur PS/2, führen Sie den folgenden Befehl:

```
reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\i8042prt\Parameters /v CrashOnCtrlScroll /t REG_DWORD /d 1 /f
```

Um festzustellen, ob das Feature ordnungsgemäß aktiviert wurde, führen Sie den folgenden Befehl aus:

```
Reg query HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ i8042prt \ Parameters / v CrashOnCtrlScroll
```

Sie müssen den Server, damit die Änderungen wirksam werden neu starten. Sie können den Server neu starten, indem Sie den folgenden Befehl ausführen:

```
Shutdown / r / t 0
```

Sie können manuelle Arbeitsspeicher speichert mit einer PS/2-Tastatur generieren, die gedrückt halten die rechts STRG-Taste und drücken die Rollen-Taste zweimal auf Ihrem Server verbunden ist. Dadurch wird den Computer mit dem Fehlercode 0xE2 Kontrollkästchen Fehler. Nachdem Sie den Server neu starten, wird eine neue Abbilddatei im Zielpfad, den Sie in Schritt 2 hergestellt angezeigt.

## <a name="step-9-verify-that-memory-dump-files-are-being-created-correctly"></a>Schritt 9: Überprüfen Sie, ob diese Speicherabbild, die Dateien ordnungsgemäß erstellt werden

Die dumpchk.exe Utlity können Sie sicherstellen, dass die Speicherabbilddateien ordnungsgemäß erstellt werden. Das Dienstprogramm dumpchk.exe ist nicht mit der Server Core-Installationsoption installiert, müssen Sie es von einem Server mit der Desktopdarstellung oder von Windows 10 ausführen. Darüber hinaus müssen die Debugtools für Windows-Produkte installiert werden.  

Die dumpchk.exe können Sie mithilfe von das Medium Ihrer Wahl der Speicherabbild aus der Server Core-Installation von Windows Server 2008 auf dem anderen Computer übertragen.

> [!WARNING]
> Auslagerungsdateien können sehr groß sein, sorgfältig berücksichtigen Sie die Übertragung-Methode und die Ressourcen, die-Methode erfordert.
 

Weitere Informationsquellen

Allgemeine Informationen zur Verwendung von Arbeitsspeicher Abbilddateien finden Sie unter [Übersicht über die Dateioptionen für das Speicherabbild für Windows](https://support.microsoft.com/help/254649/overview-of-memory-dump-file-options-for-windows).

Weitere Informationen zu dedizierten Abbilddateien finden Sie unter [Gewusst wie: Verwenden Sie den Registrierungswert DedicatedDeumpFile um Platzes auf dem Systemlaufwerk während der Aufnahme ein Speicherabbild System zu umgehen](https://blogs.msdn.microsoft.com/ntdebugging/2010/04/02/how-to-use-the-dedicateddumpfile-registry-value-to-overcome-space-limitations-on-the-system-drive-when-capturing-a-system-memory-dump/).



