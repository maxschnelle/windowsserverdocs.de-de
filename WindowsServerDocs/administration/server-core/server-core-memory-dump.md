---
title: Konfigurieren von Speicher Abbild Dateien für die Server Core-Installation
description: Erfahren Sie, wie Sie Speicher Abbild Dateien für eine Server Core-Installation von Windows Server konfigurieren.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: 0cea3118abce156acdd9ad933518015a25f8afbf
ms.sourcegitcommit: 216d97ad843d59f12bf0b563b4192b75f66c7742
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476551"
---
# <a name="configure-memory-dump-files-for-server-core-installation"></a>Konfigurieren von Speicher Abbild Dateien für die Server Core-Installation

>Gilt für: Windows Server 2019, Windows Server 2016 und Windows Server (halbjährlicher Kanal)

Führen Sie die folgenden Schritte aus, um ein Speicher Abbild für die Server Core-Installation zu konfigurieren. 

## <a name="step-1-disable-the-automatic-system-page-file-management"></a>Schritt 1: Deaktivieren der automatischen Dateiverwaltung von System Seiten

Der erste Schritt besteht darin, die Systemfehler-und Wiederherstellungsoptionen manuell zu konfigurieren. Dies ist erforderlich, um die restlichen Schritte abzuschließen.

Führen Sie den folgenden Befehl aus: 

```
wmic computersystem set AutomaticManagedPagefile=False
```
 
## <a name="step-2-configure-the-destination-path-for-a-memory-dump"></a>Schritt 2: Konfigurieren des Zielpfads für ein Speicher Abbild

Sie müssen nicht über die Auslagerungs Datei auf der Partition verfügen, auf der das Betriebssystem installiert ist. Wenn Sie die Auslagerungs Datei auf einer anderen Partition platzieren möchten, müssen Sie einen neuen Registrierungs Eintrag mit dem Namen **dedikateddumpfile**erstellen. Sie können die Größe der Auslagerungs Datei mit dem Registrierungs Eintrag **DumpFileSize** definieren. Führen Sie die folgenden Schritte aus, um die Registrierungseinträge dedikateddumpfile und DumpFileSize zu erstellen: 

1. Führen Sie an der Eingabeaufforderung den Befehl **Regedit** aus, um den Registrierungs-Editor zu öffnen.
2. Suchen Sie den folgenden Registrierungsunterschlüssel, und klicken Sie darauf: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl
3. Klicken Sie **> neue > Zeichen folgen Wert bearbeiten**.
4. Benennen Sie den neuen Wert **dediereddumpfile**, und drücken Sie dann die EINGABETASTE.
5. Klicken Sie mit der rechten Maustaste auf **dedialisieddumpfile**, und klicken Sie dann auf **ändern**.
6. Geben Sie im Feld **Wert Datentyp**  **\<Laufwerk\>:\\\<dediereddumpfile\>. sys**ein, und klicken Sie dann auf **OK**.

   >[!NOTE] 
   > Ersetzen \<Sie\> Drive durch ein Laufwerk, das über ausreichend Speicherplatz für die Auslagerungs Datei \<verfügt, und ersetzen Sie dedipdumpfile. dmp\> durch den vollständigen Pfad zu der dedizierten Datei.
 
7. Klicken Sie auf **> neuen > DWORD-Wert bearbeiten**.
8. Geben Sie **DumpFileSize**ein, und drücken Sie dann die EINGABETASTE.
9. Klicken Sie mit der rechten Maustaste auf **DumpFileSize**, und klicken Sie dann auf **ändern**.
10. Klicken Sie unter **DWORD-Wert bearbeiten**unter **Basis**auf **Dezimal**.
11. Geben Sie unter **Wertdaten**den entsprechenden Wert ein, und klicken Sie dann auf **OK**.
    >[!NOTE]
    > Die Größe der Dumpdatei liegt in Megabyte (MB).
12. Beenden Sie den Registrierungs-Editor.

Nachdem Sie den Partitions Speicherort des Speicher Abbilds bestimmt haben, konfigurieren Sie den Zielpfad für die Auslagerungs Datei. Führen Sie den folgenden Befehl aus, um den aktuellen Zielpfad für die Auslagerungs Datei anzuzeigen:

```
wmic RECOVEROS get DebugFilePath
```

Das Standardziel für "Debug **FilePath** " ist%SystemRoot%\Memory.dmp. Um den aktuellen Zielpfad zu ändern, führen Sie den folgenden Befehl aus:

