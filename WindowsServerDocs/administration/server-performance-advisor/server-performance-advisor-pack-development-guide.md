---
title: Server Performance Advisor Pack-Entwicklungsleitfaden
description: Server Performance Advisor Pack-Entwicklungsleitfaden
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cdf812f862534ba8cd07d4558e424faf3c56c699
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75947147"
---
# <a name="server-performance-advisor-pack-development-guide"></a>Server Performance Advisor Pack-Entwicklungsleitfaden

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 8, Windows 10

In diesem Entwicklungs Leit Faden für Microsoft Server Performance Advisor (Spa) finden Sie Richtlinien, die Entwicklern und Systemadministratoren bei der Entwicklung von Advisor Packs zur Analyse der Server Leistung helfen.

Dabei wird davon ausgegangen, dass Sie mit Leistungsprotokolle und-Warnungen (PLA), Leistungsindikatoren, Registrierungs Einstellungen, Windows-Verwaltungsinstrumentation (WMI), Ereignis Ablauf Verfolgung für Windows (ETW) und Transact SQL (T-SQL) vertraut sind.

Weitere Informationen zur Verwendung von Spa finden Sie [im Benutzerhandbuch für den Server Performance Advisor](server-performance-advisor-users-guide.md).

## <a name="spa-advisor-pack-overview"></a>Übersicht über das Spa Advisor Pack


Ein Advisor Pack ist in der Regel für eine bestimmte Server Rolle konzipiert und definiert Folgendes:

* Daten, die über die Pla gesammelt werden sollen, einschließlich Windows-Verwaltungsinstrumentation (WMI), Leistungsindikatoren, Registrierungs Einstellungen, Dateien und Ereignis Ablauf Verfolgung für Windows (ETW)

* Regeln, die Warnungen und Empfehlungen anzeigen

* Daten, die angezeigt werden sollen (gesammelte Rohdaten, aggregierte Daten oder Top 10-Listen)

* Statistik zum Anzeigen eines Werts, der sich im Laufe der Zeit ändert

* Statistik Werte, für die ein Trend durchgeführt werden kann

Ein Advisor-Pack umfasst die folgenden Elemente:

