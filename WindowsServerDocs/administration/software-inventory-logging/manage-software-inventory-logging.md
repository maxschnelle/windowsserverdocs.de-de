---
title: Verwaltung der Protokollierung des Softwarebestands
description: Beschreibt, wie die Protokollierung des Software Bestands verwaltet wird
ms.topic: article
ms.assetid: 812173d1-2904-42f4-a9e2-de19effec201
author: brentfor
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 548158fd1df4ee4fbd8d6f1bcee28693961c8d79
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87991859"
---
# <a name="manage-software-inventory-logging"></a>Verwaltung der Protokollierung des Softwarebestands

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

In diesem Dokument wird beschrieben, wie Sie die Protokollierung des Software Bestands verwalten, ein Feature, mit dem Daten Center Administratoren Microsoft-softwareasset-Verwaltungsdaten problemlos für Ihre bereit Stellungen protokollieren können. In diesem Dokument wird beschrieben, wie Sie die Protokollierung des Softwarebestands verwalten. Bevor Sie die Protokollierung des Software Bestands mit Windows Server 2012 R2 verwenden, stellen Sie sicher, dass auf jedem System, das inventarisiert werden muss, Windows Update [KB 3000850](https://support.microsoft.com/kb/3000850) und [KB 3060681](https://support.microsoft.com/kb/3060681) installiert sind. Für Windows Server 2016 sind keine wndows-Updates erforderlich. Diese Funktion wird auf jedem Server lokal ausgeführt, dessen Bestand protokolliert werden soll. Es werden keine Daten von Remoteservern gesammelt.

Das Feature zur Protokollierung des Softwarebestands kann auch zu zwei Versionen von Windows Server vor Windows Server 2012 R2hinzugefügt werden. Sie können die folgenden Updates installieren, um die Funktionalität zur Protokollierung des Softwarebestands zu Windows Server 2012 und Windows Server 2008 R2 SP1hinzuzufügen:

- **Windows Server 2012 (Standard oder Datacenter Edition)**

> [!NOTE]
> Stellen Sie sicher, dass [WMF 4.0](https://www.microsoft.com/download/details.aspx?id=40855) installiert ist, bevor Sie das nachstehende Updatepaket anwenden.

-  WMF 4.0-Updatepaket für Windows Server 2012: [KB 3119938](https://support.microsoft.com/kb/3119938)

- **Windows Server 2008 R2 SP1**

> [!NOTE]
> Stellen Sie sicher, dass [WMF 4.0](https://www.microsoft.com/download/details.aspx?id=40855) installiert ist, bevor Sie das nachstehende Updatepaket anwenden.


- Erfordert [.NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)


- WMF 4.0-Updatepaket für Windows Server 2008 R2: [KB 3109118](https://support.microsoft.com/kb/3109118)


Es gibt bei der Nutzung dieser Funktion zwei primäre Methoden für die Inventur:

1.  Starten der SIL-Protokollfunktion zum Sammeln aus SIL-Datenquellen und stündliches Weiterleiten der Nutzlast über das Netzwerk an ein angegebenes Ziel (URI).

2.  Manuelles Abfragen der SIL-Daten in beliebigen Abständen mithilfe von PowerShell oder WMI.

Das Starten der SIL-Protokollierung erfordert einige Planung und Vorausschau, hat jedoch erhebliche Vorteile gegenüber dem manuellen Abfragen der Daten. Die SIL-Protokollierung bietet folgende drei Hauptvorteile für Administratoren im Rechenzentrum:

-   Eine Verlauf (Protokoll) kann im Lauf der Zeit erfasst werden und ermöglicht flexible und umfassende Berichte aus einer einzigen Quelle.

-   Herausforderungen bei der Ermittlung von Computern, die für viele Inventurwerkzeuge typisch sind, lassen sich überwinden.

-   Herausforderungen in Bezug auf Vertrauensgrenzen und Anforderungen für erhöhte Benutzerrechte, die für viele Inventurwerkzeuge typisch sind, lassen sich trotz Erhalt des Sicherheitsniveaus überwinden, da die Daten per SSL über HTTPS verschlüsselt werden.

Die Protokollierung des Softwarebestands wird standardmäßig installiert, aber die Protokollierung nicht standardmäßig gestartet. Die gesamte Konfiguration der Protokollierung des Softwarebestands erfolgt mit PowerShell-Cmdlets. Für die Protokollierung des Softwarebestands sind nur wenige Konfigurationsoptionen verfügbar. Dieses Dokument beschreibt diese Optionen und deren Verwendungszweck, sowie die zum Sammeln von Daten verwendeten Cmdlets (bei Verwendung der zweiten oben genannten Methode).

**Inhalt dieses Dokuments**

In diesem Dokument werden folgende Konfigurationsoptionen behandelt:

-   [Starten und Beenden der Protokollierung des Softwarebestands](manage-software-inventory-logging.md#BKMK_Step1)

-   [Verlauf der Protokollierung des Softwarebestands](manage-software-inventory-logging.md#BKMK_Step2)

-   [Anzeigen von Daten der Protokollierung des Softwarebestands](manage-software-inventory-logging.md#BKMK_Step3)

-   [Löschen protokollierter Daten der Protokollierung des Softwarebestands](manage-software-inventory-logging.md#BKMK_Step4)

-   [Sichern und Wiederherstellen von Daten, die von der Protokollierung des Software Bestands protokolliert werden] Manage-Software-Inventory-Logging. MD # BKMK_Step5)

-   [Lesen protokollierter und veröffentlichter Daten der Protokollierung des Softwarebestands](manage-software-inventory-logging.md#BKMK_Step6)

-   [Sicherheit bei der Protokollierung des Softwarebestands](manage-software-inventory-logging.md#BKMK_Step7)

-   [Arbeiten mit Datums-und Uhrzeit Einstellungen in der Windows Server-Software Inventur Protokollierung](manage-software-inventory-logging.md#BKMK_Step8)

-   [Aktivieren und Konfigurieren der Protokollierung des Softwarebestands auf einem bereitgestellten virtuellen Datenträger](manage-software-inventory-logging.md#BKMK_Step10)

-   [Übersicht über die Verwendung der Protokollierung des Softwarebestands in Windows Server 2012 R2 ohne KB 3000850](manage-software-inventory-logging.md#BKMK_Step11)

-   [Verwendung der Protokollierung des Softwarebestands in einer Windows Server 2012 R2 Hyper-V-Umgebung ohne KB 3000850](manage-software-inventory-logging.md#BKMK_Step12)

> [!NOTE]
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter Verwenden von Cmdlets.


## <a name="starting-and-stopping-software-inventory-logging"></a><a name="BKMK_Step1"></a>Starten und Beenden der Protokollierung des Softwarebestands
Die tägliche Erfassung der Software Inventur Protokollierung und die Weiterleitung über das Netzwerk müssen auf einem Computer mit Windows Server 2012 R2 aktiviert sein, um die Software Inventur protokollieren

> [!NOTE]
> Sie können das PowerShell-Cmdlet **[Get-SilLogging](/previous-versions/windows/powershell-scripting/dn283396(v=wps.630))** verwenden, um Informationen zum Dienst für die Protokollierung des Softwarebestands abzurufen, z. B. ob er ausgeführt wird oder beendet wurde.

#### <a name="to-start-software-inventory-logging"></a>So starten Sie die Protokollierung des Softwarebestands

1.  Melden Sie sich mit einem Konto mit lokalen Administratorrechten am Server an.

2.  Öffnen Sie PowerShell als Administrator.

3.  Geben Sie an der PowerShell-Eingabeaufforderung **[Start SilLogging](/previous-versions/windows/powershell-scripting/dn283391(v=wps.630))** ein.

> [!NOTE]
> Es ist möglich, das Ziel festzulegen, ohne einen Fingerabdruck des Zertifikats einzurichten. Ein solches Vorgehen führt jedoch dazu, dass Weiterleitungen fehlschlagen und Daten lokal bis zu 30 Tage lang vorgehalten werden. (Nach Ablauf dieser Zeit werden sie gelöscht.) Sobald ein gültiges Zertifikat-Hash für das Ziel festgelegt (und das entsprechende gültige Zertifikat im LocalMachine/Personal Speicher installiert) wurde, werden lokal gespeicherte Daten an das Ziel weitergeleitet, sofern das Ziel so konfiguriert wurde, dass diese Daten mit diesem Zertifikat akzeptiert werden (weitere Informationen finden Sie unter [Software Inventory Logging Aggregator](Software-Inventory-Logging-Aggregator.md) ).

#### <a name="to-stop-software-inventory-logging"></a>So beenden Sie die Protokollierung des Softwarebestands

1.  Melden Sie sich mit einem Konto mit lokalen Administratorrechten am Server an.

2.  Öffnen Sie PowerShell als Administrator.

3.  Geben Sie an der PowerShell-Eingabeaufforderung **[Stop- SilLogging](/previous-versions/windows/powershell-scripting/dn283394(v=wps.630))**

## <a name="configuring-software-inventory-logging"></a>Konfigurieren der Protokollierung des Softwarebestands
Sie führen drei Schritte aus, um die Protokollierung des Softwarebestands so zu konfigurieren, dass Daten nach und nach an einen Aggregationsserver weitergeleitet werden:

1.  Verwenden Sie **Set-sillogging – targetUri** , um die Webadresse Ihres Aggregations Servers anzugeben (muss mit "https://" beginnen).

2.  Verwenden Sie **Set-SilLogging –CertificateThumbprint** , um den Fingerabdruckhash Ihres gültigen SSL-Zertifikats anzugeben, der zum Authentifizieren der Datenübertragungen an den Aggregationsserver verwendet werden soll (der Aggregationsserver muss so konfiguriert werden, dass ein Hash akzeptiert wird).

3.  Installieren Sie ein gültiges SSL-Zertifikat (für Ihr Netzwerk) im **LocalMachine/Personal-Speicher** (bzw. **/LocalMachine/MY**) des lokalen Servers, von dem aus die Daten weitergeleitet werden sollen.

Es empfiehlt sich, die Schritte vor der Verwendung von **Start-SilLogging** auszuführen.  Wenn Sie die Schritte nach der Verwendung von **Start-SilLogging** ausführen möchten, müssen Sie SIL nur beenden und erneut starten.  Sie können auch mit dem Cmdlet Publish-SilData sicherstellen, dass der Aggregationsserver über eine vollständige Ergänzung der Daten für diesen Server verfügt.

Eine umfassende Anleitung zum Einrichten des SIL-Frameworks als Ganzes finden Sie unter [Software Inventory Logging Aggregator](software-inventory-logging-aggregator.md).  Insbesondere sollten Sie den Abschnitt über die Problembehandlung zurate ziehen, wenn bei **Publish-SilData** ein Fehler auftritt oder wenn die SIL-Protokollierung auf andere Weise fehlschlägt.

## <a name="software-inventory-logging-over-time"></a><a name="BKMK_Step2"></a>Verlauf der Protokollierung des Softwarebestands
Wenn die Protokollierung des Softwarebestands von einem Administrator gestartet wurde, beginnt die stündliche Sammlung und Weiterleitung der Daten an den Aggregationsserver (Ziel-URI). Die erste Weiterleitung besteht aus einem vollständigen Datensatz, den [Get-SilData](/previous-versions/windows/powershell-scripting/dn283388(v=wps.630)) abruft und zu einem bestimmten Zeitpunkt auf der Konsole anzeigt. Danach prüft SIL bei jedem Intervall die Daten und leitet nur eine kleine ID-Bestätigung an den Aggregationszielserver weiter, sofern seit der letzten Sammlung keine Änderung aufgetreten ist. Wenn ein Wert geändert wurde, sendet SIL erneut einen vollständigen Datensatz.

> [!IMPORTANT]
> Wenn in jedem Intervall der Ziel-URI nicht erreichbar ist, oder die Datenübertragung über das Netzwerk aus irgendeinem Grund nicht erfolgreich ist, werden gesammelte Daten lokal bis zu einem Standardwert von 30 Tagen gespeichert. (Nach Ablauf dieser Zeit werden sie gelöscht.) Bei der nächsten erfolgreichen Weiterleitung von Daten auf den Zielserver für die Aggregation werden alle lokal gespeicherten Daten weitergeleitet und lokal zwischengespeicherte Daten werden gelöscht.

## <a name="displaying-software-inventory-logging-data"></a><a name="BKMK_Step3"></a>Anzeigen von Daten der Protokollierung des Softwarebestands
Neben den im vorherigen Abschnitt beschriebenen PowerShell-Cmdlets stehen Ihnen in sechs weitere Cmdlets zum Sammeln von Daten der Protokollierung des Softwarebestands zur Verfügung:

-   **[Get-SilComputer](/previous-versions/windows/powershell-scripting/dn283392(v=wps.630))**: Zeigt sowohl den zeitlichen Verlauf der Werte für bestimmte server- und betriebssystembezogene Daten an, als auch den FQDN oder Hostnamen des physischen Hosts, falls verfügbar.

-   **[Get-SilComputerIdentity (KB 3000850)](/previous-versions/windows/powershell-scripting/dn858074(v=wps.630))**: Zeigt die von SIL verwendeten Bezeichner für einzelne Server an.

-   **[Get-SilData](/previous-versions/windows/powershell-scripting/dn283388(v=wps.630))**: Zeigt den gesammelten zeitlichen Verlauf aller Daten der Protokollierung des Softwarebestands an.

-   **[Get-SilSoftware](/previous-versions/windows/powershell-scripting/dn283397(v=wps.630))**: Zeigt die Identität im zeitlichen Verlauf der gesamten auf dem Computer installierten Software an.

-   **[Get-SilUalAccess](/previous-versions/windows/powershell-scripting/dn283389(v=wps.630))**: Zeigt für die vergangenen zwei Tage die Gesamtzahl der eindeutigen Clientanforderungen für Geräte und Benutzer an.

-   **[Get-SilWindowsUpdate](/previous-versions/windows/powershell-scripting/dn283393(v=wps.630))**: Zeigt den zeitlichen Verlauf der Liste aller auf dem Computer installierten Windows-Updates an.

Ein typischer Anwendungsfall für Cmdlets zur Protokollierung des Softwarebestands wäre das Abfragen der Protokollierung des Softwarebestands für einen bestimmten Zeitpunkt der gesamten Protokollierung durch einen Administrator mithilfe von [Get-SilSoftware](/previous-versions/windows/powershell-scripting/dn283397(v=wps.630)).

**Ausgabe Beispiel**

```
PS C:\> Get-SilData

ID                 : 961FF8A1-8549-4BEC-8DF6-3B3E32C26FFA
UUID               : B49ACB4C-7D9C-4806-9917-AE750BB3DA84
VMGUID             : E84CCCBD-0D0F-486B-A424-9780C7CF92E4
Name               : Server01Guest.Test.Contoso.com
HypervisorHostName : Server01.Test.Contoso.com

ID          : {F0C3E5D1-1ADE-321E-8167-68EF0DE699A5}
Name        : Microsoft Visual C++ 2010  x86 Redistributable - 10.0.40219
InstallDate : 12/5/2013
Publisher   : Microsoft Corporation
Version     : 10.0.40219

ID          : {89F4137D-6C26-4A84-BDB8-2E5A4BB71E00}
Name        : Microsoft Silverlight
InstallDate : 3/20/2014
Publisher   : Microsoft Corporation
Version     : 5.1.30214.0

ChassisSerialNumber       : 4452-0564-0284-2290-0113-6804-05
CollectedDateTime         : 10/27/2014 4:01:33 PM
Model                     : Virtual Machine
Name                      : Server01Guest.Test.Contoso.com
NumberOfCores             : 1
NumberOfLogicalProcessors : 1
NumberOfProcessors        : 1
OSName                    : Microsoft Windows Server 2012 R2 Datacenter
OSSku                     : 8
OSSuite                   : 400
OSSuiteMask               : 400
OSVersion                 : 6.3.9600
ProcessorFamily           : 179
ProcessorManufacturer     : GenuineIntel
ProcessorName             : Intel(R) Xeon(R) CPU           E5440  @ 2.83GHz
SystemManufacturer        : Microsoft Corporation

```

> [!NOTE]
> Die Ausgabe dieses Cmdlets ist identisch mit der kombinierten Ausgabe aller anderen **Get-Sil**-Cmdlets, wobei sich durch die asynchrone Ausgabe auf der Konsole möglicherweise eine unterschiedliche Reihenfolge der Objekte ergibt.
>
> Die Protokollierung des Softwarebestands muss nicht gestartet sein, um die **Get-Sil**-Cmdlets verwenden zu können.

## <a name="deleting-data-logged-by-software-inventory-logging"></a><a name="BKMK_Step4"></a>Löschen protokollierter Daten der Protokollierung des Softwarebestands
Die Protokollierung des Softwarebestands wurde nicht als unternehmenskritische Komponente beabsichtigt. Sie ist so konzipiert, dass ihre Auswirkungen auf lokale Systemvorgänge so gering wie möglich sind und gleichzeitig eine hohe Zuverlässigkeit gewahrt wird. Dadurch kann der Administrator die Software Inventur Protokollierungs Datenbank und die unterstützenden Dateien (jede Datei im Verzeichnis "\windows\system32\logfiles\sil") auch manuell löschen, um betriebliche Anforderungen zu erfüllen.

#### <a name="to-delete-data-logged-by-software-inventory-logging"></a>So löschen Sie mit der Protokollierung des Softwarebestands protokollierte Daten

1. Beenden Sie in PowerShell die Protokollierung des Softwarebestands mit dem Befehl **[Stop-SilLogging](/previous-versions/windows/powershell-scripting/dn283394(v=wps.630))**.

2. Öffnen Sie Windows-Explorer.

3. Wechseln Sie zu " **\windows\system32\logfiles\sil \\ ** ".

4. Löschen Sie alle Dateien im Ordner.

## <a name="backing-up-and-restoring-data-logged-by-software-inventory-logging"></a><a name="BKMK_Step5"></a>Sichern und Wiederherstellen protokollierter Daten der Protokollierung des Softwarebestands
Die Protokollierung des Softwarebestands speichert vorübergehend eine stündliche Datenerfassung, wenn die Weiterleitung über das Netzwerk fehlschlägt. Die Protokolldateien werden im Verzeichnis „\Windows\System32\LogFiles\SIL\“ gespeichert. Mit der regelmäßigen Server-Sicherung können auch diese Daten der Protokollierung des Softwarebestands gesichert werden.

> [!IMPORTANT]
> Wenn aus irgendeinem Grund eine Reparaturinstallation oder ein Upgrade des Betriebssystems erforderlich ist, gehen alle lokal gespeicherten Protokolldateien verloren.Wenn diese Daten wichtig für betriebliche Vorgänge sind, wird empfohlen, sie vor der Installation eines neuen Betriebssystems zu sichern. Führen Sie nach der Reparatur oder Aktualisierung einfach die Wiederherstellung am gleichen Speicherort durch.

> [!NOTE]
> Wenn aus irgendeinem Grund die Verwaltung der Beibehaltungs Dauer von Daten, die von SIL lokal protokolliert werden, wichtig ist, kann dies durch Ändern des folgenden Registrierungs Werts konfiguriert werden: \ HKEY_LOCAL_MACHINE \\ software\microsoft\windows\softwareinventorylogging. Der Standardwert ist "30" für 30 Tage.

## <a name="reading-data-logged-and-published-by-software-inventory-logging"></a><a name="BKMK_Step6"></a>Lesen protokollierter und veröffentlichter Daten der Protokollierung des Softwarebestands
Daten, die von SIL protokolliert, aber lokal gespeichert werden (wenn der Forward zum Ziel-URI fehlschlägt), oder Daten, die erfolgreich an den Ziel Aggregations Server weitergeleitet werden, werden in einer Binärdatei gespeichert (für die Daten der einzelnen Tage). Um diese Daten in PowerShell anzuzeigen, verwenden Sie das Cmdlet [Import-BinaryMiLog](https://technet.microsoft.com/library/dn262592.aspx) .

## <a name="software-inventory-logging-security"></a><a name="BKMK_Step7"></a>Sicherheit bei der Protokollierung des Softwarebestands
Auf dem lokalen Server sind Administratorrechte erforderlich, um erfolgreich Daten aus dem WMI der Protokollierung des Softwarebestands über PowerShell-APIs abzurufen.

Um alle Funktionen der Protokollierung des Softwarebestands zum stündlichen Weiterleiten von Verlaufsdaten an einen Aggregationspunkt nutzen zu können, muss der Administrator mithilfe von Clientzertifikaten sichere SSL-Sessions für das Weiterleiten von Daten über HTTPS gewährleisten. Eine grundlegende Übersicht über HTTPS-Authentifizierung finden Sie hier: [HTTPS-Authentifizierung](/previous-versions/windows/it-pro/windows-server-2003/cc736680(v=ws.10)).

Auf alle Daten, die lokal auf einem Windows-Server gespeichert sind (tritt nur auf, wenn die Funktion gestartet wurde, aber das Ziel nicht erreichbar ist), kann nur mit Administratorrechten auf dem lokalen Server zugegriffen werden.

## <a name="working-with-date-and-time-settings-in-windows-server-2012-r2-software-inventory-logging"></a><a name="BKMK_Step8"></a>Umgang mit Datums- und Uhrzeiteinstellungen bei der Windows Server 2012 R2-Protokollierung des Softwarebestands

-   Bei Verwendung von „ [Set-SilLogging](/previous-versions/windows/powershell-scripting/dn283387(v=wps.630)) - TimeOfDay“ zum Festlegen des Ausführungszeitpunkts für die SIL-Protokollierung müssen Sie ein Datum und eine Uhrzeit angeben.Das Kalenderdatum wird festgelegt, und die Protokollierung erfolgt erst, wenn das betreffende Datum in der lokalen Systemzeit erreicht wird.

-   Bei Verwendung von [Get-silsoftware](/previous-versions/windows/powershell-scripting/dn283397(v=wps.630))oder [Get-silwindowsupdate](/previous-versions/windows/powershell-scripting/dn283393(v=wps.630))zeigt "InstallDate" immer den bedeutungslosen Wert "12:00:00AM" an.

-   Bei Verwendung von [Get-silualaccess](/previous-versions/windows/powershell-scripting/dn283389(v=wps.630))zeigt "Sample Date" immer den bedeutungslosen Wert "11:59:00PM" an.Für diese Cmdlet-Abfragen ist „Date“ entscheidend.

## <a name="enabling-and-configuring-software-inventory-logging-in-a-mounted-virtual-hard-disk"></a><a name="BKMK_Step10"></a>Aktivieren und Konfigurieren der Protokollierung des Softwarebestands auf einem bereitgestellten virtuellen Datenträger
Die Protokollierung des Softwarebestands unterstützt auch das Konfigurieren und Aktivieren auf offline geschalteten virtuellen Computern. Die praktische Verwendung hierfür ist das Einrichten der "Gold Image"-Einrichtung für die weite Bereitstellung in Rechenzentren sowie das Konfigurieren von Endbenutzer Images, die von einem lokalen Standort zu einer cloudbereitstellung ausgehen.

Um diese Einsatzbereiche zu unterstützen, sind der Protokollierung des Softwarebestands Registrierungseinträge für jede konfigurierbare Option zugeordnet.  Diese Registrierungs Werte finden Sie unter \ HKEY_LOCAL_MACHINE \\ software\microsoft\windows\softwareinventorylogging.

| Funktion | Wertname | Daten | Entsprechendes Cmdlet (nur im ausgeführten Betriebssystem verfügbar) |
| --- | --- | --- | --- |
|Start/Stopp-Feature|CollectionState|1 oder 0|[Start-SilLogging](/previous-versions/windows/powershell-scripting/dn283391(v=wps.630)), [Stop-SilLogging](/previous-versions/windows/powershell-scripting/dn283394(v=wps.630))|
|Legt den Aggregationszielpunkt im Netzwerk fest|TargetUri|Zeichenfolge|[Set-SilLogging](/previous-versions/windows/powershell-scripting/dn283387(v=wps.630)) -TargetURI|
|Legt den Zertifikatfingerabdruck oder Hash des Zertifikats für die SSL-Authentifizierung für den Ziel-Webserver fest|CertificateThumbprint|Zeichenfolge|[Set-SilLogging](/previous-versions/windows/powershell-scripting/dn283387(v=wps.630)) -CertificateThumbprint|
|Legt das Datum und die Uhrzeit für den Startzeitpunkt der Funktion fest (sofern der angegebene Wert in der lokalen Systemzeit in der Zukunft liegt)|CollectionTime|Standard: 2000-01-01T03:00:00|[Set-SilLogging](/previous-versions/windows/powershell-scripting/dn283387(v=wps.630)) -TimeOfDay|

Um diese Werte auf einer offline geschalteten virtuellen Festplatte (VM-Betriebssystem wird nicht ausgeführt) zu ändern, muss die VHD zunächst bereitgestellt werden, und dann können die folgenden Befehle verwendet werden, um Änderungen vorzunehmen.

-   [Reg load](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc742053(v=ws.11))

-   [Reg delete](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc742145(v=ws.11))

-   [Reg add](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc742162(v=ws.11))

-   [Reg unload](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc742043(v=ws.11))

Die Protokollierung des Softwarebestands überprüft diese Werte beim Start des Betriebssystems und verfährt entsprechend.

## <a name="overview-of-using-software-inventory-logging-in-windows-server-2012-r2-without-kb-3000850"></a><a name="BKMK_Step11"></a>Übersicht über die Verwendung der Protokollierung des Softwarebestands in Windows Server 2012 R2 ohne KB 3000850
Die folgenden Änderungen am Umfang der Protokollierung des Softwarebestands und an den Standardeinstellungen wurden mit [KB 3000850](https://support.microsoft.com/kb/3000850) vorgenommen:

-   Das Standardintervall für die Sammlung und Weiterleitung über das Netzwerk beim Starten der SIL-Protokollierung wurde von täglich auf stündlich geändert (nach dem Zufallsprinzip innerhalb jeder Stunde).

-   Die Standard-Datennutzlast wurde reduziert und enthält nur Objekte aus Get-SilComputer, Get-SilComputerIdentity und Get-SilSoftware.

-   Die Gast-zu-Host-Kanalkommunikation in Hyper-V-Umgebungen wurde entfernt.

## <a name="using-software-inventory-logging-in-a-windows-server-2012-r2-hyper-v-environment-without-kb-3000850"></a><a name="BKMK_Step12"></a>Verwendung der Protokollierung des Softwarebestands in einer Windows Server 2012 R2 Hyper-V-Umgebung ohne KB 3000850

> [!NOTE]
> Diese Funktion wird bei Installation des [KB 3000850](https://support.microsoft.com/kb/3000850)-Updates entfernt.

Wenn Sie die Protokollierung des Software Bestands auf einem Hyper-V-Host unter Windows Server 2012 R2 verwenden, ist es möglich, SIL-Daten von Windows Server 2012 R2-Gast Computern abzurufen, die lokal ausgeführt werden, wenn die SIL-Protokollierung in den Gastbetriebssystemen gestartet wurde. Dies ist jedoch nur bei Verwendung der PowerShell-Cmdlets Get-sildata und Publish-sildata möglich und nur mit Windows Server 2012 R2 sowohl auf dem Host als auch auf dem Gast möglich.Diese Funktion ermöglicht Administratoren im Rechenzentrum, die Gast-VMs für ihre Mandanten bzw. andere Teilbereiche von Großunternehmen bereitstellen, das Erfassen von Softwarebestandsdaten auf dem Hypervisorhost und das anschließende Weiterleiten dieser Daten an einen Aggregator (oder Ziel-URI).

Im folgenden finden Sie zwei Beispiele dafür, wie die Ausgabe in der PowerShell-Konsole auf einem Windows Server 2012 R2 Hyper-V-Host, auf dem eine Windows Server 2012 R2-Gast-VM ausgeführt wird, mit der SIL-Protokollierung gestartet wird.Im ersten Beispiel, in dem nur Get-SilData verwendet wird, werden erwartungsgemäß alle Daten vom Host ausgegeben.Ebenfalls enthalten sind alle SIL-Daten des Gasts, jedoch in einem reduzierten Format.Um diese Daten vom Gast zu erweitern und anzuzeigen, verwenden Sie einfach per Ausschneiden und Einfügen das unten im zweiten Beispiel gezeigte Fragment.SDl-Datenobjekte des Gasts besitzen immer die mit dem Objekt verknüpfte VM-GUID.

> [!NOTE]
> Da SIL-Daten auf der Konsole ausgegeben werden, werden bei Verwendung des Get-SilData-Cmdlets mit Datenströmen die Objekte nicht immer in vorhersehbarer Reihenfolge ausgegeben.In beiden folgenden Beispielen wurde der Text nur zur Veranschaulichung farblich gekennzeichnet (Daten physischer Hosts in Blau, Daten virtueller Gäste in Grün).

**Ausgabebeispiel 1**

![Bild eines Beispielausgabe Berichts](../media/software-inventory-logging/SILHyper-VExample1.png)

**Ausgabe Beispiel 2** (w/Expand-sildata-Funktion)

![Bild eines Beispielausgabe Berichts](../media/software-inventory-logging/SILHyper-VExample2.png)

## <a name="see-also"></a>Weitere Informationen
[Beginnen Sie mit der Protokollierung](get-started-with-software-inventory-logging.md) 
 des Software Bestands Aggregator der Protokollierung des [Software Bestands](software-inventory-logging-aggregator.md) 
 [Cmdlets für die Protokollierung des Software Bestands in Windows PowerShell](/powershell/module/softwareinventorylogging/?view=winserver2012R2-ps) 
 [Import-binarymilog](https://technet.microsoft.com/library/dn262592.aspx) 
 [Export-binarymilog](https://technet.microsoft.com/library/dn262591.aspx)