```
wmic RECOVEROS set DebugFilePath = <FilePath>
```

Legen \<Sie filePath\> auf den Zielpfad fest. Der folgende Befehl legt z. b. den Zielpfad des Speicher Abbilds auf "c:\WINDOWS\MEMORY" fest. DMP 

```
wmic RECOVEROS set DebugFilePath = C:\WINDOWS\MEMORY.DMP
```
 
## <a name="step-3-set-the-type-of-memory-dump"></a>Schritt 3: Typ des Speicher Abbilds festlegen

Bestimmen Sie den Typ des Speicher Abbilds, das für den Server konfiguriert werden soll. Führen Sie den folgenden Befehl aus, um den aktuellen speicherdumptyp anzuzeigen:

```
wmic RECOVEROS get DebugInfoType
```

Führen Sie den folgenden Befehl aus, um den aktuellen Speicherdump-Typ zu ändern: 

```
wmic RECOVEROS set DebugInfoType = <Value>
```

\<Der\> Wert kann wie unten definiert 0, 1, 2 oder 3 sein.

- 0: Deaktivieren Sie das Entfernen eines Speicher Abbilds.
- 1: Vollständiges Speicher Abbild. Zeichnet den gesamten Inhalt des System Arbeitsspeichers auf, wenn der Computer unerwartet angehalten wird. Ein vollständiges Speicher Abbild kann Daten aus Prozessen enthalten, die bei der Erfassung des Speicher Abbilds ausgeführt wurden.
- 2: Kernel Speicher Abbild (Standard). Zeichnet nur den Kernelspeicher auf. Dies beschleunigt den Prozess der Aufzeichnung von Informationen in einer Protokolldatei, wenn der Computer unerwartet angehalten wird.
- 3: Kleines Speicher Abbild. Zeichnet die kleinsten nützlichen Informationen auf, anhand derer ermittelt werden kann, warum der Computer unerwartet angehalten wurde.

## <a name="step-4-configure-the-server-to-restart-automatically-after-generating-a-memory-dump"></a>Schritt 4: Konfigurieren des Servers für den automatischen Neustart nach dem Erstellen eines Speicher Abbilds

Standardmäßig wird der Server automatisch neu gestartet, nachdem ein Speicher Abbild generiert wurde. Führen Sie den folgenden Befehl aus, um die aktuelle Konfiguration anzuzeigen:

```
wmic RECOVEROS get AutoReboot
```

Wenn der Wert für **AutoReboot** den Wert true hat, wird der Server nach dem Erstellen eines Speicher Abbilds automatisch neu gestartet. Es ist keine Konfiguration erforderlich, und Sie können mit dem nächsten Schritt fortfahren.

Wenn der Wert für **AutoReboot** den Wert false hat, wird der Server nicht automatisch neu gestartet. Führen Sie den folgenden Befehl aus, um den Wert zu ändern:

```
wmic RECOVEROS set AutoReboot = true
```
 
## <a name="step-5-configure-the-server-to-overwrite-the-existing-memory-dump-file"></a>Schritt 5: Konfigurieren des Servers zum Überschreiben der vorhandenen Speicher Abbild Datei

Standardmäßig überschreibt der Server die vorhandene Speicher Abbild Datei, wenn ein neuer erstellt wird. Führen Sie den folgenden Befehl aus, um zu ermitteln, ob vorhandene Speicher Abbild Dateien bereits überschrieben werden können:

```
wmic RECOVEROS get OverwriteExistingDebugFile
```

Wenn der Wert 1 ist, wird die vorhandene Speicher Abbild Datei vom Server überschrieben. Es ist keine Konfiguration erforderlich, und Sie können mit dem nächsten Schritt fortfahren.

Wenn der Wert 0 ist, wird die vorhandene Speicher Abbild Datei vom Server nicht überschrieben. Führen Sie den folgenden Befehl aus, um den Wert zu ändern: 

```
wmic RECOVEROS set OverwriteExistingDebugFile = 1
```
 
## <a name="step-6-set-an-administrative-alert"></a>Schritt 6: Festlegen einer administrativen Warnung

Stellen Sie fest, ob eine administrative Warnung geeignet ist, und legen Sie **sendadminalert** entsprechend fest. Um den aktuellen Wert für sendadminalert anzuzeigen, führen Sie den folgenden Befehl aus:

```
wmic RECOVEROS get SendAdminAlert
```

