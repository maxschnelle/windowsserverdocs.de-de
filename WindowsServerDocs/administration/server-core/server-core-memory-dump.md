---
title: Konfigurieren von Speicherabbilddateien für Server Core-installation
description: Informationen Sie zum Konfigurieren von Speicher-Abbilddateien für eine Server Core-Installation von Windows Server
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: bd22378ec7ce5a1ff4e39546246e6e85ca859c45
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828841"
---
# <a name="configure-memory-dump-files-for-server-core-installation"></a>Konfigurieren von Speicherabbilddateien für Server Core-installation

>Gilt für: WindowsServer (Halbjährlicher Kanal) und WindowsServer 2016

Verwenden Sie die folgenden Schritte aus, um ein Speicherabbild für die Server Core-Installation zu konfigurieren. 

## <a name="step-1-disable-the-automatic-system-page-file-management"></a>Schritt 1: Deaktivieren Sie die automatische systemprüfung Seite dateiverwaltung

Der erste Schritt besteht Ihr System Wiederherstellungsoptionen manuell konfigurieren. Dies ist erforderlich, um die verbleibenden Schritte auszuführen.

Führen Sie den folgenden Befehl aus: 

```
wmic computersystem set AutomaticManagedPagefile=False
```
 
## <a name="step-2-configure-the-destination-path-for-a-memory-dump"></a>Schritt 2: Konfigurieren Sie den Zielpfad für ein Speicherabbild

Sie müssen nicht die Auslagerungsdatei auf der Partition haben, in denen das Betriebssystem installiert ist. Um die Auslagerungsdatei auf einer anderen Partition zu versetzen, müssen Sie einen neuen Registrierungseintrag, mit dem Namen erstellen **DedicatedDumpFile**. Sie können die Größe der Auslagerungsdatei definieren, mit der **DumpFileSize** Registrierungseintrag. Um die Registrierungseinträge DedicatedDumpFile und DumpFileSize zu erstellen, gehen Sie folgendermaßen vor: 

1. Führen Sie an der Eingabeaufforderung die **"regedit"** Befehl aus, um den Registrierungs-Editor zu öffnen.
2. Suchen Sie den folgenden Registrierungsunterschlüssel, und klicken Sie darauf: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl
3. Klicken Sie auf **Bearbeiten > Neu > Zeichenfolgenwert**.
4. Benennen Sie den Wert **DedicatedDumpFile**, und drücken Sie dann die EINGABETASTE.
5. Mit der rechten Maustaste **DedicatedDumpFile**, und klicken Sie dann auf **ändern**.
6. In **Wertdaten** Typ  **\<Laufwerk\>:\\\<Dedicateddumpfile.sys\>**, und klicken Sie dann auf **OK**.

   >[!NOTE] 
   > Ersetzen Sie dies \<Laufwerk\> mit einem Laufwerk mit genügend Datenträger Speicherplatz für die Auslagerungsdatei, und Ersetzen Sie \<Dedicateddumpfile.dmp\> durch den vollständigen Pfad zu der dedizierten Datei.
 
7. Klicken Sie auf **Bearbeiten > Neu > DWORD-Wert**.
8. Typ **DumpFileSize**, und drücken Sie dann die EINGABETASTE.
9. Mit der rechten Maustaste **DumpFileSize**, und klicken Sie dann auf **ändern**.
10. In **DWORD-Wert bearbeiten**unter **Base**, klicken Sie auf **Decimal**.
11. In **Wertdaten**, geben Sie den entsprechenden Wert ein, und klicken Sie dann auf **OK**.
   >[!NOTE]
   > Die Größe der Dumpdatei wird in Megabyte (MB).
12. Beenden Sie den Registrierungs-Editor.

Nachdem Sie den Speicherort der Partition, der das Speicherabbild des ermittelt haben, konfigurieren Sie den Zielpfad für die Auslagerungsdatei. Um den aktuellen Zielpfad für die Auslagerungsdatei anzuzeigen, führen Sie den folgenden Befehl aus:

```
wmic RECOVEROS get DebugFilePath
```

Das Standardziel für **DebugFilePath** % systemroot%\memory.dmp ist. Um den aktuellen Zielpfad zu ändern, führen Sie den folgenden Befehl aus:

```
wmic RECOVEROS set DebugFilePath = <FilePath>
```

