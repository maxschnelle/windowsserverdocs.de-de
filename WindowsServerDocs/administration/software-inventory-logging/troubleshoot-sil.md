---
title: Problembehandlung der Protokollierung des Softwarebestands
description: Beschreibt, wie häufige Bereitstellungs Probleme bei der Protokollierung des Software Bestands gelöst werden
ms.custom: na
ms.prod: windows-server
ms.technology: manage-software-inventory-logging
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
author: brentfor
ms.author: coreyp
manager: lizapo
ms.date: 10/16/2017
ms.openlocfilehash: fb6e6fbba835e049748ca8578f24a1ff7fc750bf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382898"
---
# <a name="troubleshoot-software-inventory-logging"></a>Problembehandlung der Protokollierung des Softwarebestands 

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

## <a name="understanding-sil"></a>Grundlegendes zu SIL

Bevor Sie mit der Problembehandlung von SIL beginnen, sollten Sie über ein gutes Verständnis der zugehörigen Komponenten und deren Funktionsweise verfügen. In den folgenden Videos erhalten Sie eine Übersicht über den SIL-und SIL-Aggregator und deren Verwendung zum Weiterleiten und melden von Inventur Daten:

1. [Eine Einführung in die Protokollierung des Software Bestands (SIL) (10:57)](https://channel9.msdn.com/Blogs/Regular-IT-Guy/An-Introduction-to-Software-Inventory-Logging-SIL)

2. [Protokollierung des Software Bestands: Einrichten des SIL-Aggregators (14:34)](https://channel9.msdn.com/Blogs/windowsserver/Software-Inventory-Logging-Setting-up-SIL-Aggregator)

3. [Protokollierung des Software Bestands: Aktivieren der SIL-Weiterleitung (7:20)](https://channel9.msdn.com/Blogs/windowsserver/Software-Inventory-Logging-Enabling-SIL-Forwarding)

## <a name="how-sil-data-flow-works"></a>Funktionsweise des SIL-Datenflusses

Das SIL-Framework verfügt über zwei Hauptkomponenten und zwei Kommunikationskanäle. Der Datenfluss über beide Kanäle und zwischen beiden Komponenten ist für eine erfolgreiche SIL-Bereitstellung erforderlich (Hierbei handelt es sich um eine virtualisierte oder Cloud-Umgebung). reine physische Umgebungen benötigen nur einen der Kommunikationskanäle. Sie müssen die Komponenten und den Datenfluss von SIL verstehen, um ihn ordnungsgemäß bereitzustellen. Nach dem Ansehen der obigen Übersichts Videos sehen Sie das Architektur Diagramm, in dem die Komponenten und der Datenfluss über beide Kanäle veranschaulicht werden. Orangefarbene Pfeile zeigen Remote Abfragen über WinRM an, grüne Gestrichelte Pfeile geben HTTPS-Beiträge an den SIL-Aggregator von SIL in jedem WS-Endknoten an:

![](../media/software-inventory-logging/image1.png)

Wenn ein Problem mit SIL auftritt, liegt es wahrscheinlich in Bezug auf eine Unterbrechung im Datenfluss über die Kanäle und zwischen den Komponenten. Im folgenden finden Sie die häufigsten Probleme im Zusammenhang mit dem Datenfluss. im nächsten Abschnitt finden Sie die Schritte zur Problembehandlung, um die drei Probleme zu beheben:

-   **Datenfluss Problem 1** – **keine Daten im Bericht bei Verwendung des Cmdlets Publish-silreport** (oder im allgemeinen fehlende Daten).

-   **Datenfluss Problem 2** – **zu viele Server mit einem unbekannten Host** im Bericht.

-   **Datenfluss Problem 3** – **zu viele VMS unter physischen Hosts, die im Bericht als Unbekanntes Betriebssystem aufgeführt** sind, und/oder ein Fehler, der bei der Verwendung von " **Publish-sildata** " auf Windows-Servern mit SIL auftritt.

## <a name="troubleshooting-data-flow-issues"></a>Problembehandlung bei Datenfluss Problemen

Bevor Sie beginnen, müssen Sie wissen, wie lange der SIL-Aggregator mit dem " **Start-silaggregator"-** Cmdlet gestartet wurde.

>[!IMPORTANT]
>Es werden erst dann Daten im Bericht angezeigt, wenn der SQL-Datencube zum Zeitpunkt der lokalen Systemzeit von 3 Uhr verarbeitet wird. Fahren Sie nicht mit den Schritten zur Problembehandlung fort, bis der Cube Daten verarbeitet hat.

Wenn Sie Daten im Bericht behandeln (oder aus dem Bericht fehlen), der aktueller ist als der Zeitpunkt, zu dem der Cube zuletzt verarbeitet wurde, oder bevor der Cube jemals verarbeitet wurde (bei einer neuen Installation), führen Sie die folgenden Schritte aus, um den SQL-Datencube in Echtzeit zu verarbeiten. :

1. Melden Sie sich als Administrator von SQL Server an, und führen Sie **SSMS** an einer Eingabeaufforderung aus.
2. Stellen Sie eine Verbindung mit dem Datenbankmodul her.
3. Erweitern Sie **SQL Server-Agent** , und erweitern Sie dann **Aufträge**.
4. Klicken Sie mit der rechten Maustaste auf **silstagingrefresh** , und wählen Sie **Auftrag starten bei Schritt**.
5. Klicken Sie auf **Start** , und warten Sie, bis die Statusanzeige der Aktualisierung abgeschlossen ist.
6. Öffnen Sie PowerShell als Administrator, und führen Sie das Cmdlet **Publish-silreport-OpenReport** aus.

Wenn im Bericht noch keine Daten vorhanden sind, können Sie mit der Problembehandlung der drei Datenfluss Probleme fortfahren.

### <a name="data-flow-issue-1"></a>Datenfluss Problem 1 

#### <a name="no-data-in-the-report-when-using-the-publish-silreport-cmdlet-or-data-is-generally-missing"></a>Keine Daten im Bericht, wenn das Cmdlet Publish-silreport verwendet wird (oder wenn die Daten im allgemeinen fehlen)

Wenn Daten fehlen, ist dies wahrscheinlich darauf zurückzuführen, dass der SQL-Datencube noch nicht verarbeitet wurde. Wenn Sie kürzlich verarbeitet wurde und Sie glauben, dass fehlende Daten beim Aggregator vor der Cubeverarbeitung eintreffen müssen, befolgen Sie den Pfad der Daten in umgekehrter Reihenfolge. Wählen Sie einen eindeutigen Host und einen eindeutigen virtuellen Computer für die Problembehandlung aus. Der Dateipfad in umgekehrter Reihenfolge ist der Sila- **Bericht** &lt; **Sila-Datenbank** &lt; , lokaler Remote- **Verzeichnis** &lt; **physischer Host** oder **WS-VM mit SIL-Agent/Task**.

#### <a name="check-to-see-if-data-is-in-the-database"></a>Überprüfen Sie, ob die Daten in der Datenbank gespeichert sind.

Es gibt zwei Möglichkeiten, um nach Daten zu suchen: **PowerShell** oder **SSMS**.

>[!Important]
>Wenn der Cube mindestens einmal verarbeitet hat, seitdem Daten in die Datenbank eingefügt wurden, sollten sich diese Daten im Bericht widerspiegeln. Wenn in der Datenbank keine Daten vorhanden sind, schlägt das Abrufen der physischen Hosts fehl, oder über HTTPS wird nichts empfangen.

 #### <a name="powershell"></a>PowerShell

1. Öffnen Sie PowerShell als Administrator, führen Sie das Cmdlet " **Get-silvmhost** " aus, und führen Sie dann " **Get-silaggregator**" aus.

    >[!NOTE]
    >Die Ausgabe von " **Get-silaggregator** " imitiert immer die **Registerkarte "Windows Server-Details** " des Excel-Berichts. Ein anderes Ergebnis wird nicht erwartet.

2. Ausführen von " **Get-silvmhost** "
   - Wenn keine Hosts aufgelistet sind, fügen Sie Hosts mithilfe des Cmdlets **Add-silvmhost** hinzu.
   - Wenn Hosts als **unbekannt**aufgeführt werden, gehen Sie zu Problem 2. 
   d: Wenn die Hosts aufgelistet sind, aber kein **DateTime** -Wert unter der **aktuellen Umfrage** Spalte vorhanden ist, gehen Sie unten zu **Problem 2** .

**Weitere verwandte Befehle**

**Get-silaggregator-Computername &lt;der voll qualifizierte Server, von dem Daten&gt;übertragen werden**: Dadurch werden Informationen aus der Datenbank zu einem Computer (VM) erstellt, auch wenn der Cube verarbeitet wurde. Folglich kann dieses Cmdlet verwendet werden, um Daten in der Datenbank für einen Windows-Server zu übertragen, der SIL-Daten über HTTPS, vor oder ohne den Cube-Prozess bei 3AM überträgt (oder wenn Sie den Cube nicht in Echtzeit aktualisiert haben, wie am Anfang dieses Abschnitts beschrieben).

**Get-silaggregator-vmhostname &lt;der voll qualifizierte Name eines abgeleiteten physischen Hosts, bei dem bei Verwendung des Cmdlets&gt;"Get-silvmhost" unter der Spalte Aktueller Abruf ein Wert vorhanden ist**: Dadurch werden Informationen aus der Datenbank über einen physischen Host erstellt, auch wenn der Cube verarbeitet wurde.

#### <a name="ssms"></a>SSMS

n**Suchen Sie nach Daten von den abgeleiteten Hosts:**
 
1. Öffnen Sie **SSMS** , und stellen Sie eine Verbindung zum **Datenbank-Engine**her.
2. Erweitern Sie **Datenbanken**, erweitern Sie die Datenbank **softwareinventorylogging** und **Tabellen**, klicken Sie mit der rechten Maustaste auf die Tabelle **Hostinfo** , und wählen Sie dann oberste 1000 Zeilen aus. 

    Wenn Daten für einen oder mehrere Hosts in der Tabelle vorhanden sind, ist das Abrufen dieser/der Hosts mindestens einmal erfolgreich.

   **Überprüfen Sie, ob Daten von VMS oder eigenständigen Servern übermittelt wurden, die Daten über HTTPS übermittelt haben:** 

3. Öffnen Sie **SSMS** , und stellen Sie eine Verbindung zum **Datenbank-Engine**her.
   a2. Erweitern Sie **Datenbanken**, erweitern Sie die Datenbank **softwareinventorylogging** und **Tabellen**, klicken Sie mit der rechten Maustaste auf die **vminfo** -Tabelle, und wählen Sie dann die obersten 1000 Zeilen aus. 

    >[!NOTE] 
    >Jede Zeile für eine eindeutige VM stellt eine verarbeitete **bmil** -Datei dar, die erfolgreich per Pushvorgang über HTTPS übermittelt und vom SIL-Aggregator verarbeitet wird. Bei bmil-Dateien handelt es sich um proprietäre Dateien, die von SIL verwendet werden. eine wird von jeder SIL-Instanz erstellt. Beachten Sie, dass dies nur erforderlich ist, wenn SIL und Sila in virtuellen Umgebungen verwendet werden. Andernfalls ist nur HTTPS-Datenverkehr erforderlich/erwartet).

   Alle Daten in der Datenbank sollten nach der Verarbeitung des Cubes in SIL-Berichten berücksichtigt werden.

### <a name="data-flow-issue-2"></a>Datenfluss Problem 2
#### <a name="too-many-servers-under-unknown-host"></a>Zu viele Server unter einem unbekannten Host

Dies tritt wahrscheinlich in virtuellen Umgebungen auf, wenn der SIL-Aggregator keine physischen Hosts abfragt, die die virtuellen Computer hosten.

1. Öffnen Sie **PowerShell** als Administrator, und führen Sie das Cmdlet " **Get-silvmhost** " aus.

    -   Wenn Hosts als **unbekannt**aufgelistet sind, funktionierte das **Add-silvmhost-** Cmdlet nicht ordnungsgemäß – in der Regel aufgrund von ungültigen Anmelde Informationen für den Zugriff auf diese Hosts (daher unbekannt). Wenn die Anmelde Informationen jedoch überprüft werden, könnte dies bedeuten, dass die automatische Erkennung von **HostType** und **"hypervisortype"** im Cmdlet " **Add-silvmhost** " die Plattform nicht erkennen konnte. Für diese Situationen sind erweiterte Schritte zur Problembehandlung verfügbar, die hier jedoch nicht behandelt werden (überprüfen Sie die EventViewer SIL-Aggregator-Kanäle).

    -   Wenn Hosts aufgelistet werden und **HostType** und **"hypervisortype"** mit nicht **unbekannten**Werten aufgelistet sind, d. h. Windows und HyperV, Ubuntu und Xen usw., aber es ist kein **DateTime** -Wert unter **letzte Umfrage** Spalte vorhanden. der Abruf wurde noch nicht erfolgreich durchgeführt.

        -   Nach dem Hinzufügen des Hosts für den Abruf müssen Sie eine Stunde warten (vorausgesetzt, dieses Intervall ist auf Default festgelegt – kann mithilfe des Cmdlets **Get-silaggregator** aktiviert werden).

        -   Wenn eine Stunde vergangen ist, seit der Host hinzugefügt wurde, überprüfen Sie, ob der Abruf Task ausgeführt wird: Wählen Sie in **Taskplaner**den **Aggregator der Protokollierung des Software Bestands** unter **Microsoft** &gt; **Windows** aus, und überprüfen Sie den Verlauf der Aufgabe.

    -   Wenn ein Host aufgelistet ist, aber kein Wert für " **recentfetch**", " **HostType**" oder " **hypervisortype**" vorhanden ist, kann dies größtenteils ignoriert werden. Dies erfolgt nur in HyperV-Umgebungen. Diese Daten stammen tatsächlich von der Windows Server-VM und identifizieren den physischen Host, der über HTTPS ausgeführt wird. Dies kann nützlich sein, um einen bestimmten virtuellen Computer zu identifizieren, der Bericht erstattet, erfordert jedoch das Mining der Datenbank mithilfe des Cmdlets **Get-silaggregatordata** .

Wenn die Hosts ordnungsgemäß abgerufen werden, können Sie die Daten für diese physischen Hosts in der Sila-Datenbank anzeigen, in denen ein **DateTime** -Wert in der **aktuellen Umfrage**vorhanden ist. Der obige Abschnitt Problem 1 enthält Schritte zum Abrufen dieser Daten.

### <a name="data-flow-issue-3"></a>Datenfluss Problem 3
#### <a name="too-many-physical-hosts-with-vms-listed-as-unknown-os"></a>Zu viele physische Hosts mit VMS, die als Unbekanntes Betriebssystem aufgeführt sind.

1. Wählen Sie einen Windows Server-Endknoten (VM) aus, den Sie auf einem dieser Hosts kennen, und melden Sie sich als Administrator an.
2. Öffnen Sie PowerShell als Administrator.
3. Überprüfen Sie mithilfe des Cmdlets **Get-sillogging** , ob **sillogging** ausgeführt wird.
   - Wenn Sie ausführen, versuchen Sie, SIL-Daten mithilfe von **Publish-sildata**manuell zu überführen.

   - Wenn ein Fehler auftritt:
     - Stellen Sie sicher, dass **targetUri** über **https://** im Eintrag verfügt.
     - Stellen Sie sicher, dass alle Voraussetzungen erfüllt sind. 
     - Stellen Sie sicher, dass alle erforderlichen Updates für Windows Server installiert sind (siehe "Voraussetzungen für SIL"). Eine schnelle Möglichkeit zum Überprüfen (nur auf WS 2012 R2) besteht darin, diese mithilfe des folgenden Cmdlets zu suchen: **Get-silwindowsupdate \*3060, \*3000**
     - Stellen Sie sicher, dass das zur Authentifizierung bei dem Aggregator verwendete Zertifikat im richtigen Speicher auf dem lokalen Server installiert ist, um mit **sillogging**inventarisiert zu werden.
     - Stellen Sie auf dem SIL-Aggregator sicher, dass der Zertifikat Fingerabdruck des Zertifikats, mit dem der Aggregator authentifiziert wird, mithilfe des Cmdlets **Set-silaggregator** **– addcertifikatethrebprint** der Liste hinzugefügt wird.
     - Bei Verwendung von Enterprise-Zertifikaten überprüfen Sie, ob der Server mit aktivierter SIL der Domäne beigetreten ist, für die das Zertifikat erstellt wurde, bzw. anderweitig bei einer Stammzertifizierungsstelle überprüfbar ist. Wenn ein Zertifikat auf dem lokalen Computer, der versucht, Daten an den Aggregator weiterzuleiten oder per Push zu übertragen, nicht vertrauenswürdig ist, schlägt diese Aktion mit einem Fehler fehl.

     Wenn alle oben genannten Punkte überprüft und überprüft wurden, das Problem jedoch weiterhin besteht:

     - Überprüfen Sie, ob das zur Installation des SIL-Aggregators verwendete Zertifikat fehlerfrei ist und mit dem Namen des SIL-aggregatorservers selbst übereinstimmt. Auch wenn Unternehmenszertifikate für die Installation des SIL-Aggregators verwendet werden, muss der Aggregator möglicherweise der Domäne hinzugefügt werden, in der das Zertifikat erstellt wurde (diese Schritte sind nicht erforderlich, wenn andere Computer erfolgreich an denselben SIL-Aggregator weiterleiten).

     -  Zum Schluss können Sie den folgenden Speicherort auf zwischengespeicherte SIL-Dateien auf dem Server überprüfen, der versucht, den Forward/Push-Vorgang durchzusetzen, **\windows\system32\logfiles\sil**. Wenn " **sillogging** " seit mehr als einer Stunde gestartet wurde und ausgeführt wird, oder wenn " **Publish-sildata** " vor kurzem ausgeführt wurde und keine Dateien in diesem Verzeichnis vorhanden sind, ist die Protokollierung für den Aggregator erfolgreich.

Wenn kein Fehler vorliegt und keine Ausgabe in der Konsole vorhanden ist, war das Verschieben/Veröffentlichen von Daten vom Windows Server-Endknoten zum SIL-Aggregator über HTTPS erfolgreich. Wenn Sie den Pfad der Daten weiterleiten möchten, melden Sie sich als Administrator beim SIL-Aggregator an, und untersuchen Sie die Datendatei (en), die eingetroffen sind. Wechseln Sie zum Verzeichnis **Programmdateien (x86)** &gt; **Microsoft SIL-Aggregator** &gt; sila. Sie können Datendateien, die in Echtzeit eintreffen, ansehen.

>[!NOTE] 
>Möglicherweise wurden mehrere Datendateien mit dem Cmdlet **Publish-sildata** übertragen. Von SIL auf dem Endknoten werden fehlerhafte Pushvorgänge für bis zu 30 Tage zwischengespeichert. Beim nächsten erfolgreichen Push werden alle Datendateien zur Verarbeitung an den Aggregator weitergeleitet. Auf diese Weise kann ein neu eingelegter SIL-Aggregator Daten von einem Endknoten vor seiner eigenen Einrichtung anzeigen.

>[!NOTE] 
>Beim Verarbeiten von Datendateien im Sila-Verzeichnis, die nur in Situationen mit geringem Datenverkehr relevant sind, befolgt Sila-Regeln. Mit hohem Datenverkehr wird die Verarbeitung immer in Echtzeit auslöst. Das Standardverhalten ist, dass die Verarbeitung entweder nach dem Eintreffen der 100-Dateien im Verzeichnis oder nach 15 Minuten startet. Bei der End-to-End-Problembehandlung in einer kleinen Umgebung ist es häufig erforderlich, 15 Minuten zu warten.

Nachdem diese Dateien verarbeitet wurden, werden die Daten in der Datenbank angezeigt.
