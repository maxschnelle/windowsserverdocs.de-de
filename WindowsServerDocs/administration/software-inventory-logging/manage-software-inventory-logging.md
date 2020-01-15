---
title: Verwaltung der Protokollierung des Softwarebestands
description: Beschreibt, wie die Protokollierung des Software Bestands verwaltet wird
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: a14233e01c19df650d1059e1b60cd5398b05709a
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75946996"
---
# <a name="manage-software-inventory-logging"></a>Verwaltung der Protokollierung des Softwarebestands

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

In diesem Dokument wird beschrieben, wie Sie die Protokollierung des Software Bestands verwalten, ein Feature, mit dem Daten Center Administratoren Microsoft-softwareasset-Verwaltungsdaten problemlos für Ihre bereit Stellungen protokollieren können. In diesem Dokument wird beschrieben, wie Sie die Protokollierung des Softwarebestands verwalten. Bevor Sie die Protokollierung des Software Bestands mit Windows Server 2012 R2 verwenden, stellen Sie sicher, dass auf jedem System, das inventarisiert werden muss, Windows Update [KB 3000850](https://support.microsoft.com/kb/3000850) und [KB 3060681](https://support.microsoft.com/kb/3060681) installiert sind. Für Windows Server 2016 sind keine wndows-Updates erforderlich. Diese Funktion wird auf jedem Server lokal ausgeführt, dessen Bestand protokolliert werden soll. Es werden keine Daten von Remoteservern gesammelt.  

Die Protokollierung des Software Bestands kann auch zu zwei Versionen von Windows Server vor Windows Server 2012 R2 hinzugefügt werden. Sie können die folgenden Updates installieren, um die Protokollierungs Funktionalität für den Software bestand zu Windows Server 2012 und Windows Server 2008 R2 SP1 hinzuzufügen:

- **Windows Server 2012 (Standard oder Datacenter Edition)** 

> [!NOTE] 
> Vergewissern Sie sich, dass [WMF 4,0](https://www.microsoft.com/download/details.aspx?id=40855) installiert ist, bevor Sie das Update Paket unten anwenden.

-  WMF 4.0-Updatepaket für Windows Server 2012: [KB 3119938](https://support.microsoft.com/kb/3119938)

- **Windows Server 2008 R2 SP1**

> [!NOTE] 
> Vergewissern Sie sich, dass [WMF 4,0](https://www.microsoft.com/download/details.aspx?id=40855) installiert ist, bevor Sie das Update Paket unten anwenden.


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
  
**In diesem Dokument**  
  
In diesem Dokument werden folgende Konfigurationsoptionen behandelt:  
  
-   [Starten und Beenden der Protokollierung des Software Bestands](manage-software-inventory-logging.md#BKMK_Step1)  
  
-   [Protokollierung des Software Bestands im Zeitverlauf](manage-software-inventory-logging.md#BKMK_Step2)  
  
-   [Anzeigen der Protokollierungs Daten des Software Bestands](manage-software-inventory-logging.md#BKMK_Step3)  
  
-   [Löschen der von der Software Inventur Protokollierung protokollierten Daten](manage-software-inventory-logging.md#BKMK_Step4)  
  
-   [Sichern und Wiederherstellen von Daten, die von der Protokollierung des Software Bestands protokolliert werden] Manage-Software-Inventory-Logging. MD # BKMK_Step5)  
  
-   [Lesen und Veröffentlichen von Daten, die von der Protokollierung des Software Bestands](manage-software-inventory-logging.md#BKMK_Step6)  
  
-   [Sicherheit der Software Inventur Protokollierung](manage-software-inventory-logging.md#BKMK_Step7)  
  
-   [Arbeiten mit Datums-und Uhrzeit Einstellungen in der Windows Server-Software Inventur Protokollierung](manage-software-inventory-logging.md#BKMK_Step8)  
  
-   [Aktivieren und Konfigurieren der Protokollierung des Software Bestands auf einer bereitgestellten virtuellen Festplatte](manage-software-inventory-logging.md#BKMK_Step10)  
  
-   [Übersicht über die Verwendung der Protokollierung des Software Bestands in Windows Server 2012 R2 ohne KB 3000850](manage-software-inventory-logging.md#BKMK_Step11)  
  
-   [Verwenden der Protokollierung des Software Bestands in einer Windows Server 2012 R2 Hyper-V-Umgebung ohne KB 3000850](manage-software-inventory-logging.md#BKMK_Step12)  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter Verwenden von Cmdlets.

  
## <a name="BKMK_Step1"></a>Starten und Beenden der Protokollierung des Software Bestands  
Die tägliche Erfassung der Software Inventur Protokollierung und die Weiterleitung über das Netzwerk müssen auf einem Computer mit Windows Server 2012 R2 aktiviert sein, um die Software Inventur protokollieren  
  
> [!NOTE]  
> Sie können das PowerShell-Cmdlet **[Get-SilLogging](https://technet.microsoft.com/library/dn283396.aspx)** verwenden, um Informationen zum Dienst für die Protokollierung des Softwarebestands abzurufen, z. B. ob er ausgeführt wird oder beendet wurde.  
  
#### <a name="to-start-software-inventory-logging"></a>So starten Sie die Protokollierung des Softwarebestands  
  
1.  Melden Sie sich mit einem Konto mit lokalen Administratorrechten am Server an.  
  
2.  Öffnen Sie PowerShell als Administrator.  
  
3.  Geben Sie an der PowerShell-Eingabeaufforderung **[Start SilLogging](https://technet.microsoft.com/library/dn283391.aspx)**  
  
> [!NOTE]  
> Es ist möglich, das Ziel festzulegen, ohne einen Fingerabdruck des Zertifikats einzurichten. Ein solches Vorgehen führt jedoch dazu, dass Weiterleitungen fehlschlagen und Daten lokal bis zu 30 Tage lang vorgehalten werden. (Nach Ablauf dieser Zeit werden sie gelöscht.) Sobald ein gültiges Zertifikat-Hash für das Ziel festgelegt (und das entsprechende gültige Zertifikat im LocalMachine/Personal Speicher installiert) wurde, werden lokal gespeicherte Daten an das Ziel weitergeleitet, sofern das Ziel so konfiguriert wurde, dass diese Daten mit diesem Zertifikat akzeptiert werden (weitere Informationen finden Sie unter [Software Inventory Logging Aggregator](Software-Inventory-Logging-Aggregator.md) ).  
  
#### <a name="to-stop-software-inventory-logging"></a>So beenden Sie die Protokollierung des Softwarebestands  
  
1.  Melden Sie sich mit einem Konto mit lokalen Administratorrechten am Server an.  
  
2.  Öffnen Sie PowerShell als Administrator.  
  
3.  Geben Sie an der PowerShell-Eingabeaufforderung **[Stop- SilLogging](https://technet.microsoft.com/library/dn283394.aspx)**  
  
## <a name="configuring-software-inventory-logging"></a>Konfigurieren der Protokollierung des Softwarebestands  
Sie führen drei Schritte aus, um die Protokollierung des Softwarebestands so zu konfigurieren, dass Daten nach und nach an einen Aggregationsserver weitergeleitet werden:  
  
1.  Verwenden Sie **Set-sillogging – targetUri** , um die Webadresse Ihres Aggregations Servers anzugeben (muss mit "https://" beginnen).  
  
2.  Verwenden Sie **Set-SilLogging –CertificateThumbprint** , um den Fingerabdruckhash Ihres gültigen SSL-Zertifikats anzugeben, der zum Authentifizieren der Datenübertragungen an den Aggregationsserver verwendet werden soll (der Aggregationsserver muss so konfiguriert werden, dass ein Hash akzeptiert wird).  
  
3.  Installieren Sie ein gültiges SSL-Zertifikat (für Ihr Netzwerk) im **LocalMachine/Personal-Speicher** (bzw. **/LocalMachine/MY**) des lokalen Servers, von dem aus die Daten weitergeleitet werden sollen.  
  
Es empfiehlt sich, die Schritte vor der Verwendung von **Start-SilLogging**auszuführen.  Wenn Sie die Schritte nach der Verwendung von **Start-SilLogging**ausführen möchten, müssen Sie SIL nur beenden und erneut starten.  Sie können auch mit dem Cmdlet Publish-SilData sicherstellen, dass der Aggregationsserver über eine vollständige Ergänzung der Daten für diesen Server verfügt.  
  
Eine umfassende Anleitung zum Einrichten des SIL-Frameworks als Ganzes finden Sie unter [Software Inventory Logging Aggregator](software-inventory-logging-aggregator.md).  Insbesondere sollten Sie den Abschnitt über die Problembehandlung zurate ziehen, wenn bei **Publish-SilData** ein Fehler auftritt oder wenn die SIL-Protokollierung auf andere Weise fehlschlägt.  
  
## <a name="BKMK_Step2"></a>Protokollierung des Software Bestands im Zeitverlauf  
Wenn die Protokollierung des Softwarebestands von einem Administrator gestartet wurde, beginnt die stündliche Sammlung und Weiterleitung der Daten an den Aggregationsserver (Ziel-URI). Die erste Weiterleitung besteht aus einem vollständigen Datensatz, den [Get-SilData](https://technet.microsoft.com/library/dn283388.aspx) abruft und zu einem bestimmten Zeitpunkt auf der Konsole anzeigt. Danach prüft SIL bei jedem Intervall die Daten und leitet nur eine kleine ID-Bestätigung an den Aggregationszielserver weiter, sofern seit der letzten Sammlung keine Änderung aufgetreten ist. Wenn ein Wert geändert wurde, sendet SIL erneut einen vollständigen Datensatz.  
  
> [!IMPORTANT]  
> Wenn in jedem Intervall der Ziel-URI nicht erreichbar ist, oder die Datenübertragung über das Netzwerk aus irgendeinem Grund nicht erfolgreich ist, werden gesammelte Daten lokal bis zu einem Standardwert von 30 Tagen gespeichert. (Nach Ablauf dieser Zeit werden sie gelöscht.) Bei der nächsten erfolgreichen Weiterleitung von Daten auf den Zielserver für die Aggregation werden alle lokal gespeicherten Daten weitergeleitet und lokal zwischengespeicherte Daten werden gelöscht.  
  
## <a name="BKMK_Step3"></a>Anzeigen der Protokollierungs Daten des Software Bestands  
Neben den im vorherigen Abschnitt beschriebenen PowerShell-Cmdlets stehen Ihnen in sechs weitere Cmdlets zum Sammeln von Daten der Protokollierung des Softwarebestands zur Verfügung:  
  
-   **[Get-silcomputer](https://technet.microsoft.com/library/dn283392.aspx)** : zeigt die Zeit Punktwerte für bestimmte Server-und betriebssystembezogene Daten sowie den voll qualifizierten Namen oder den Hostnamen des physischen Hosts an, falls verfügbar.  
  
-   **[Get-silcomputeridentity (KB 3000850)](https://technet.microsoft.com/library/dn858074.aspx)** : zeigt die von SIL verwendeten Bezeichner für einzelne Server an.  
  
-   **[Get-sildata](https://technet.microsoft.com/library/dn283388.aspx)** : zeigt eine Zeit Punkt Sammlung aller Protokollierungs Daten des Software Bestands an.  
  
-   **[Get-silsoftware](https://technet.microsoft.com/library/dn283397.aspx)** : zeigt die Identität des Zeitpunkts für die gesamte auf dem Computer installierte Software an.  
  
-   **[Get-silualaccess](https://technet.microsoft.com/library/dn283389.aspx)** : zeigt die Gesamtanzahl der eindeutigen Client Geräteanforderungen und Client Benutzer Anforderungen des Servers ab zwei Tagen an.  
  
-   **[Get-silwindowsupdate](https://technet.microsoft.com/library/dn283393.aspx)** : zeigt den Zeit Punkt der Liste aller auf dem Computer installierten Windows-Updates an.  
  
Ein typischer Anwendungsfall für Cmdlets zur Protokollierung des Softwarebestands wäre das Abfragen der Protokollierung des Softwarebestands für einen bestimmten Zeitpunkt der gesamten Protokollierung durch einen Administrator mithilfe von [Get-SilSoftware](https://technet.microsoft.com/library/dn283397.aspx).  
  
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
> Die Ausgabe dieses Cmdlets ist identisch mit der kombinierten Ausgabe aller anderen **Get-Sil** -Cmdlets, wobei sich durch die asynchrone Ausgabe auf der Konsole möglicherweise eine unterschiedliche Reihenfolge der Objekte ergibt.  
>   
> Die Protokollierung des Softwarebestands muss nicht gestartet sein, um die **Get-Sil** -Cmdlets verwenden zu können.  
  
## <a name="BKMK_Step4"></a>Löschen der von der Software Inventur Protokollierung protokollierten Daten  
Die Protokollierung des Softwarebestands wurde nicht als unternehmenskritische Komponente beabsichtigt. Sie ist so konzipiert, dass ihre Auswirkungen auf lokale Systemvorgänge so gering wie möglich sind und gleichzeitig eine hohe Zuverlässigkeit gewahrt wird. Dadurch kann der Administrator die Software Inventur Protokollierungs Datenbank und die unterstützenden Dateien (jede Datei im Verzeichnis "\windows\system32\logfiles\sil") auch manuell löschen, um betriebliche Anforderungen zu erfüllen.  
  
#### <a name="to-delete-data-logged-by-software-inventory-logging"></a>So löschen Sie mit der Protokollierung des Softwarebestands protokollierte Daten  
  
1. Beenden Sie in PowerShell die Protokollierung des Softwarebestands mit dem Befehl **[Stop-SilLogging](https://technet.microsoft.com/library/dn283394.aspx)** .  
  
2. Öffnen Sie Windows-Explorer.  
  
3. Wechseln Sie zu **\windows\system32\logfiles\sil\\**  
  
4. Löschen Sie alle Dateien im Ordner.  
  
## <a name="BKMK_Step5"></a>Sichern und Wiederherstellen von mit der Protokollierung des Software Bestands protokollierten Daten  
Die Protokollierung des Softwarebestands speichert vorübergehend eine stündliche Datenerfassung, wenn die Weiterleitung über das Netzwerk fehlschlägt. Die Protokolldateien werden im Verzeichnis „\Windows\System32\LogFiles\SIL\“ gespeichert. Mit der regelmäßigen Server-Sicherung können auch diese Daten der Protokollierung des Softwarebestands gesichert werden.  
  
> [!IMPORTANT]  
> Wenn aus irgendeinem Grund eine Reparaturinstallation oder ein Upgrade des Betriebssystems erforderlich ist, gehen alle lokal gespeicherten Protokolldateien verloren.  Wenn diese Daten für Vorgänge wichtig sind, sollten Sie vor der Installation eines neuen Betriebssystems gesichert werden. Führen Sie nach der Reparatur oder Aktualisierung einfach die Wiederherstellung am gleichen Speicherort durch.  
  
> [!NOTE]  
> Wenn aus irgendeinem Grund die Verwaltung der Beibehaltungs Dauer von Daten, die von SIL lokal protokolliert werden, wichtig ist, kann dies durch Ändern des folgenden Registrierungs Werts konfiguriert werden: \ HKEY_LOCAL_MACHINE\\software\microsoft\windows\softwareinventorylogging. Der Standardwert ist "30" für 30 Tage.  
  
## <a name="BKMK_Step6"></a>Lesen und Veröffentlichen von Daten, die von der Protokollierung des Software Bestands  
Daten, die von SIL protokolliert, aber lokal gespeichert werden (wenn der Forward zum Ziel-URI fehlschlägt), oder Daten, die erfolgreich an den Ziel Aggregations Server weitergeleitet werden, werden in einer Binärdatei gespeichert (für die Daten der einzelnen Tage). Um diese Daten in PowerShell anzuzeigen, verwenden Sie das Cmdlet [Import-BinaryMiLog](https://technet.microsoft.com/library/dn262592.aspx) .  
  
## <a name="BKMK_Step7"></a>Sicherheit der Software Inventur Protokollierung  
Auf dem lokalen Server sind Administratorrechte erforderlich, um erfolgreich Daten aus dem WMI der Protokollierung des Softwarebestands über PowerShell-APIs abzurufen.  
  
Um alle Funktionen der Protokollierung des Softwarebestands zum stündlichen Weiterleiten von Verlaufsdaten an einen Aggregationspunkt nutzen zu können, muss der Administrator mithilfe von Clientzertifikaten sichere SSL-Sessions für das Weiterleiten von Daten über HTTPS gewährleisten. Eine grundlegende Übersicht über HTTPS-Authentifizierung finden Sie hier: [HTTPS-Authentifizierung](https://technet.microsoft.com/library/cc736680(v=WS.10).aspx).  
  
Auf alle Daten, die lokal auf einem Windows-Server gespeichert sind (tritt nur auf, wenn die Funktion gestartet wurde, aber das Ziel nicht erreichbar ist), kann nur mit Administratorrechten auf dem lokalen Server zugegriffen werden.  
  
## <a name="BKMK_Step8"></a>Arbeiten mit Datums-und Uhrzeit Einstellungen in der Windows Server 2012 R2-Protokollierung des Software Bestands  
  
-   Bei Verwendung von „ [Set-SilLogging](https://technet.microsoft.com/library/dn283387.aspx) - TimeOfDay“ zum Festlegen des Ausführungszeitpunkts für die SIL-Protokollierung müssen Sie ein Datum und eine Uhrzeit angeben. Das Kalenderdatum wird festgelegt, und die Protokollierung erfolgt erst, wenn das Datum in der lokalen Systemzeit erreicht ist.  
  
-   Bei Verwendung von [Get-silsoftware](https://technet.microsoft.com/library/dn283397.aspx)oder [Get-silwindowsupdate](https://technet.microsoft.com/library/dn283393.aspx)zeigt "InstallDate" immer den bedeutungslosen Wert "12:00:00AM" an.  
  
-   Bei Verwendung von [Get-silualaccess](https://technet.microsoft.com/library/dn283389.aspx)zeigt "Sample Date" immer den bedeutungslosen Wert "11:59:00PM" an.  Date sind die relevanten Daten für diese Cmdlet-Abfragen.  
  
## <a name="BKMK_Step10"></a>Aktivieren und Konfigurieren der Protokollierung des Software Bestands auf einer bereitgestellten virtuellen Festplatte  
Die Protokollierung des Softwarebestands unterstützt auch das Konfigurieren und Aktivieren auf offline geschalteten virtuellen Computern. Die praktische Verwendung hierfür ist das Einrichten der "Gold Image"-Einrichtung für die weite Bereitstellung in Rechenzentren sowie das Konfigurieren von Endbenutzer Images, die von einem lokalen Standort zu einer cloudbereitstellung ausgehen.  
  
Um diese Einsatzbereiche zu unterstützen, sind der Protokollierung des Softwarebestands Registrierungseinträge für jede konfigurierbare Option zugeordnet.  Diese Registrierungs Werte finden Sie unter \ HKEY_LOCAL_MACHINE\\software\microsoft\windows\softwareinventorylogging.  
  
|||||  
|-|-|-|-|  
|**Funktion**|**Wertname**|**Daten**|**Entsprechendes Cmdlet (nur im laufenden Betriebssystem verfügbar)**|  
|Start/Stopp-Feature|CollectionState|1 oder 0|[Start-SilLogging](https://technet.microsoft.com/library/dn283391.aspx), [Stop-SilLogging](https://technet.microsoft.com/library/dn283394.aspx)|  
|Legt den Aggregationszielpunkt im Netzwerk fest|TargetUri|String|[Set-SilLogging](https://technet.microsoft.com/library/dn283387.aspx) -TargetURI|  
|Legt den Zertifikatfingerabdruck oder Hash des Zertifikats für die SSL-Authentifizierung für den Ziel-Webserver fest|CertificateThumbprint|String|[Set-SilLogging](https://technet.microsoft.com/library/dn283387.aspx) -CertificateThumbprint|  
|Legt das Datum und die Uhrzeit für den Startzeitpunkt der Funktion fest (sofern der angegebene Wert in der lokalen Systemzeit in der Zukunft liegt)|CollectionTime|Standard: 2000-01-01T03:00:00|[Set-SilLogging](https://technet.microsoft.com/library/dn283387.aspx) -TimeOfDay|  
  
Um diese Werte auf einer offline geschalteten virtuellen Festplatte (VM-Betriebssystem wird nicht ausgeführt) zu ändern, muss die VHD zunächst bereitgestellt werden, und dann können die folgenden Befehle verwendet werden, um Änderungen vorzunehmen.  
  
-   [Reg load](https://technet.microsoft.com/library/cc742053.aspx)  
  
-   [Reg delete](https://technet.microsoft.com/library/cc742145.aspx)  
  
-   [Reg add](https://technet.microsoft.com/library/cc742162.aspx)  
  
-   [Reg unload](https://technet.microsoft.com/library/cc742043.aspx)  
  
Die Protokollierung des Softwarebestands überprüft diese Werte beim Start des Betriebssystems und verfährt entsprechend.  
  
## <a name="BKMK_Step11"></a>Übersicht über die Verwendung der Protokollierung des Software Bestands in Windows Server 2012 R2 ohne KB 3000850  
Die folgenden Änderungen am Umfang der Protokollierung des Softwarebestands und an den Standardeinstellungen wurden mit [KB 3000850](https://support.microsoft.com/kb/3000850)vorgenommen:  
  
-   Das Standardintervall für die Sammlung und Weiterleitung über das Netzwerk beim Starten der SIL-Protokollierung wurde von täglich auf stündlich geändert (nach dem Zufallsprinzip innerhalb jeder Stunde).  
  
-   Die Standard-Datennutzlast wurde reduziert und enthält nur Objekte aus Get-SilComputer, Get-SilComputerIdentity und Get-SilSoftware.  
  
-   Die Gast-zu-Host-Kanalkommunikation in Hyper-V-Umgebungen wurde entfernt.  
  
## <a name="BKMK_Step12"></a>Verwenden der Protokollierung des Software Bestands in einer Windows Server 2012 R2 Hyper-V-Umgebung ohne KB 3000850  
  
> [!NOTE]  
> Diese Funktion wird bei Installation des [KB 3000850](https://support.microsoft.com/kb/3000850) -Updates entfernt.  
  
Wenn Sie die Protokollierung des Software Bestands auf einem Hyper-V-Host unter Windows Server 2012 R2 verwenden, ist es möglich, SIL-Daten von Windows Server 2012 R2-Gast Computern abzurufen, die lokal ausgeführt werden, wenn die SIL-Protokollierung in den Gastbetriebssystemen gestartet wurde. Dies ist jedoch nur bei Verwendung der PowerShell-Cmdlets Get-sildata und Publish-sildata möglich und nur mit Windows Server 2012 R2 sowohl auf dem Host als auch auf dem Gast möglich.  Der Zweck dieser Funktion besteht darin, Administratoren von Rechenzentren, die Gast-VMs für Mandanten oder andere Entitäten eines großen Unternehmens bereitstellen, das Erfassen von Software Inventur Daten auf dem Hypervisor-Host und das anschließende Weiterleiten dieser Daten an einen Aggregator (oder Ziel-URI).  
  
Im folgenden finden Sie zwei Beispiele dafür, wie die Ausgabe in der PowerShell-Konsole auf einem Windows Server 2012 R2 Hyper-V-Host, auf dem eine Windows Server 2012 R2-Gast-VM ausgeführt wird, mit der SIL-Protokollierung gestartet wird.  Sie werden feststellen, dass im ersten Beispiel, in dem "Get-sildata" allein verwendet wird, alle Daten von dem Host wie erwartet ausgegeben werden.  Ebenfalls enthalten sind alle SIL-Daten des Gasts, jedoch in einem reduzierten Format.  Um diese Daten vom Gast zu erweitern und anzuzeigen, schneiden Sie einfach den im zweiten Beispiel verwendeten Ausschnitt aus, und fügen Sie ihn ein.  SIL-Datenobjekte vom Gast verfügen immer über die VM-GUID, die dem Objekt zugeordnet ist.  
  
> [!NOTE]  
> Da SIL-Daten auf der Konsole ausgegeben werden, werden bei Verwendung des Get-SilData-Cmdlets mit Datenströmen die Objekte nicht immer in vorhersehbarer Reihenfolge ausgegeben.  In den beiden folgenden Beispielen wurde der Text farblich (blau für physische Hostdaten und grün für virtuelle Gastdaten) als Illustrations Tool für dieses Dokument codiert.  
  
**Ausgabe Beispiel 1**  
  
![](../media/software-inventory-logging/SILHyper-VExample1.png)  
  
**Ausgabe Beispiel 2** (w/Expand-sildata-Funktion)  
  
![](../media/software-inventory-logging/SILHyper-VExample2.png)  
  
## <a name="see-also"></a>Siehe auch  
[Beginnen Sie mit der Protokollierung des Software Bestands](get-started-with-software-inventory-logging.md)  
[Aggregator der Protokollierung des Softwarebestands](software-inventory-logging-aggregator.md)  
[Cmdlets für die Protokollierung des Software Bestands in Windows PowerShell](https://technet.microsoft.com/library/dn283390.aspx)  
[Import-binarymilog](https://technet.microsoft.com/library/dn262592.aspx)  
[Export-binarymilog](https://technet.microsoft.com/library/dn262591.aspx)  
  