* **XML-Metadaten** ("provisionmetadata. xml")

    * [Leistungsprotokolle und-Warnungen (PLA)](https://msdn.microsoft.com/library/windows/desktop/aa372635.aspx) -Datensammler Satz

    * Berichtslayout

* **SQL-Skripts**

    * Eine gespeicherte Haupt Prozedur

    * SQL-Objekte, z. b. gespeicherte Prozeduren und benutzerdefinierte Funktionen

* **Etw-Schema Datei** (Schema. man) Dies ist optional.

### <a name="advisor-pack-workflow"></a>Advisor Pack-Workflow

![Advisor Pack-Workflow](../media/server-performance-advisor/spa-dev-guide-workflow.png)

In diesem Flussdiagramm stellen die grünen Kreise Advisor-Pakete dar. Alle anderen Kreise stellen die Phasen dar, die im Rahmen des Spa-Frameworks ausgeführt werden. Spa verwendet ein Advisor Pack zum Sammeln von Daten, Importieren der Daten in die Datenbank, Initialisieren der Ausführungsumgebung und Ausführen von SQL-Skripts.

### <a name="collect-data"></a>Sammeln von Daten

Wenn ein Advisor-Pack mithilfe von Spa für einen bestimmten Server in die Warteschlange eingereiht wird, fragt das Daten Sammlungsmodul den Datensammler Satz-XML-Code aus dem Advisor Pack ab und sammelt Daten vom Zielserver. Die Rohdaten werden in einer benutzerdefinierten Dateifreigabe gespeichert. Die Datensammlung wird erst beendet, wenn die vom Benutzer festgelegte Spa-Ausführungsdauer überschritten wurde.

### <a name="import-data-into-the-database"></a>Importieren von Daten in die Datenbank

Nachdem die Datensammlung abgeschlossen ist, wird jeder Datentyp in eine entsprechende Tabelle in der SQL Server-Datenbank importiert. Registrierungs Einstellungen werden z. b. in eine Tabelle namens "\#RegistryKeys" importiert.

zum Importieren der etw-Datei ist eine ETW-Schema Datei zum Decodieren der ETL-Datei erforderlich. Die ETW-Schema Datei ist eine XML-Datei. Sie kann mithilfe von tracerpt. exe generiert werden, das in Windows enthalten ist. Die ETW-Schema Datei ist nur erforderlich, wenn das Advisor-Paket etw-Daten importieren muss.

### <a name="switch-to-low-user-rights"></a>Zu niedrigen Benutzerrechten wechseln

Das Spa-Framework passt die Berechtigungen automatisch an, um die erforderliche Sicherheits Zugriffsebene zu minimieren. Da Advisor Packs von jedem Benutzer entwickelt oder geändert werden können, ist es möglich, dass ein Advisor-Pack manipulierte SQL-Skripts enthält. Um das Sicherheitsrisiko zu verringern, sollte jedes SQL-Skript für ein Advisor-Pack mit niedrigen Benutzerrechten ausgeführt werden. Sie kann nur auf eingeschränkte Datenbankobjekte zugreifen, z.b. temporäre Tabellen und Spa-APIs, die als gespeicherte Prozeduren verfügbar gemacht werden. Die SQL-Skripts in einem Advisor-Pack können diese gespeicherten Prozeduren zum interagieren mit dem Spa-Framework aufruft.

### <a name="initialize-execution-environment"></a>Ausführungsumgebung initialisieren

Advisor Packs können unterschiedliche Arten von Ausgaben generieren, z. b. Benachrichtigungen, Empfehlungen, Fakten Tabellen, Statistiken und Diagramme für Statistiken. Die SQL-Skripts führen bestimmte Berechnungen für die gesammelten Daten aus. Die Ergebnisse der Ergebnisse werden in temporären Tabellen über öffentliche Spa-APIs gespeichert. in der Initialisierungsphase müssen diese temporären Tabellen und anderen Systemressourcen bereitgestellt werden.

### <a name="run-sql-scripts"></a>SQL-Skripts ausführen

Es gibt eine Haupt gespeicherte Prozedur, die vom Advisor Pack-Entwickler benannt wird. Das Spa-Framework ruft diese gespeicherte Prozedur auf, um die Berechnung zu initiieren. Die gespeicherte Prozedur verwendet die gesammelten Daten und kommuniziert das Endergebnis an das Spa-Framework.

### <a name="switch-to-administrative-rights"></a>Zu Administratorrechten wechseln

Zum Generieren eines Berichts sind Administrator Rechte erforderlich. Die Bericht Generierung wird vollständig von Spa gesteuert. Es ist weniger wahrscheinlich, manipuliert zu werden.

### <a name="generate-a-report"></a>Generieren eines Berichts

Bevor die gespeicherte Haupt Prozedur für ein Advisor Pack abgeschlossen wird, werden alle berechneten Ergebnisse, wie z. b. Benachrichtigungen und Statistiken, nicht beibehalten. In dieser Phase überträgt das Spa-Framework die Endergebnisse aus temporären Tabellen auf Tabellen in einem bestimmten Format. Nachdem diese Phase fertiggestellt wurde, können Sie die Berichte mithilfe der Spa-Konsole anzeigen.

## <a name="authoring-an-advisor-pack"></a>Erstellen eines Advisor-Pakets


### <a name="quick-guidelines"></a>Schnelle Richtlinien

Im folgenden Flussdiagramm werden die Schritte beschrieben, mit denen Sie ein voll funktionsfähiges Advisor Pack entwickeln können. Dieser Abschnitt enthält auch schrittweise Anleitungen zur besseren Erläuterung der einzelnen Schritte.

![Advisor Pack-Entwicklungsprozess](../media/server-performance-advisor/spa-dev-guide-dev-flowchart.png)

Ein Advisor-Pack ist normalerweise wie folgt strukturiert:

Advisor-Pack

"Provisionmetadata. xml"

Scripts

Main. SQL

Func. SQL

Schema. man

Jedes Advisor-Paket muss über eine Datei namens "provisionmetadata. xml" verfügen. Es definiert grundlegende Advisor-Paketinformationen, die zu sammelnden Daten, Benachrichtigungen und Regeln sowie die Art und Weise, wie der Bericht gespeichert und angezeigt werden muss. Das Spa-Framework verwendet diese Informationen zum Generieren einer temporären Tabelle und zum anschließenden übertragen der Ergebnisse in der temporären Tabelle in eine Tabelle, auf die Benutzer zugreifen können.

Alle Berichts-SQL-Skripts müssen in einem Unterordner namens " **Scripts**" gespeichert werden. Zu Wartungszwecken empfiehlt es sich, unterschiedliche Datenbankobjekte in verschiedenen SQL Server Dateien zu speichern. Es muss mindestens eine gespeicherte Prozedur als Haupteinstiegspunkt vorhanden sein.

> [!NOTE]
> Die Datei "Schema. man" ist nur erforderlich, wenn Ihr Advisor-Pack etw-Ablauf Verfolgungen sammelt. Diese Schema Datei wird verwendet, um das Schema der ETW-Ereignisse zu beschreiben und ETW-Ereignisse zu decodieren.

### <a name="defining-basic-information"></a>Definieren grundlegender Informationen

In diesem Abschnitt werden einige der grundlegenden Elemente beschrieben, aus denen ein Advisor-Pack besteht, einschließlich "provisionmetadata. xml" und Attribute.

Im folgenden finden Sie eine Beispiel Kopfzeile für die Datei "provisionmetadata. xml":

``` syntax
<advisorPack
xmlns="https://microsoft.com/schemas/ServerPerformanceAdvisor/ap/2010"
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

### <a name="advisor-pack-version"></a>Advisor Pack-Version

Attribut Name: **Version**

Advisor Pack-Entwickler können die Haupt-und neben Versionen für das Advisor-Pack definieren:

* Eine Hauptversion umfasst in der Regel bedeutende Verbesserungen. Die Ergebnisse, die von einer alten Version generiert werden, sind möglicherweise nicht mit der neuen kompatibel. Es wird dringend empfohlen, dass Sie die Hauptversion in den Advisor Pack-Namen einschließen.

* Spa ermöglicht neben Versions Upgrades, wenn es nur geringfügige Änderungen ohne Daten Inkompatibilitäts Probleme gibt.

Weitere Informationen zur Versionsverwaltung finden Sie unter [Advanced Topics](#bkmk-advancedtopics).

### <a name="script-entry-point"></a>Skript Einstiegspunkt

Attribut Name: **Report Script**

Das Spa-Framework sucht im Skript Einstiegspunkt nach dem Namen der gespeicherten Haupt Prozedur und führt ihn auf sichere Weise aus.

### <a name="other-attributes"></a>Andere Attribute

Im folgenden finden Sie einige weitere Attribute, die zum Identifizieren eines Advisor-Pakets verwendet werden können:

* Anzeige Name: Display **Name**

* Beschreibung: **Beschreibung**

* Autor: **Autor**

* Framework-Version: **Frameworkversion** (standardmäßig 3,0)

* Mindestversion des Betriebssystems: **minosversion** (diese ist für die spätere Erweiterbarkeit reserviert)

* Benachrichtigung über verlorene Ereignisse: **showeventlostwarning**

### <a href="" id="bkmk-definedatacollector"></a>Definieren des Datensammler Satzes

Ein Datensammler Satz definiert die Leistungsdaten, die das Spa-Framework vom Zielserver sammeln soll. Es unterstützt Registrierungs Einstellungen, WMI, Leistungsindikatoren, Dateien vom Zielserver und etw.

``` syntax
<advisorPack>
<dataSourceDefinition xmlns="https://microsoft.com/schemas/ServerPerformanceAdvisor/dc/2010">
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

Mit dem **Duration** -Attribut von **&lt;datacollector Set/&gt;** im vorherigen Beispiel wird die Dauer der Datensammlung definiert (die Zeiteinheit ist Sekunden). **Duration** ist ein erforderliches Attribut. Mit dieser Einstellung wird die von Leistungsindikatoren und etw verwendete Sammlungs Dauer gesteuert.

### <a name="collect-registry-data"></a>Sammeln von Registrierungsdaten

Sie können Registrierungsdaten aus den folgenden Registrierungs Strukturen erfassen:

* HKEY-\_Klassen\_root

* HKEY-\_aktuelle\_config

* HKEY-\_aktueller\_Benutzer

* HKEY\_lokalen\_Computer

* HKEY-\_Benutzer

Um eine Registrierungs Einstellung zu erfassen, geben Sie den vollständigen Pfad zum Wertnamen an: HKEY\_lokalen\_Computer\\MyKey\\meinWert

Um alle Einstellungen unter einem Registrierungsschlüssel zu erfassen, geben Sie den vollständigen Pfad zum Registrierungsschlüssel an: HKEY\_lokalen\_Computers\\MyKey\\

Wenn Sie alle Werte unter einem Registrierungsschlüssel und seinen untergeordneten Schlüsseln erfassen möchten (die Daten werden von der Datenbank rekursiv gesammelt), verwenden Sie zwei umgekehrte Schrägstriche für das letzte Pfad Trennzeichen: HKEY\_local\_Machine\\MyKey\\\\

Um Registrierungsinformationen von einem Remote Computer zu erfassen, fügen Sie den Computernamen am Anfang des Registrierungs Pfads ein: HKEY\_lokalen\_Machine\\MyKey\\meinWert

Beispielsweise können Sie über einen Registrierungsschlüssel verfügen, der wie folgt aussieht:

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

Beispiel 1: Zurückgeben der aktiven powerschemas und ihrer Werte:

``` syntax
<registryKey>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes</registryKey>
```

Beispiel 2: gibt alle Schlüssel-Wert-Paare unter diesem Pfad zurück:

> [!NOTE]
> Die Ausführung von Pla erfolgt unter Benutzer Anmelde Informationen. Für einige Registrierungsschlüssel sind administrative Anmelde Informationen erforderlich. Die Enumeration wird beendet, wenn der Zugriff auf keine der untergeordneten Schlüssel fehlschlägt.

``` syntax
<registryKey>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\User\PowerSchemes\\</registryKey>
```

Alle gesammelten Daten werden in eine temporäre Tabelle namens **\#RegistryKeys** importiert, bevor ein SQL-Berichts Skript ausgeführt wird. In der folgenden Tabelle werden die Ergebnisse für Beispiel 2 angezeigt:

KeyName | Keytypeid | Value
------ | ----- | -------
HKEY_LOCAL_MACHINE. ..\powerschemas | 1 | db310065-829b-4671-9647-2261c00e86ef
\db310065-829b-4671-9647-2261c00e86ef\description | 2 | |
\db310065-829b-4671-9647-2261c00e86ef\friendlyname | 2 | Stromquelle optimiert
. ..\6738e2c4-e8a5-4a42-b16a-e040e769756e\acsettingindex | 4 | 180
. ..\6738e2c4-e8a5-4a42-b16a-e040e769756e\dcsettingindex | 4 | 30

Das Schema für die **#registryKeys** Tabelle lautet wie folgt:

Name der Spalte | SQL-Datentyp | Beschreibung
-------- | -------- | --------
KeyName | Nvarchar (300) nicht NULL | Vollständiger Pfadname des Registrierungsschlüssels
Keytypeid | Smallint not NULL | Interne Typ-ID
Value | Nvarchar (4000) nicht NULL | Alle Werte

Die **keytypeid** -Spalte kann einen der folgenden Typen aufweisen:

ID | Geben Sie in das Suchfeld auf der Taskleiste
--- | ---
1 | Zeichenfolge
2 | ExpandString
3 | Binär
4 | DWord
5 | Dwordbigendian
6 | Link
7 | "Multiplestring"
8 | ResourceList
9 | Fullresourcedescriptor
10 | Resourcerequirementslist
11 | QWord

### <a name="collect-wmi"></a>WMI-Erfassung

Sie können eine beliebige WMI-Abfrage hinzufügen. Weitere Informationen zum Schreiben von WMI-Abfragen finden Sie unter [WQL (SQL für WMI)](https://msdn.microsoft.com/library/windows/desktop/aa394606.aspx). Im folgenden Beispiel wird eine Auslagerungs Datei abgefragt:

``` syntax
<path>Root\Cimv2:select * FROM Win32_PageFileUsage</path>
```

Die Abfrage im obigen Beispiel gibt einen Datensatz zurück:

Untertitel für Hörgeschädigte | Name | Peer Usage
----- | ----- | -----
C:\pagefile.sys | C:\pagefile.sys | 215

Da WMI eine Tabelle mit unterschiedlichen Spalten zurückgibt und die gesammelten Daten in eine Datenbank importiert werden, führt Spa eine Daten Normalisierung durch und wird den folgenden Tabellen hinzugefügt:

**wmiobjects-Tabelle (\#)**

SequenceID | Namespace | ClassName | RelativePath | Wmiqueryid
----- | ----- | ----- | ----- | -----
10 | Root\Cimv2 | Win32_PageFileUsage | Win32_PageFileUsage. Name =<br>C:\\Pagefile. sys | 1

**\#Tabelle "wmiobjectsproperties"**

ID | query
--- | ---
1 | Root\cimv2: SELECT * from Win32_PageFileUsage

**\#wmiqueries-Tabelle**

ID | query
--- | ---
1 | Root\cimv2: SELECT * from Win32_PageFileUsage

**wmiobjects-Tabellen Schema (\#)**

Name der Spalte | SQL-Datentyp | Beschreibung
--- | --- | ---
SequenceId | Int not NULL | Korrelieren der Zeile und ihrer Eigenschaften
Namespace | Nvarchar (200) nicht NULL | WMI-Namespace
ClassName | Nvarchar (200) nicht NULL | WMI-Klassenname
RelativePath | Nvarchar (500) nicht NULL | Relativer WMI-Pfad
Wmiqueryid | Int not NULL | Korrelieren Sie den Schlüssel #WmiQueries

**wmiobjectproperties-Tabellen Schema \#**

Name der Spalte | SQL-Datentyp | Beschreibung
--- | --- | ---
SequenceId | Int not NULL | Korrelieren der Zeile und ihrer Eigenschaften
Name | Nvarchar (1000) nicht NULL | Eigenschaftenname
Value | Nvarchar (4000) NULL | Der Wert der aktuellen Eigenschaft.

**\#wmiqueries-Tabellen Schema**

Name der Spalte | SQL-Datentyp | Beschreibung
--- | --- | ---
ID | Int not NULL | eindeutige Abfrage-ID >
query | Nvarchar (4000) nicht NULL | Ursprüngliche Abfrage Zeichenfolge in den Bereitstellungs Metadaten

### <a name="collect-performance-counters"></a>Leistungsindikatoren erfassen

Hier finden Sie ein Beispiel für die Erfassung eines Leistungs Zählers:

``` syntax
<performanceCounters interval="1">
  <performanceCounter>\PhysicalDisk(*)\Avg. Disk sec/Transfer</performanceCounter>
</performanceCounters>
```

Das **Interval** -Attribut ist eine erforderliche globale Einstellung für alle Leistungsindikatoren. Er definiert das Intervall (die Zeiteinheit ist Sekunden) für die Erfassung von Leistungsdaten.

Im vorherigen Beispiel wird die Leistungsindikator \\PhysicalDisk (\*)\\Mittlere Sek./Übertragung pro Sekunde abgefragt.

Es können zwei Instanzen vorhanden sein: **\_Gesamt** und **0 C: D:** , und die Ausgabe könnte wie folgt lauten:

timestamp | CategoryName | CounterName | Instanzwert _Total | Instanzwert 0 C: D:
---- | ---- | ---- | ---- | ----
13:45:52.630 | PhysicalDisk | Mittlere Sek./Übertragung | 0.00100008362473995 |0.00100008362473995
13:45:53.629 | PhysicalDisk | Mittlere Sek./Übertragung | 0.00280023414927187 | 0.00280023414927187
13:45:54.627 | PhysicalDisk | Mittlere Sek./Übertragung | 0.00385999853230048 | 0.00385999853230048
13:45:55.626 | PhysicalDisk | Mittlere Sek./Übertragung | 0.000933297607934224 | 0.000933297607934224

Um die Daten in die Datenbank zu importieren, werden die Daten in eine Tabelle mit dem Namen **\#performanceCounters**normalisiert.

Categorydisplayname | InstanceName | Counter Display Name | Value
---- | ---- | ---- | ----
PhysicalDisk | _Gesamt | Mittlere Sek./Übertragung | 0.00100008362473995
PhysicalDisk | 0 C: D: | Mittlere Sek./Übertragung | 0.00100008362473995
PhysicalDisk | _Gesamt | Mittlere Sek./Übertragung | 0.00280023414927187
PhysicalDisk | 0 C: D: | Mittlere Sek./Übertragung | 0.00280023414927187
PhysicalDisk | _Gesamt | Mittlere Sek./Übertragung | 0.00385999853230048
PhysicalDisk | 0 C: D: | Mittlere Sek./Übertragung | 0.00385999853230048
PhysicalDisk | _Gesamt | Mittlere Sek./Übertragung | 0.000933297607934224
PhysicalDisk | 0 C: D: | Mittlere Sek./Übertragung | 0.000933297607934224

**Hinweis** Die lokalisierten Namen, wie z. b. **categorydisplayname** und **counterdisplayname**, variieren je nach der auf dem Zielserver verwendeten Anzeige Sprache. Verwenden Sie diese Felder nicht, wenn Sie ein sprach neutrales Advisor Pack erstellen möchten.

**\#performanceCounters** -Tabellen Schema

Name der Spalte | SQL-Datentyp | Beschreibung
---- | ---- | ---- | ----
timestamp | datetime2 (3) nicht NULL | Datum/Uhrzeit der Erfassung in UNC
CategoryName | Nvarchar (200) nicht NULL | Kategoriename
Categorydisplayname | Nvarchar (200) nicht NULL | Lokalisierter Kategoriename
InstanceName | Nvarchar (200) NULL | Instanzenname
CounterName | Nvarchar (200) nicht NULL | Name des Leistungsindikators
Counter Display Name | Nvarchar (200) nicht NULL | Lokalisierter namens Name
Value | Float not NULL | Der gesammelte Wert

### <a name="collect-files"></a>Dateien sammeln

Die Pfade können absolut oder relativ sein. Der Dateiname kann das Platzhalter Zeichen (\*) und das Fragezeichen (?) enthalten. Wenn Sie z. b. alle Dateien im temporären Ordner sammeln möchten, können Sie c:\\Temp\\\*angeben. Das Platzhalter Zeichen gilt für Dateien im angegebenen Ordner.

Wenn Sie auch Dateien aus den Unterordnern des angegebenen Ordners sammeln möchten, verwenden Sie zwei umgekehrte Schrägstriche für das letzte Ordner Trennzeichen, z. b. c:\\Temp\\\\\*.

Hier ist ein Beispiel für die Abfrage der Datei " **ApplicationHost. config** ":

``` syntax
<path>%windir%\System32\inetsrv\config\applicationHost.config</path>
```

Die Ergebnisse finden Sie in einer Tabelle namens **\#Dateien**, z. b.:

querypath | FullPath | Element Pfad | Dateiname | Inhalt
----- | ----- | ----- | ----- | -----
% windir%\... \applicationhost.config |C:\Windows<br>\... \applicationhost.config | C:\Windows<br>\... \Config | ApplicationHost. | 0x3c3f

**Tabellen Schema für \#Dateien**

Name der Spalte | SQL-Datentyp | Beschreibung
---- | ---- | ----
querypath | Nvarchar (300) nicht NULL | Ursprüngliche Abfrage Anweisung
FullPath | Nvarchar (300) nicht NULL | Absoluter Dateipfad und Dateiname
Element Pfad | Nvarchar (300) nicht NULL | Dateipfad
Dateiname | Nvarchar (300) nicht NULL | Dateiname
Inhalt | Varbinary (max) NULL | Dateiinhalt in Binärdatei

### <a name="defining-rules"></a>Definieren von Regeln

Nachdem genügend Daten mithilfe von Pla von einem Zielserver gesammelt wurden, kann das Advisor Pack diese Daten für die Überprüfung verwenden und eine kurze Zusammenfassung der Systemadministratoren anzeigen.

Mit Regeln wird eine kurze Übersicht über die Leistung des Servers erzielt. Es werden Probleme hervorgehoben und Empfehlungen bereitgestellt. Sie können alle Regeln auflisten, die Sie für ein Advisor-Pack überprüfen möchten. Wenn Sie z. b. ein Kernbetriebssystem Advisor-Paket entwickeln möchten, können Sie folgende Regeln einschließen:

* Ob der CPU-Energiesparmodus Energiesparmodus ist

* Ob sich der Server in einer virtualisierten Umgebung befindet

* Ob Datenträger-e/a-Druck vorhanden ist

Regeln enthalten die folgenden Elemente:

* Abhängiger Schwellenwert (ein konfigurierbarer Teil einer Regel)

* Regel Definition (Warnungen und Empfehlungen)

Hier ist ein Beispiel für eine einfache Regel:

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

Der Schwellenwert ist ein konfigurierbarer Faktor, mit dem Systemadministratoren entscheiden können, wann eine Regel einen guten oder einen ungültigen Status aufweisen soll. Das folgende Beispiel zeigt eine Regel, mit der der freie Speicherplatz auf einem Systemlaufwerk erkannt wird, und eine Warnung, wenn der freie Speicherplatz weniger als 10 GB beträgt.

``` syntax
<threshold name="freediskSize" caption="Free Disk Size (GB)" description="Free Disk Size  value="10" />
```

In diesem Fall verfügt der Systemadministrator jedoch über eine kleinere Festplatte. Er meint, dass 5 GB freier Speicherplatz immer noch eine gute Bedingung sind, und er möchte keine Warnung anzeigen. Er kann den Standardwert von 10 auf 5 über die Spa-Konsole aktualisieren, ohne sich mit der Entwicklung eines Advisor-Pakets vertraut machen zu müssen.

Durch die Einführung eines Schwellenwerts können Systemadministratoren den Wert schnell ändern, ohne das Advisor-Paket ändern zu müssen.

Im Beispiel sind alle Attribute außer **Description** erforderlich. Sie können eine beliebige Zahl als **Wert**verwenden.

Ein Schwellenwert kann über die Regeln hinweg gemeinsam genutzt werden.

### <a name="alerts-and-recommendations"></a>Warnungen und Empfehlungen

Die Regel Definition umfasst keine Logik Berechnungen. Es definiert, wie die Benutzeroberfläche aussehen könnte und wie das SQL Server Berichts Skript die Ergebnisse an die Benutzeroberfläche übermittelt.

Eine Regel besteht aus drei Teilen:

* Warnung (Regel Beschriftung)

* Empfehlung (Ratschläge)

* Zugeordneter Schwellenwert (optionale Informationen zu Abhängigkeiten)

Im folgenden finden Sie ein Beispiel für eine Regel:

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

Sie können beliebig viele Ratschläge definieren, und Sie sollten in der Regel Empfehlungen definieren. Der **Grad** der Empfehlung kann " **Erfolg** " oder " **Warnung**" lauten.

Sie können mit beliebig vielen Schwellenwerten verknüpfen. Sie können sogar eine Verknüpfung mit einem Schwellenwert herstellen, der für die aktuelle Regel irrelevant ist. Durch die Verknüpfung können Sie die Schwellenwerte problemlos verwalten.

Der Regelname und die Empfehlungen sind Schlüssel, die in Ihrem Bereich eindeutig sind. Es können nicht zwei Regeln denselben Namen aufweisen, und es können nicht zwei Empfehlungen innerhalb einer Regel denselben Namen haben. Diese Namen sind sehr wichtig, wenn Sie einen SQL-Skript Bericht schreiben. Sie können den \[dbo-\]abrufen.\[setnotification\] API, um den Regel Status festzulegen.

### <a name="defining-ui-display-elements"></a>Definieren von Benutzeroberflächen-Anzeigeelementen

Nachdem die Regeln definiert wurden, können Systemadministratoren die Berichts Zusammenfassung anzeigen. Allerdings sind Systemadministratoren oft an den aggregierten Daten interessiert und möchten die Datenquellen überprüfen, die in den Leistungs Regeln verwendet wurden.

Wenn Sie mit dem vorherigen Beispiel fortfahren, weiß der Benutzer, ob genügend freier Speicherplatz auf dem Systemlaufwerk vorhanden ist. Benutzer sind möglicherweise auch an der tatsächlichen Größe des freien Speicherplatzes interessiert. Eine einzelne Wert Gruppe wird zum Speichern und anzeigen derartiger Ergebnisse verwendet. Mehrere einzelne Werte können gruppiert und in einer Tabelle in der Spa-Konsole angezeigt werden. Die Tabelle hat nur zwei Spalten, Name und Wert, wie hier gezeigt.

Name | Value
---- | ----
Freie Datenträger Größe auf System Laufwerk (GB) | 100
Gesamte installierte Datenträger Größe (GB) | 500 

Wenn ein Benutzer eine Liste aller Festplatten sehen möchte, die auf dem Server und dessen Datenträger Größe installiert sind, können wir einen Listen Wert, der drei Spalten und mehrere Zeilen enthält, wie hier gezeigt, abrufen.

Festplatte | Größe des freien Datenträgers (GB) | Gesamtgröße (GB)
---- | ---- | ----
0 | 100 | 500
1 | 20 | 320

In einem Advisor-Pack können viele Tabellen vorhanden sein (Einzelwert Gruppen und Listen Wert Tabellen). Wir können einen Abschnitt verwenden, um diese Tabellen zu organisieren und zu kategorisieren.

Zusammenfassend gibt es drei Typen von Benutzeroberflächen Elementen:

* [Abschnitte](#bkmk-ui-section)

* [Einzelwert Gruppen](#bkmk-ui-svg)

* [Auflisten von Wert Tabellen](#bkmk-ui-lvt)

Hier sehen Sie ein Beispiel, das die Elemente der Benutzeroberfläche anzeigt:

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

### <a href="" id="bkmk-ui-section"></a>Strecken

Ein Abschnitt ist ausschließlich für das Layout der Benutzeroberfläche vorgesehen. Er ist nicht an logischen Berechnungen beteiligt. Jeder einzelne Bericht enthält eine Reihe von Abschnitten der obersten Ebene, für die kein übergeordneter Abschnitt vorhanden ist. Die Abschnitte der obersten Ebene werden als Registerkarten im Bericht angezeigt. Abschnitte können Unterabschnitte mit maximal 10 Ebenen aufweisen. Alle Unterabschnitte in den Abschnitten der obersten Ebene werden in erweiterbaren Bereichen angezeigt. Ein Abschnitt kann mehrere Unterabschnitte, Einzelwert Gruppen und Listen Wert Tabellen enthalten. Einzelwert Gruppen und Listen Wert Tabellen werden als Tabellen dargestellt.

Im folgenden finden Sie ein Beispiel für den Abschnitt der obersten Ebene.

``` syntax
<section name="CPU" caption="CPU"/>
```

Ein Abschnitts Name muss eindeutig sein. Sie wird als Schlüssel verwendet, der mit anderen Abschnitten, Einzelwert Gruppen und Listen Wert Tabellen verknüpft werden kann.

Das folgende Beispiel verfügt über ein über **geordnetes**Attribut, das auf den Abschnitt CPU zeigt. Cpufacts ist ein untergeordnetes Element des Abschnitts mit dem Namen CPU. das über **geordnete** Element muss auf einen vorherigen Abschnittsnamen verweisen. Andernfalls kann dies zu einer-Schleife führen.

``` syntax
<section name="CPUFacts" caption="Facts" parent="CPU"/>
```

Die folgende Einzelwert Gruppe verfügt über ein-Attribut **, und**es kann auf einen beliebigen Abschnitt verweisen, der auf dem Benutzeroberflächen Entwurf basiert.

``` syntax
<singleValue name="CPUInformation" section="CPUFacts" caption="Physical CPU Information"> </singleValue>
```

### <a name="data-types"></a>Datentypen

Eine Einzelwert Gruppe und eine Listen Wert Tabelle enthalten unterschiedliche Datentypen, z. b. String, int und float. Da diese Werte in der SQL Server-Datenbank gespeichert werden, können Sie einen SQL-Datentyp für jede Dateneigenschaft definieren. Die Definition eines SQL-Datentyps ist jedoch recht kompliziert. Sie müssen die Länge oder Genauigkeit angeben, die möglicherweise geändert werden kann.

Zum Definieren logischer Datentypen können Sie das erste untergeordnete Element von **&lt;ReportDefinition/&gt;** verwenden. hier können Sie eine Zuordnung des SQL-Datentyps und des logischen Typs definieren.

Im folgenden Beispiel werden zwei Datentypen definiert. Eine ist eine **Zeichenfolge** , und die andere ist " **companycode**".

``` syntax
<datatype name="string" = sqltype="nvarchar(4000)" />
<datatype name="companyCode" sqltype="nvarchar(100)" />
```

Ein Datentyp Name kann eine beliebige gültige Zeichenfolge sein. Im folgenden finden Sie eine Liste der zulässigen SQL-Datentypen:

* BIGINT

* binär

* bit

* char

* date

* datetime

* datetime2

* datetimeoffset

* Dezimalzahl

* float

* int

* Verdienst

* nchar

* numeric

* nvarchar

* Reelle

* smalldatetime

* smallint

* SMALLMONEY

* Zeit

* tinyint

* uniqueidentifier

* varbinary

* varchar

Weitere Informationen zu diesen SQL-Datentypen finden Sie unter [Datentypen (Transact-SQL)](https://msdn.microsoft.com/library/ms187752.aspx).

### <a href="" id="bkmk-ui-svg"></a>Einzelwert Gruppen

In einer Einzelwert Gruppe werden mehrere einzelne Werte in einer Tabelle gruppiert, wie hier gezeigt.

``` syntax
<singleValue name="Systemoverview" section="SystemoverviewSection" caption="Facts">
<value name="OsName" type="string" caption="Operating system" description="WMI: Win32_OperatingSystem/Caption"/>
<value name="Osversion" type="string" caption="OS version" description="WMI: Win32_OperatingSystem/version"/>
<value name="OsLocation" type="string" caption="OS location" description="WMI: Win32_OperatingSystem/SystemDrive"/>
</singleValue>
```

Im vorherigen Beispiel haben wir eine Einzelwert Gruppe definiert. Es handelt sich um einen untergeordneten Knoten des Abschnitts **systemoverviewsection**. Diese Gruppe verfügt über einzelne Werte, d... **osname**, **OSVersion**und **osloation**.

Ein einzelner Wert muss über ein globales Attribut für einen eindeutigen Namen verfügen. In diesem Beispiel ist das Attribut Global Unique Name **systemoverview**. Der eindeutige Name wird verwendet, um eine entsprechende Ansicht für den benutzerdefinierten Bericht zu generieren. Jede Ansicht enthält das Präfix **VW**, z. b. vwsystemoverview.

Obwohl Sie mehrere Einzelwert Gruppen definieren können, dürfen keine zwei einzelnen Werte Namen identisch sein, auch wenn Sie sich in unterschiedlichen Gruppen befinden. Der Einzelwert Name wird vom SQL-Skript Bericht verwendet, um den Wert entsprechend festzulegen.

Sie können einen Datentyp für jeden einzelnen Wert definieren. Die zulässige Eingabe für **Type** ist in **&lt;DataType/&gt;** definiert. Der endgültige Bericht könnte wie folgt aussehen:

**Fakten**

Name | Value
--- | ---
Betriebssystem | &lt;_ein Wert vom Berichts Skript festgelegt wird_&gt;
BS-Version | &lt;_ein Wert vom Berichts Skript festgelegt wird_&gt;
Betriebssystem Standort | &lt;_ein Wert vom Berichts Skript festgelegt wird_&gt;

Das **Caption** -Attribut **&lt;Werts/&gt;** wird in der ersten Spalte angezeigt. Werte in der Spalte Wert werden in der Zukunft vom Skript Bericht über \[dbo-\]festgelegt.\[setsinglevalue-\]. Das **Description** -Attribut von **&lt;Wert/&gt;** wird in einer QuickInfo angezeigt. Normalerweise zeigt die QuickInfo den Benutzern die Quelle der Daten an. Weitere Informationen zu Quick [Infos finden Sie](#bkmk-tooltips)unter Quick Infos.

### <a href="" id="bkmk-ui-lvt"></a>Auflisten von Wert Tabellen

Die Definition eines Listen Werts entspricht dem Definieren einer Tabelle.

``` syntax
<listValue name="NetworkAdapterInformation" section="NetworkIOFacts" caption="Physical network adapter information">
<column name="NetworkAdapterId" type="string" caption="ID" description="WMI: Win32_NetworkAdapter/DeviceID"/>
<column name="NetworkAdapterName" type="string" caption="Name" description="WMI: Win32_NetworkAdapter/Name"/>
<column name="type" type="string" caption="type" description="WMI: Win32_NetworkAdapter/Adaptertype"/>
<column name="Speed" type="decimal" caption="Speed (Mbps)" description="WMI: Win32_NetworkAdapter/Speed"/>
<column name="MACaddress" type="string" caption="MAC address" description="WMI: Win32_NetworkAdapter/MACaddress"/>
</listValue>
```

Der Name des Listen Werts muss global eindeutig sein. Dieser Name wird zum Namen einer temporären Tabelle. Im vorherigen Beispiel wird die Tabelle mit dem Namen \#networkadapterinformation in der Initialisierungsphase der Ausführungsumgebung erstellt, in der alle beschriebenen Spalten enthalten sind. Ähnlich wie bei einem einzelnen Wertnamen wird auch ein Listen Wert Name als Teil des benutzerdefinierten Ansichts namens verwendet, z.b. vwnetworkadapterinformation.

@type von &lt;Column/&gt; wird durch &lt;DataType/&gt; definiert.

Die Mock-Benutzeroberfläche des letzten Berichts könnte wie folgt aussehen:

**Informationen zum physischen Netzwerkadapter**

ID | Name | Geben Sie in das Suchfeld auf der Taskleiste | Geschwindigkeit (Mbit/s) | MAC-Adresse
--- | --- | --- | --- | ---
 | <br> | | |
 | | | |


Das **Caption** -Attribut &lt;Spalte/&gt; wird als Spaltenname angezeigt, und das **Beschreibungs** Attribut &lt;Spalte/&gt; wird als QuickInfo für den entsprechenden Spaltenheader angezeigt. In der Regel wird der Benutzer von der QuickInfo die Quelle der Daten angezeigt. Weitere [Informationen finden Sie](#bkmk-tooltips)unter Quick Infos.

In einigen Fällen kann eine Tabelle viele Spalten und nur wenige Zeilen enthalten, sodass das Austauschen der Spalten und Zeilen die Tabelle erheblich besser aussehen würde. Zum Austauschen der Spalten und Zeilen können Sie das folgende Formatvorlagen Attribut hinzufügen:

``` syntax
<listValue style="Transpose"  
```

### <a name="defining-charting-elements"></a>Definieren von Diagrammelementen

Sie können einen beliebigen Statistik Schlüssel auswählen und die Werte in einem Verlaufs Diagramm oder einem Trend Diagramm anzeigen. Es gibt zwei Arten von Statistiken:

* **Statische Statistik** Ein einzelner Wert, der zur Entwurfszeit bekannt ist. Der freie Speicherplatz auf einem Systemlaufwerk wäre z. b. eine statische Statistik.

* **Dynamische Statistik** Möglicherweise ist zur Entwurfszeit unbekannt. Beispielsweise ist die durchschnittliche CPU-Auslastung der einzelnen Kerne eine dynamische Statistik, da Sie nicht wissen, wie viele CPU-Kerne zur Entwurfszeit im System stehen können.

Der Statistik Schlüssel weist eine Einschränkung auf, dass die Daten mit dem Double-Datentyp kompatibel sein müssen. Dabei kann es sich um eine ganze Zahl, einen Dezimalwert oder eine Zeichenfolge handeln, die in Double konvertiert werden kann.

Spa verwendet eine Einzelwert Gruppe zur Unterstützung statischer Statistiken und eine Listen Wert Tabelle, um dynamische Statistiken zu unterstützen. In den folgenden Abschnitten wird beschrieben, wie statische Statistik-und dynamische Statistik Schlüssel definiert werden.

### <a name="static-statistics"></a>Statische Statistik

Wie bereits erwähnt, ist eine statische Statistik ein einzelner Wert. Logisch können alle einzelnen Werte als statische Statistik definiert werden. Es ist jedoch bedeutungslos, einen einzelnen Wert anzuzeigen, der nicht in einen Nummertyp umgewandelt werden kann. Wenn Sie eine statische Statistik definieren möchten, können Sie **das Attribut einfach** dem entsprechenden Einzelwert Schlüssel hinzufügen, wie unten gezeigt:

``` syntax
<value name="freediskSize" type="int" trendable="true"  
```

### <a name="dynamic-statistics"></a>Dynamische Statistik

Dynamische Statistik Schlüssel sind zur Entwurfszeit nicht bekannt, sodass die Anzahl möglicher Werte unbekannt ist. Da Listen Werte jedoch in mehreren Zeilen gespeichert werden, wäre es einfach, eine Listen Wert Tabelle zum Speichern dynamischer Statistiken zu verwenden.

Wenn wir z. b. Diagramme für die durchschnittliche CPU-Auslastung unterschiedlicher Kerne anzeigen müssen, können wir eine Tabelle mit Spalten für **CPUID** und **averagecpuusage**definieren:

``` syntax
<listValue name="CpuPerformance">
<column name="CpuId" type="string" caption="CPU ID" columntype="Key"/>
<column name="AverageCpuUsage" type="decimal" caption="Average" columntype="Value"/>
</listValue>
```

Ein anderes Attribut, **ColumnType**, kann **Schlüssel**, **Wert**oder **Information**sein. Der Datentyp der **Schlüssel** Spalte muss "Double" oder "Double" konvertierbar sein. In einer **Schlüssel** Spalte können Sie dieselben Schlüssel nicht in eine Tabelle einfügen. **Werte** oder **Informations** Spalten weisen diese Einschränkung nicht auf.

Die Statistik Werte werden in **Wert** Spalten gespeichert.

**Informations** Spalten ähneln gewöhnlichen Spalten in normalen Listen Wert Tabellen. **Information** ist der Standard Spaltentyp, wenn Sie keinen angeben. Solche Spalten wirken sich nicht auf die Anzahl der Statistik Schlüssel aus oder nehmen an Statistik bezogenen Berechnungen Teil.

Wenn ein Server über zwei CPU-Kerne verfügt, könnte das Ergebnis in der Tabelle wie folgt aussehen:

CpuId | Averagecpuusage
:---: | :---:
0 | 10
1 | 30

Gleichzeitig werden zwei Statistik Schlüssel durch das Spa-Framework generiert. Eine ist für CPU 0 und die andere für CPU 1.

Das folgende Beispiel zeigt, dass mehrere **Wert** Spalten mit mehreren **Schlüssel** Spalten unterstützt werden.

CounterName | InstanceName | Mittelmäßig | Summe
--- | :---: | :---: | :---:
Prozessorzeit (%) | _Gesamt | 10 | 20
Prozessorzeit (%) | CPU0 | 20 | 30 

In diesem Beispiel verfügen Sie über zwei **Schlüssel** Spalten und zwei **Wert** Spalten. Spa generiert zwei Statistik Schlüssel für die Average-Spalte und weitere zwei Schlüssel für die Sum-Spalte. Die Statistik Schlüssel lauten:

* Counter Name (Prozessorzeit (%))/instanceName (\_gesamt)/Durchschnitt

* Counter Name (Prozessorzeit (%)/instanceName (cpu0)/Durchschnitt

* Counter Name (Prozessorzeit (%)/instanceName (\_gesamt)/Summe

* Counter Name (Prozessorzeit (%)/instanceName (cpu0)/Sum

Counter Name und instanceName werden als ein Schlüssel kombiniert. Der kombinierte Schlüssel darf keine Duplizierung aufweisen.

Die Spa generiert viele Statistik Schlüssel. Einige davon sind für Sie möglicherweise nicht interessant, und Sie möchten Sie möglicherweise über die Benutzeroberfläche ausblenden. Mithilfe von Spa können Entwickler einen Filter erstellen, um nur hilfreiche Statistik Schlüssel anzuzeigen.

im vorherigen Beispiel sind die Systemadministratoren möglicherweise nur an Schlüsseln interessiert, bei denen "instanceName" \_"Total" oder "CPU1" ist. Der Filter kann wie folgt definiert werden:

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

**&lt;trendablekeyvalues/&gt;** können unter jeder Schlüssel Spalte definiert werden. Wenn mehr als eine Schlüssel Spalte einen solchen Filter konfiguriert hat, wird Logik angewendet.

### <a name="developing-report-scripts"></a>Entwickeln von Berichts Skripts

Nachdem die Bereitstellungs Metadaten definiert sind, können Sie mit dem Schreiben des Berichts Skripts beginnen, bei dem es sich um eine gespeicherte T-SQL-Prozedur handelt.

Der Header "Bereitstellen von Metadaten" enthält die Attribute " **Name** " und " **reportscript** ", wie hier gezeigt:

``` syntax
<advisorPack name="Microsoft.ServerPerformanceAdvisor.CoreOS.V1" reportScript="ReportScript"  
```

Das Hauptberichts Skript wird durch Kombinieren der Attribute " **Name** " und " **reportscript** " benannt. Im folgenden Beispiel wird \[Microsoft. serverperformanceadvisor. coreos. v2\].\[reportscript-\].

``` syntax
create PROCEDURE [Microsoft.ServerPerformanceAdvisor.CoreOS.V2].[ReportScript] AS SET NOCOUNT ON

- Set alert and notification

- Prepare data for report view
```

Das **Name** -Attribut wird als Name des Datenbankschemas verwendet, z. b. als Namespace. Diese Regel gilt für alle anderen Datenbankobjekte, die zum aktuellen Advisor-Paket gehören, z. b. Listen Wert und gespeicherte Prozeduren.

Zu den Vorteilen dieses Schema namens vor den Datenbankobjekten gehören:

* Vermeiden von Namenskonflikten für verschiedene Advisor-Pakete

* Höhere Sicherheit

In der SQL Server-Datenbank lautet der Standardschema Name **dbo**. Datenbankbesitzer-Anmelde Informationen sind normalerweise erforderlich, um Datenbankobjekte unter **dbo**auszuführen. Wenn wir kein Schema für jedes Advisor-Paket erstellen, ist es wahrscheinlich, dass zwei Advisor-Pakete einen Listen Wert mit demselben Namen definieren. Dies sollte unerheblich sein, da Sie einen Schema Namen einführen können, um dieses Problem zu beheben. Außerdem ist das Aufheben der Bereitstellung eines Advisor-Pakets viel einfacher. Da das Advisor Pack-Objekt zu einem anderen Schema als **dbo**gehört, ermöglicht es Spa, eine niedrigere Benutzer Berechtigung für den Zugriff auf diese zu verwenden.

Ein normales Berichts Skript führt folgende Schritte aus:

* Greift auf aufgelistete Daten zu

* Führt Berechnungen auf Grundlage der Rohdaten aus.

* Änderungen an Warnungen und Empfehlungen

* Bereitet Daten für die Berichtsansicht vor

### <a name="access-raw-collected-data"></a>Auf Rohdaten der gesammelten Daten zugreifen

Alle gesammelten Daten werden in die folgenden entsprechenden Tabellen importiert. Weitere Informationen zum Tabellen Schema finden Sie unter [Definieren des Datensammler Satzes](#bkmk-definedatacollector).

* registry

    * RegistryKeys \#

* WMI

    * wmiobjects-\#

    * wmiobjectproperties-\#

    * \#wmiqueries

* Leistungsindikator

    * \#Performance Counters

* File

    * \#Dateien

* ETW

    * Ereignisse \#

    * \#eventproperties

### <a name="set-rule-status"></a>Festlegen des Regel Status

Der \[dbo-\].\[setnotification\] API den Regel Status festlegt, wird auf der Benutzeroberfläche ein Symbol für **Erfolg** oder **Warnung** angezeigt.

* @ruleName nvarchar (50)

* @adviceName nvarchar (50)

Die Warn-und Empfehlungs Nachrichten werden in der XML-Datei mit den Bereitstellungs Metadaten gespeichert. Dadurch wird das Berichts Skript einfacher zu verwalten.

Anfänglich ist jeder Regel Status N/v. Sie können diese API verwenden, um einen Regel Status festzulegen, indem Sie einen Namen für die Empfehlung angeben. Der Name der Empfehlung wird als Regel Status verwendet.

Denken Sie daran, dass wir die folgende Regel bereits definiert haben:

``` syntax
<rule name="freediskSize" caption="Free Disk Size on System Drive" description="This rule checks free disk size on the system drive ">
<advice name="SuccessAdvice" level="Success" message="No issue found.">No recommendation.</advice>
<advice name="WarningAdvice" level="Warning" message="Not enough free space on system drive.">Install the operating system on a larger disk.</advice>
</rule>
```

Wenn der freie Speicherplatz weniger als 2 GB beträgt, muss die Regel auf die **Warnstufe** festgelegt werden. Das SQL-Skript sieht wie folgt aus:

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

### <a name="get-threshold-value"></a>Schwellenwert erhalten

Der \[dbo-\].\[getthreshold\] API die Schwellenwerte abrufen:

* @key nvarchar (50)

* @value float-Ausgabe

> [!NOTE]
> Die Schwellenwerte sind Name-Wert-Paare, auf die in beliebigen Regeln verwiesen werden kann. Die Systemadministratoren können die-Konsole verwenden, um die Schwellenwerte zu ändern.

 Wenn Sie mit dem vorherigen Beispiel fortfahren, lautet die Definition für einen Schwellenwert wie folgt:

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

Das Berichts Skript kann wie hier gezeigt geändert werden:

``` syntax
DECLARE @freediskSize FLOat
exec dbo.GetThreshold N freediskSize , @freediskSize output

if (@freediskSizeInGB < @freediskSize)

```

### <a name="set-or-remove-the-single-value"></a>Festlegen oder Entfernen eines einzelnen Werts

Der \[dbo-\].\[setsinglevalue\]-API legt den einzelnen Wert fest:

* @key nvarchar (50)

* @value SQL-\_Variant

Dieser Wert kann mehrmals für den gleichen Einzelwert Schlüssel ausgeführt werden. Der letzte Wert wird gespeichert.

Das folgende Beispiel zeigt einige definierte Einzelwerte:

``` syntax
<singleValue section="Systemoverview" caption="Facts">
<value name="OsName" type="string" caption="Operating System" description="WMI: Win32_OperatingSystem/Caption"/>
<value name="Osversion" type="string" caption="OS version" description="WMI: Win32_OperatingSystem/version"/>
<value name="OsLocation" type="string" caption="OS Location" description="WMI: Win32_OperatingSystem/SystemDrive"/>
</singleValue>
```

Anschließend können Sie den einzelnen Wert festlegen, wie hier gezeigt:

``` syntax
exec dbo.SetSingleValue N OsName ,  Windows 7 
exec dbo.SetSingleValue N Osversion ,  6.1.7601 
exec dbo.SetSingleValue N OsLocation ,  c:\ 
```

In seltenen Fällen möchten Sie möglicherweise das zuvor festgelegte Ergebnis mithilfe der \[dbo-\]entfernen.\[removesinglevalue\] API.

* @key nvarchar (50)

Sie können das folgende Skript verwenden, um den zuvor festgelegten Wert zu entfernen.

``` syntax
exec dbo.removeSingleValue N Osversion 
```

### <a name="get-data-collection-information"></a>Sammeln von Informationen zur Datensammlung

Der \[dbo-\].\[getduration\]-API ruft die vom Benutzer festgelegte Dauer in Sekunden für die Datensammlung ab:

* @duration int-Ausgabe

Hier ist ein Beispiel für ein Berichts Skript:

``` syntax
DECLARE @duration int
exec dbo.GetDuration @duration output
```

Der \[dbo-\].\[getinternal\]-API ruft das Intervall eines Leistungs Zählers ab. Der Wert kann NULL zurückgeben, wenn der aktuelle Bericht keine Leistungsdaten des Leistungs Zählers enthält.

* @interval int-Ausgabe

Hier ist ein Beispiel für ein Berichts Skript:

``` syntax
DECLARE @interval int
exec dbo.GetInterval @interval output
```

### <a name="set-a-list-value-table"></a>Festlegen einer Listen Wert Tabelle

Es ist keine API zum Aktualisieren von Listen Wert Tabellen vorhanden. Sie können jedoch direkt auf die Listen Wert Tabellen zugreifen. in der Initialisierungsphase wird eine entsprechende temporäre Tabelle für jeden Listen Wert erstellt.

Das folgende Beispiel zeigt eine Listen Wert Tabelle:

``` syntax
<listValue name="NetworkAdapterInformation" section="NetworkIOFacts" caption="Physical Network Adapter Information">
<column name="NetworkAdapterId" type="string" caption="ID" description="WMI: Win32_NetworkAdapter/DeviceID"/>
<column name="NetworkAdapterName" type="string" caption="Name" description="WMI: Win32_NetworkAdapter/Name"/>
<column name="type" type="string" caption="type" description="WMI: Win32_NetworkAdapter/Adaptertype"/>
<column name="Speed" type="decimal" caption="Speed (Mbps)" description="WMI: Win32_NetworkAdapter/Speed"/>
<column name="MACaddress" type="string" caption="MAC address" description="WMI: Win32_NetworkAdapter/MACaddress"/>
</listValue>
```

Anschließend können Sie ein SQL-Skript schreiben, um die Ergebnisse einzufügen, zu aktualisieren oder zu löschen:

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

## <a name="development-and-debugging"></a>Entwicklung und Debuggen


### <a name="writing-logs"></a>Schreiben von Protokollen

Wenn weitere Informationen vorhanden sind, die Sie mit den Systemadministratoren kommunizieren möchten, können Sie Protokolle schreiben. Wenn ein Protokoll für einen bestimmten Bericht vorhanden ist, wird ein gelbes Banner in der Berichts Kopfzeile angezeigt. Im folgenden Beispiel wird gezeigt, wie Sie ein Protokoll schreiben können:

``` syntax
exec dbo.WriteSystemLog N'Any information you want to show to the system administrators , N Warning 
```

Der erste Parameter ist die Meldung, die im Protokoll angezeigt werden soll. Der zweite Parameter ist die Protokollebene. Die gültige Eingabe für den zweiten Parameter kann " **Information**", " **Warning**" oder " **Error**" lauten.

### <a name="debug"></a>Debugprotokolle

Die Spa-Konsole kann in zwei Modi ausgeführt werden: "Debug" oder "Release". Der Releasemodus ist die Standardeinstellung und bereinigt alle gesammelten Rohdaten, nachdem der Bericht generiert wurde. Im Debugmodus werden alle Rohdaten in der Dateifreigabe und in der Datenbank gespeichert, sodass Sie das Berichts Skript in Zukunft Debuggen können.

**So debuggen Sie ein Berichts Skript**

1.  Installieren Sie Microsoft SQL Server Management Studio (SSMS).

2.  Stellen Sie nach dem Starten von SSMS eine Verbindung mit localhost\\SQLExpress her. Beachten Sie, dass Sie localhost anstelle von verwenden müssen. . Andernfalls können Sie den Debugger möglicherweise nicht in SQL Server starten.

3.  Führen Sie folgendes Skript aus, um den Debugmodus zu aktivieren:

    ``` syntax
    USE SPADB
    UPdate dbo.Configurations
    SET Value = N'true'
    WHERE Name = N'Debugmode'
    ```

4.  Starten Sie die-Konsole, und führen Sie das Advisor-Paket aus, das Sie debuggen möchten.

5.  Warten Sie, bis die Aufgabe beendet wurde. Wenn der Bericht erfolgreich generiert wurde, wechseln Sie zurück zu SSMS, und suchen Sie nach der aktuellen Aufgabe.

    ``` syntax
    select TOP 1 * FROM dbo.Tasks OrdER BY Id DESC
    ```

    Beispielsweise könnte die Ausgabe wie folgt lauten:

    ID | SessionId | Advisorypackageid | ReportStatus-ID | Lastupdatetime | Stammoldversionid
    :---: | :---: | :---: | :---: | :---: | :---:
    12 | 17 | 1 | 2 | 2011-05-11 05:35:24.387 | 1

6.  Sie können das folgende Skript so oft ausführen, wie Sie das Berichts Skript für ID 12 ausführen möchten:

    ``` syntax
    exec dbo.DebugReportScript 12
    ```

    **Hinweis** Sie können auch F11 drücken, um die vorherige Anweisung zu durchlaufen und zu debuggen.



Ausführen \[dbo-\].\[debugreportscript\] gibt mehrere Resultsets zurück, einschließlich:

1.  Microsoft SQL Server Meldungen und Advisor Pack-Protokolle

2.  Ergebnisse von Regeln

3.  Statistik Schlüssel und-Werte

4.  Einzelne Werte

5.  Alle Listen Wert Tabellen

## <a name="best-practices"></a>Bewährte Verfahren

### <a name="naming-convention-and-styles"></a>Benennungs Konventionen und Stile

|                                                                 Pascal-Schreibweise                                                                 |                       Camel-Case-Schreibweise                        |             Großbuchstaben             |
|-----------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------|-----------------------------------|
| <ul><li>Namen in "provisionmetadata. xml"</li><li>Gespeicherte Prozeduren</li><li>Funktionen</li><li>Namen anzeigen</li><li>Temporäre Tabellennamen</li></ul> | <ul><li>Parameternamen</li><li>Lokale Variablen</li></ul> | Für alle reservierten SQL-Schlüsselwörter verwenden |

### <a name="other-recommendations"></a>Weitere Empfehlungen

* Verschieben Sie die meisten logischen Teile in andere gespeicherte Prozeduren und benutzerdefinierte Funktionen.

* Machen Sie Ihr Hauptskript zu Wartungszwecken so kurz wie möglich.

* Verwenden Sie den vollständigen Namen des SQL-Objekts.

* Behandeln Sie den SQL-Code als Groß-/Kleinschreibung

* Fügen Sie **SET NOCOUNT am** Anfang jeder gespeicherten Prozedur hinzu.

* Verwenden Sie temporäre Tabellen für die Übertragung großer Datenmengen.

* Verwenden Sie ggf. **Set XACT\_Abort on** , um den Prozess zu beenden, wenn ein Fehler auftritt.

* Schließen Sie die Hauptversionsnummer immer in den Anzeige Namen des Advisor-Pakets ein.

## <a href="" id="bkmk-advancedtopics"></a>Erweiterte Themen

### <a name="run-multiple-advisor-packs-simultaneously"></a>Gleichzeitiges Ausführen mehrerer Advisor-Pakete

Spa unterstützt gleichzeitig das Ausführen mehrerer Advisor Packs. Dies ist besonders nützlich, wenn Sie die Leistung von Internetinformationsdienste (IIS) und des Kern Betriebssystems gleichzeitig untersuchen möchten. Viele Datensammler, die vom IIS Advisor Pack verwendet werden, können auch vom Core OS Advisor Pack verwendet werden. Wenn zwei oder mehr Advisor-Pakete auf demselben Zielcomputer ausgeführt werden, sammelt Spa die gleichen Daten nicht zweimal.

Das folgende Beispiel zeigt den Workflow für das Ausführen von zwei Advisor-Paketen.

![Ausführen von mehreren Advisor-Paketen](../media/server-performance-advisor/spa-dev-guide-multi-advisor-packs.png)

Der Zusammenführungs Daten-sammlersatz dient nur zum Erfassen von Leistungsdaten Quellen und etw-Datenquellen. Die folgenden Zusammenschluss Regeln gelten:

1. Spa hat die größte Dauer wie die neue Dauer.

2. Bei Mergekonflikten werden folgende Regeln befolgt:

   1. Nehmen Sie das kleinste Intervall für das neue Intervall an.

   2. Nehmen Sie die Obermenge der Leistungsindikatoren an. Beispielsweise werden mit dem **Prozess (\*)\\% Prozessorzeit** und **Prozess (\*)\\\*\\Prozess (\*)\\\\** * mehr Daten zurückgegeben, sodass **Prozess (\*)\\Prozessorzeit (%)** und Prozess ( **\*)\\\\** * aus dem zusammengeführten Datensammler Satz entfernt wird.

### <a name="collect-dynamic-data"></a>Dynamische Daten erfassen

Spa benötigt zur Entwurfszeit einen definierten Datensammler Satz. Es ist nicht immer möglich zu wissen, welche Daten für die Bericht Generierung benötigt werden, da die dynamischen Daten und der Abfrage Pfad erst bekannt sind, wenn die abhängigen Daten verfügbar sind.

Wenn Sie z. b. alle anzeigen Amen von Netzwerkadaptern auflisten möchten, müssen Sie zuerst WMI Abfragen, um alle Netzwerkadapter aufzuzählen. Jedes zurückgegebene WMI-Objekt verfügt über einen Registrierungsschlüssel Pfad, in dem der Anzeige Name gespeichert wird. Der Registrierungsschlüssel Pfad ist zur Entwurfszeit nicht bekannt. In diesem Fall benötigen wir dynamische Daten Unterstützung.

Zum Auflisten aller Netzwerkadapter können Sie die folgende WMI-Abfrage mithilfe von Windows PowerShell verwenden:

``` syntax
Get-WmiObject -Namespace Root\Cimv2 -query "select PNPDeviceID FROM Win32_NetworkAdapter" | forEach-Object { Write-Output $_.PNPDeviceID }
```

Es wird eine Liste der Netzwerkadapter Objekte zurückgegeben. Jedes-Objekt verfügt über eine Eigenschaft mit dem Namen " **pnpdebug Eid**", die einen relativen Registrierungsschlüssel Pfad beibehält. Hier sehen Sie eine Beispielausgabe aus der vorherigen Abfrage:

``` syntax
ROOT\*ISatAP\0001
PCI\VEN_8086&DEV_4238&SUBSYS_11118086&REV_35\4&372A6B86&0&00E4
ROOT\*IPHTTPS\0000

```

Um den Wert **FriendlyName** zu ermitteln, öffnen Sie den Registrierungs-Editor, und navigieren Sie zu der Registrierungs Einstellung, indem Sie **HKEY\_lokalen\_Machine\\System\\CurrentControlSet\\Enum-\\** mit jeder Zeile im vorherigen Beispiel kombinieren. Beispiel: **HKEY\_local\_Machine\\System\\CurrentControlSet\\Enum\\ root\\\*IPHTTPS\\0000**.

Fügen Sie das Skript im folgenden Codebeispiel hinzu, um die vorherigen Schritte in die Spa-Bereitstellungs Metadaten zu übersetzen:

``` syntax
<advisorPack>
<dataSourceDefinition xmlns="https://microsoft.com/schemas/ServerPerformanceAdvisor/dc/2010">
 <dataCollectorSet >
<registryKeys>
 ?<registryKey>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Enum\$(NetworkAdapter.PNPDeviceID)\FriendlyName</registryKey>
</registryKeys>
<managementpaths>
 ?<path name="NetworkAdapter">Root\Cimv2:select PNPDeviceID FROM Win32_NetworkAdapter</path>
</managementpaths>
```

In diesem Beispiel fügen Sie zunächst eine WMI-Abfrage unter Management Path hinzu und definieren den Schlüsselnamen **NetworkAdapter**. Fügen Sie dann einen Registrierungsschlüssel hinzu, und verweisen Sie mithilfe der Syntax **$ (NetworkAdapter. pnpdeviceid)** auf **Network Adapter** .

In der folgenden Tabelle wird definiert, ob ein Datensammler in Spa dynamische Daten unterstützt und ob von anderen Datensammlern darauf verwiesen werden kann:

Datentyp | Dynamische Daten unterstützen | Kann referenziert werden
--- | :---: | :---:
Registrierungsschlüssel | „Ja“ | „Ja“
WMI | „Ja“ | „Ja“
File | „Ja“ | Nein
Leistungsindikator | Nein | Nein
ETW | Nein | Nein

Bei einem WMI-Datensammler verfügt jedes WMI-Objekt über viele angefügte Attribute. Jeder Typ von WMI-Objekt hat immer drei Attribute: \_\_Namespace, \_\_Klasse und \_\_RelPath.

Um einen Datensammler zu definieren, auf den von anderen Datensammlern verwiesen wird, weisen Sie das **Name** -Attribut mit einem eindeutigen Schlüssel in der Datei "provisionmetadata. xml" zu. Dieser Schlüssel wird von abhängigen Datensammlern verwendet, um dynamische Daten zu generieren.

Hier ist ein Beispiel für den Registrierungsschlüssel:

``` syntax
<registryKey  name="registry">HKEY_LOCAL_MACHINE </registryKey>
```

Und ein Beispiel für WMI:

``` syntax
<path name="wmi">Root\Cimv2:select PNPDeviceID FROM Win32_NetworkAdapter</path>
```

Zum Definieren eines abhängigen Daten Sammlers wird die folgende Syntax verwendet: $ ( *{Name}* ). *{Attribute}* ).

" *{Name}* " und " *{Attribute}* " sind Platzhalter.

Wenn das Spa Daten von einem Zielserver sammelt, ersetzt es dynamisch das Muster $ (\*.\*) durch die tatsächlich gesammelten Daten aus dem zugehörigen Verweis Datensammler (Registrierungsschlüssel/WMI), z. b.:

``` syntax
<registryKey>HKEY_LOCAL_MACHINE\$(registry.key)\ </registryKey>
<registryKey  name="registry">HKEY_LOCAL_MACHINE\$(wmi.Relativeregistrypath)\ </registryKey>
<path name="wmi"> </path>
<file>$(wmi.FileName)</file>
```

**Hinweis** Spa unterstützt eine unbegrenzte Tiefe der Referenz, aber beachten Sie den Leistungs Aufwand, wenn Sie zu viele Ebenen haben. Stellen Sie sicher, dass kein Zirkel Verweis oder selbst Verweis vorhanden ist, der nicht unterstützt wird.

### <a name="versioning-limitations"></a>Einschränkungen der Versionsverwaltung

Spa unterstützt Updates für zurücksetzen und neben Versionen. Diese Prozesse verwenden denselben Algorithmus. Der Prozess besteht darin, alle Datenbankobjekte und Schwellenwert Einstellungen zu aktualisieren, aber die vorhandenen Daten beizubehalten. Dies kann auf eine höhere Version aktualisiert oder auf eine niedrigere Version herabgestuft werden. Wählen Sie das Advisor-Paket aus, und klicken Sie dann im Dialogfeld **Advisor-Pakete konfigurieren** in Spa auf zurück **setzen** , um die Updates zurückzusetzen oder anzuwenden.

Diese Funktion ist hauptsächlich bei geringfügigen Updates. Die Anzeigeelemente der Benutzeroberfläche können nicht drastisch geändert werden. Wenn Sie bedeutende Änderungen vornehmen möchten, müssen Sie ein anderes Advisor-Pack erstellen. Sie sollten die Hauptversion in den Advisor Pack-Namen einschließen.

Die Einschränkungen von Änderungen an der geringfügigen Version bestehen darin, dass Sie keine der folgenden Aktionen ausführen **können** :

* Ändern des Schema namens

* Ändern des Datentyps einer einzelnen Wertegruppe oder der Spalten einer Listen Wert Tabelle

* Schwellenwerte hinzufügen oder entfernen

* Regeln hinzufügen oder entfernen

* Hinzufügen oder Entfernen von Empfehlungen

* Einzelne Werte hinzufügen oder entfernen

* Hinzufügen oder Entfernen von Listen Werten

* Hinzufügen oder Entfernen einer Spalte mit Listen Werten

### <a href="" id="bkmk-tooltips"></a>Quick Infos

Fast alle **Beschreibungs** Attribute werden in der Spa-Konsole als QuickInfo angezeigt.

für eine Listen Wert Tabelle kann eine zeilenbasierte QuickInfo durch Hinzufügen des folgenden Attributs erreicht werden:

``` syntax
<listValue descriptionColumn="Description">
<column name="Name"/>
<column name="Description"/>
</listValue>
```

Das **descriptioncolumn** -Attribut verweist auf den Namen der Spalte. In diesem Beispiel wird die Beschreibungs Spalte nicht als physische Spalte angezeigt. Es wird jedoch als QuickInfo angezeigt, wenn Sie mit der Maus auf die einzelnen Zeilen der ersten Spalte zeigen.

Es wird empfohlen, dass in der QuickInfo die Datenquelle für den Benutzer angezeigt wird. Im folgenden finden Sie die folgenden Formate für die Anzeige der Datenquellen:

Datenquelle | Format | Beispiel
--- | --- | ---
WMI | WMI: &lt;WMIClass-&gt;/&lt;Feld&gt; | WMI: Win32_OperatingSystem/Caption
Leistungsindikator | PerfCounter: &lt;CategoryName&gt;/&lt;instanceName&gt; | PerfCounter: Prozess\Prozessorzeit (%)
registry | Registrierung: &lt;Register Key&gt; | Registrierung: HKLM\Software\Microsoft<br>\\ASP.net\\Rootver
Konfigurationsdatei | Configfile: &lt;filePath&gt;\[; XPath: &lt;XPath-&gt;\]<br>**Hinweis**<br>XPath ist optional und nur gültig, wenn es sich bei der Datei um eine XML-Datei handelt. | Configfile: windir%\\System32\\inetsrv\config\\ApplicationHost. config<br>XPath: Configuration&frasl;System. Webserver<br>&frasl;httpProtocol&frasl;@allowKeepAlive
ETW | Etw: &lt;Provider/&gt;(Schlüsselwörter) | Etw: Windows-Kernel-Ablauf Verfolgung (Prozess, net)

### <a name="table-collation"></a>Tabellen Sortierung

Wenn ein Advisor-Paket komplizierter wird, können Sie eigene Variablen Tabellen oder temporäre Tabellen erstellen, um Zwischenergebnisse im Berichts Skript zu speichern.

Das Sortieren von Zeichen folgen Spalten kann problematisch sein, da die von Ihnen erstellte Tabellen Sortierung sich von der Tabelle unterscheiden kann, die durch das Spa-Framework erstellt wird. Wenn Sie zwei Zeichen folgen Spalten in verschiedenen Tabellen korrelieren, wird möglicherweise ein Sortierungs Fehler angezeigt. Um dieses Problem zu vermeiden, sollten Sie immer die Zeichenfolge für eine Spalten Sortierung als **SQL\_latin1\_allgemein\_CP1\_CI\_** definieren, als wenn Sie eine Tabelle definieren.

Hier finden Sie Informationen zum Definieren einer Variablen Tabelle:

``` syntax
DECLARE @filesIO TABLE (
 Name nvarchar(500) COLLatE SQL_Latin1_General_CP1_CI_AS,
 AverageFileAccessvolume float,
 AverageFileAccessCount float,
 Filepath nvarchar(500) COLLatE SQL_Latin1_General_CP1_CI_AS
)
```

### <a name="collect-etw"></a>Etw erfassen

Hier finden Sie Informationen zum Definieren von etw in einer Datei "provisionmetadata. xml":

``` syntax
<dataSourceDefinition>
  <providers>
    <provider session="NT Kernel Logger" guid="{9E814AAD-3204-11D2-9A82-006008A86939}"/>
  </providers>
</dataSourceDefinition>
```

Die folgenden Anbieter Attribute sind für die Erfassung von etw verfügbar:

Attribut | Geben Sie in das Suchfeld auf der Taskleiste | Beschreibung
--- | --- | ---
guid | GUID | Anbieter-GUID
Sitzung | String | Etw-Sitzungsname (optional, nur für Kernel Ereignisse erforderlich)
keywordsany | Hexadezimal | Beliebige Schlüsselwörter (optional, kein 0x-Präfix)
keywordsall | Hexadezimal | Alle Schlüsselwörter (optional)
Eigenschaften | Hexadezimal | Eigenschaften (optional)
level | Hexadezimal | Ebene (optional)
bufferSize | Ganze Zahl | Puffergröße (optional)
flushtime | Ganze Zahl | Leerungs Zeit (optional)
maxBuffer | Ganze Zahl | Maximaler Puffer (optional)
minbuffer | Ganze Zahl | Minimaler Puffer (optional)

Es gibt zwei Ausgabe Tabellen, wie hier gezeigt.

**Tabellen Schema für \#Ereignisse**

Name der Spalte | SQL-Datentyp | Beschreibung
--- | --- | ---
SequenceID | Int not NULL | Korrelations Sequenz-ID
Eventtypeid | Int not NULL | Ereignistyp-ID (siehe [dbo]. [ EventTypes])
ProcessId | Bigint not NULL | Prozess-ID
ThreadID | Bigint not NULL | Thread-ID
timestamp | datetime2 nicht NULL | timestamp
Kernelzeit | Bigint not NULL | Kernel Zeit
Usertime | Bigint not NULL | Benutzer Zeit

**\#eventproperties-Tabellen Schema**

Name der Spalte | SQL-Datentyp | Beschreibung
--- | --- | ---
SequenceID | Int not NULL | Korrelations Sequenz-ID
Name | Nvarchar (100) | Eigenschaftenname
Value | Nvarchar(4000) | Value

### <a name="etw-schema"></a>Etw-Schema

Ein etw-Schema kann durch Ausführen von "tracerpt. exe" für die ETL-Datei generiert werden. Eine "Schema. man"-Datei wird generiert. Da das Format der ETL-Datei Computer abhängig ist, funktioniert das folgende Skript nur in den folgenden Situationen:

1.  Führen Sie das Skript auf dem Computer aus, auf dem die entsprechende ETL-Datei gesammelt wird.

2.  Oder führen Sie das Skript auf einem Computer aus, auf dem dasselbe Betriebssystem und dieselben Komponenten installiert sind.

``` syntax
tracerpt *.etl -export
```

## <a name="glossary"></a>Glossar


In diesem Dokument werden die folgenden Begriffe verwendet:

**Advisor-Pack**

Ein Advisor-Paket ist eine Sammlung von Metadaten und SQL-Skripts, die die Leistungs Protokolle verarbeiten, die vom Zielserver gesammelt werden. Das Advisor-Pack generiert dann Berichte aus den Leistungs Protokolldaten. Die Metadaten im Advisor-Pack definieren die Daten, die vom Zielserver für Leistungsmessungen gesammelt werden sollen. Die Metadaten definieren auch den Satz von Regeln, die Schwellenwerte und das Berichtsformat. In den meisten Fällen wird ein Advisor-Pack speziell für eine einzelne Server Rolle geschrieben, z. b. Internetinformationsdienste (IIS).

**Spa-Konsole**

Die Spa-Konsole bezieht sich auf spaconsole. exe, das der zentrale Bestandteil von Server Performance Advisor ist. Die Spa muss nicht auf dem Zielserver ausgeführt werden, den Sie testen. Die Spa-Konsole enthält alle Benutzeroberflächen für Spa, von der Einrichtung des Projekts bis hin zur Ausführung von Analysen und Anzeigen von Berichten. Das Spa ist eine Anwendung mit zwei Ebenen. Die Spa-Konsole enthält die UI-Schicht und einen Teil der Geschäftslogik Ebene. Die Spa-Konsole plant und verarbeitet Leistungsanalyse Anforderungen.

**Spa-Framework**

Spa enthält zwei Hauptkomponenten: das Framework und die Advisor-Pakete. Das Spa-Framework bietet alle Benutzeroberflächen, die Verarbeitung von Leistungs Protokollen, die Konfiguration, die Fehlerbehandlung und Datenbank-APIs sowie Verwaltungs Prozeduren.

**Spa-Projekt**

Ein Spa-Projekt ist eine Datenbank, die alle Informationen zu den Ziel Servern, Advisor Packs und Leistungsanalyse Berichten enthält, die auf den Ziel Servern für die Advisor-Pakete generiert werden. Sie können Verlaufs-und Trenddiagramme innerhalb desselben Spa-Projekts vergleichen und anzeigen. Der Benutzer kann mehr als ein Projekt erstellen. Die Spa-Projekte sind voneinander unabhängig, und es gibt keine Daten, die von allen Projekten gemeinsam genutzt werden.

**Zielserver**

Der Zielserver ist der physische oder virtuelle Computer, auf dem der Windows-Server mit bestimmten Server Rollen (z. b. IIS) ausgeführt wird.

**Datenanalyse Sitzung**

Eine Datenanalyse Sitzung ist eine Leistungsanalyse auf einem bestimmten Zielserver. Eine Datenanalyse Sitzung kann mehrere Advisor-Pakete enthalten. Die Datensammler Sätze aus diesen Advisor-Paketen werden zu einem einzelnen Datensammler Satz zusammengeführt. Alle Leistungs Protokolle für eine einzelne Datenanalyse Sitzung werden innerhalb desselben Zeitraums gesammelt. Das Analysieren von Berichten, die von Advisor-Paketen generiert werden, die in derselben Datenanalyse Sitzung ausgeführt werden, kann Benutzern helfen, die Gesamtleistung zu verstehen und die Ursachen für Leistungsprobleme zu identifizieren.

**Ereignisablaufverfolgung für Windows**

Die Ereignis Ablauf Verfolgung für Windows ( [Event Tracing](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) for Windows, etw) ist ein hochleistungsfähiges, skalierbares Ablauf Verfolgungssystem, das in den Windows-Betriebssystemen bereitgestellt wird. Es bietet Profil Erstellungs-und Debuggingfunktionen, die zur Problembehandlung für eine Vielzahl von Szenarien verwendet werden können. Spa verwendet ETW-Ereignisse als Datenquelle zum Erstellen von Leistungs Berichten. Allgemeine Informationen zu etw finden Sie unter verbessertes [Debugging und Leistungsoptimierung mit etw](https://msdn.microsoft.com/magazine/cc163437.aspx).

**WMI-Abfrage**

Windows-Verwaltungsinstrumentation (WMI) ist die Infrastruktur für Verwaltungsdaten und Vorgänge in Windows-Betriebssystemen. Sie können WMI-Skripts oder-Anwendungen schreiben, um administrative Aufgaben auf Remote Computern zu automatisieren. WMI stellt auch Verwaltungsdaten für andere Teile des Betriebssystems und für Produkte bereit. Spa verwendet WMI-Klassen Informationen und Datenpunkte als Quellen zum Erstellen von Leistungs Berichten.

**Leistungsindikatoren**

Leistungsindikatoren werden verwendet, um Informationen darüber bereitzustellen, wie gut die Leistung des Betriebssystems oder einer Anwendung, eines Diensts oder Treibers ist. Die Leistungsdaten können Ihnen helfen, Engpässe im System zu ermitteln und die System-und Anwendungsleistung zu optimieren. Das Betriebssystem, das Netzwerk und die Geräte bieten Leistungsdaten, die von einer Anwendung genutzt werden können, um Benutzern eine grafische Ansicht der Leistung des Systems zu bieten. Die Spa verwendet Leistungsdaten und Datenpunkte als Quellen zum Generieren von Leistungs Berichten.

**Leistungsprotokolle und -warnungen**

Leistungsprotokolle und-Warnungen (PLA) ist ein integrierter Dienst im Windows-Betriebssystem. Es ist für die Erfassung von Leistungs Protokollen und Ablauf Verfolgungen konzipiert und löst auch Leistungs Warnungen aus, wenn bestimmte Trigger erfüllt sind. Mithilfe von Pla können Leistungsindikatoren, Ereignis Ablauf Verfolgung für Windows (ETW), WMI-Abfragen, Registrierungsschlüssel und Konfigurationsdateien erfasst werden. Außerdem unterstützt die Verwendung von Remote Prozedur aufrufen (RPC) die Remote Datensammlung. Der Benutzer definiert einen Datensammler Satz, der Informationen über die zu sammelnden Daten, die Häufigkeit der Datensammlung, die Dauer der Datenerfassung, Filter und einen Speicherort zum Speichern der Ergebnisdateien enthält. Spa sammelt mithilfe von PLA alle Leistungsdaten von den Ziel Servern.

**Einzelner Bericht**

Ein einzelner Bericht ist der Spa-Bericht, der auf der Grundlage einer Datenanalyse Sitzung für ein Advisor Pack auf einem einzelnen Zielserver generiert wird. Es kann Benachrichtigungen und verschiedene Datenabschnitte enthalten.

**Paralleler Bericht**

Ein paralleler Bericht ist ein Spa-Bericht, in dem zwei einzelne Berichte für dasselbe Advisor Pack verglichen werden. Die beiden Berichte können von verschiedenen Ziel Servern oder von separaten Leistungsanalysen auf demselben Zielserver generiert werden. Der parallele Bericht erstellt die Funktion zum Vergleichen von zwei Berichten, damit Benutzer ungewöhnliche Verhalten oder Einstellungen in einem der Berichte identifizieren können. Ein paralleler Bericht enthält Benachrichtigungen und verschiedene Datenabschnitte. In jedem Abschnitt werden die Daten aus beiden Berichten nebeneinander aufgelistet.

**Trend Diagramm**

Ein Trend Diagramm ist der Spa-Bericht, der verwendet wird, um sich wiederholende Muster von Leistungsproblemen zu untersuchen. Viele sich wiederholende Leistungsprobleme werden durch geplante Server Lade Änderungen vom Server oder von Client Computern verursacht, die täglich oder wöchentlich auftreten können. Spa bietet ein 24-Stunden-Trend Diagramm und ein 7-Tage-Trend Diagramm, um diese Probleme zu identifizieren.

Der Benutzer kann eine oder mehrere Datenreihen gleichzeitig auswählen, wobei es sich um einen numerischen Wert innerhalb des einzelnen Berichts handelt, z. b. die **durchschnittliche CPU-Gesamtauslastung**. genauer gesagt handelt es sich bei einem numerischen Wert um einen skalaren Wert von einem einzelnen Server, der von einem einzelnen AP-Wert zu einer bestimmten Zeit Instanz generiert wird. Spa gruppiert diese Werte in 24 Gruppen, eine für jede Stunde des Tages (sieben für einen 7-tägigen Bericht, eine für jeden Tag der Woche). Spa berechnet durchschnittliche, minimale, maximale und standardmäßige Abweichungen für jede Gruppe.

**Verlaufs Diagramm**

Ein Verlaufs Diagramm ist der Spa-Bericht, der verwendet wird, um Änderungen an bestimmten numerischen Werten in einzelnen Berichten für ein bestimmtes Server-und Advisor Pack-Paar im Zeitverlauf anzuzeigen. Der Benutzer kann mehrere Datenreihen auswählen und diese zusammen im Verlaufs Diagramm anzeigen, um die Korrelation zwischen verschiedenen Datenreihen nachzuvollziehen.

**Datenreihe**

Bei einer Datenreihe handelt es sich um numerische Daten, die über einen bestimmten Zeitraum aus derselben Datenquelle gesammelt werden. Dieselbe Quelle bedeutet, dass die Daten vom gleichen Zielserver stammen müssen, z. b. die durchschnittliche Länge der Anforderungs Warteschlange für IIS auf einem Server.

**Regeln**

Regeln sind Kombinationen aus Logik, Schwellenwerten und Beschreibungen. Sie stellen ein mögliches Leistungsproblem dar. Jedes Advisor-Paket enthält mehrere Regeln. Jede Regel wird durch einen Bericht Generierungsprozess ausgelöst. Eine Regel wendet die Logik und die Schwellenwerte auf die Daten in einem einzelnen Bericht an. Wenn die Kriterien erfüllt sind, wird eine Warnmeldung ausgelöst. Wenn dies nicht der Wert ist, wird die Benachrichtigung auf den Status **OK** festgelegt. Wenn die Regel nicht angewendet wird, wird die Benachrichtigung auf den Status nicht zutreffend (**na**) festgelegt.

**Benachrichtigungen**

Eine Benachrichtigung sind die Informationen, die von einer Regel für Benutzer angezeigt werden. Sie enthält den Status der Regel ("**OK**", " **na**" oder " **Warnung**"), den Namen der Regel und mögliche Empfehlungen, um die Leistungsprobleme zu beheben.