Legen Sie \<"FilePath"\> in den Zielpfad. Beispielsweise legt der folgende Befehl den Memory Dump Zielpfad auf C:\WINDOWS\MEMORY. DMP: 

```
wmic RECOVEROS set DebugFilePath = C:\WINDOWS\MEMORY.DMP
```
 
## <a name="step-3-set-the-type-of-memory-dump"></a>Schritt 3: Legen Sie den Typ des Speicherabbilds

Bestimmen Sie den Typ des Speicherabbilds für Ihren Server konfigurieren. Um den aktuellen Memory Dump Typ anzuzeigen, führen Sie den folgenden Befehl aus:

```
wmic RECOVEROS get DebugInfoType
```

Um den aktuellen Memory Dump-Typ zu ändern, führen Sie den folgenden Befehl aus: 

```
wmic RECOVEROS set DebugInfoType = <Value>
```

\<Wert\> kann sein, 0, 1, 2 oder 3, wie unten definiert.

- 0: Deaktivieren Sie das Entfernen eines Speicherabbilds.
- 1: Vollständiges Speicherabbild. Zeichnet den Inhalt des Systemspeichers auf, wenn Ihr Computer unerwartet anhält. Ein vollständiges Speicherabbild enthält möglicherweise Daten von Prozessen, die ausgeführt wurden, wenn das Speicherabbild erfasst wurde.
- 2: Kernel-Speicherabbild (Standard). Zeichnet nur den Kernelspeicher auf. Dies beschleunigt den Prozess des Aufzeichnens von Informationen in einer Protokolldatei, wenn Ihr Computer unerwartet beendet wird.
- 3: Kleines Speicherabbild. Zeichnet die kleinste Menge der nützlichen Informationen, mit deren Hilfe möglicherweise herausfinden, warum es sich bei Ihrem Computer unerwartet beendet wurde.

## <a name="step-4-configure-the-server-to-restart-automatically-after-generating-a-memory-dump"></a>Schritt 4: Konfigurieren Sie den Server automatisch neu gestartet wird nach dem Generieren eines Speicherabbilds

Standardmäßig startet der Server automatisch neu, nachdem ein Speicherabbild generiert. Um die aktuelle Konfiguration anzuzeigen, führen Sie den folgenden Befehl aus:

```
wmic RECOVEROS get AutoReboot
```

Wenn der Wert für **AutoReboot** ist "true", der Server startet automatisch neu, nach dem Generieren eines Speicherabbilds. Ist keine Konfiguration erforderlich, und Sie können mit dem nächsten Schritt fortfahren.

Wenn der Wert für **AutoReboot** ist "false", der Server wird nicht automatisch neu gestartet. Führen Sie den folgenden Befehl zum Ändern des Werts:

```
wmic RECOVEROS set AutoReboot = true
```
 
## <a name="step-5-configure-the-server-to-overwrite-the-existing-memory-dump-file"></a>Schritt 5: Konfigurieren Sie den Server zum Überschreiben der vorhandenen Speicherabbilddatei

Standardmäßig überschreibt der Server die vorhandene Speicherabbilddatei, wenn eine neue, die eine erstellt wird. Um festzustellen, ob vorhandene Speicherabbilddateien bereits konfiguriert sind, überschrieben werden sollen, führen Sie den folgenden Befehl aus:

```
wmic RECOVEROS get OverwriteExistingDebugFile
```

Wenn der Wert 1 ist, wird der Server die vorhandene Speicherabbilddatei überschrieben. Ist keine Konfiguration erforderlich, und Sie können mit dem nächsten Schritt fortfahren.

Wenn der Wert 0 ist, wird nicht der Server die vorhandene Speicherabbilddatei überschreiben. Führen Sie den folgenden Befehl zum Ändern des Werts: 

```
wmic RECOVEROS set OverwriteExistingDebugFile = 1
```
 
## <a name="step-6-set-an-administrative-alert"></a>Schritt 6: Richten Sie eine administrative Warnung

Zu bestimmen, ob eine administrative Warnung entsprechenden und festgelegte **SendAdminAlert** entsprechend. Um den aktuellen Wert SendAdminAlert anzuzeigen, führen Sie den folgenden Befehl aus:

```
wmic RECOVEROS get SendAdminAlert
```

