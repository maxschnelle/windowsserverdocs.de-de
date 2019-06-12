---
title: Server Performance Advisor Pack-Entwicklungsleitfaden
description: Server Performance Advisor Pack-Entwicklungsleitfaden
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c27dd0602c5993fd84e6956c2f50f6e2bfec8691
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435474"
---
# <a name="server-performance-advisor-pack-development-guide"></a>Server Performance Advisor Pack-Entwicklungsleitfaden

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows 8, Windows 10

Diese Entwicklungshandbuch für Microsoft Server Performance Advisor (SPA) bietet Richtlinien für Entwickler und Systemadministratoren, die Advisor-Packs entwickeln, um serverleistung zu analysieren.

Es wird davon ausgegangen, dass Sie mit Leistungsprotokolle und Warnungen (PLA), Leistungsindikatoren, registrierungseinstellungen, Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI), Event Tracing for Windows (ETW) und Transact-SQL (T-SQL) vertraut sind.

Weitere Informationen zum Verwenden von SPA finden Sie unter [Server Performance Advisor-Benutzerhandbuch](server-performance-advisor-users-guide.md).

## <a name="spa-advisor-pack-overview"></a>SPA Advisor Pack – Übersicht


Ein Advisor-Pack ist für eine bestimmte Serverrolle in der Regel für die ein, und es definiert Folgendes:

* Daten über PLA, einschließlich der Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI), Leistungsindikatoren, registrierungseinstellungen, Dateien und Ereignisablaufverfolgung für Windows (ETW) erfasst werden sollen

* Regeln, Warnungen und Empfehlungen angezeigt.

* Daten (erfassten Rohdaten, aggregierte Daten oder Top 10-Listen) angezeigt werden sollen

* Statistiken können einen Wert anzeigen, der im Laufe der Zeit ändert

* Statistikwerte, die hochgerechnet werden können

Ein Advisor-Pack enthält die folgenden Elemente:

