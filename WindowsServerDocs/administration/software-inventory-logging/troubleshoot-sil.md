---
title: Problembehandlung der Protokollierung des Softwarebestands
description: Beschreibt, wie häufig die Protokollierung des Softwarebestands auftretende Bereitstellungsprobleme zu beheben.
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: manage-software-inventory-logging
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
author: brentfor
ms.author: coreyp
manager: lizapo
ms.date: 10/16/2017
ms.openlocfilehash: 8a1fe22a1f721c0ac94096fe22c559c9bb092293
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435315"
---
# <a name="troubleshoot-software-inventory-logging"></a>Problembehandlung der Protokollierung des Softwarebestands 

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2019, Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2

## <a name="understanding-sil"></a>Grundlegendes zu SIL

Bevor Sie die Problembehandlung von SIL beginnen, benötigen Sie ein gutes Verständnis der zugehörigen Komponenten und deren Funktionsweise. Die folgenden Videos bieten eine Übersicht über SIL und SIL-Aggregator und deren Verwendung zum Weiterleiten und Inventurdaten von Bericht:

1. [Eine Einführung in die (SIL) (10:57) Protokollierung des Softwarebestands](https://channel9.msdn.com/Blogs/Regular-IT-Guy/An-Introduction-to-Software-Inventory-Logging-SIL)

2. [Software Softwareinventurprotokollierung: Einrichten des SIL-Aggregator (14:34)](https://channel9.msdn.com/Blogs/windowsserver/Software-Inventory-Logging-Setting-up-SIL-Aggregator)

3. [Software Softwareinventurprotokollierung: Aktivieren der SIL-Weiterleitung (7:20)](https://channel9.msdn.com/Blogs/windowsserver/Software-Inventory-Logging-Enabling-SIL-Forwarding)

## <a name="how-sil-data-flow-works"></a>Wie funktioniert flow SIL-Daten

Der SIL-Frameworks verfügt über zwei Hauptkomponenten und zwei Kommunikationskanäle. Fluss der Daten für beide Kanäle und zwischen beiden Komponenten für eine erfolgreiche SIL-Bereitstellung (Dies setzt voraus eine virtualisierte und Cloud-Umgebung – ausschließlich physische Umgebungen müssen nur eine der Kommunikationskanäle) erforderlich ist. Sie müssen verstehen, die Komponenten und Datenfluss von SIL ordnungsgemäß bereitgestellt. Nach dem beobachten die oben genannten übersichtsvideos an, werden Sie das Architekturdiagramm gesehen haben, das die Komponenten und den Fluss der Daten über beide Kanäle veranschaulicht. Orange Pfeile zeigen die Remoteabfragen über WinRM, grüne gestrichelten Pfeile zeigen die, dass HTTPS an den SIL-Aggregator von SIL in den einzelnen Knoten der WS-End sendet:

![](../media/software-inventory-logging/image1.png)

Wenn Sie ein Problem mit SIL auftreten, es wahrscheinlich eine Unterbrechung in den Fluss der Daten über die Kanäle und zwischen den Komponenten bezieht sich auf. Es folgen die häufigsten Probleme im Zusammenhang mit der Datenfluss im nächsten Abschnitt befolgt werden, indem Sie die Schritte zur Problembehandlung, um jedes dieser drei Probleme zu beheben:

-   **Problem 1 der Datenfluss** – **keine Daten im Bericht bei Verwendung mit dem Cmdlet Publish-SilReport** (oder in der Regel Daten fehlen).

-   **Problem 2 der Datenfluss** – **zu viele Server unter Unbekannter Host** im Bericht.

-   **Datenfluss Problem 3** – **zu viele virtuelle Computer unter physischen Hosts, die als unbekanntes Betriebssystem** in den Bericht bzw. ein Fehler ausgelöst, wenn mit **Publish-SilData** auf Windows-Servern, die mit der SIL.

## <a name="troubleshooting-data-flow-issues"></a>Problembehandlung von Data flow

Bevor Sie beginnen, müssen Sie wissen, wann die SIL-Aggregator ausprobieren der **Start-SilAggregator** Cmdlet.

>[!IMPORTANT]
>Es werden keine Daten im Bericht, bis der SQL-Daten-Cube auf 3: 00 Uhr lokale Systemzeit verarbeitet wird. Fahren Sie nicht mit Schritten zur Problembehandlung, bis der Cube Daten verarbeitet hat.

Wenn Sie Daten in den Bericht (oder aus dem Bericht fehlt) behandeln möchten, die neuer als beim letzten Mal ist der Cube verarbeitet oder führen Sie diese Schritte, um die SQL-Datencube in Echtzeit zu verarbeiten, vor dem Cube je (für eine Neuinstallation), verarbeitet hat :

1. Melden Sie sich als Administrator für SQL Server, und führen Sie **SSMS** an einer Eingabeaufforderung.
2. Stellen Sie eine Verbindung mit dem Datenbankmodul her.
3. Erweitern Sie **SQL Server-Agent** und erweitern Sie dann **Aufträge**.
4. Klicken Sie mit der rechten Maustaste auf **SILStagingRefresh** und wählen Sie dann **Auftrag starten bei Schritt**.
5. Klicken Sie auf **starten** und warten Sie, bis die Statusanzeige der veröffentlichungsaktualisierung abgeschlossen.
6. Öffnen Sie PowerShell als Administrator, und führen die **veröffentlichen Silreport - Openreport** Cmdlet.

Wenn weiterhin keine Daten im Bericht vorhanden sind, werden mit dem die drei Data Flow Problembehandlung fortfahren.

### <a name="data-flow-issue-1"></a>Data Flow Problem 1 

#### <a name="no-data-in-the-report-when-using-the-publish-silreport-cmdlet-or-data-is-generally-missing"></a>Keine Daten in den Bericht aus, wenn Sie das Cmdlet "Publish-SilReport" verwenden (oder in der Regel fehlen Daten)

Wenn Daten nicht vorhanden ist, ist es wahrscheinlich aufgrund des SQL-Data-Cubes müssen nicht noch nicht verarbeitet. Wenn sie zuletzt verarbeitet wurde, und Sie glauben, dass Daten, die nicht vorhanden ist, die vom Aggregator vor der Verarbeitung eines Cubes angekommen sind sollte, folgen Sie den Pfad der Daten in umgekehrter Reihenfolge. Wählen Sie einen eindeutigen Hostnamen und einer eindeutigen VM, um zu beheben. Der Datenpfad in umgekehrter Reihenfolge wäre **SILA Bericht** &lt; **SILA Datenbank** &lt; **SILA lokales Verzeichnis** &lt;  **physische Remotehost** oder **WS-VM, die mit SIL agenttask**.

#### <a name="check-to-see-if-data-is-in-the-database"></a>Überprüfen Sie, wenn Daten in der Datenbank

Es gibt zwei Möglichkeiten, Daten aus: **PowerShell** oder **SSMS**.

>[!Important]
>Wenn der Cube mindestens einmal verarbeitet hat, da SILA Daten in die Datenbank eingefügt, sollten diese Daten im Bericht berücksichtigt werden. Wenn keine Daten vorhanden, in der Datenbank sind klicken Sie dann entweder die physischen Hosts Abrufen tritt ein Fehler auf oder nichts über HTTPS oder beides empfangen wird.

 #### <a name="powershell"></a>PowerShell

1. Öffnen Sie PowerShell als Administrator, und führen die **Get-Silvmhost** -Cmdlet, und führen Sie dann **Get-Silaggregator**.

    >[!NOTE]
    >Die Ausgabe des **Get-Silaggregator** immer imitiert die **Windows Server-Registerkarte "Details"** für die Excel-Bericht. Erwarten Sie nicht zu, dass ein anderes Ergebnis.

2. Führen Sie **Get-Silvmhost**
   - Wenn es keine Hosts aufgelistet sind anschließend Hosts hinzufügen, mit der **hinzufügen-Silvmhost** Cmdlet.
   - Wenn Hosts, als aufgelistet sind **unbekannte**, navigieren Sie zu dem Problem 2. 
   d – Wenn Hosts aufgelistet sind, aber es gibt keine **"DateTime"** unter der **jüngsten Abrufs** Spalte, und klicken Sie dann auf Gehe zu **Problem 2** unten.

**Weitere verwandte Befehle**

**Get-SilAggregator - Computername &lt;Fqdn eines bekannten-Servers mithilfe von Push übertragen Daten&gt;** : Dadurch können Informationen aus der Datenbank zu einem Computer (VM) wird generiert, noch bevor der Cube verarbeitet wurde. Daher kann dieses Cmdlet verwendet werden, überprüfen Sie auf Daten in der Datenbank für einen Windows-Server, die Übertragung der SIL-Daten über HTTPS, vor dem oder ohne den Cubeprozess, um 3 Uhr (oder wenn Sie den Cube in Echtzeit aktualisiert nicht getan haben, wie am Anfang dieses Abschnitts beschrieben).

**Get-SilAggregator - %vmhostname &lt;Fqdn eines abgerufene physischen Hosts, wenn ein Wert in der jüngsten Abrufs-Spalte vorhanden ist, bei der Verwendung des Cmdlets Get-SilVmHost&gt;** : Dadurch können Informationen aus der Datenbank zu einem physischen Host wird generiert, noch bevor der Cube verarbeitet wurde.

#### <a name="ssms"></a>SSMS

n**prüfen, ob Daten von Hosts, die abgerufen werden:**
 
1. Open **SSMS** und Herstellen einer Verbindung mit der **Datenbank-Engine**.
2. Erweitern Sie **Datenbanken**, erweitern Sie die **SoftwareInventoryLogging** Datenbank **Tabellen**, klicken Sie mit der rechten Maustaste auf die **HostInfo** Tabelle und dann Wählen Sie die ersten 1000 Zeilen. 

    Wenn die Daten für einen oder mehrere Hosts in der Tabelle vorhanden sind, war Abfragen von dem/den angegebenen Hosts mindestens einmal erfolgreich.

   **Überprüfen Sie Daten auf virtuellen Computern und eigenständigen Servern, die Daten über HTTPS mithilfe von Push übertragen haben:** 

3. Open **SSMS** und Herstellen einer Verbindung mit der **Datenbank-Engine**.
   a2. Erweitern Sie **Datenbanken**, erweitern Sie die **SoftwareInventoryLogging** Datenbank **Tabellen**, klicken Sie mit der rechten Maustaste auf die **VMInfo** Tabelle und dann Wählen Sie die ersten 1000 Zeilen. 

    >[!NOTE] 
    >Jede Zeile für eine eindeutige VM einen verarbeitet darstellen **Bmil** Datei erfolgreich über HTTPS mithilfe von Push übertragen und von dem SIL-Aggregator verarbeitet werden. Bmil-Dateien werden geschützte Dateien, die von SIL verwendeten, erstellt jede unsere von jeder Instanz SIL Beachten Sie, dass dies nur erforderlich bei ist SIL und SILA in virtuellen Umgebungen verwendet werden. Andernfalls ist nur HTTPS-Datenverkehr erforderlich/erwartet).

   Alle Daten in der Datenbank sollte im SIL-Berichte angezeigt werden, nachdem der Cube verarbeitet wurde.

### <a name="data-flow-issue-2"></a>Data Flow Problem 2
#### <a name="too-many-servers-under-unknown-host"></a>Zu viele Server unter Host unbekannt

Dies ist wahrscheinlich in virtuellen Umgebungen ausgeführt werden soll, wenn SIL-Aggregator nicht erfolgreich physischen Hosts abgerufen wird, die die virtuellen Computer hosten.

1. Open **PowerShell** als Administrator, und führen die **Get-Silvmhost** Cmdlet.

    -   Wenn Hosts, als aufgelistet sind **unbekannte**, **hinzufügen-Silvmhost** Cmdlet funktionierte nicht ordnungsgemäß – in der Regel aufgrund ungültiger Anmeldeinformationen, die für den Zugriff auf diese Hosts hinzugefügt (daher unbekannt). Aber wenn Anmeldeinformationen überprüft wurden, kann dies bedeuten, dass die automatische Erkennung von **"HostType"** und **"hypervisortype"** in die **hinzufügen-Silvmhost** Cmdlet konnte nicht zur Erkennung der die Plattform. Erweiterte Tipps zur Problembehandlung für diese Situationen zur Verfügung, jedoch werden hier nicht behandelt (Überprüfen der Ereignisanzeige (eventviewer) SIL-Aggregator-Kanäle).

    -   Wenn Hosts aufgelistet sind, und **"HostType"** und **"hypervisortype"** mit Werten, die nicht aufgelisteten **unbekannte**, d.h. Windows und Hyper-v, oder Ubuntu verwenden und Xen, usw., aber es gibt keine **"DateTime"** unter **jüngsten Abrufs** Spalte Abfragen wurde nicht erfolgreich war noch.

        -   Müssen Sie die Wartezeit von einer Stunde nach dem Hinzufügen des Hosts für den Abruf stattfinden (vorausgesetzt, dieses Intervall ist festgelegt auf den Standardwert – können überprüft werden mithilfe der **Get-Silaggregator** Cmdlet).

        -   Wenn es eine Stunde seit der Host hinzugefügt wurde, überprüfen Sie, dass eine abrufaufgabe ausgeführt wird: In **Taskplaner**Option **Software Inventory Logging Aggregator** unter **Microsoft** &gt; **Windows** , und überprüfen der Verlauf des Vorgangs.

    -   Wenn ein Host aufgeführt ist, aber es keinen Wert für gibt **RecentPoll**, **"HostType"** , oder **"hypervisortype"** , kann dies weitgehend ignoriert werden. Dies geschieht nur in Hyper-v-Umgebungen. Diese Daten bestehen tatsächlich von der Windows Server-VM, Identifizieren von physischen Hosts, die sie über HTTPS ausgeführt wird. Dies kann bei der Identifizierung einer bestimmten virtuellen Maschine, die meldet, erfordert aber mining, die Datenbank mit nützlich sein, die **Get-SilAggregatorData** Cmdlet.

Nachdem Sie die Hosts ordnungsgemäß abrufen, Sie werden die Daten für diese physischen Hosts in der Datenbank SILA finden Sie unter sich eine **"DateTime"** unter **jüngsten Abrufs**. Die obigen Ausgabe 1-Abschnitt enthält eine schrittweise Anleitung zum Abrufen dieser Daten.

### <a name="data-flow-issue-3"></a>Data Flow Problem 3
#### <a name="too-many-physical-hosts-with-vms-listed-as-unknown-os"></a>Zu viele physische Hosts mit virtuellen Computern, die als unbekanntes Betriebssystem

1. Wählen Sie eine Windows Server Endknoten (VM), die Sie wissen, ist auf einem dieser Hosts, melden Sie sich als Administrator an.
2. Öffnen Sie PowerShell als Administrator an.
3. Stellen Sie sicher **SilLogging** ausgeführt wird, indem Sie mit der **Get-SilLogging** Cmdlet.
   - Wenn ausgeführt wird, versuchen Sie manuell die SIL-Daten mithilfe von push **Publish-SilData**.

   - Wenn ein Fehler vorliegt:
     - Stellen Sie sicher die **Targeturi** hat **https://** im Eintrag.
     - Stellen Sie sicher, dass alle Voraussetzungen erfüllt sind 
     - Stellen Sie sicher, alle erforderlichen Updates für Windows Server installiert sind (siehe die Voraussetzungen für SIL). Eine schnelle Möglichkeit um (nur WS 2012 R2) zu überprüfen ist nach diesen gesucht werden soll, mit dem folgenden Cmdlet: **Get-SilWindowsUpdate \*3060, \*3000**
     - Stellen Sie sicher, das für die Authentifizierung mit Aggregator verwendete Zertifikat installiert ist, im richtigen Speicher auf dem lokalen Server mit inventarisiert werden **SilLogging**.
     - Auf dem SIL-Aggregator achten, dass die Zertifikatfingerabdruck des Zertifikats verwendet wird, für die Authentifizierung mit Aggregator wird hinzugefügt, Liste mithilfe der **Set-SilAggregator** **– AddCertificateThumbprint** -Cmdlet.
     - Bei Verwendung von Enterprise-Zertifikaten überprüfen Sie, ob der Server mit aktivierter SIL der Domäne beigetreten ist, für die das Zertifikat erstellt wurde, bzw. anderweitig bei einer Stammzertifizierungsstelle überprüfbar ist. Wenn ein Zertifikat auf dem lokalen Computer, der versucht, Daten an den Aggregator weiterzuleiten oder per Push zu übertragen, nicht vertrauenswürdig ist, schlägt diese Aktion mit einem Fehler fehl.

     Wenn alle oben genannten überprüft und überprüft wurde, aber das Problem weiterhin besteht:

     - Überprüfen Sie, dass das Installieren des SIL-Aggregators verwendete Zertifikat fehlerfrei ist und mit dem Namen des SIL-aggregatorservers selbst übereinstimmt. Auch wenn Unternehmenszertifikate für die Installation des SIL-Aggregators verwendet werden, muss der Aggregator möglicherweise der Domäne hinzugefügt werden, in der das Zertifikat erstellt wurde (diese Schritte sind nicht erforderlich, wenn andere Computer erfolgreich an denselben SIL-Aggregator weiterleiten).

     -  Zum Schluss sehen Sie den folgenden Speicherort für zwischengespeicherte SIL-Dateien auf dem Server, es wird versucht, die Weiterleitung bzw. den Push, **\Windows\System32\Logfiles\SIL**. Wenn **SilLogging** gestartet wurde und verfügt über mehr als eine Stunde ausgeführt wurden oder **Publish-SilData** vor kurzem ausgeführt wurde und keine Dateien in diesem Verzeichnis vorhanden sind, als die Protokollierung auf dem Aggregator wurde erfolgreich.

Wenn kein Fehler, und keine Ausgabe in der Konsole vorhanden sind, klicken Sie dann war die Daten Push/veröffentlichen aus dem Windows Server-Endknoten SIL-Aggregator über HTTPS erfolgreich. Führen den Pfad der Anmeldung weiterleiten, Daten an den SIL-Aggregator als Administrator aus, und überprüfen die Datendateien, die angekommen sind. Wechseln Sie zu **Programmdateien (x86)** &gt; **Microsoft SIL-Aggregator** &gt; SILA-Verzeichnis. Sie können Datendateien Eintreffen in Echtzeit verfolgen.

>[!NOTE] 
>Mehr als eine Datendatei kann übertragen wurden, weisen mit dem **Publish-SilData** Cmdlet. SIL für den Endknoten werden fehlerhafte Pushvorgänge für bis zu 30 Tage lang zwischengespeichert. ALLE Datendateien geht auf die nächste erfolgreicher Push an den Aggregator für die Verarbeitung verwendet wird. Auf diese Weise kann eine neu Einrichten des SIL-Aggregators Daten aus einem Endknoten vor eigene Setup anzeigen.

>[!NOTE] 
>Es sind Regeln, die SILA folgt bei der Verarbeitung von Datendateien in das Verzeichnis SILA, die nur in Situationen mit wenig Datenverkehr relevant sind. Hoher Datenverkehr wird immer ausgelöst, in Echtzeit verarbeitet. Das Standardverhalten ist, dass die Verarbeitung entweder beginnen wird, nachdem 100 Dateien im Verzeichnis oder nach 15 Minuten eingehen. Bei der Problembehandlung End-to-End in einer kleinen Umgebung ist es oft notwendig, warten Sie 15 Minuten.

Nachdem diese Dateien verarbeitet wurden, sehen Sie die Daten in der Datenbank.