Die möglichen Werte für SendAdminAlert sind "true" oder "false". Um den vorhandenen SendAdminAlert-Wert auf "true" zu ändern, führen Sie den folgenden Befehl aus: 

```
wmic RECOVEROS set SendAdminAlert = true
```
 
## <a name="step-7-set-the-memory-dumps-page-file-size"></a>Schritt 7: Legen Sie das Speicherabbild Größe der Auslagerungsdatei

Um die aktuellen seiteneinstellungen für die Datei zu überprüfen, führen Sie einen der folgenden Befehle aus:

   ```
   wmic.exe pagefile
   ```

   oder

   ```
   wmic.exe pagefile list /format:list
   ```

Führen Sie beispielsweise den folgenden Befehl so konfigurieren Sie die anfängliche und maximale Größe der Auslagerungsdatei:

```
wmic pagefileset where name="c:\\pagefile.sys" set InitialSize=1000,MaximumSize=5000
```

## <a name="step-8-configure-the-server-to-generate-a-manual-memory-dump"></a>Schritt 8: Konfigurieren Sie den Server zum Generieren eines manuellen Speicherabbilds

Sie können ein Speicherabbild manuell generieren, mit einem PS/2-Tastatur. Dieses Feature ist standardmäßig deaktiviert, und es ist nicht verfügbar für Serial Bus USB (Universal) Tastaturen.

Gibt mit einem PS/2-Tastatur, und führen Sie den folgenden Befehl, um manuelle Arbeitsspeicher zu aktivieren:

```
reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\i8042prt\Parameters /v CrashOnCtrlScroll /t REG_DWORD /d 1 /f
```

Um festzustellen, ob das Feature ordnungsgemäß aktiviert wurde, führen Sie den folgenden Befehl aus:

```
Reg query HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ i8042prt \ Parameters / v CrashOnCtrlScroll
```

Sie müssen den Server für die Änderungen wirksam werden neu starten. Sie können den Server neu starten, durch den folgenden Befehl ausführen:

```
Shutdown / r / t 0
```

Sie können mit einem PS/2-Tastatur manuelle Speicherabbilder generieren, die die rechte STRG-Taste gedrückt halten, und drücken die Rollen-Taste zwei Mal auf Ihrem Server verbunden ist. Dadurch wird den Computer überprüfen, mit dem Fehlercode 0xE2 Fehler. Nachdem Sie den Server neu starten, wird eine neue Dumpdatei in den Zielpfad an, dem Sie in Schritt 2 eingerichtet angezeigt.

## <a name="step-9-verify-that-memory-dump-files-are-being-created-correctly"></a>Schritt 9: Stellen Sie sicher, Speicherabbild, die Dateien ordnungsgemäß erstellt werden

Sie können die dumpchk.exe Utlity verwenden, um sicherzustellen, dass die Speicherabbilddateien ordnungsgemäß erstellt werden. Das Hilfsprogramm dumpchk.exe ist nicht mit der Installationsoption Server Core installiert, müssen für die Ausführung von einem Server mit der Desktopdarstellung oder aus dem Windows 10. Darüber hinaus müssen die Debugtools für Windows-Produkte installiert werden.  

Die dumpchk.exe-Dienstprogramm können Sie mithilfe des Mediums Ihrer Wahl die Speicherabbilddatei aus der Server Core-Installation von Windows Server 2008 auf den anderen Computer übertragen.

> [!WARNING]
> Auslagerungsdateien können sehr groß sein, sollten Sie sorgfältig die Übertragung berücksichtigen, Methode und die Ressourcen, die Methode erforderlich ist.
 

Weitere Verweise

Allgemeine Informationen zur Verwendung von Speicherabbilddateien finden Sie unter [Überblick über die Speicherabbilddatei "Optionen" für Windows](https://support.microsoft.com/help/254649/overview-of-memory-dump-file-options-for-windows).

Weitere Informationen zum dedizierten von Dumpdateien finden Sie unter [wie Sie den Registrierungswert DedicatedDeumpFile zu verwenden, um Platz auf dem Systemlaufwerk zu überwinden, beim Aufzeichnen eines Speicherabbilds System](https://blogs.msdn.microsoft.com/ntdebugging/2010/04/02/how-to-use-the-dedicateddumpfile-registry-value-to-overcome-space-limitations-on-the-system-drive-when-capturing-a-system-memory-dump/).