* **XML-Metadaten** (ProvisionMetadata.xml)

    * [Leistungsprotokolle und Warnungen (PLA)](https://msdn.microsoft.com/library/windows/desktop/aa372635.aspx) datensammlersatz

    * Berichtslayout

* **SQL-Skripts**

    * Eine main-Prozedur

    * SQL-Objekte, z. B. gespeicherte Prozeduren und benutzerdefinierten Funktionen

* **ETW-Schemadatei** ("Schema.man") Dies ist optional

### <a name="advisor-pack-workflow"></a>Advisor-Pack-workflow

![Advisor-Pack-workflow](../media/server-performance-advisor/spa-dev-guide-workflow.png)

In diesem Flussdiagramm stellen die grünen Kreise Advisor-Packs dar. Alle anderen Kreise dar, die Phasen, die gerade die SPA-Framework ausgeführt werden. SPA verwendet einen Advisor-Pack, um Daten sammeln, in der Datenbank zu importieren, initialisieren die ausführungsumgebung und SQL-Skripts.

### <a name="collect-data"></a>Sammeln von Daten

Bei ein Advisor-Pack für einen bestimmten Server mithilfe der SPA eingereiht wird, das Datenmodul für die Sammlung aus dem Advisor-Pack den datensammlersatz XML-Abfragen und Sammeln von Daten auf dem Zielserver Die unformatierten Daten werden in einer vom Benutzer angegebene Dateifreigabe gespeichert. Die Datensammlung wird nicht beendet, bis der einseitigen Anwendung, die vom Benutzer festgelegten Dauer der Ausführung überschritten wird.

### <a name="import-data-into-the-database"></a>Importieren von Daten in der Datenbank

Nachdem die Datensammlung abgeschlossen ist, wird jede Art von Daten in eine entsprechende Tabelle in der SQL Server-Datenbank importiert. Registrierungseinstellungen werden z. B. in eine Tabelle namens importiert \#RegistryKeys.

Importieren von ETW erfordert Datei eine ETW-Schemadatei für das Decodieren der ETL-Datei an. Die ETW-Schema-Datei ist eine XML-Datei. Er kann generiert werden, mithilfe der tracerpt.exe, die in Windows enthalten ist. Die ETW-Schemadatei ist nur erforderlich, wenn das Advisor-Pack, um ETW-Daten zu importieren muss.

### <a name="switch-to-low-user-rights"></a>Wechseln Sie zur Benutzers mit geringen rechten

Die SPA-Framework wird automatisch die Berechtigungen, um die erforderliche sicherheitszugriffsebene zu minimieren. Da es sich bei Advisor-Packs entwickelt wurden, oder von jedem Benutzer geändert werden können, ist es möglich, für eine Advisor-Pack manipulierte SQL-Skripts enthalten. Um das Sicherheitsrisiko zu verringern, sollten alle SQL-Skript für eine Advisor-Pack mit Benutzers mit geringen Rechten ausgeführt werden. Es kann nur begrenzte Datenbankobjekte, z. B. temporäre Tabellen und SPA-APIs, die verfügbar gemacht werden, wie gespeicherte Prozeduren zugreifen. Die SQL-Skripts in einem Advisor-Pack können diese Aufrufen gespeicherter Prozeduren für die Interaktion mit der SPA-Framework.

### <a name="initialize-execution-environment"></a>Initialisieren der ausführungsumgebung

Advisor-Packs können verschiedene Arten von Ausgabe, wie etwa Benachrichtigungen, Empfehlungen, Faktentabellen, Statistiken und Diagramme für Statistiken generieren. Die SQL-Skripts Berechnungen bestimmte anhand der gesammelten Daten. Die zurückgegebenen Ergebnisse werden in temporären Tabellen über öffentliche APIs SPA gespeichert. Klicken Sie auf der Initialisierungsphase müssen diese temporären Tabellen und andere Systemressourcen bereitgestellt werden.

### <a name="run-sql-scripts"></a>SQL-Skripts

Es gibt eine main gespeicherte Prozedur, mit dem Namen der Advisor-Pack-Entwickler. Die SPA-Framework ruft diese gespeicherte Prozedur, um die Berechnung zu initiieren. Die gespeicherte Prozedur nutzt die gesammelten Daten und das Endergebnis der SPA-Framework kommuniziert.

### <a name="switch-to-administrative-rights"></a>Wechseln Sie zur Administratorrechte

Administratorrechte sind erforderlich, um einen Bericht zu generieren. Berichterstellung wird vollständig von SPA gesteuert. Es ist weniger wahrscheinlich, dass Sie nicht manipuliert werden.

### <a name="generate-a-report"></a>Generieren eines Berichts

Bevor Sie die main-Prozedur für eine Advisor-Pack abgeschlossen ist, werden die berechneten Ergebnisse, wie etwa Benachrichtigungen und Statistiken nicht beibehalten. Während dieser Phase werden die SPA-Framework die Ergebnisse von temporären Tabellen auf Tabellen in einem bestimmten Format übertragen. Nach Abschluss dieser Phase können Sie die Berichte mithilfe der SPA-Konsole anzeigen.

## <a name="authoring-an-advisor-pack"></a>Erstellen einen Advisor-pack


### <a name="quick-guidelines"></a>Kurze Richtlinien

Das folgende Flussdiagramm beschreibt die Schritte für die Sie entwickeln eine voll funktionsfähige Advisor-Pack. Dieser Abschnitt enthält auch detaillierte Beispiele, die jeden Schritt besser zu erläutern.

![Advisor-Pack-Entwicklungsprozess](../media/server-performance-advisor/spa-dev-guide-dev-flowchart.png)

Ein Advisor-Pack ist in der Regel wie folgt strukturiert:

Advisor-pack

ProvisionMetadata.xml

Scripts

main.sql

func.sql

Schema.man

Alle Advisor-Pack benötigen eine Datei namens ProvisionMetadata.xml. Sie definiert die grundlegenden Advisor-Pack-Informationen, welche Daten zu sammeln, Benachrichtigungen, Regeln und wie der Bericht gespeichert und angezeigt werden muss. Die SPA-Framework verwendet diese Informationen, um eine temporäre Tabelle zu generieren und übertragen dann die Ergebnisse in die temporäre Tabelle in eine Tabelle, die Benutzer zugreifen können.

Alle Berichts SQL-Skripts müssen gespeichert werden, in einem Unterordner namens **Skripts**. Zu Wartungszwecken empfehlen wir, dass Sie andere Datenbankobjekte in verschiedenen SQL Server-Dateien speichern. Es muss mindestens eine gespeicherte Prozedur als Einstiegspunkt in main Verwaltungspunkt vorhanden sein.

> [!NOTE]
> Die Datei "Schema.man" ist nicht erforderlich, es sei denn, das Advisor-Pack ETW-ablaufverfolgungen werden erfasst. Die Schemadatei wird um das Schema der ETW-Ereignisse zu beschreiben und Decodierung von ETW-Ereignissen verwendet.

### <a name="defining-basic-information"></a>Definieren grundlegenden Informationen

Dieser Abschnitt beschreibt einige der grundlegenden Elemente, die einem Advisor-Pack, einschließlich ProvisionMetadata.xml und Attribute bilden.

Im folgenden finden ein Beispiel für einen Header für die ProvisionMetadata.xml-Datei:

``` syntax
<advisorPack
xmlns="http://microsoft.com/schemas/ServerPerformanceAdvisor/ap/2010"
name="Microsoft.ServerPerformanceAdvisor.CoreOS.V2"
displayName="Microsoft CoreOS Advisor Pack V2"
description="Microsoft CoreOS Advisor Pack"
author="Microsoft"
version="1.0"
frameworkversion="3.0"
minOSversion="6.0"
reportScript="ReportScript">
</advisorPack>
```

### <a name="advisor-pack-version"></a>Advisor-Pack-version

Attributname: **Version**

Advisor-Pack-Entwickler können die Haupt- und Nebenversionsnummern Versionen für das Advisor-Pack definieren:

* Eine Hauptversion umfasst normalerweise erhebliche Verbesserungen. Die Ergebnisse, die mit einer älteren Version generiert werden möglicherweise nicht kompatibel mit den neuen Wert. Es wird dringend empfohlen, einschließlich der Hauptversion in der Advisor-Pack-Name.

* SPA ermöglicht Nebenversion Upgrades, wenn nur geringfügige Änderungen problemlos Inkompatibilität Daten vorhanden sind.

Weitere Informationen zur versionsverwaltung finden Sie unter [Weiterführende Themen](#bkmk-advancedtopics).

### <a name="script-entry-point"></a>Skript-Einstiegspunkt

Attributname: **ReportScript**

Die SPA-Framework sucht nach Namen der wichtigsten gespeicherten Prozedur, von der Skript-Einstiegspunkt und auf sichere Weise ausgeführt.

### <a name="other-attributes"></a>Andere Attribute

Hier sind einige andere Attribute, die zum Identifizieren eines Advisor-Packs verwendet werden können:

* Anzeigename: **"DisplayName"**

* Beschreibung: **Beschreibung**

* Autor: **Autor**

* Framework-Version: **Frameworkversion** (standardmäßig 3.0)

* Mindestens erforderliche Betriebssystemversion: **MinOSversion** (Dies ist für eine zukünftige Erweiterbarkeit reserviert)

* Ereignisbenachrichtigung verloren: **ShowEventLostWarning**

### <a href="" id="bkmk-definedatacollector"></a>Definieren den datensammlersatz

Ein Sammlungssatz definiert die Leistungsdaten, die die SPA-Framework auf dem Zielserver gesammelt werden sollen. Es unterstützt die Registrierung, WMI-Einstellungen von Leistungsindikatoren, die aus der Zielserver, und klicken Sie auf ETW-Dateien.

``` syntax
<advisorPack>
<dataSourceDefinition xmlns="http://microsoft.com/schemas/ServerPerformanceAdvisor/dc/2010">
 <dataCollectorSet duration="10">
<registryKeys>
 ?<registryKey>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes\\</registryKey>
</registryKeys>
<managementpaths>
 ?<path>Root\Cimv2:select * FROM Win32_DiskDrive</path>
</managementpaths>
<performanceCounters interval="2">
 ?<performanceCounter>\PhysicalDisk(*)\Avg. Disk sec/Transfer</performanceCounter>
</performanceCounters>
<files>
 ?<path>%windir%\System32\inetsrv\config\applicationHost.config</path>
</files>
<providers>
 ?<provider session="NT Kernel Logger" guid="{9E814AAD-3204-11D2-9A82-006008A86939}" keywordsany="06010201" keywordsAll="00000000" level="00000000" />
</providers>
 </dataCollectorSet>
</dataSourceDefinition>
</advisorPack>
```

Die **Dauer** Attribut **&lt;DataCollectorSet /&gt;** im vorherigen Beispiel definiert die Dauer der Datensammlung (die Zeiteinheit ist Sekunden). **Dauer** ist ein erforderliches Attribut. Diese Einstellung steuert die Dauer von Auflistung, die von Leistungsindikatoren und ETW verwendet wird.

### <a name="collect-registry-data"></a>Sammeln von Registrierungsdaten

Sie können die folgenden Registrierungsstrukturen Registrierungsdaten zusammenfassen:

* HKEY\_KLASSEN\_STAMM

* HKEY\_CURrenT\_CONFIG

* HKEY\_CURrenT\_USER

* HKEY\_LOKALEN\_COMPUTER

* HKEY\_BENUTZER

Um einen Registrierungseintrag zu erfassen, geben Sie den vollständigen Pfad zu den Namen des Werts: HKEY\_LOCAL\_MACHINE\\MyKey\\MyValue

Um alle Einstellungen unter dem Registrierungsschlüssel sammeln möchten, geben Sie den vollständigen Pfad zum Registrierungsschlüssel: HKEY\_LOCAL\_MACHINE\\MyKey\\

Um alle Werte unter einem Registrierungsschlüssel und dessen Unterschlüssel (PLA rekursiv sammelt die Registrierungsdaten,) zu erfassen, verwenden Sie zwei umgekehrte Schrägstriche für das letzte Pfadtrennzeichen aus: HKEY\_LOCAL\_MACHINE\\MyKey\\\\

Um Informationen in der Registrierung von einem Remotecomputer zu sammeln, enthalten Sie den Namen des Computers am Anfang des Registrierungspfads: HKEY\_LOCAL\_MACHINE\\MyKey\\MyValue

Beispielsweise müssen Sie einen Registrierungsschlüssel möglicherweise, der wie folgt aussieht:

``` syntax
Windows registry editor version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes]
"activePowerScheme"="db310065-829b-4671-9647-2261c00e86ef"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes\db310065-829b-4671-9647-2261c00e86ef]
"Description"=
 FriendlyName = Power Source Optimized 

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes\db310065-829b-4671-9647-2261c00e86ef \0012ee47-9041-4b5d-9b77-535fba8b1442\6738e2c4-e8a5-4a42-b16a-e040e769756e
"ACSettingIndex"=dword:000000b4
"DCSettingIndex"=dword:0000001e
```

Beispiel 1: Geben Sie nur die aktiven PowerSchemes und deren Werte zurück:

``` syntax
<registryKey>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes</registryKey>
```

Beispiel 2: Gibt alle Schlüssel-Wert-Paare unter diesem Pfad:

> [!NOTE]
> PLA, die unter den Anmeldeinformationen des Benutzers ausgeführt werden. Einige Registrierungsschlüssel werden administrative Anmeldeinformationen erforderlich sind. Die Enumeration wird beendet, wenn es nicht auf einen der untergeordneten Schlüssel zugegriffen.

``` syntax
<registryKey>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes\\</registryKey>
```

Alle gesammelte Daten in eine temporäre Tabelle namens importiert  **\#RegistryKeys** vor einem Bericht SQL-Skript ausgeführt wird. Die folgende Tabelle zeigt die Ergebnisse-Beispiel 2:

KeyName | KeytypeId | Wert
------ | ----- | -------
HKEY_LOCAL_MACHINE...\PowerSchemes | 1 | db310065-829b-4671-9647-2261c00e86ef
\db310065-829b-4671-9647-2261c00e86ef\Description | 2 | |
\db310065-829b-4671-9647-2261c00e86ef\FriendlyName | 2 | Die Stromquelle optimiert
...\6738e2c4-e8a5-4a42-b16a-e040e769756e\ACSettingIndex | 4 | 180
...\6738e2c4-e8a5-4a42-b16a-e040e769756e\DCSettingIndex | 4 | 30

Das Schema für die **#registryKeys** Tabelle ist eine wie folgt:

Spaltenname | SQL-Datentyp | Beschreibung
-------- | -------- | --------
KeyName | Nvarchar(300) nicht NULL | Vollständiger Pfad des Schlüssels Registrierungsname
KeytypeId | Smallint nicht NULL | Interner Typ-Id
Wert | Nvarchar(4000) nicht NULL | Alle Werte

Die **KeytypeID** Spalte kann einen der folgenden Typen aufweisen:

ID | Typ
--- | ---
1 | Zeichenfolge
2 | expandString
3 | Binär
4 | DWord
5 | DWordBigEndian
6 | Link
7 | MultipleString
8 | ResourceList
9 | FullResourceDescriptor
10 | ResourceRequirementslist
11 | Qword

### <a name="collect-wmi"></a>Sammeln von WMI

Sie können alle WMI-Abfrage hinzufügen. Weitere Informationen zum Schreiben von WMI-Abfragen finden Sie unter [WQL (WMI SQL)](https://msdn.microsoft.com/library/windows/desktop/aa394606.aspx). Das folgende Beispiel fragt einen Seite-Dateispeicherort:

``` syntax
<path>Root\Cimv2:select * FROM Win32_PageFileUsage</path>
```

Die Abfrage im obigen Beispiel gibt einen Datensatz zurück:

Beschriftung | Name | PeakUsage
----- | ----- | -----
C:\pagefile.sys | C:\pagefile.sys | 215

Da WMI gibt eine Tabelle mit unterschiedlichen Spalten zurück, wenn die gesammelten Daten in einer Datenbank importiert werden, wird SPA führt die datennormalisierung und wird in den folgenden Tabellen hinzugefügt:

**\#WMIObjects-Tabelle**

SequenceID | Namespace | ClassName | RelativePath | WmiqueryID
----- | ----- | ----- | ----- | -----
10 | Root\Cimv2 | Win32_PageFileUsage | Win32_PageFileUsage.Name=<br>C:\\pagefile.sys | 1

**\#WmiObjectsProperties-Tabelle**

ID | query
--- | ---
1 | Root\Cimv2:select * FROM Win32_PageFileUsage

**\#WmiQueries-Tabelle**

ID | query
--- | ---
1 | Root\Cimv2:select * FROM Win32_PageFileUsage

**\#Tabellenschema WmiObjects**

Spaltenname | SQL-Datentyp | Beschreibung
--- | --- | ---
SequenceId | Int nicht NULL | Korrelieren Sie die Zeile und seine Eigenschaften
Namespace | Nvarchar(200)-Datentyp gepackt ist nicht NULL | WMI-namespace
ClassName | Nvarchar(200)-Datentyp gepackt ist nicht NULL | WMI-Klassennamen
RelativePath | Nvarchar(500) nicht NULL | WMI-relativer Pfad
WmiqueryId | Int nicht NULL | Den Schlüssel des #WmiQueries korrelieren

**\#Tabellenschema WmiObjectProperties**

Spaltenname | SQL-Datentyp | Beschreibung
--- | --- | ---
SequenceId | Int nicht NULL | Korrelieren Sie die Zeile und seine Eigenschaften
Name | Nvarchar(1000) nicht NULL | Eigenschaftenname
Wert | Nvarchar(4000) NULL | Der Wert der aktuellen Eigenschaft

**\#Tabellenschema WmiQueries**

Spaltenname | SQL-Datentyp | Beschreibung
--- | --- | ---
Id | Int nicht NULL | > eindeutige Abfrage-ID
query | Nvarchar(4000) nicht NULL | Ursprüngliche Abfragezeichenfolge in den Metadaten bereitstellen

### <a name="collect-performance-counters"></a>Erfassen von Leistungsindikatoren

Hier ist s verdeutlicht, wie Sie einen Leistungsindikator erfassen:

``` syntax
<performanceCounters interval="1">
  <performanceCounter>\PhysicalDisk(*)\Avg. Disk sec/Transfer</performanceCounter>
</performanceCounters>
```

Die **Intervall** -Attribut ist eine erforderliche globale Einstellung für alle Leistungsindikatoren. Definiert das Intervall (die Zeiteinheit ist Sekunden) Sammeln von Leistungsdaten.

Im vorherigen Beispiel Leistungsindikator \\PhysicalDisk (\*)\\durchschn. Sek./Übertragung wird jede Sekunde abgefragt werden.

Es können zwei Instanzen vorhanden sein: **\_Insgesamt** und **0 "c:" D:** , und die Ausgabe könnte wie folgt:

timestamp | "CategoryName" | CounterName | Instanzwert _Total | Instanzwert von 0 "c:" D:
---- | ---- | ---- | ---- | ----
13:45:52.630 | PhysicalDisk | Durchschnittl. Sek./Übertragung | 0.00100008362473995 |0.00100008362473995
13:45:53.629 | PhysicalDisk | Durchschnittl. Sek./Übertragung | 0.00280023414927187 | 0.00280023414927187
13:45:54.627 | PhysicalDisk | Durchschnittl. Sek./Übertragung | 0.00385999853230048 | 0.00385999853230048
13:45:55.626 | PhysicalDisk | Durchschnittl. Sek./Übertragung | 0.000933297607934224 | 0.000933297607934224

Um die Daten in der Datenbank zu importieren, die Daten in eine Tabelle namens normalisiert  **\#PerformanceCounters**.

CategoryDisplayName | InstanceName | CounterdisplayName | Wert
---- | ---- | ---- | ----
PhysicalDisk | _Gesamt | Durchschnittl. Sek./Übertragung | 0.00100008362473995
PhysicalDisk | 0 C: D: | Durchschnittl. Sek./Übertragung | 0.00100008362473995
PhysicalDisk | _Gesamt | Durchschnittl. Sek./Übertragung | 0.00280023414927187
PhysicalDisk | 0 C: D: | Durchschnittl. Sek./Übertragung | 0.00280023414927187
PhysicalDisk | _Gesamt | Durchschnittl. Sek./Übertragung | 0.00385999853230048
PhysicalDisk | 0 C: D: | Durchschnittl. Sek./Übertragung | 0.00385999853230048
PhysicalDisk | _Gesamt | Durchschnittl. Sek./Übertragung | 0.000933297607934224
PhysicalDisk | 0 C: D: | Durchschnittl. Sek./Übertragung | 0.000933297607934224

**Beachten Sie** den Namen, z. B. lokalisierte **CategoryDisplayName** und **CounterdisplayName**, variieren abhängig von der Anzeigesprache auf dem Zielserver verwendet. Vermeiden Sie diese Felder verwenden, wenn Sie ein sprachneutrales Advisor Pack erstellen möchten.

**\#PerformanceCounters** Tabellenschema

Spaltenname | SQL-Datentyp | Beschreibung
---- | ---- | ---- | ----
timestamp | datetime2(3) nicht NULL | Die erfassten Datum-Zeit in UNC
"CategoryName" | Nvarchar(200)-Datentyp gepackt ist nicht NULL | Kategoriename
CategoryDisplayName | Nvarchar(200)-Datentyp gepackt ist nicht NULL | Lokalisierte Kategoriename
InstanceName | Nvarchar(200)-Datentyp gepackt ist NULL | Instanzenname
CounterName | Nvarchar(200)-Datentyp gepackt ist nicht NULL | Name des Leistungsindikators
CounterdisplayName | Nvarchar(200)-Datentyp gepackt ist nicht NULL | Lokalisierte Indikatorname
Wert | "Float" nicht NULL | Der ermittelte Wert

### <a name="collect-files"></a>Dateien sammeln

Die Pfade können absolut oder relativ sein. Der Dateiname kann das Platzhalterzeichen enthalten (\*) und Fragezeichen (?). Z. B. zum erfassen alle Dateien im temporären Ordner können, geben Sie "c:"\\Temp\\\*. Das Platzhalterzeichen gilt für Dateien im angegebenen Ordner.

Wenn Sie Dateien auch aus den Unterordnern des angegebenen Ordners sammeln möchten, verwenden Sie zwei umgekehrte Schrägstriche für das letzte Ordner Trennzeichen, z. B. "c:"\\Temp\\\\\*.

Hier s ein Beispiel, das Abfragen der **"applicationHost.config"** Datei:

``` syntax
<path>%windir%\System32\inetsrv\config\applicationHost.config</path>
```

Die Ergebnisse finden Sie in eine Tabelle namens  **\#Dateien**, z.B.:

querypath | Vollständiger Pfad | Parentpath | FileName | Inhalt
----- | ----- | ----- | ----- | -----
%windir%\...\applicationHost.config |C:\Windows<br>\...\applicationHost.config | C:\Windows<br>\...\config | applicationHost.confi | 0x3C3F78

**\#Schema der Tabellen für Dateien**

Spaltenname | SQL-Datentyp | Beschreibung
---- | ---- | ----
querypath | Nvarchar(300) nicht NULL | Ursprüngliche abfrageanweisung
Vollständiger Pfad | Nvarchar(300) nicht NULL | Absoluter Dateipfad und Dateinamen
Parentpath | Nvarchar(300) nicht NULL | Dateipfad
FileName | Nvarchar(300) nicht NULL | Dateiname
Inhalt | Varbinary(MAX) NULL | In den binären Inhalt der Datei

### <a name="defining-rules"></a>Definieren von Regeln

Nachdem genügend Daten mithilfe von PLA aus einen Zielserver erfasst wurde, kann das Advisor-Pack verwendet diese Daten für die Validierung, und zeigen Sie eine kurze Zusammenfassung der Systemadministratoren.

Regeln geben eine Kurzübersicht über die Server-s-Leistung. Diese Probleme hervorzuheben und Empfehlungen. Sie können alle Regeln aufgelistet, die Sie für eine Advisor-Paket überprüfen möchten. Wenn Sie eine Core-Betriebssystem Advisor Pack entwickeln möchten, können z. B. die möglichen Regeln enthalten:

* Ob die CPU-Leistung Modus speichert Power

* Gibt an, ob der Server in einer virtualisierten Umgebung ist

* Ob, e/a-Druck vorliegt

Regeln werden die folgenden Elemente enthalten:

* Abhängige Schwellenwert (eine konfigurierbare Teil einer Regel)

* Regel-Definition (Warnungen und Empfehlungen)

Hier ist s ein Beispiel für eine einfache Regel:

``` syntax
<advisorPack>

  <reportDefinition>
    <thresholds>
      <threshold  />
    </thresholds>
    <rules>
      <rule  />
      </rule>
    </rules>
  </reportDefinition>
</advisorPack>
```

### <a name="threshold"></a>Schwellenwert

Schwellenwert ist eine konfigurierbare Faktor, der die Systemadministratoren zu entscheiden, wenn eine Regel eine gute oder einen ungültigen Status angezeigt werden sollen. Das folgende Beispiel zeigt eine Regel, um freien Speicherplatz auf einem Systemlaufwerk und eine Warnung zu erkennen, wenn der freie Speicherplatz weniger als 10 GB ist.

``` syntax
<threshold name="freediskSize" caption="Free Disk Size (GB)" description="Free Disk Size  value="10" />
```

In diesem Fall hat der Systemadministrator jedoch eine kleinere Festplatte. Er geht davon aus, 5 GB freien Speicherplatz möglicherweise weiterhin einem guten Zustand, und er möchte keine Warnung angezeigt. Er kann den Standardwert von 10 bis 5 über die SPA-Konsole aktualisieren, ohne zu verstehen, wie einen Advisor-Pack entwickeln.

Einführung in einen Schwellenwert kann Systemadministratoren, die den Wert schnell zu ändern, ohne das Advisor-Pack ändern zu müssen.

Im Beispiel alle Attribute, mit Ausnahme von **Beschreibung** erforderlich sind. Sie können eine beliebige Anzahl für **Wert**.

Ein Schwellenwert kann über die Regeln freigegeben werden.

### <a name="alerts-and-recommendations"></a>Warnungen und Empfehlungen

Die Definition der Regel beinhaltet jedoch alle Berechnungen Logik nicht. Es definiert, wie die Benutzeroberfläche aussehen könnte, und wie SQL Server Script melden die Ergebnisse in der Benutzeroberfläche kommuniziert.

Eine Regel besteht aus drei Teilen:

* Warnung (Regel Beschriftung)

* Empfehlung (Hinweise)

* Zugeordnete Schwellenwert (optionale Informationen zu Abhängigkeiten)

Hier ist ein Beispiel für eine Regel aus:

``` syntax
<rule name="freediskSize" caption="Free Disk Size on System Drive" description="This rule checks free disk size on system drive ">
<advice name="SuccessAdvice" level="Success" message="No issue found.">No Recommendation.</advice>
<advice name="WarningAdvice" level="Warning" message="Not enough free space on system drive.">
Install OS on larger disk.</advice>
<dependencies>
 <threshold ref="freediskSize"/>
</dependencies>
</rule>
```

Sie können so viele Ratschläge, wie Sie möchten, und in der Regel Sie Empfehlungen definieren definieren. Die **Ebene** Rat möglich **Erfolg** oder **Warnung**.

Sie können mit beliebig viele Schwellenwerte wie gewünscht verknüpfen. Sie können auch mit einem Schwellenwert verknüpfen, die für die aktuelle Regel nicht relevant ist. Verknüpfen, wird die SPA-Konsole, die Schwellenwerte problemlos zu verwalten.

Der Regelname und die Empfehlungen sind Schlüssel, und sie in ihrem Bereich eindeutig sind. Keine zwei Regeln können den gleichen Namen aufweisen, und keine zwei Empfehlungen in eine Regel können den gleichen Namen haben. Diese Namen werden sehr wichtig, wenn Sie einen Bericht der SQL-Skript schreiben. Rufen Sie die \[Dbo\].\[ SetNotification\] API, um den Regelstatus festzulegen.

### <a name="defining-ui-display-elements"></a>Definieren die Elemente der Benutzeroberfläche anzeigen

Nachdem die Regeln definiert sind, können Systemadministratoren den zusammenfassende Bericht sehen. Allerdings häufig Systemadministratoren die aggregierten Daten interessiert sind, und werden soll, überprüfen Sie die Datenquellen, die in den Leistungsregeln für die verwendet wurden.

Fortfahren mit dem vorherigen Beispiel, weiß der Benutzer, ob ausreichend freier Speicherplatz vorhanden, auf dem Systemlaufwerk ist. Benutzer können auch die tatsächliche Größe des freien Speicherplatzes interessiert ist. Eine Gruppe einzelner Wert wird zum Speichern und diese Ergebnisse werden angezeigt. Mehrerer einzelner Werte können gruppiert und in einer Tabelle in der SPA-Konsole angezeigt werden. Die Tabelle enthält nur zwei Spalten, Namen und Wert an, wie hier gezeigt.

Name | Wert
---- | ----
Größe der Speicherplatz auf dem Systemlaufwerk (GB) | 100
Gesamtgröße des Datenträgers installiert (GB) | 500 

Wenn ein Benutzer benötigt, um eine Liste aller Festplatten, die auf dem Server und die Datenträgergröße installiert sind, können wir einen Listenwert Aufrufen mit drei Spalten und Zeilen, wie hier gezeigt.

Datenträger | Kostenlose Datenträgergröße (GB) | Gesamtgröße (GB)
---- | ---- | ----
0 | 100 | 500
1 | 20 | 320

In einem Advisor-Pack kann es viele Tabellen (Einzelwert Gruppen und Auflisten von Wertetabellen). Wir können einen Abschnitt zum Organisieren und kategorisieren diese Tabellen verwenden.

Zusammenfassend lässt sich sagen gibt es drei Arten von Elementen der Benutzeroberfläche:

* [Abschnitte](#bkmk-ui-section)

* [Einzelner Wertgruppen](#bkmk-ui-svg)

* [Auflisten von Wertetabellen](#bkmk-ui-lvt)

S-Beispiel zeigt, dass hier die Elemente der Benutzeroberfläche:

``` syntax
<advisorPack>
<dataSourceDefinition/>
<reportDefinition>
 <datatypes>
<datatype .../>
 </datatypes>
 <thresholds/>
 <rule/>
 <sections>
<section .../>
 </sections>
 <singleValues>
<singleValue .../>
 </singleValues>
 <listValues>
<listValue .../>
 </listValues>
</reportDefinition>
</advisorPack>
```

### <a href="" id="bkmk-ui-section"></a>Abschnitte

Ein Abschnitt ist ausschließlich für das UI-Layout. Er wird in jedem logischen Berechnungen nicht berücksichtigt. Jeder einzelnen Bericht enthält eine Reihe von Abschnitten auf oberster Ebene, die nicht mit einen übergeordneten Abschnitt verfügen. In den Abschnitten auf oberster Ebene werden als Registerkarten im Bericht angezeigt. Abschnitte können in den Unterabschnitten, mit einem Maximum von 10 Ebenen enthalten. Alle in den Bereichen der obersten Ebene in den Unterabschnitten werden in der erweiterbaren Bereiche angezeigt. Ein Abschnitt kann es sich um mehrere Unterabschnitte, Einzelwert Gruppen und Auflisten von Wertetabellen enthalten. Einzelner Wert-Gruppen und Auflisten von Wertetabellen werden als Tabellen dargestellt.

Hier ist ein Beispiel der obersten Ebene Abschnitt.

``` syntax
<section name="CPU" caption="CPU"/>
```

Ein Abschnittsname muss eindeutig sein. Es wird als Schlüssel verwendet, die durch andere Abschnitte, Einzelwert Gruppen und Auflisten von Wertetabellen verknüpft werden können.

Das folgende Beispiel enthält ein Attribut **übergeordneten**, und diese verweist auf den CPU-Abschnitt. CPUFacts ist ein untergeordnetes Element des Namens der CPU-Abschnitts. **übergeordnete** muss auf einen vorherigen Abschnitt an; verweisen, andernfalls kann es dazu führen, in einer Schleife.

``` syntax
<section name="CPUFacts" caption="Facts" parent="CPU"/>
```

Die folgende Gruppe von Single-Wert ist ein Attribut **Abschnitt**, und sie können jeden Bereich, basierend auf Ihren Entwurf der Benutzeroberfläche verweisen.

``` syntax
<singleValue name="CPUInformation" section="CPUFacts" caption="Physical CPU Information"> </singleValue>
```

### <a name="data-types"></a>Datentypen

Eine Gruppe einzelner Wert und eine Liste-Wert-Tabelle enthalten andere Datentypen, wie z. B. String, Int und "float". Da diese Werte in der SQL Server-Datenbank gespeichert werden, können Sie einen SQL-Datentyp für jede Data-Eigenschaft definieren. Definieren einen SQL-Datentyp ist jedoch ziemlich kompliziert. Sie müssen angeben, die Länge oder Genauigkeit, die möglicherweise anfällig für ändern.

Um logische-Datentypen zu definieren, können Sie das erste untergeordnete Element des  **&lt;ReportDefinition /&gt;** , d.h., in dem Sie eine Zuordnung von der SQL-Datentyp und den logischen Typ definieren können.

Das folgende Beispiel definiert zwei Typen von Daten. Eine **Zeichenfolge** und der andere **Unternehmenscode**.

``` syntax
<datatype name="string" = sqltype="nvarchar(4000)" />
<datatype name="companyCode" sqltype="nvarchar(100)" />
```

Ein Datentypnamen kann eine beliebige gültige Zeichenfolge sein. Hier ist eine Liste der zulässigen SQL-Datentypen:

* BIGINT

* Binärdatei

* bit

* Char

* date

* DATETIME

* datetime2

* datetimeoffset

* decimal

* float

* ssNoversion

* Verdienst

* NCHAR

* Numerisch

* nvarchar

* Real

* smalldatetime

* smallint

* smallmoney

* Zeit

* tinyint

* uniqueidentifier

* varbinary

* varchar

Weitere Informationen zu dieser SQL-Datentypen, finden Sie unter [-Datentypen (Transact-SQL)](https://msdn.microsoft.com/library/ms187752.aspx).

### <a href="" id="bkmk-ui-svg"></a>Einzelner Wertgruppen

Eine Gruppe einzelner Wert gruppiert mehrerer einzelner Werte zusammen, um in einer Tabelle zu präsentieren, wie hier gezeigt.

``` syntax
<singleValue name="Systemoverview" section="SystemoverviewSection" caption="Facts">
<value name="OsName" type="string" caption="Operating system" description="WMI: Win32_OperatingSystem/Caption"/>
<value name="Osversion" type="string" caption="OS version" description="WMI: Win32_OperatingSystem/version"/>
<value name="OsLocation" type="string" caption="OS location" description="WMI: Win32_OperatingSystem/SystemDrive"/>
</singleValue>
```

Im vorherigen Beispiel definierten wir eine Gruppe einzelner Wert. Es ist ein untergeordneter Knoten des Abschnitts **SystemoverviewSection**. Diese Gruppe verfügt über die sind einzelne Werte **OsName**, **"osversion"** , und **OsLocation**.

Ein einzelner Wert muss es sich um ein global eindeutiger Name-Attribut aufweisen. In diesem Beispiel wird das Attribut global eindeutigen Namen **Systemoverview**. Der eindeutige Name wird verwendet werden, um eine entsprechende Ansicht für benutzerdefinierten Berichts zu generieren. Jede Ansicht enthält das Präfix **Vw**, z. B. VwSystemoverview.

Auch wenn Sie mehrere Einzelwert Gruppen definieren können, können keine zwei Einzelwert Namen identisch, auch wenn sie sich in unterschiedlichen Gruppen sind. Der Namen des einzelnen Werts wird durch der Bericht zum SQL-Skript verwendet, den Wert entsprechend festlegen.

Sie können einen Datentyp für jeden einzelnen Wert definieren. Die zulässigen Eingabe für **Typ** ist definiert  **&lt;Datatype /&gt;** . Der endgültige Bericht könnte folgendermaßen aussehen:

**Fakten**

Name | Wert
--- | ---
Betriebssystem | &lt;_ein Wert wird vom Berichts-Skript festgelegt werden_&gt;
BS-Version | &lt;_ein Wert wird vom Berichts-Skript festgelegt werden_&gt;
Betriebssystem-Speicherort | &lt;_ein Wert wird vom Berichts-Skript festgelegt werden_&gt;

Die **Beschriftung** Attribut **&lt;Wert /&gt;** wird in der ersten Spalte angezeigt. Werte in der Wertspalte werden in der Zukunft festgelegt, von dem Skript-Bericht über \[Dbo\].\[ SetSingleValue\]. Die **Beschreibung** Attribut **&lt;Wert /&gt;** in einer QuickInfo angezeigt wird. In der Regel zeigt die QuickInfo Benutzern die Quelle der Daten. Weitere Informationen zu QuickInfos finden Sie unter [QuickInfos](#bkmk-tooltips).

### <a href="" id="bkmk-ui-lvt"></a>Auflisten von Wertetabellen

Definieren einen Listenwert ist identisch mit der eine Tabelle definiert wird.

``` syntax
<listValue name="NetworkAdapterInformation" section="NetworkIOFacts" caption="Physical network adapter information">
<column name="NetworkAdapterId" type="string" caption="ID" description="WMI: Win32_NetworkAdapter/DeviceID"/>
<column name="NetworkAdapterName" type="string" caption="Name" description="WMI: Win32_NetworkAdapter/Name"/>
<column name="type" type="string" caption="type" description="WMI: Win32_NetworkAdapter/Adaptertype"/>
<column name="Speed" type="decimal" caption="Speed (Mbps)" description="WMI: Win32_NetworkAdapter/Speed"/>
<column name="MACaddress" type="string" caption="MAC address" description="WMI: Win32_NetworkAdapter/MACaddress"/>
</listValue>
```

Der Wertname Liste muss global eindeutig sein. Dieser Name wird der Name einer temporären Tabelle sein. Im vorherigen Beispiel ist die Tabelle mit dem Namen \#NetworkAdapterInformation an der Ausführung Umgebung Initialisierungsphase, die alle Spalten enthält, die beschrieben werden, erstellt werden. Ähnlich wie auf einen einzelnen Wert, wird eine Liste Wertname auch als Teil des Namens der benutzerdefinierten Ansicht, z. B. VwNetworkAdapterInformation verwendet.

@type der &lt;Spalte /&gt; wird definiert, indem &lt;Datatype /&gt;

Das mock UI des Abschlussberichts könnte wie folgt aussehen:

**Informationen zum physischen Netzwerkadapter**

ID | Name | Typ | Geschwindigkeit (Mbit/s) | MAC-Adresse
--- | --- | --- | --- | ---
 | <br> | | |
 | | | |


Die **Beschriftung** Attribut &lt;Spalte /&gt; als ein Name der Spalte angezeigt wird und die **Beschreibung** Attribut &lt;Spalte /&gt; als für eine QuickInfo angezeigt wird die entsprechende Spaltenüberschrift. In der Regel zeigt die QuickInfo dem Benutzer die Quelle der Daten. Weitere Informationen finden Sie unter [QuickInfos](#bkmk-tooltips).

In einigen Fällen eine Tabelle hat viele Spalten aus, und suchen Sie nur einige Zeilen, sodass austauschen, die Spalten und Zeilen die Tabelle stellen viel besser. Um die Spalten und Zeilen zu wechseln, können Sie das folgende Stilattribut hinzufügen:

``` syntax
<listValue style="Transpose"  
```

### <a name="defining-charting-elements"></a>Zum Erstellen von Diagrammen Elemente definieren

Sie können wählen Sie eine beliebige Taste, Statistiken und die Werte in ein Verlaufsdiagramm oder als ein Trenddiagramm. Es gibt zwei Arten von Statistiken:

* **Statische Statistiken** einen einzelnen Wert, der zur Entwurfszeit bekannt ist. Beispielsweise wäre der Speicherplatz auf einem Systemlaufwerk eine statische Statistik.

* **Dynamische Statistiken** zur Entwurfszeit möglicherweise unbekannt. Beispielsweise ist die durchschnittliche CPU-Auslastung jeder Kern eine dynamische Statistik, da Sie nicht wissen, wie viele CPU-Kerne im System zur Entwurfszeit konnte.

Statistikschlüssels verfügt über eine Einschränkung, dass die Daten mit double-Datentyp kompatibel sein müssen. Es kann sein, eine ganze Zahl, Dezimalzahl oder eine Zeichenfolge, die nach double konvertiert werden kann.

SPA verwendet eine Gruppe einzelner Wert, um statische Statistiken und eine Liste-Wert-Tabelle zur Unterstützung von dynamischer Statistiken zu unterstützen. In den folgenden Abschnitten wird beschrieben, wie statische Statistik und dynamische Statistik-Schlüssel zu definieren.

### <a name="static-statistics"></a>Statische Statistiken

Wie bereits erwähnt, ist eine statische Statistik einen einzelnen Wert. Logischerweise kann jeden einzelnen Wert als eine statische Statistik definiert werden. Es ist jedoch keine Bedeutung, um einen einzelnen Wert anzuzeigen, der nicht in Zahlentyp umgewandelt werden kann. Um eine statische Statistik zu definieren, können Sie einfach das Attribut hinzufügen **trendable** an die entsprechenden Einzelwert Schlüssel wie unten:

``` syntax
<value name="freediskSize" type="int" trendable="true"  
```

### <a name="dynamic-statistics"></a>Dynamische Statistiken

Dynamische Statistik Schlüssel sind zur Entwurfszeit nicht bekannt, damit die Anzahl von möglichen Werten unbekannt ist. Jedoch, da Listenwerte in mehreren Zeilen gespeichert werden, es einfach, eine Liste-Wert-Tabelle zu verwenden, um dynamische Statistiken zu speichern wäre.

z. B. wenn wir Diagramme für die durchschnittliche CPU-Auslastung von verschiedenen Kernen anzeigen möchten, könnten definieren wir eine Tabelle mit Spalten für **CpuId** und **AverageCpuUsage**:

``` syntax
<listValue name="CpuPerformance">
<column name="CpuId" type="string" caption="CPU ID" columntype="Key"/>
<column name="AverageCpuUsage" type="decimal" caption="Average" columntype="Value"/>
</listValue>
```

Ein weiteres Attribut **"ColumnType"** , kann **Schlüssel**, **Wert**, oder **Information**. Der Datentyp der **Schlüssel** Spalte muss doppelte oder double konvertiert werden kann. In einem **Schlüssel** Spalte, Sie können nicht die gleichen Schlüssel in eine Tabelle einfügen. **Wert** oder **Information** Spalten müssen sich nicht auf diese Einschränkung.

Die Statistikwerte werden gespeichert, **Wert** Spalten.

**Nur zu Informationszwecken** Spalten werden wie normale Spalten in Tabellen der normalen Liste-Wert. **Nur zu Informationszwecken** ist der Standardtyp für die Spalte aus, wenn Sie nicht angeben. Solche Spalten nicht auf die Anzahl der Schlüssel für Statistiken oder Statistik Berechnungen teilnehmen.

Fortfahren mit dem vorherigen Beispiel, wenn ein Server mit zwei CPU-Kerne verfügt, kann das Ergebnis in der Tabelle wie folgt aussehen:

CpuId | AverageCpuUsage
:---: | :---:
0 | 10
1 | 30

Zur gleichen Zeit werden zwei Statistiken Schlüssel durch die SPA-Framework generiert. Eine für CPU 0 ist, und die andere ist für die CPU 1.

Wie im folgende Beispiel mehrere zeigt **Wert** Spalten mit mehreren **Schlüssel** Spalten wird unterstützt.

CounterName | InstanceName | Durchschnitt | Summe
--- | :---: | :---: | :---:
Prozessorzeit (%) | _Gesamt | 10 | 20
Prozessorzeit (%) | CPU0 | 20 | 30 

In diesem Beispiel verfügen Sie über zwei **Schlüssel** Spalten und zwei **Wert** Spalten. SPA generiert zwei Statistiken-Schlüssel für die durchschnittliche Spalte und einen anderen zwei Schlüssel für die Sum-Spalte. Die Schlüssel für die Statistiken sind:

* "CounterName" (% Prozessorzeit) / InstanceName (\_gesamt) / durchschnittliche

* "CounterName" (% Prozessorzeit) / InstanceName (CPU 0) / durchschnittliche

* "CounterName" (% Prozessorzeit) / InstanceName (\_gesamt) / Summe

* "CounterName" (% Prozessorzeit) / InstanceName (CPU 0) / Summe

CounterName "und" InstanceName werden als ein Schlüssel kombiniert. Eine Wiederholung kann nicht über den kombinierte Schlüssel verfügen.

SPA generiert viele Statistiken-Schlüssel. Einige von ihnen möglicherweise nicht in der für Sie interessant, und Sie möchten sie von der Benutzeroberfläche auszublenden. SPA ermöglicht Entwicklern das Erstellen eines Filters zum Anzeigen von nur Schlüssel, die nützliche Statistiken.

für das vorherige Beispiel, die Systemadministratoren möglicherweise nur in Schlüsseln, die in der der Instanzname ist interessant \_Gesamt- oder CPU 1. Der Filter kann wie folgt definiert werden:

``` syntax
<listValue name="CpuPerformance">
<column name="CounterName" type="string" columntype="Key"/>
<column name="InstanceName" type="string" columntype="Key">
 <trendableKeyValues>
<value>_Total</value>
<value>CPU1</value>
 </trendableKeyValues>
</column>
<column name="Average" type="decimal" columntype="Value"/>
<column name="Sum" type="decimal" columntype="Value"/>
</listValue>
```

**&lt;TrendableKeyValues /&gt;**  unter Schlüsselspalte definiert werden können. Wenn mehr als eine Schlüsselspalte verfügt über eine solche ein Filter konfiguriert und wird Logik angewendet werden.

### <a name="developing-report-scripts"></a>Entwickeln von Skripts für Bericht

Nach der Bereitstellung-Metadaten definiert sind, können wir starten das Berichtsserver-Skript schreiben können, das eine gespeicherte T-SQL-Prozedur ist.

Es gibt **Namen** und **ReportScript** Attribute im Metadaten-Header bereitstellen, wie hier gezeigt:

``` syntax
<advisorPack name="Microsoft.ServerPerformanceAdvisor.CoreOS.V1" reportScript="ReportScript"  
```

Der Hauptbericht-Skript namens aus der **Namen** und **ReportScript** Attribute. Im folgenden Beispiel werden sie \[Microsoft.ServerPerformanceAdvisor.CoreOS.V2\].\[ ReportScript\].

``` syntax
create PROCEDURE [Microsoft.ServerPerformanceAdvisor.CoreOS.V2].[ReportScript] AS SET NOCOUNT ON

- Set alert and notification

- Prepare data for report view
```

Die **Namen** Attribut wird als Schema einen Datenbanknamen ein, z. B. einem Namespace verwendet werden. Diese Regel gilt für alle anderen Datenbankobjekte, die auf das aktuelle Advisor-Pack, z. B. Listenwert und gespeicherten Prozeduren gehören.

Mit dieser Schemaname vor die Datenbankobjekte bietet folgende Vorteile:

* Vermeiden von Benennungskonflikt für verschiedene Advisor-packs

* Eine höhere Sicherheit

In der SQL Server-Datenbank ist der Name des Standardschemas **Dbo**. Anmeldeinformationen des Datenbankbesitzers müssen in der Regel Datenbankobjekte in Betrieb **Dbo**. Wenn wir kein Schema für jedes Advisor Pack erstellen, ist es wahrscheinlich, dass zwei Packs für Advisor einen Listenwert mit demselben Namen definieren. Dies sollte nicht relevant sein, da Sie einen Schemanamen zur Lösung dieses Problems führen können. Darüber hinaus ist die Aufhebung der Bereitstellung eines Advisor-Packs viel einfacher. Da das Advisor-Pack-Objekt nicht zu einem Schema gehört **Dbo**, dadurch SPA mit einer niedrigen Berechtigungen für den Benutzer darauf zugreifen können.

Ein normaler Bericht-Skript führt Folgendes aus:

* Greift auf unformatierte gesammelten Daten

* Führt Berechnungen auf Grundlage von Rohdaten

* Änderungen Warnungen und Empfehlungen

* Bereitet Daten für die Berichtsansicht

### <a name="access-raw-collected-data"></a>Access-gesammelten Rohdaten

Alle gesammelte Daten in den folgenden entsprechenden Tabellen importiert. Weitere Informationen über das Tabellenschema, finden Sie unter [definieren den datensammlersatz](#bkmk-definedatacollector).

* Registrierung

    * \#registryKeys

* WMI

    * \#WMIObjects

    * \#WmiObjectProperties

    * \#WmiQueries

* Leistungsindikator

    * \#PerformanceCounters

* Datei

    * \#Dateien

* ETW

    * \#Ereignisse

    * \#EventProperties

### <a name="set-rule-status"></a>Set-Regelstatus

Die \[Dbo\].\[ SetNotification\] API-Sätze den Regelstatus aus, damit Sie sehen eine **Erfolg** oder **Warnung** Symbol in der Benutzeroberfläche.

* @ruleName nvarchar(50)

* @adviceName nvarchar(50)

Die Warnung "und" Empfehlung Nachrichten werden in der Bereitstellung Metadaten-XML-Datei gespeichert. Dadurch wird das Skript Bericht einfacher zu verwalten.

Jede Regelstatus ist zunächst n/v. Sie können diese API verwenden, den Status einer Regel festlegen, durch Angeben eines Tipps. Die Ebene mit dem Namen der Empfehlungen wird der Status der Regel verwendet werden.

Denken Sie daran, dass die zuvor definierten die folgende Regel:

``` syntax
<rule name="freediskSize" caption="Free Disk Size on System Drive" description="This rule checks free disk size on the system drive ">
<advice name="SuccessAdvice" level="Success" message="No issue found.">No recommendation.</advice>
<advice name="WarningAdvice" level="Warning" message="Not enough free space on system drive.">Install the operating system on a larger disk.</advice>
</rule>
```

Wenn der freie Speicherplatz ist weniger als 2 GB, müssen wir die Regel zum Festlegen der **Warnung** Ebene. Das SQL-Skript wird wie folgt lauten:

``` syntax
if (@freediskSizeInGB < 2)
BEGIN
    exec dbo.SetNotification N'freediskSize', N'WarningAdvice'
END
ELSE
BEGIN
    exec dbo.SetNotification N'freediskSize', N'SuccessAdvice'
END 
```

### <a name="get-threshold-value"></a>Abrufen der Schwellenwert

Die \[Dbo\].\[ GetThreshold\] API ruft die Schwellenwerte:

* @key nvarchar(50)

* @value Ausgabe von "float"

> [!NOTE]
> Die Schwellenwerte sind Name / Wert-Paare ein, und sie können in den Regeln verwiesen werden. Die Systemadministratoren können die SPA-Konsole verwenden, um die Schwellenwerte anzupassen.

 Anhand der im vorherigen Beispiel für einen Schwellenwert, wird die Definition wie folgt lauten:

``` syntax
<thresholds>
  <threshold name="freediskSize" caption="Free Disk Size (GB)" description="Free Disk Size  value="10" />
</thresholds>
<rule name="freediskSize" caption="Free Disk Size on System Drive" description="This rule checks free disk size on system drive ">
<advice name="SuccessAdvice" level="Success" message="No issue found.">No recommendation.</advice>
<advice name="WarningAdvice" level="Warning" message="Not enough free space on the system drive.">
Install the operating system on a larger disk.</advice>
<dependencies>
 <threshold ref="freediskSize"/>
</dependencies>
</rule>
```

Das Skript des Berichts kann geändert werden, wie hier gezeigt:

``` syntax
DECLARE @freediskSize FLOat
exec dbo.GetThreshold N freediskSize , @freediskSize output

if (@freediskSizeInGB < @freediskSize)

```

### <a name="set-or-remove-the-single-value"></a>Festlegen oder Entfernen von den einmaligen Wert

Die \[Dbo\].\[ SetSingleValue\] API-Sätze den single-Wert:

* @key nvarchar(50)

* @value sql\_variant

Dieser Wert kann mehrmals für denselben Schlüssel Einzelwert führen. Der letzte Wert wird gespeichert.

Das folgende Beispiel zeigt, dass einige einzelne Werte definiert:

``` syntax
<singleValue section="Systemoverview" caption="Facts">
<value name="OsName" type="string" caption="Operating System" description="WMI: Win32_OperatingSystem/Caption"/>
<value name="Osversion" type="string" caption="OS version" description="WMI: Win32_OperatingSystem/version"/>
<value name="OsLocation" type="string" caption="OS Location" description="WMI: Win32_OperatingSystem/SystemDrive"/>
</singleValue>
```

Sie können dann den einzelnen Wert festlegen, wie hier gezeigt:

``` syntax
exec dbo.SetSingleValue N OsName ,  Windows 7 
exec dbo.SetSingleValue N Osversion ,  6.1.7601 
exec dbo.SetSingleValue N OsLocation ,  c:\ 
```

In seltenen Fällen sollten Sie das Ergebnis zu entfernen, die Sie zuvor festgelegt haben, mithilfe der \[Dbo\].\[ RemoveSingleValue\] API.

* @key nvarchar(50)

Sie können das folgende Skript verwenden, so entfernen Sie den zuvor festgelegten Wert.

``` syntax
exec dbo.removeSingleValue N Osversion 
```

### <a name="get-data-collection-information"></a>Abrufen von Informationen zur modelldatensammlung

Die \[Dbo\].\[ GetDuration\] API erhält der Benutzer, die Dauer in Sekunden für die Auflistung festgelegt:

* @duration Int-Ausgabe

Auch hier melden s ein Beispiel für Skripts:

``` syntax
DECLARE @duration int
exec dbo.GetDuration @duration output
```

Die \[Dbo\].\[ GetInternal\] API ruft das Intervall eines Leistungsindikators ab. Es kann NULL zurückgeben, wenn der aktuelle Bericht keine Informationen für Leistungsindikatoren.

* @interval Int-Ausgabe

Auch hier melden s ein Beispiel für Skripts:

``` syntax
DECLARE @interval int
exec dbo.GetInterval @interval output
```

### <a name="set-a-list-value-table"></a>Legen Sie eine Liste-Wert-Tabelle

Es ist keine API zum Auflisten von Wertetabellen aktualisieren. Allerdings können Sie die Liste-Wert-Tabellen direkt zugreifen. in der Initialisierungsphase wird eine entsprechende temporäre Tabelle für jeden Listenwert erstellt.

Das folgende Beispiel zeigt eine Liste-Wert-Tabelle:

``` syntax
<listValue name="NetworkAdapterInformation" section="NetworkIOFacts" caption="Physical Network Adapter Information">
<column name="NetworkAdapterId" type="string" caption="ID" description="WMI: Win32_NetworkAdapter/DeviceID"/>
<column name="NetworkAdapterName" type="string" caption="Name" description="WMI: Win32_NetworkAdapter/Name"/>
<column name="type" type="string" caption="type" description="WMI: Win32_NetworkAdapter/Adaptertype"/>
<column name="Speed" type="decimal" caption="Speed (Mbps)" description="WMI: Win32_NetworkAdapter/Speed"/>
<column name="MACaddress" type="string" caption="MAC address" description="WMI: Win32_NetworkAdapter/MACaddress"/>
</listValue>
```

Anschließend können Sie eine SQL-Skript zum Einfügen, aktualisieren oder löschen die Ergebnisse schreiben:

``` syntax
INSERT INTO #NetworkAdapterInformation (
  NetworkAdapterId,
  NetworkAdapterName,
  type,
  Speed,
  MACaddress
)
VALUES (

)
```

## <a name="development-and-debugging"></a>Entwickeln und Debuggen


### <a name="writing-logs"></a>Das Schreiben von Protokollen

ist ggf. Weitere Informationen, die Sie den Systemadministratoren kommunizieren möchten, können Sie die Protokolle schreiben. Ein gelbes Banner wird bei jedem Protokoll für einen bestimmten Bericht wird in der Kopfzeile des Berichts angezeigt. Das folgende Beispiel zeigt, wie Sie ein Protokoll schreiben können:

``` syntax
exec dbo.WriteSystemLog N'Any information you want to show to the system administrators , N Warning 
```

Der erste Parameter ist die gewünschte Nachricht im Protokoll angezeigt. Der zweite Parameter ist der Protokolliergrad. Die gültige Eingabe für den zweiten Parameter ist möglicherweise **Information**, **Warnung**, oder **Fehler**.

### <a name="debug"></a>Debugging

Die SPA-Konsole ausführen kann, in zwei Modi Debug oder Release. Release-Modus ist die Standardeinstellung, und es die gesammelten Rohdaten bereinigt, nachdem der Bericht generiert wird. Der Debugmodus behält allen unformatierte Daten in die Dateifreigabe und die Datenbank, damit Sie das Berichtsserver-Skript in der Zukunft Debuggen können.

**So debuggen Sie einen Bericht-Skript**

1.  Installieren Sie Microsoft SQL Server Management Studio (SSMS).

2.  Nach dem Start SSMS Herstellen einer Verbindung mit "localhost"\\SQLExpress. Denken Sie daran, dass Sie anstelle von "localhost" verwenden müssen. . Andernfalls, Sie können den Debugger zu starten, in SQL Server möglicherweise nicht.

3.  Führen Sie das folgende Skript zum Aktivieren der Debug-Modus:

    ``` syntax
    USE SPADB
    UPdate dbo.Configurations
    SET Value = N'true'
    WHERE Name = N'Debugmode'
    ```

4.  Starten Sie die SPA-Konsole, und führen Sie den Advisor-Pack, den Sie debuggen möchten.

5.  Warten Sie, bis die Aufgabe abgeschlossen. Wenn der Bericht wurde erfolgreich erstellt wird, wechseln Sie zurück zur SSMS und suchen Sie nach der aktuellen Aufgabe.

    ``` syntax
    select TOP 1 * FROM dbo.Tasks OrdER BY Id DESC
    ```

    Die Ausgabe könnte beispielsweise wie folgt aussehen:

    Id | SessionId | AdvisoryPackageId | ReportStatusId | LastUpdatetime | ThresholdversionId
    :---: | :---: | :---: | :---: | :---: | :---:
    12 | 17 | 1 | 2 | 2011-05-11 05:35:24.387 | 1

6.  Sie können das folgende Skript ausführen, so oft wie der Berichtsserver-Skript für Id-12 ausgeführt werden soll:

    ``` syntax
    exec dbo.DebugReportScript 12
    ```

    **Beachten Sie** drücken Sie F11, um Sie zu Schritt in der vorherigen Anweisung, und Debuggen.



Ausführung \[Dbo\].\[ DebugReportScript\] mehrere Resultsets, einschließlich zurückgibt:

1.  Microsoft SQL Server-Nachrichten und Advisor-Pack-Protokollen

2.  Ergebnisse von Regeln

3.  Statistiken-Schlüssel und Werte

4.  Einzelne Werte

5.  Alle auflisten werttabellen

## <a name="best-practices"></a>Empfohlene Methoden

### <a name="naming-convention-and-styles"></a>Benennungskonvention und Stile

|                                                                 Pascal-Schreibweise zur Groß-und Kleinschreibung                                                                 |                       Kamel-Schreibweise                        |             Großbuchstaben             |
|-----------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------|-----------------------------------|
| <ul><li>Namen in ProvisionMetadata.xml</li><li>Gespeicherte Prozeduren</li><li>Funktionen</li><li>Die Namen von Sichten</li><li>Temporäre Tabellennamen</li></ul> | <ul><li>Parameternamen</li><li>Lokale Variablen</li></ul> | Verwendung für alle SQL-Schlüsselwörter |

### <a name="other-recommendations"></a>Weitere Empfehlungen

* Verschieben Sie die meisten logischen Komponenten in andere gespeicherte Prozeduren und benutzerdefinierte Funktionen.

* Stellen Sie Ihr Hauptskript so kurz wie möglich zu Wartungszwecken.

* Verwenden Sie den vollständigen Namen des SQL-Objekts.

* Behandeln von SQL-Code als Groß-/Kleinschreibung beachtet.

* Hinzufügen **SET NOCOUNT ON** am Anfang jeder gespeicherten Prozedur.

* Erwägen Sie die Verwendung von temporärer Tabellen übertragen großen Datenmengen.

* Erwägen Sie die Verwendung **XACT festgelegt\_ABORT ON** zum Beenden des Prozesses, wenn ein Fehler auftritt.

* Schließen Sie immer Hauptversionsnummer in den Advisor-Pack-Anzeigenamen ein.

## <a href="" id="bkmk-advancedtopics"></a>Weiterführende Themen

### <a name="run-multiple-advisor-packs-simultaneously"></a>Führen Sie gleichzeitig mehrere Advisor-packs

SPA unterstützt mehrere Advisor-Packs zur gleichen Zeit ausgeführt. Dies ist besonders nützlich, wenn Sie Internet Information Services (IIS) und Core-Betriebssystem – Leistung zur gleichen Zeit ansehen möchten. Viele Datensammler, die von der Advisor-Pack für IIS verwendet möglicherweise auch durch das Advisor-Pack Core-Betriebssystem verwendet werden. Wenn zwei oder mehr Advisor-Packs auf dem gleichen Computer ausgeführt werden, erfasst SPA nicht dieselben Daten doppelt.

Das folgende Beispiel zeigt den Workflow für die Ausführung von zwei Packs für Advisor.

![Ausführen von mehreren Packs für advisor](../media/server-performance-advisor/spa-dev-guide-multi-advisor-packs.png)

Fusion Data Collector Set ist nur für das Sammeln von Leistungsindikator und ETW-Datenquellen. Die folgenden Mergeregeln gelten:

1. SPA nimmt die größte Dauer als die neue Dauer.

2. Wenn Mergekonflikte vorhanden sind, werden die folgenden Regeln befolgt:

   1. Nehmen Sie das kleinste Intervall, als das neue Intervall.

   2. Nehmen Sie die Obermenge der Leistungsindikatoren. Z. B. mit **Prozess (\*)\\Prozessorzeit (%)** und **Prozess (\*)\\\*,\\Prozess (\*)\\ \\** * weitere Daten zurückgegeben, sodass **Prozess (\*)\\Prozessorzeit (%)** und **Prozess (\*)\\ \\** * aus den zusammengeführten datensammlersatz entfernt wird.

### <a name="collect-dynamic-data"></a>Dynamische Daten sammeln

SPA-Anforderungen, die einer definierten datensammlersatzes an die Entwurfszeit an. Es ist nicht immer möglich, zu wissen, welche Daten für die berichterstellung erforderlich ist, da die dynamische Daten und den Abfragepfad nicht bekannt sind, bis die abhängige Daten verfügbar ist.

z. B. Wenn Sie die Anzeigenamen der Netzwerkadapter auflisten möchten, müssen Sie zuerst die WMI zum Auflisten aller Netzwerkadapter Abfragen. Jede zurückgegebene, dass WMI-Objekt der Registrierungsschlüsselpfad, verfügt, in dem sie den angezeigten Namen speichert. Der Registrierungsschlüsselpfad ist unbekannt, zur Entwurfszeit. In diesem Fall benötigen wir dynamische Daten unterstützt.

Zum Auflisten aller Netzwerkadapter können Sie die folgende WMI-Abfrage mithilfe von Windows PowerShell:

``` syntax
Get-WmiObject -Namespace Root\Cimv2 -query "select PNPDeviceID FROM Win32_NetworkAdapter" | forEach-Object { Write-Output $_.PNPDeviceID }
```

Es gibt eine Liste der netzwerkadapterobjekten zurück. Jedes Objekt verfügt über eine Eigenschaft namens **PNPDeviceID**, der relative Registrierungsschlüsselpfad verwaltet. Hier ist s eine Beispielausgabe aus der vorherigen Abfrage:

``` syntax
ROOT\*ISatAP\0001
PCI\VEN_8086&DEV_4238&SUBSYS_11118086&REV_35\4&372A6B86&0&00E4
ROOT\*IPHTTPS\0000

```

Finden der **FriendlyName** Wert, Registrierungs-Editor und navigieren Sie zu registrierungseinstellung durch Kombinieren von **HKEY\_lokalen\_Computer\\SYSTEM\\ CurrentControlSet\\Enum\\**  mit jeder Zeile aus dem vorherigen Beispiel. Zum Beispiel: **HKEY\_lokalen\_Computer\\SYSTEM\\CurrentControlSet\\Enum\\ Stamm\\\*IPHTTPS\\0000**.

Um den vorherigen Schritten SPA-bereitstellen-Metadaten zu übersetzen, fügen Sie das Skript im folgenden Codebeispiel hinzu:

``` syntax
<advisorPack>
<dataSourceDefinition xmlns="http://microsoft.com/schemas/ServerPerformanceAdvisor/dc/2010">
 <dataCollectorSet >
<registryKeys>
 ?<registryKey>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\$(NetworkAdapter.PNPDeviceID)\FriendlyName</registryKey>
</registryKeys>
<managementpaths>
 ?<path name="NetworkAdapter">Root\Cimv2:select PNPDeviceID FROM Win32_NetworkAdapter</path>
</managementpaths>
```

In diesem Beispiel zunächst fügen Sie eine WMI-Abfrage unter Managementpaths und definieren den Namen des Schlüssels **Netzwerkadapter**. Sie fügen Sie einen Registrierungsschlüssel hinzu, und finden Sie unter **Netzwerkadapter** mithilfe der Syntax, **$(NetworkAdapter.PNPDeviceID)** .

In der folgende Tabelle definiert, wenn ein Datensammler in die SPA unterstützt dynamische Daten und gibt an, ob es von anderen Datensammlern verwiesen werden kann:

Datentyp | Unterstützung für dynamische Daten | Kann verwiesen werden
--- | :---: | :---:
Registrierungsschlüssel | Ja | Ja
WMI | Ja | Ja
Datei | Ja | Nein
Leistungsindikator | Nein | Nein
ETW | Nein | Nein

Für eine WMI-Datensammler verfügt jedes WMI-Objekt viele angefügten Attribute. Jede Art von WMI-Objekt hat immer drei Attribute: \_\_NAMESPACE \_ \_-Klasse, und \_ \_RELpath.

Um einen Datensammler zu definieren, die von anderen Datensammlern verwiesen wird, weisen die **Namen** Attribut mit einem eindeutigen Schlüssel in der ProvisionMetadata.xml. Dieser Schlüssel wird von abhängigen Datensammler verwendet, um dynamische Daten zu generieren.

Hier ist s ein Beispiel für Registrierungsschlüssel:

``` syntax
<registryKey  name="registry">HKEY_LOCAL_MACHINE </registryKey>
```

Und ein Beispiel für WMI:

``` syntax
<path name="wmi">Root\Cimv2:select PNPDeviceID FROM Win32_NetworkAdapter</path>
```

Um einen abhängigen Datensammler zu definieren, wird die folgende Syntax verwendet: $( *{Name}* . *{}-Attribut*).

*{Name}*  und *{-Attribut}* sind Platzhalter.

Bei der SPA-Daten von einem Zielserver sammelt, ersetzt er dynamisch die Muster $(\*.\*) durch die tatsächlichen Daten aus der Referenz-Datensammler erfasst (Registrierungsschlüssel / WMI), z.B.:

``` syntax
<registryKey>HKEY_LOCAL_MACHINE\$(registry.key)\ </registryKey>
<registryKey  name="registry">HKEY_LOCAL_MACHINE\$(wmi.Relativeregistrypath)\ </registryKey>
<path name="wmi"> </path>
<file>$(wmi.FileName)</file>
```

**Beachten Sie** SPA unterstützt eine unbegrenzte Tiefe des Verweises, aber der Performance-Overhead sichtbar, wenn Sie über zu viele Ebenen verfügen. Stellen Sie sicher, dass kein Zirkelverweis vorhanden ist oder der Verweis auf sich selbst, nicht unterstützt.

### <a name="versioning-limitations"></a>versionseinschränkungen

SPA werden zurückgesetzt und der Nebenversionsnummer-Updates unterstützt. Diese Prozesse verwenden den gleichen Algorithmus. Der Prozess ist, aktualisieren Sie alle Datenbankobjekte und schwellenwerteinstellungen aber behalten Sie die vorhandenen Daten. Dies kann ein Upgrade auf eine höhere Version oder ein Downgrade auf niedrigere Version. Wählen Sie das Advisor-Pack, und klicken Sie dann auf **zurücksetzen** in die **konfigurieren Advisor Packs** im Dialogfeld Updates oder SPA zum Zurücksetzen oder beim Anwenden.

Diese Funktion ist hauptsächlich für kleinere Aktualisierungen. Sie können nicht erheblich ändern, die Elemente der Benutzeroberfläche angezeigt. Wenn Sie erhebliche Änderungen vornehmen möchten, müssen Sie einen anderen Advisor Pack zu erstellen. Sie sollten die Version in den Advisor-Pack-Namen einschließen.

Die Einschränkungen der Nebenversion Änderungen sind, die Sie **kann nicht** führen Sie einen der folgenden:

* Ändern Sie den Schemanamen

* Ändern des Datentyps einer beliebigen Gruppe von einzelnen Wert oder die Spalten der Tabelle eine Liste-Wert

* Schwellenwerte hinzufügen oder entfernen

* Hinzufügen oder Entfernen von Regeln

* Hinzufügen oder Entfernen von Empfehlungen

* Hinzufügen oder Entfernen von einzelnen Werten

* Fügen Sie hinzu oder entfernen Sie die Werte in der Liste

* Fügen Sie hinzu oder entfernen Sie eine Spalte mit Listenwerten

### <a href="" id="bkmk-tooltips"></a>QuickInfos

Fast alle **Beschreibung** werden Attribute als QuickInfo in der SPA-Konsole angezeigt.

eine Liste-Wert-Tabelle kann eine QuickInfo zeilenbasierter erreicht werden, durch das folgende Attribut hinzufügen:

``` syntax
<listValue descriptionColumn="Description">
<column name="Name"/>
<column name="Description"/>
</listValue>
```

Die **DescriptionColumn** -Attribut verweist auf den Namen der Spalte. In diesem Beispiel wird die Spalte "Beschreibung" nicht als physische Spalte angezeigt. Es wird jedoch als QuickInfo, wenn Sie den Mauszeiger über die jede Zeile der ersten Spalte.

Es wird empfohlen, dass die QuickInfo die Datenquelle, die dem Benutzer angezeigt. Hier sind die Formate für die Anzeige von Datenquellen:

Datenquelle | Format | Beispiel
--- | --- | ---
WMI | WMI: &lt;Wmiclass&gt;/&lt;Feld&gt; | WMI: Win32_OperatingSystem/Caption
Leistungsindikator | PerfCounter: &lt;"CategoryName"&gt;/&lt;Instanzname&gt; | PerfCounter: Process/% Prozessorzeit
Registrierung | registry: &lt;registerKey&gt; | Registrierung: HKLM\SOFTWARE\Microsoft<br>\\ASP.NET\\Rootver
Konfigurationsdatei | ConfigFile: &lt;Filepath&gt;\[; Xpath: &lt;Xpath&gt;\]<br>**Hinweis**<br>XPath ist optional, und es gilt nur, wenn die Datei eine XML-Datei ist. | ConfigFile: %Windir%\\"System32"\\Inetsrv\config\\"applicationHost.config"<br>Xpath: configuration&frasl;system.webServer<br>&frasl;httpProtocol&frasl;@allowKeepAlive
ETW | ETW: &lt;Anbieter /&gt;(Keywords) | ETW: Windows-Kernel-Ablaufverfolgungsanbieter (Process, net)

### <a name="table-collation"></a>Tabellensortierung

Bei ein Advisor-Pack komplizierter wird, können Sie Ihre eigenen Variablen Tabellen oder temporäre Tabellen zum Speichern der Zwischenergebnisse in der Berichtsserver-Skript erstellen.

Sortieren Zeichenfolgenspalten kann problematisch sein, da die tabellensortierung, die Sie erstellen die abweichen kann, die durch das SPA-Framework erstellt wird. Wenn Sie zwei Zeichenfolgenspalten in verschiedenen Tabellen in Beziehung setzen, können Sie einen Sortierungsfehler finden Sie unter. Um dieses Problem zu vermeiden, sollten Sie immer die Zeichenfolge für eine spaltensortierung als definieren **SQL\_Latin1\_allgemeine\_CP1\_CI\_AS** beim Definieren einer Tabelle.

Hier s wie eine Variable Tabelle definiert:

``` syntax
DECLARE @filesIO TABLE (
 Name nvarchar(500) COLLatE SQL_Latin1_General_CP1_CI_AS,
 AverageFileAccessvolume float,
 AverageFileAccessCount float,
 Filepath nvarchar(500) COLLatE SQL_Latin1_General_CP1_CI_AS
)
```

### <a name="collect-etw"></a>Sammeln von ETW

Hier s ETW in einer Datei ProvisionMetadata.xml definieren:

``` syntax
<dataSourceDefinition>
  <providers>
    <provider session="NT Kernel Logger" guid="{9E814AAD-3204-11D2-9A82-006008A86939}"/>
  </providers>
</dataSourceDefinition>
```

Die folgenden Anbieterattribute sind für das Sammeln von ETW verwendet:

Attribut | Typ | Beschreibung
--- | --- | ---
guid | GUID | Anbieter-GUID
Sitzung | String | ETW-Sitzung ein (optional, nur für die Kernelereignisse erforderlich)
keywordsany | Hex | Keine Schlüsselwörter (optional, kein Präfix 0 X)
keywordsAll | Hex | Alle Schlüsselwörter (optional)
Eigenschaften | Hex | Eigenschaften (optional)
level | Hex | Ebene (optional)
bufferSize | Ganze Zahl | Größe des Puffers (optional)
flushtime | Ganze Zahl | Leeren Sie die Uhrzeit (optional)
maxBuffer | Ganze Zahl | Maximale Puffergröße (optional)
minBuffer | Ganze Zahl | Mindestgröße des Puffers (optional)

Es gibt zwei Ausgabetabellen wie hier gezeigt.

**\#Schema für table**

Spaltenname | SQL-Datentyp | Beschreibung
--- | --- | ---
SequenceID | Int nicht NULL | Korrelations-Sequenz-ID
EventtypeId | Int nicht NULL | Ereignis-Typ-ID (finden Sie unter [Dbo]. [ EventTypes])
ProcessId | BigInt, die nicht NULL | Prozess-ID
ThreadId | BigInt, die nicht NULL | Thread-ID
timestamp | datetime2 nicht NULL | timestamp
Kerneltime | BigInt, die nicht NULL | Kernelzeit
Usertime | BigInt, die nicht NULL | Benutzerzeit

**\#Tabellenschema EventProperties**

Spaltenname | SQL-Datentyp | Beschreibung
--- | --- | ---
SequenceID | Int nicht NULL | Korrelations-Sequenz-ID
Name | nvarchar(100) | Eigenschaftenname
Wert | nvarchar(4000) | Wert

### <a name="etw-schema"></a>ETW-schema

Ein ETW-Schema kann durch Ausführen von tracerpt.exe für die ETL-Datei generiert werden. Eine Datei "Schema.man" generiert. Da das Format der ETL-Datei Computer abhängig ist, funktioniert das folgende Skript nur in den folgenden Situationen:

1.  Führen Sie das Skript auf dem Computer, wo die entsprechenden ETL-Datei erfasst wird.

2.  Oder führen Sie das Skript auf einem Computer mit dem gleichen Betriebssystem und Komponenten, die installiert werden.

``` syntax
tracerpt *.etl -export
```

## <a name="glossary"></a>Glossar


Die folgenden Begriffe werden in diesem Dokument verwendet:

**Advisor-pack**

Ein Advisor-Pack ist eine Sammlung von Metadaten und SQL-Skripts, die die Leistungsprotokolle zu verarbeiten, die auf dem Zielserver erfasst werden. Das Advisor-Pack generiert dann Berichte über die leistungsprotokolldaten aus. Die Metadaten in das Advisor-Pack definiert die Daten von der Zielserver für Leistungsindikatoren gesammelt werden sollen. Die Metadaten definieren auch den Satz von Regeln, Schwellenwerten und das Format des Berichts. In den meisten Fällen wird ein Advisor-Pack speziell für eine einzige Serverrolle, z. B. Internet Information Services (IIS) geschrieben.

**SPA-Konsole**

Die SPA-Konsole bezieht sich auf SpaConsole.exe, die der zentrale Teil des Server Performance Advisor ist. SPA muss nicht auf dem Zielserver ausgeführt wird, die Sie testen. Die SPA-Konsole enthält die Benutzeroberflächen für SPA vom das Projekt Analyse ausführen und Anzeigen von Berichten einrichten. Standardmäßig ist die SPA eine Anwendung mit zwei Ebenen. Die SPA-Konsole enthält die UI-Ebene und der Teil der Geschäftslogik-Ebene. Die SPA-Konsole plant und Performance Analysis-Anforderungen verarbeitet.

**SPA-framework**

SPA enthält zwei Hauptbereiche, die das Framework und des Advisor-Packs. Das SPA-Framework bietet alle Benutzeroberflächen, protokollverarbeitung Leistung, Konfiguration, Fehlerbehandlung und Prozeduren für Datenbank-APIs und die Verwaltung.

**SPA-Projekt**

Ein SPA-Projekt ist eine Datenbank, die enthält alle Informationen zu den Zielservern, Advisor-Packs und Berichte zur transaktionsleistungsanalyse, die generiert werden auf den Zielservern für die Advisor-Packs. Sie können vergleichen und Anzeigen von Verlauf und Trend Diagrammen innerhalb des gleichen SPA-Projekts. Der Benutzer kann mehr als ein Projekt erstellen. Die SPA-Projekte sind voneinander unabhängig, und es sind keine Daten für Projekte freigegeben.

**Zielserver**

Der Zielserver ist der physische oder virtuelle Maschine, die die Windows-Server mit bestimmten Serverrollen, wie z. B. IIS ausgeführt wird.

**Data Analysis-Sitzung**

Eine Data-Analyse-Sitzung wird dem Systemmonitor Leistungsanalysen an einen bestimmten Zielserver. Eine Data-Analyse-Sitzung kann mehrere Packs für Advisor enthalten. Die Sammlungssätze aus diesen Packs für Advisor werden in einer einzelnen Datensammlergruppe zusammengeführt. Alle Leistungsprotokolle für eine einzelne Analysis-Sitzung werden im gleichen Zeitraum gesammelt werden. Analysieren von Berichten, die von Advisor-Packs ausgeführt wird, in der gleichen Sitzung des Data-Analyse generiert werden, können Benutzer verstehen, die gesamtleistung Situation und Ursachen, um Leistungsprobleme zu identifizieren.

**Ereignisablaufverfolgung für Windows**

[Ereignisablaufverfolgung](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) für Windows (ETW) eine hohe Leistung, mit geringem Verwaltungsaufwand, skalierbare Ablaufverfolgungssystem ist, die in den Windows-Betriebssystemen bereitgestellt wird. Es bietet die profilerstellung und Debuggen Funktionen, die verwendet werden kann, um eine Vielzahl von Szenarien zu beheben. SPA verwendet ETW-Ereignisse als Datenquelle für das Generieren von die Leistungsberichte. Allgemeine Informationen zu ETW finden Sie in [verbessertes Debugging und Leistungsoptimierung mit ETW](https://msdn.microsoft.com/magazine/cc163437.aspx).

**WMI-Abfrage**

Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) ist die Infrastruktur für Verwaltungsdaten und Vorgängen in Windows-Betriebssysteme. Sie können WMI-Skripts oder Anwendungen zum Automatisieren administrativer Aufgaben auf Remotecomputern schreiben. WMI bietet auch die Verwaltungsdaten für andere Teile des Betriebssystems und Produkte. SPA verwendet WMI-Klasseninformationen und Datenpunkte als Quellen zum Generieren von Leistungsberichten.

**Leistungsindikatoren**

Leistungsindikatoren werden verwendet, um Informationen über das Betriebssystem oder eine Anwendung, Dienst oder Treiber Leistung bereitzustellen. Die Leistungsindikatordaten können helfen, Engpässe im System festzustellen und System- und Anwendungsleistung zu optimieren. Geben Sie das Betriebssystem, Netzwerk, und Geräte Leistungsindikatordaten, die eine Anwendung nutzen kann, um Benutzern eine grafische Ansicht der Leistung des Systems zur Verfügung stellen. SPA werden Informationen für Leistungsindikatoren und Datenpunkte als Datenquellen verwendet, um Leistungsberichte zu generieren.

**Leistungsprotokolle und-Warnungen**

Leistungsprotokolle und Warnungen (PLA) ist ein integrierter Dienst im Windows-Betriebssystem. Wurde entwickelt, um die Leistungsprotokolle und ablaufverfolgungen zu erfassen, und es auch leistungswarnungen ausgelöst, wenn bestimmte Trigger erfüllt sind. PLA kann zum Sammeln von Leistungsindikatoren, ereignisablaufverfolgung für Windows (ETW), WMI-Abfragen, Registrierungsschlüssel und -Konfiguration Dateien verwendet werden. PLA unterstützt auch die remotedatensammlung über Remoteprozeduraufrufe (RPC). Der Benutzer definiert einen datensammlersatz, der Informationen über die zu sammelnden Daten, die Häufigkeit der Datensammlung, Daten sammlungsdauer, Filter und einen Speicherort zum Speichern der Ergebnisdateien enthält. SPA verwendet PLA, um alle Leistungsdaten von den Zielservern zu sammeln.

**Berichtsdefinitionssprache**

Einzelnen Bericht ist die SPA-Bericht, der generiert wird, für eine Sitzung mit Daten und Analyse für eine Advisor-Pack auf einem einzelnen Ziel-Server. Sie können Benachrichtigungen und die verschiedenen Datenabschnitte enthalten.

**Seite-an-Seite-Bericht**

Ein Seite-an-Seite-Bericht handelt es sich um eine SPA-Bericht, in dem zwei einzelne Berichte für das gleiche Advisor Pack verglichen. Die beiden Berichte können von anderen Servern oder aus separaten Performance Analysis ausgeführt wird, auf dem gleichen Zielserver generiert werden. Der Bericht für die Seite-an-Seite erstellt die Funktion zum Vergleichen von zwei Berichte, die Benutzer erkennen nicht normalem Verhalten oder die Einstellungen in einen Bericht zu erleichtern. Ein Seite-an-Seite-Bericht enthält, Benachrichtigungen und die verschiedenen Datenabschnitte. In jedem Abschnitt sind die Daten aus sowohl Berichten aufgelisteten Seite-an-Seite.

**Trenddiagramm**

Ein Trenddiagramm ist die SPA-Bericht, der verwendet wird, um sich wiederholende Muster von Leistungsproblemen zu untersuchen. Viele sich wiederholende Leistungsprobleme werden durch geplante serveränderungen verursacht, auf dem Server oder -Clientcomputern, die auftreten, können täglich oder wöchentlich. SPA bietet ein 24-Stunden-Trenddiagramm und ein Trenddiagramm für 7 Tage um diese Probleme zu identifizieren.

Wahlweise kann der Benutzer eine oder mehrere Datenreihen zu einem Zeitpunkt, die einen numerischen Wert in den einzelnen Bericht, wie z. B. ist **durchschnittliche CPU-gesamtnutzung**. genauer gesagt ist ein numerischer Wert einen skalaren Wert aus einem einzelnen Server, der durch einen einzelnen Zugriffspunkt an einem bestimmten Zeitpunkt-Instanz generiert wird. SPA gruppiert diese Werte in 24-Gruppen, eine für jede Stunde des Tages (für einen Bericht für 7 Tage, eine für jeden Tag der Woche: sieben). SPA berechnet, Mittelwert, Minimum, Maximum und Standardabweichungen für jede Gruppe.

**Verlaufsdiagramm**

Ein Verlaufsdiagramm wird die SPA-Bericht, der verwendet wird, um Änderungen in bestimmten numerischen Werten in den einzelnen Berichten für einen bestimmten Server und die Advisor-Pack-Paar im Laufe der Zeit anzuzeigen. Der Benutzer kann mehrere Datenreihen wählen und gemeinsam im das Verlaufsdiagramm zu die Korrelation zwischen unterschiedliche Datenreihen anzeigen.

**Datenreihe**

Eine Datenreihe ist die numerische Daten, die von der gleichen Datenquelle über einen Zeitraum gesammelt werden. Die gleiche Quelle bedeutet, dass die Daten aus dem gleichen Zielserver, z. B. die durchschnittliche Länge der Anforderungswarteschlange für IIS auf einem Server stammen.

**Regeln**

Regeln sind Kombinationen von Logik-, Schwellenwerte und Beschreibungen. Sie stellen ein mögliches Leistungsproblem dar. Jedes Advisor Pack enthält mehrere Regeln. Jede Regel wird durch die Verarbeitung eines Berichts Generation ausgelöst. Eine Regel gilt die Logik und die Schwellenwerte auf die Daten in den einzelnen Bericht. Wenn die Kriterien erfüllt sind, wird eine Benachrichtigung für eine Warnung ausgelöst. Wenn nicht, die Benachrichtigung, um festgelegt ist die **OK** Zustand. Wenn nicht die Regel gilt, wird die Benachrichtigung, die nicht anwendbar festgelegt (**NA**) Zustand.

**Benachrichtigungen**

Eine Benachrichtigung ist, die Informationen, die eine Regel für Benutzer angezeigt wird. Es enthält den Status der Regel (**OK**, **NA**, oder **Warnung**), wird der Name der Regeln und möglichen Empfehlungen, um die Leistungsprobleme zu beheben.
