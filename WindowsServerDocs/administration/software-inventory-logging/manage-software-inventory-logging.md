---
title: Verwaltung der Protokollierung des Softwarebestands
description: Beschreibt, wie Sie die Protokollierung des Softwarebestands verwalten
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: manage-software-inventory-logging
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 812173d1-2904-42f4-a9e2-de19effec201
author: brentfor
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 095cd2ad799857b789943b4f477aa9e6a8c3ae50
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815181"
---
# <a name="manage-software-inventory-logging"></a>Verwaltung der Protokollierung des Softwarebestands

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2019, Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2

Dieses Dokument beschreibt, wie Sie die Protokollierung des Softwarebestands, eine Funktion zu verwalten, die Administratoren im Rechenzentrum einfaches Protokollieren der Microsoft-Software Asset Management-Daten für ihre Bereitstellungen im Laufe der Zeit ermöglicht. In diesem Dokument wird beschrieben, wie Sie die Protokollierung des Softwarebestands verwalten. Bevor Sie die Protokollierung des Softwarebestands in Windows Server 2012 R2 verwenden, stellen Sie sicher, dass Windows Update [KB 3000850](https://support.microsoft.com/kb/3000850) und [KB 3060681](https://support.microsoft.com/kb/3060681) installiert sind, auf jedem System, dessen Bestand protokolliert werden. Es sind keine Windows-Updates für Windows Server 2016 erforderlich. Diese Funktion wird auf jedem Server lokal ausgeführt, dessen Bestand protokolliert werden soll. Es werden keine Daten von Remoteservern gesammelt.  

Die Funktion die Protokollierung des Softwarebestands kann auch zu zwei Versionen von Windows Server vor Windows Server 2012 R2 hinzugefügt werden. Sie können die folgenden Updates zum Hinzufügen von Protokollierung des Softwarebestands Funktionalität auf Windows Server 2012 und Windows Server 2008 R2 SP1 installieren:

- **Unter WindowsServer 2012 (Standard oder Datacenter Edition)** 

> [!NOTE] 
> Stellen Sie sicher, dass [WMF 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) installiert, bevor Sie die unten stehende Updatepaket installieren.

-  WMF 4.0-Updatepaket für Windows Server 2012: [KB 3119938](https://support.microsoft.com/en-us/kb/3119938)

- **Windows Server 2008 R2 SP1**

> [!NOTE] 
> Stellen Sie sicher, dass [WMF 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) installiert, bevor Sie die unten stehende Updatepaket installieren.


- Erfordert [.NET Framework 4.5](https://www.microsoft.com/en-us/download/details.aspx?id=30653)


- WMF 4.0-Updatepaket für Windows Server 2008 R2: [KB 3109118](https://support.microsoft.com/en-us/kb/3109118)


Es gibt bei der Nutzung dieser Funktion zwei primäre Methoden für die Inventur:  
  
1.  Starten der SIL-Protokollfunktion zum Sammeln aus SIL-Datenquellen und stündliches Weiterleiten der Nutzlast über das Netzwerk an ein angegebenes Ziel (URI).  
  
2.  Manuelles Abfragen der SIL-Daten in beliebigen Abständen mithilfe von PowerShell oder WMI.  
  
Das Starten der SIL-Protokollierung erfordert einige Planung und Vorausschau, hat jedoch erhebliche Vorteile gegenüber dem manuellen Abfragen der Daten. Die SIL-Protokollierung bietet folgende drei Hauptvorteile für Administratoren im Rechenzentrum:  
  
-   Eine Verlauf (Protokoll) kann im Lauf der Zeit erfasst werden und ermöglicht flexible und umfassende Berichte aus einer einzigen Quelle.  
  
-   Herausforderungen bei der Ermittlung von Computern, die für viele Inventurwerkzeuge typisch sind, lassen sich überwinden.  
  
-   Herausforderungen in Bezug auf Vertrauensgrenzen und Anforderungen für erhöhte Benutzerrechte, die für viele Inventurwerkzeuge typisch sind, lassen sich trotz Erhalt des Sicherheitsniveaus überwinden, da die Daten per SSL über HTTPS verschlüsselt werden.  
  
Die Protokollierung des Softwarebestands wird standardmäßig installiert, aber die Protokollierung nicht standardmäßig gestartet. Die gesamte Konfiguration der Protokollierung des Softwarebestands erfolgt mit PowerShell-Cmdlets. Für die Protokollierung des Softwarebestands sind nur wenige Konfigurationsoptionen verfügbar. Dieses Dokument beschreibt diese Optionen und deren Verwendungszweck, sowie die zum Sammeln von Daten verwendeten Cmdlets (bei Verwendung der zweiten oben genannten Methode).  
  
**In diesem Dokument**  
  
In diesem Dokument werden folgende Konfigurationsoptionen behandelt:  
  
-   [Starten und beenden die Software Softwareinventurprotokollierung](manage-software-inventory-logging.md#BKMK_Step1)  
  
-   [Protokollierung des Softwarebestands im Laufe der Zeit](manage-software-inventory-logging.md#BKMK_Step2)  
  
-   [Anzeigen von Daten für die Protokollierung des Softwarebestands](manage-software-inventory-logging.md#BKMK_Step3)  
  
-   [Löschen die Protokollierung des Softwarebestands protokollierte Daten](manage-software-inventory-logging.md#BKMK_Step4)  
  
-   [Sichern und Wiederherstellen von Daten, die von der Protokollierung des Softwarebestands protokollierten] verwalten-Software-Inventur-logging.md #BKMK_Step5)  
  
-   [Lesen von Daten protokolliert und veröffentlicht werden, indem Sie die Protokollierung des Softwarebestands](manage-software-inventory-logging.md#BKMK_Step6)  
  
-   [Sicherheit bei der Software Inventory Protokollierung](manage-software-inventory-logging.md#BKMK_Step7)  
  
-   [Arbeiten mit Datums- / Einstellungen in Windows Server die Protokollierung des Softwarebestands](manage-software-inventory-logging.md#BKMK_Step8)  
  
-   [Aktivieren und Konfigurieren von in einer bereitgestellten virtuellen Festplatte Protokollierung des Softwarebestands](manage-software-inventory-logging.md#BKMK_Step10)  
  
-   [Übersicht über die Verwendung der Softwareinventur, die Anmeldung bei WindowsServer 2012 R2 ohne KB 3000850](manage-software-inventory-logging.md#BKMK_Step11)  
  
-   [Protokollierung des Softwarebestands verwenden, in einer Windows Server 2012 R2 Hyper-V-Umgebung ohne KB 3000850](manage-software-inventory-logging.md#BKMK_Step12)  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter Verwenden von Cmdlets.

  
## <a name="BKMK_Step1"></a>Starten und beenden die Software Softwareinventurprotokollierung  
Software die Protokollierung des Softwarebestands tägliche sammeln und weiterleiten, über das Netzwerk müssen auf einem Computer unter Windows Server 2012 R2 die Softwareinventur Protokoll aktiviert sein.  
  
> [!NOTE]  
> Sie können das PowerShell-Cmdlet **[Get-SilLogging](https://technet.microsoft.com/library/dn283396.aspx)** verwenden, um Informationen zum Dienst für die Protokollierung des Softwarebestands abzurufen, z. B. ob er ausgeführt wird oder beendet wurde.  
  
#### <a name="to-start-software-inventory-logging"></a>So starten Sie die Protokollierung des Softwarebestands  
  
1.  Melden Sie sich mit einem Konto mit lokalen Administratorrechten am Server an.  
  
2.  Öffnen Sie PowerShell als Administrator.  
  
3.  Geben Sie an der PowerShell-Eingabeaufforderung **[Start SilLogging](https://technet.microsoft.com/library/dn283391.aspx)**  
  
> [!NOTE]  
> Es ist möglich, das Ziel festzulegen, ohne einen Fingerabdruck des Zertifikats einzurichten. Ein solches Vorgehen führt jedoch dazu, dass Weiterleitungen fehlschlagen und Daten lokal bis zu 30 Tage lang vorgehalten werden. (Nach Ablauf dieser Zeit werden sie gelöscht.) Sobald ein gültiges Zertifikat-Hash für das Ziel festgelegt (und das entsprechende gültige Zertifikat im LocalMachine/Personal Speicher installiert) wurde, werden lokal gespeicherte Daten an das Ziel weitergeleitet, sofern das Ziel so konfiguriert wurde, dass diese Daten mit diesem Zertifikat akzeptiert werden (weitere Informationen finden Sie unter [Software Inventory Logging Aggregator](Software-Inventory-Logging-Aggregator.md) ).  
  
#### <a name="to-stop-software-inventory-logging"></a>So beenden Sie die Protokollierung des Softwarebestands  
  
1.  Melden Sie sich mit einem Konto mit lokalen Administratorrechten am Server an.  
  
2.  Öffnen Sie PowerShell als Administrator.  
  
3.  Geben Sie an der PowerShell-Eingabeaufforderung **[Stop- SilLogging](https://technet.microsoft.com/library/dn283394.aspx)**  
  
## <a name="configuring-software-inventory-logging"></a>Konfigurieren der Protokollierung des Softwarebestands  
Sie führen drei Schritte aus, um die Protokollierung des Softwarebestands so zu konfigurieren, dass Daten nach und nach an einen Aggregationsserver weitergeleitet werden:  
  
1.  Verwendung **Set-SilLogging – TargetUri** auf die Webadresse Ihres aggregationsservers festzulegen (muss mit "https://? beginnen).  
  
2.  Verwenden Sie **Set-SilLogging –CertificateThumbprint** , um den Fingerabdruckhash Ihres gültigen SSL-Zertifikats anzugeben, der zum Authentifizieren der Datenübertragungen an den Aggregationsserver verwendet werden soll (der Aggregationsserver muss so konfiguriert werden, dass ein Hash akzeptiert wird).  
  
3.  Installieren Sie ein gültiges SSL-Zertifikat (für Ihr Netzwerk) im **LocalMachine/Personal-Speicher** (bzw. **/LocalMachine/MY**) des lokalen Servers, von dem aus die Daten weitergeleitet werden sollen.  
  
Es empfiehlt sich, die Schritte vor der Verwendung von **Start-SilLogging**auszuführen.  Wenn Sie die Schritte nach der Verwendung von **Start-SilLogging** ausführen möchten, müssen Sie SIL nur beenden und erneut starten.  Sie können auch mit dem Cmdlet Publish-SilData sicherstellen, dass der Aggregationsserver über eine vollständige Ergänzung der Daten für diesen Server verfügt.  
  
Eine umfassende Anleitung zum Einrichten des SIL-Frameworks als Ganzes finden Sie unter [Software Inventory Logging Aggregator](software-inventory-logging-aggregator.md).  Insbesondere sollten Sie den Abschnitt über die Problembehandlung zurate ziehen, wenn bei **Publish-SilData** ein Fehler auftritt oder wenn die SIL-Protokollierung auf andere Weise fehlschlägt.  
  
## <a name="BKMK_Step2"></a>Protokollierung des Softwarebestands im Laufe der Zeit  
Wenn die Protokollierung des Softwarebestands von einem Administrator gestartet wurde, beginnt die stündliche Sammlung und Weiterleitung der Daten an den Aggregationsserver (Ziel-URI). Die erste Weiterleitung besteht aus einem vollständigen Datensatz, den [Get-SilData](https://technet.microsoft.com/library/dn283388.aspx) abruft und zu einem bestimmten Zeitpunkt auf der Konsole anzeigt. Danach prüft SIL bei jedem Intervall die Daten und leitet nur eine kleine ID-Bestätigung an den Aggregationszielserver weiter, sofern seit der letzten Sammlung keine Änderung aufgetreten ist. Wenn ein Wert geändert wurde, sendet SIL erneut einen vollständigen Datensatz.  
  
> [!IMPORTANT]  
> Wenn in jedem Intervall der Ziel-URI nicht erreichbar ist, oder die Datenübertragung über das Netzwerk aus irgendeinem Grund nicht erfolgreich ist, werden gesammelte Daten lokal bis zu einem Standardwert von 30 Tagen gespeichert. (Nach Ablauf dieser Zeit werden sie gelöscht.) Bei der nächsten erfolgreichen Weiterleitung von Daten auf den Zielserver für die Aggregation werden alle lokal gespeicherten Daten weitergeleitet und lokal zwischengespeicherte Daten werden gelöscht.  
  
## <a name="BKMK_Step3"></a>Anzeigen von Daten für die Protokollierung des Softwarebestands  
Neben den im vorherigen Abschnitt beschriebenen PowerShell-Cmdlets stehen Ihnen in sechs weitere Cmdlets zum Sammeln von Daten der Protokollierung des Softwarebestands zur Verfügung:  
  
-   **[Get-SilComputer](https://technet.microsoft.com/library/dn283392.aspx)**: Zeigt sowohl den zeitlichen Verlauf der Werte für bestimmte Server und betriebssystembezogene Daten an, als auch den FQDN oder Hostnamen des physischen Hosts, falls verfügbar.  
  
-   **[Get-SilComputerIdentity (KB 3000850)](https://technet.microsoft.com/library/dn858074.aspx)**: Zeigt die von SIL verwendeten Bezeichner für einzelne Server an.  
  
-   **[Get-SilData](https://technet.microsoft.com/library/dn283388.aspx)**: Zeigt den gesammelten zeitlichen Verlauf aller Daten der Protokollierung des Softwarebestands an.  
  
-   **[Get-SilSoftware](https://technet.microsoft.com/library/dn283397.aspx)**: Zeigt die Identität im zeitlichen Verlauf der gesamten auf dem Computer installierten Software an.  
  
-   **[Get-SilUalAccess](https://technet.microsoft.com/library/dn283389.aspx)**: Zeigt für die vergangenen zwei Tage die Gesamtzahl der eindeutigen Clientanforderungen für Geräte und Benutzer an.  
  
-   **[Get-SilWindowsUpdate](https://technet.microsoft.com/library/dn283393.aspx)**: Zeigt den zeitlichen Verlauf der Liste aller auf dem Computer installierten Windows-Updates an.  
  
Ein typischer Anwendungsfall für Cmdlets zur Protokollierung des Softwarebestands wäre das Abfragen der Protokollierung des Softwarebestands für einen bestimmten Zeitpunkt der gesamten Protokollierung durch einen Administrator mithilfe von [Get-SilSoftware](https://technet.microsoft.com/library/dn283397.aspx).  
  
**Ausgabebeispiel**  
  
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
> Die Ausgabe dieses Cmdlets ist identisch mit der kombinierten Ausgabe aller anderen **Get-Sil** -Cmdlets, wobei sich durch die asynchrone Ausgabe auf der Konsole möglicherweise eine unterschiedliche Reihenfolge der Objekte ergibt.  
>   
> Die Protokollierung des Softwarebestands muss nicht gestartet sein, um die **Get-Sil**-Cmdlets verwenden zu können.  
  
## <a name="BKMK_Step4"></a>Löschen die Protokollierung des Softwarebestands protokollierte Daten  
Die Protokollierung des Softwarebestands wurde nicht als unternehmenskritische Komponente beabsichtigt. Sie ist so konzipiert, dass ihre Auswirkungen auf lokale Systemvorgänge so gering wie möglich sind und gleichzeitig eine hohe Zuverlässigkeit gewahrt wird. Dieser kann Administrator auch die Datenbank die Protokollierung des Softwarebestands und unterstützende Dateien (jede Datei im Verzeichnis der \Windows\System32\LogFiles\SIL) um betriebliche Anforderungen zu erfüllen manuell löschen.  
  
#### <a name="to-delete-data-logged-by-software-inventory-logging"></a>So löschen Sie mit der Protokollierung des Softwarebestands protokollierte Daten  
  
1.  Beenden Sie in PowerShell die Protokollierung des Softwarebestands mit dem Befehl **[Stop-SilLogging](https://technet.microsoft.com/library/dn283394.aspx)** .  
  
2.  Öffnen Sie Windows-Explorer.  
  
3.  Wechseln Sie zu **\Windows\System32\Logfiles\SIL\**  
  
4.  Löschen Sie alle Dateien im Ordner.  
  
## <a name="BKMK_Step5"></a>Sichern und Wiederherstellen der Protokollierung des Softwarebestands protokollierte Daten  
Die Protokollierung des Softwarebestands speichert vorübergehend eine stündliche Datenerfassung, wenn die Weiterleitung über das Netzwerk fehlschlägt. Die Protokolldateien werden im Verzeichnis „\Windows\System32\LogFiles\SIL\“ gespeichert. Mit der regelmäßigen Server-Sicherung können auch diese Daten der Protokollierung des Softwarebestands gesichert werden.  
  
> [!IMPORTANT]  
> Wenn aus irgendeinem Grund eine Reparaturinstallation oder ein Upgrade des Betriebssystems erforderlich ist, gehen alle lokal gespeicherten Protokolldateien verloren.  Wenn diese Daten wichtig für betriebliche Vorgänge sind, wird empfohlen, sie vor der Installation eines neuen Betriebssystems zu sichern. Führen Sie nach der Reparatur oder Aktualisierung einfach die Wiederherstellung am gleichen Speicherort durch.  
  
> [!NOTE]  
> Wenn aus irgendeinem Grund, der Verwaltung der Aufbewahrungsdauer Dauer der von SIL lokal protokollierten Daten wichtig ist, kann dies durch Ändern des folgenden Registrierungswerts konfiguriert werden: \HKEY_LOCAL_MACHINE\\SOFTWARE\Microsoft\Windows\SoftwareInventoryLogging. Der Standardwert beträgt „30“ für 30 Tage.  
  
## <a name="BKMK_Step6"></a>Lesen von Daten protokolliert und veröffentlicht werden, indem Sie die Protokollierung des Softwarebestands  
Die von der Protokollierung des Softwarebestands protokollierten Daten werden pro Tag in einer Binärdatei gespeichert, die bei nicht erfolgter Weiterleitung am Ziel-URI lokal gespeichert wird oder sich bei erfolgreicher Weiterleitung auf dem Aggregationszielserver befindet. Um diese Daten in PowerShell anzuzeigen, verwenden Sie das Cmdlet [Import-BinaryMiLog](https://technet.microsoft.com/library/dn262592.aspx) .  
  
## <a name="BKMK_Step7"></a>Sicherheit bei der Software Inventory Protokollierung  
Auf dem lokalen Server sind Administratorrechte erforderlich, um erfolgreich Daten aus dem WMI der Protokollierung des Softwarebestands über PowerShell-APIs abzurufen.  
  
Um alle Funktionen der Protokollierung des Softwarebestands zum stündlichen Weiterleiten von Verlaufsdaten an einen Aggregationspunkt nutzen zu können, muss der Administrator mithilfe von Clientzertifikaten sichere SSL-Sessions für das Weiterleiten von Daten über HTTPS gewährleisten. Eine grundlegende Übersicht über HTTPS-Authentifizierung finden Sie hier: [HTTPS-Authentifizierung](https://technet.microsoft.com/library/cc736680(v=WS.10).aspx).  
  
Auf alle Daten, die lokal auf einem Windows-Server gespeichert sind (tritt nur auf, wenn die Funktion gestartet wurde, aber das Ziel nicht erreichbar ist), kann nur mit Administratorrechten auf dem lokalen Server zugegriffen werden.  
  
## <a name="BKMK_Step8"></a>Arbeiten mit Datums- / Einstellungen in Windows Server 2012 R2 die Protokollierung des Softwarebestands  
  
-   Bei Verwendung von „ [Set-SilLogging](https://technet.microsoft.com/library/dn283387.aspx) - TimeOfDay“ zum Festlegen des Ausführungszeitpunkts für die SIL-Protokollierung müssen Sie ein Datum und eine Uhrzeit angeben. Das Kalenderdatum wird festgelegt, und die Protokollierung erfolgt erst, wenn das betreffende Datum in der lokalen Systemzeit erreicht wird.  
  
-   Bei Verwendung [Get-SilSoftware](https://technet.microsoft.com/library/dn283397.aspx), oder [Get-SilWindowsUpdate](https://technet.microsoft.com/library/dn283393.aspx), "InstallDate? 12:00:00 Uhr, bedeutungslosen Wert wird immer angezeigt werden.  
  
-   Bei Verwendung [Get-SilUalAccess](https://technet.microsoft.com/library/dn283389.aspx), "SampleDate? 23:59:00 Uhr, bedeutungslosen Wert wird immer angezeigt werden.  Für diese Cmdlet-Abfragen ist „Date“ entscheidend.  
  
## <a name="BKMK_Step10"></a>Aktivieren und Konfigurieren von in einer bereitgestellten virtuellen Festplatte Protokollierung des Softwarebestands  
Die Protokollierung des Softwarebestands unterstützt auch das Konfigurieren und Aktivieren auf offline geschalteten virtuellen Computern. Praktische Verwendungsmöglichkeiten hierfür sind „Gold-Image“-Setups zur breitflächigen Bereitstellung in Rechenzentren oder das Konfigurieren von Benutzerabbildern, deren Hosting vom Standort in die Cloud verlagert werden soll.  
  
Um diese Einsatzbereiche zu unterstützen, sind der Protokollierung des Softwarebestands Registrierungseinträge für jede konfigurierbare Option zugeordnet.  Diese Registrierungswerte finden Sie unter \HKEY_LOCAL_MACHINE\\SOFTWARE\Microsoft\Windows\SoftwareInventoryLogging.  
  
|||||  
|-|-|-|-|  
|**Funktion**|**Wertname**|**Daten**|**Entsprechendes Cmdlet (nur im ausgeführten Betriebssystem verfügbar)**|  
|Start/Stopp-Feature|CollectionState|1 oder 0|[Start-SilLogging](https://technet.microsoft.com/library/dn283391.aspx), [Stop-SilLogging](https://technet.microsoft.com/library/dn283394.aspx)|  
|Legt den Aggregationszielpunkt im Netzwerk fest|TargetUri|String|[Set-SilLogging](https://technet.microsoft.com/library/dn283387.aspx) -TargetURI|  
|Legt den Zertifikatfingerabdruck oder Hash des Zertifikats für die SSL-Authentifizierung für den Ziel-Webserver fest|CertificateThumbprint|String|[Set-SilLogging](https://technet.microsoft.com/library/dn283387.aspx) -CertificateThumbprint|  
|Legt das Datum und die Uhrzeit für den Startzeitpunkt der Funktion fest (sofern der angegebene Wert in der lokalen Systemzeit in der Zukunft liegt)|CollectionTime|Standardwert:  2000-01-01T03:00:00|[Set-SilLogging](https://technet.microsoft.com/library/dn283387.aspx) -TimeOfDay|  
  
Um diese Werte auf einer offline geschalteten virtuellen Festplatte (VM-Betriebssystem wird nicht ausgeführt) zu ändern, muss die VHD zunächst bereitgestellt werden, und dann können die folgenden Befehle verwendet werden, um Änderungen vorzunehmen.  
  
-   [REG laden](https://technet.microsoft.com/library/cc742053.aspx)  
  
-   [Reg delete](https://technet.microsoft.com/library/cc742145.aspx)  
  
-   [REG hinzufügen](https://technet.microsoft.com/library/cc742162.aspx)  
  
-   [REG entladen](https://technet.microsoft.com/library/cc742043.aspx)  
  
Die Protokollierung des Softwarebestands überprüft diese Werte beim Start des Betriebssystems und verfährt entsprechend.  
  
## <a name="BKMK_Step11"></a>Übersicht über die Verwendung der Softwareinventur, die Anmeldung bei WindowsServer 2012 R2 ohne KB 3000850  
Die folgenden Änderungen am Umfang der Protokollierung des Softwarebestands und an den Standardeinstellungen wurden mit [KB 3000850](https://support.microsoft.com/kb/3000850)vorgenommen:  
  
-   Das Standardintervall für die Sammlung und Weiterleitung über das Netzwerk beim Starten der SIL-Protokollierung wurde von täglich auf stündlich geändert (nach dem Zufallsprinzip innerhalb jeder Stunde).  
  
-   Die Standard-Datennutzlast wurde reduziert und enthält nur Objekte aus Get-SilComputer, Get-SilComputerIdentity und Get-SilSoftware.  
  
-   Die Gast-zu-Host-Kanalkommunikation in Hyper-V-Umgebungen wurde entfernt.  
  
## <a name="BKMK_Step12"></a>Protokollierung des Softwarebestands verwenden, in einer Windows Server 2012 R2 Hyper-V-Umgebung ohne KB 3000850  
  
> [!NOTE]  
> Diese Funktion wird bei Installation des [KB 3000850](https://support.microsoft.com/kb/3000850) -Updates entfernt.  
  
Wenn Sie die Protokollierung des Softwarebestands auf einem Windows Server 2012 R2 Hyper-V-Host verwenden, ist es möglich, beim Abrufen des SIL-Daten aus Windows Server 2012 R2-Gäste, die lokal ausgeführt werden, wenn die SIL-Protokollierung in die-Gastcomputern gestartet wurde. Dies ist jedoch nur möglich, wenn Sie die Get-SilData und Publish-SilData-Powershell-Cmdlets verwenden, möglich und nur unter WIndows Server 2012 R2 im Host- und Gastbetriebssysteme.  Diese Funktion ermöglicht Administratoren im Rechenzentrum, die Gast-VMs für ihre Mandanten bzw. andere Teilbereiche von Großunternehmen bereitstellen, das Erfassen von Softwarebestandsdaten auf dem Hypervisorhost und das anschließende Weiterleiten dieser Daten an einen Aggregator (oder Ziel-URI).  
  
Im folgenden sind zwei Beispiele für welche die Ausgabe von der PowerShell-Konsole (stark gekürzte) auf einem Windows Server 2012 R2 Hyper-V-Host mit nur einem Windows Server 2012 R2-Gast aussehen würde, virtuelle Computer mit der SIL-Protokollierung gestartet.  Im ersten Beispiel, in dem nur Get-SilData verwendet wird, werden erwartungsgemäß alle Daten vom Host ausgegeben.  Ebenfalls enthalten sind alle SIL-Daten des Gasts, jedoch in einem reduzierten Format.  Um diese Daten vom Gast zu erweitern und anzuzeigen, verwenden Sie einfach per Ausschneiden und Einfügen das unten im zweiten Beispiel gezeigte Fragment.  SDl-Datenobjekte des Gasts besitzen immer die mit dem Objekt verknüpfte VM-GUID.  
  
> [!NOTE]  
> Da SIL-Daten auf der Konsole ausgegeben werden, werden bei Verwendung des Get-SilData-Cmdlets mit Datenströmen die Objekte nicht immer in vorhersehbarer Reihenfolge ausgegeben.  In beiden folgenden Beispielen wurde der Text nur zur Veranschaulichung farblich gekennzeichnet (Daten physischer Hosts in Blau, Daten virtueller Gäste in Grün).  
  
**Ausgabebeispiel 1**  
  
![](../media/software-inventory-logging/SILHyper-VExample1.png)  
  
**Ausgabebeispiel 2** (mit Expand-SilData-Funktion)  
  
![](../media/software-inventory-logging/SILHyper-VExample2.png)  
  
## <a name="see-also"></a>Siehe auch  
[Erste Schritte mit der Software Softwareinventurprotokollierung](get-started-with-software-inventory-logging.md)  
[Aggregator der Protokollierung des Softwarebestands](software-inventory-logging-aggregator.md)  
[Cmdlets für die Protokollierung von Software Inventory in Windows PowerShell](https://technet.microsoft.com/library/dn283390.aspx)  
[Import-BinaryMiLog](https://technet.microsoft.com/library/dn262592.aspx)  
[Export-BinaryMiLog](https://technet.microsoft.com/library/dn262591.aspx)  
  