Die möglichen Werte für sendadminalert sind true oder false. Führen Sie den folgenden Befehl aus, um den vorhandenen sendadminalert-Wert in true zu ändern: 

```
wmic RECOVEROS set SendAdminAlert = true
```
 
## <a name="step-7-set-the-memory-dumps-page-file-size"></a>Schritt 7: Festlegen der Größe der Auslagerungs Datei für den Arbeitsspeicher

Führen Sie einen der folgenden Befehle aus, um die aktuellen Seiten Datei Einstellungen zu überprüfen:

   ```
   wmic.exe pagefile
   ```

   oder

   ```
   wmic.exe pagefile list /format:list
   ```

Führen Sie z. b. den folgenden Befehl aus, um die anfängliche und die maximale Größe der Auslagerungs Datei zu konfigurieren:

```
wmic pagefileset where name="c:\\pagefile.sys" set InitialSize=1000,MaximumSize=5000
```

## <a name="step-8-configure-the-server-to-generate-a-manual-memory-dump"></a>Schritt 8: Konfigurieren des Servers für die Generierung eines manuellen Speicher Abbilds

Sie können ein Speicher Abbild mithilfe einer PS/2-Tastatur manuell generieren. Diese Funktion ist standardmäßig deaktiviert und nicht für USB (Universal Serial Bus)-Tastaturen verfügbar.

Führen Sie den folgenden Befehl aus, um manuelle Speicher Abbilder mithilfe einer PS/2-Tastatur zu aktivieren:

```
reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\i8042prt\Parameters /v CrashOnCtrlScroll /t REG_DWORD /d 1 /f
```

Führen Sie den folgenden Befehl aus, um zu ermitteln, ob die Funktion ordnungsgemäß aktiviert wurde:

```
Reg query HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ i8042prt \ Parameters / v CrashOnCtrlScroll
```

Sie müssen den Server neu starten, damit die Änderungen wirksam werden. Sie können den Server neu starten, indem Sie den folgenden Befehl ausführen:

```
Shutdown / r / t 0
```

Sie können manuelle Speicher Abbilder mit einer PS/2-Tastatur generieren, die mit dem Server verbunden ist, indem Sie die Rechte STRG-Taste gedrückt halten, während Sie die scrollsperrtaste zweimal drücken. Dadurch wird die Fehlerüberprüfung des Computers mit dem Fehlercode 0xe2 erstellt. Nachdem Sie den Server neu gestartet haben, wird eine neue Dumpdatei im Zielpfad angezeigt, den Sie in Schritt 2 erstellt haben.

## <a name="step-9-verify-that-memory-dump-files-are-being-created-correctly"></a>Schritt 9: Überprüfen Sie, ob die Speicher Abbild Dateien ordnungsgemäß erstellt werden

Sie können die Utlity Dumpchk. exe verwenden, um zu überprüfen, ob die Speicher Abbild Dateien ordnungsgemäß erstellt werden. Das Hilfsprogramm "Dumpchk. exe" wird nicht mit der Server Core-Installationsoption installiert, sodass Sie es von einem Server mit Desktop Darstellung oder Windows 10 ausführen müssen. Außerdem müssen die Debugtools für Windows-Produkte installiert sein.  

Mit dem Hilfsprogramm "Dumpchk. exe" können Sie die Speicher Abbild Datei von der Server Core-Installation von Windows Server 2008 auf den anderen Computer übertragen, indem Sie das Mittel ihrer Wahl verwenden.

> [!WARNING]
> Auslagerungs Dateien können sehr groß sein, daher sollten Sie die Übertragungsmethode und die von der Methode benötigten Ressourcen sorgfältig berücksichtigen.
 

Weitere Verweise

Allgemeine Informationen zur Verwendung von Speicher Abbild Dateien finden Sie unter Übersicht über die [Optionen für die Speicher Abbild Datei für Windows](https://support.microsoft.com/help/254649/overview-of-memory-dump-file-options-for-windows).

Weitere Informationen zu dedizierten Dumpdateien finden Sie unter Gewusst [wie: Verwenden des Registrierungs Werts "dedikateddeumpfile" zum überwinden von Speicherplatz Beschränkungen auf dem Systemlaufwerk beim Erfassen eines Systemspeicher Abbilds](https://blogs.msdn.microsoft.com/ntdebugging/2010/04/02/how-to-use-the-dedicateddumpfile-registry-value-to-overcome-space-limitations-on-the-system-drive-when-capturing-a-system-memory-dump/).



