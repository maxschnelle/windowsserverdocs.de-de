---
title: Server Performance Advisor-Benutzerhandbuch
description: Server Performance Advisor-Benutzerhandbuch
ms.assetid: be99a5a9-b9c0-436b-912c-e5c5839a533d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: manage
ms.openlocfilehash: 97fab1a36db2e903b3a909bee9e2f1748f7841fd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834141"
---
# <a name="server-performance-advisor-users-guide"></a>Server Performance Advisor-Benutzerhandbuch

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows 10, Windows 8

In diesem Benutzerhandbuch für Microsoft Server Performance Advisor (SPA) bietet Richtlinien zum SPA verwenden, um Leistungsengpässe zu erkennen, in Systemen, die in verschiedenen Serverrollen bereitgestellt.

SPA helfen Ihnen bei der folgenden Schritte:

* Verwalten Sie die serverleistung aus, und Beheben von Problemen mit der serverleistung.

* Geben Sie Berichte für Daten und Empfehlungen zur allgemeinen Konfiguration und Leistungsprobleme.

* Geben Sie die Empfehlungen für bewährte Erwägung basierend auf den gesammelten Daten.

> [!NOTE]
> Der SPA-Konsole macht keine Änderungen an den Server.

Weitere Informationen zum Entwickeln von SPA-Advisor-Packs finden Sie unter [Server Performance Advisor Pack Development Guide](server-performance-advisor-pack-development-guide.md).

## <a name="server-performance-advisor-overview"></a>Server Performance Advisor – Übersicht


In diesem Abschnitt wird erläutert, den Verlauf der SPA, beschreibt die Zielgruppe und die Szenarien und bietet eine architektonische Übersicht über das Tool.

### <a name="history-of-spa"></a>Verlauf der SPA

Die ursprüngliche Version von Microsoft Server Performance Advisor (SPA) wurde im Jahr 2005-2006 veröffentlicht. Es in erster Linie für Windows Server 2003, einschließlich der Core-Betriebssystem und Serverrollen wie z. B. Internet Information Services (IIS) und active Directory verwendet. Das Ziel des Tools ist auf die serverleistung zu bewerten und Beheben von Problemen mit der serverleistung.

SPA enthält Berichte für Daten und Empfehlungen für Systemadministratoren, die zur allgemeinen Konfiguration und Leistungsprobleme. SPA sammelt leistungsbezogener Daten aus verschiedenen Quellen auf Servern, z. B. Leistungsindikatoren, Registrierungsschlüssel, WMI-Abfragen, Konfigurationsdateien und Ereignisablaufverfolgung für Windows (ETW). Basierend auf dem Server-Leistungsdaten, die er Daten sammelt, bieten SPA einen detaillierten Einblick in die Ausgangssituation für Server-Leistung und die Problem Empfehlungen dazu, was verbessert werden kann.

Es wurden mehr als eine Million Downloads des ursprünglichen SPA-Tools, und konnten dadurch viele Systemadministratoren, die die Leistung von ihren Servern zu verwalten. Es wurde ein sehr erfolgreicher Performance-Tool zur Problembehandlung.

Seit der Veröffentlichung der ursprünglichen SPA gibt es mehrere wichtige Änderungen in der Welt der Server-Leistung. Am wichtigsten ist die Version von Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008 mit neuen Versionen der entsprechenden Serverrollen wie z. B. IIS 8.5 (Internetinformationsdienste). Neuere Versionen von Server Performance Advisor erweitern die Funktionen der ursprünglichen SPA auf den aktuellen Server-Betriebssysteme und Serverrollen.

Obwohl die gleichen Ziele beim Entwurf und die Performance Analysis-Paradigma als das ursprüngliche Tool SPA 3.1 freigegeben hat, wurde sie mit der neuesten Technologie umgeschrieben. Es verfügt auch über die folgenden wichtigen Verbesserungen:

* Kann für Server mit Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008 analysiert.

* Unterstützt die remoteanalyse-Funktion, die SPA 3.1 zum Erfassen und Analysieren von Daten in einer zentralen Konsole, ohne dass Code zu installieren, auf den Servern analysiert werden kann.

* Verwendet eine Microsoft SQL Server für die Analyse und Speicherung, ermöglicht es, verarbeiten und speichern große Datenmengen.

* Trennt das Tool aus dem Advisor-Packs. Performance Analysis-Logik für jede Serverrolle wird in Form von einem Advisor-Pack, veröffentlicht, die veröffentlicht oder separat aus dem Tool aktualisiert werden können.

* Stellt die Advisor-Packs, die in SQL-Skripts mit einer offenen Architektur entwickelt wurden. Nicht-Microsoft-Parteien Advisor-Packs entwickeln oder erweitern die vorhandenen Advisor Packs von Microsoft, um spezielle Anforderungen zu behandeln.

* Unterstützt neue Funktionen wie Seite-an-Seite-Vergleichs-Berichte und Trend und historische Diagramme können Sie Anomalien gefunden.

* Bietet Funktionen wie z. B. ändern, Import und Export von Schwellenwerten können Sie problemlos die Berichte und Benachrichtigungen zu optimieren und diese Feinabstimmungen für andere SPA-Benutzer freigeben.

* Unterstützt mehrere Projekte, die zum Gruppieren von Zielservern verwendet werden kann.

* Enthält die wiederholte Sammeln von Daten in der SPA-Konsole.

* Können benutzerdefinierte Abfragen und berichterstellung mithilfe von Microsoft SQL Server (für fortgeschrittene Benutzer).

* Angepasste Windows PowerShell-Cmdlets stehen für die Verwendung mit der SPA

* Abwärtskompatibel für das Importieren und Anzeigen von Berichten aus einer SPA 3.0-Datenbank

### <a name="target-audience"></a>Zielgruppe

Das SPA-Tool dient in erster Linie für Systemadministratoren, die weniger als 100 Servern in verschiedenen Serverrollen zu verwalten. Sie können auch von Supporttechnikern zum Sammeln von Leistungsdaten und zum Beheben von Leistungsproblemen für Kunden, die verwendet werden.

SPA bietet Empfehlungen zum Lösen von Leistungsproblemen. Allerdings Annahmen basiert auf, die möglicherweise nicht für Ihre Umgebung spezifischen Server gelten. Die Empfehlungen, die in der SPA angebotenen sollte Vorschläge angesehen werden. Wir erwarten, dass SPA-Benutzer haben ein gutes Verständnis ihrer Systemkonfiguration, Anwendungsfälle und die Auswirkungen von System zu optimieren, auf das Verhalten des gesamten Systems. Systemadministratoren müssen entscheiden, wenn die SPA-Empfehlungen zu ihrer Umgebung angewendet werden soll.

### <a href="" id="what-s-new-in-spa-3-1-"></a>Neuerungen, die neuen SPA-3.1?

Die folgenden Features und Verbesserungen wurden im SPA 3.1 hinzugefügt:

* Active Directory Advisor Pack können Sie die allgemeine Leistung der Server s active Directory-Domänendienste-Serverrolle zu analysieren.

* Unterstützung für Entwickler verloren ETW-ereigniswarnungen Benachrichtigungen des Advisor-Packs hinzu und Sichtbarmachen von die Warnung beim Generieren eines Berichts und Ereignisse sind aufgrund hoher Frequenz zu protokollieren, auf einer langsamen oder stark verloren gegangen Konflikten Datenträger

### <a name="target-scenarios"></a>Zielszenarien

Es folgen die Zielszenarien für die SPA:

* **Server-Umgebung**

    SPA soll einfach einrichten und verwalten. Dies gilt für serverumgebungen, die 1 bis 100-Servern verwenden. SPA skaliert nicht gut, wenn Sie die Leistung für mehr als 100 Server verwalten möchten. Bei größeren oder komplexere Umgebungen sollten Sie mit System Center Operations Manager.

* **Behandeln von Leistungsproblemen**

    Sie können die SPA als eine Leistung Problembehandlungstool verwenden. Es bietet die Möglichkeit zum Sammeln von Leistungsdaten, sie führt eine umfassende Post Verarbeitung für die Daten erhalten Sie einen besseren Überblick des gesamten Systems Verhaltens und alle Anomalien kennzeichnet. Wenn von einem Kunden ein Leistungsproblem vermuten, können Sie SPA zum Erfassen und Analysieren von Leistungsdaten vom Server.

    SPA generiert einen Bericht, den Sie anzeigen können. SPA-Berichte bieten eine Benachrichtigungsliste die wichtigsten potenziellen Probleme, und ein Data-Abschnitt, der verschiedene Leistungsindex, Konfigurationen und Einstellungen für den Server enthält. In diesem Bericht können Sie die spezifischen Leistungsproblem identifizieren und verwenden Sie die Empfehlungen, um Lösungen zum Beheben des Problems zu finden. Berichte können für andere Berichte verglichen werden, die zu einem anderen Zeitpunkt oder von einem anderen Server generiert wurden. Anhand dieses Vergleichs Seite-an-Seite können Sie Unterschiede zwischen Baseline normales und ungewöhnliches Verhalten bestimmen.

    **Beachten Sie** SPA fungiert nicht als ein Debuggen oder Tool Messung. Darüber hinaus aus der Perspektive der Server wird ein nur-Lese Tool berücksichtigt werden, und die Serverkonfigurationen nicht geändert.

     

* **Leistungsüberwachung für index**

    Sie können SPA verwenden, um den Leistungsindex von Servern zu überwachen. Sie können auswählen, zum Ausführen der SPA routinemäßig auf Servern zum Sammeln von Leistungsdaten aus, und führen Sie ein Trenddiagramm oder ein Verlaufsdiagramm die Anomalien zu erkennen. Sie können den Bericht für eine bestimmte Analyse anzeigen, finden Sie weitere Informationen zu das Leistungsproblem und verwenden Sie dann die Empfehlungen oder andere Berichtsdaten zur Behebung des Problems.

### <a name="spa-architecture"></a>SPA-Architektur

Die SPA-Datenlogik Auflistung basiert auf ein Protokoll in Windows-Leistungsprotokolle und Warnungen (PLA) aufgerufen. PLA kann Programme zum Erfassen von Leistungsdaten von lokalen Servern oder Remoteservern, z. B. Leistungsindikatoren, WMI-Abfragen, ETW-ablaufverfolgungen, Registrierungsschlüssel und Konfigurationsdateien. Wenn SPA Leistungsanalyse auf einen Zielserver ausgeführt wird, wird eine PLA-Datensammler-Menge, die basierend auf den bestimmten SPA-Advisor-Pack, das Sie ausgewählt. Das Advisor-Pack enthält die Datenquelle gesammelt werden und die Dateifreigabe, in dem die Protokolle gespeichert sind. SPA-Datensammlung speichert nur einem einzigen Benutzerkonto anmelden. dasselbe Benutzerkonto ein, die PLA wird auch verwendet, um die Protokolle schreiben.

SPA verwendet eine SQL Server-Datenbank zum Speichern der Performance-Protokolle, die von Zielservern gesammelt werden. SPA importiert alle Leistungsprotokolle von der Dateifreigabe in die Datenbank, und klicken Sie dann die Analyselogik für Daten innerhalb jedes Advisor Pack verwendet, um die Daten verarbeiten und die Berichte zu generieren. Ein Advisor-Pack analysiert die Leistungsdaten, die von Zielservern erfasst wurde und die SPA-Berichte generiert. Weitere Informationen zum Erstellen eines Advisor-Packs finden Sie unter [Server Performance Advisor Pack Development Guide](server-performance-advisor-pack-development-guide.md).

Die SPA-Konsole von Benutzeroberflächen und Interaktionen werden im Rahmen der SPAConsole.exe erstellt. Die Konsole können Sie mit einer Datenbank zu erstellen, hinzufügen oder entfernen Packs für Advisor, Zielserver verwalten, Durchführen einer Leistungsanalyse, und zeigen Leistungsberichten.

Die SPA-Konsole kann unter den folgenden Betriebssystemen ausgeführt:

* Windows 8.1

* Windows 8

* Windows 7

* Windows Server 2012 R2

* Windows Server 2012

* Windows Server 2008 R2

* WindowsServer 2008

In eine typische Geschäftsanwendung, es gibt drei Ebenen: die Darstellungsschicht der Geschäftslogikebene und der Speicherschicht. SPA dient als ein Produkt Ebene, die Konsole und der Datenbank. Die Konsole dient als Darstellungsschicht mit bestimmten prozessbezogene Logik enthalten, und die Datenbank fungiert als die Speicherebene und der Geschäftslogikebene. Die Konsole erfasst Benutzereingaben, und es steuert, die Schritte für die Datensammlung, Datenverarbeitung und berichterstellung. SPA ist nicht auf Windows-System-Diensten abhängig.

Das folgende Diagramm zeigt die allgemeine Architektur des Systems SPA. Der Prozess ist:

1.  In der SPA-Konsole führen Sie zur Leistungsanalyse, auf die angegebenen Server.

2.  Wenn die Leistungsdaten erfasst werden, schreibt PLA auf den Zielservern die Protokolle zurück in die Dateifreigabe, die vom datensammlersatz angegeben ist.

3.  Nachdem die Datensammlung auf einem Zielcomputer abgeschlossen ist, importiert die SPA-Konsole die Protokolle in SQL Server-Datenbank.

4.  Die Konsole wird die Datenverarbeitungslogik von bestimmten Advisor Pack aufgerufen.

5.  Das Advisor-Pack verarbeitet die Daten und ruft SPA-APIs zum Einfügen von Datensätzen in die Systemtabellen für den Bericht, die durch das SPA-Framework definiert sind.

6.  Sie können im Berichts-Viewer in der Konsole verwenden, um die Berichte anzuzeigen, generiert. Damit Sie die Leistungsprobleme zu beheben, SPA bietet drei Arten von Berichten: einzelne Berichte, Seite-an-Seite Berichte und Trends oder Verlaufsdaten Diagramme. Weitere Informationen zu Berichten finden Sie unter [Anzeigen von Berichten](#bkmk-viewingreports).

![SPA-Architektur](../media/server-performance-advisor/spa-user-manual-architecture.png)

## <a name="getting-started-with-spa"></a>Erste Schritte mit der SPA


### <a name="requirements"></a>Anforderungen

Die SPA-Konsole kann auf Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008 installiert werden. Ausführen von SPA in früheren Versionen des Betriebssystems Windows Server wird nicht unterstützt. SPA X86 oder X64 ausgeführt, aber die IA64- oder ARM-Architekturen werden nicht unterstützt.

SPA ist in Windows Presentation Foundation (WPF) 2.0 integriert. Dies Teil von Microsoft .NET Framework 4, ist also .NET Framework 4 erforderlich.

Sie müssen auch SQL Server 2008 R2 Express auf dem gleichen Computer installieren, auf die SPA installiert ist. SQL Server 2008 R2 Express ist eine kostenlose Datenbank-Engine, die von Microsoft veröffentlicht wird. Sie können die Microsoft SQL Server 2008 R2 Express aus dem Microsoft Download Center herunterladen. SQL Server 2008 R2 Express es wird empfohlen, ggf. neuere Versionen von SQL Server auch mit SPA kompatibel.

**Beachten Sie** SPA enthält keine SQL Server und .NET Framework als Teil der SPA-Installationspaket. Nach der Installation von Microsoft SQL Server 2008 R2 und .NET Framework 4.0, empfehlen wir, dass Sie Windows Update vor der Installation von SPA ausführen.

 

Da können Benutzer erstellen und Verwalten von Datenbanken mit SPA, sollte das Benutzerkonto, das zum Ausführen der SPA verwendet wird als SQL Server die gleichen Administratorrechte haben.

### <a href="" id="bkmk-setupspa"></a>Einrichten der SPA

SPA wird verpackt, als eine CAB-Datei, die alle Binärdateien für die SPA-Framework, die Windows PowerShell-Cmdlets enthält, die in erweiterten Szenarien verwendet werden, und die folgende Advisor packt: Kernbetriebssystem, Hyper-V, active Directory und IIS. Nachdem Sie die CAB-Datei in einen Ordner extrahiert haben, ist keine zusätzliche Installation erforderlich. Um SPA auszuführen, müssen Sie jedoch die Datensammlung von den Zielservern wie folgt aktivieren:

* Um Datensammlung PLA auszuführen, muss das Benutzerkonto, mit denen Sie die SPA-Konsole ausführen Teil der Sicherheitsgruppe "Administratoren" auf dem Zielserver sein. Wenn der Zielserver und die Konsole in der gleichen Domäne sind, muss das Domänenbenutzerkonto, das Teil der Sicherheitsgruppe "Administratoren" auf dem Zielserver sein. Wenn der Zielserver und die Konsole nicht in derselben Domäne sind, erstellen Sie eines Administratorkontos auf dem Zielserver mit dem gleichen Benutzernamen und Kennwort wie das Benutzerkonto, mit denen Sie die SPA-Konsole ausführen.

* Erstellen Sie einen freigegebenen Ordner aus, um Ergebnisse zu erzielen, auf dem Server.

* Stellen Sie sicher, dass das Benutzerkonto an, die Sie verwenden zum Ausführen der SPA-Konsole über Lese- und Schreibberechtigungen für den freigegebenen Ordner. PLA verwendet dieses Konto zum Schreiben von Protokollen in den Ordner an.
Die SPA-Konsole verwendet das gleiche Konto, um Protokolle zu lesen, und importieren Sie sie in der Datenbank.

    **Beachten Sie** ETW implementiert einen zirkulären Puffer zum Speichern der Ablaufverfolgungs, und verschiebt sie in den freigegebenen Ordner, wenn möglich. Wenn der Server ausgelastet ist, oder der Schreibvorgang langsam ist, löscht-ETW-ablaufverfolgungen, wenn der Puffer voll ist. Es ist wichtig, die der freigegebene Ordner befindet sich auf einem Server mit schnellen e/a-Zugriff. Es wird empfohlen, dass alle Zielserver aus einen freigegebenen Ordner Datenverlust aufgrund von langsamen-Datei-e/a minimiert ist.

     

* Für PLA auf Zielservern Festlegen der Windows-Firewall für den remote Leistungsprotokolle und Warnungen den Zugriff auf Zielservern zu ermöglichen. PLA verwendet TCP-Port 139.

* Stellen Sie sicher, dass die **Leistungsprotokolle und Warnungen** -Dienst wird ausgeführt.

* Wenn der Server-Konsole und Ziel in unterschiedlichen Subnetzen befinden, müssen Sie auch zum Festlegen von Feld remote-IP-Adresse in den eingehenden Firewallregeln in der **Bereich** Einstellungen auf der **Leistungsprotokolle und-Warnungen** Seite, wie hier gezeigt.

    ![PLA-Eigenschaften](../media/server-performance-advisor/spa-user-manual-pla-firewall.png)

* Aktivieren Sie die Netzwerkermittlung in der Konsole und auf jedem der Zielserver.

* Wenn der Zielserver nicht zu einer Domäne angehört, aktivieren Sie die folgende registrierungseinstellung: **HKLM\\SOFTWARE\\Microsoft\\Windows\\Currentversion\\Policies\\system\\LocalAccountTokenFilterPolicy**.

**Beachten Sie** Standardmäßig schreibt die SPA-Diagnoseprotokolle zu dem Ordner, in denen SpaConsole.exe befindet. Wenn SPA unter dem Ordner "Programme" installiert ist, SPA ist nur in der Lage, zu schreiben, dass das Protokoll, wenn SpaConsole.exe ist als Administrator ausgeführt würden.

Wenn Sie Data-Analysen für die Computer-Konsole ausführen möchten, müssen Sie SPA als Administrator ausführen. PLA durchläuft einen anderen Codepfad, bei der Ausführung für einen lokalen Computer, die Administratorrechte erforderlich.

Wenn Sie das IIS-SPA-Advisor-Pack für Ihre Server ausführen möchten, müssen Sie WMI-Abfrage und ETW-Ablaufverfolgung für den IIS-Server zu ermöglichen. Aktivieren Sie hierzu **Ablaufverfolgung** unter der **Systemzustand und Diagnose** -Rollendienst und **IIS-Verwaltungsskripts und-Tools** unter **-Verwaltungstools**  von der **Webserver (IIS)** -Serverrolle.

 

### <a name="creating-your-first-project"></a>Erstellen Ihres ersten Projekts

Nachdem alles eingerichtet ist, können Sie Ihr erste SPA-Projekt erstellen. Wie im vorherigen Abschnitt beschrieben wird, speichert die SPA alle Elemente, die Leistung der Datenanalyse innerhalb einer Datenbank zugeordnet ist. Jedes Projekt SPA entspricht einer einzelnen Datenbank. Die **erstmalige Verwendung Assistenten** führt Sie durch die folgenden Schritte aus.

**So erstellen Sie eine SPA-Projekt**

1.  Starten Sie SpaConsole.exe. Die Konsole gibt einen nicht verbundenen Modus, in denen SPA nicht mit einer beliebigen Datenbank verbunden ist, und es wird das Hauptfenster ist leer.

2.  Klicken Sie zum Erstellen eines neuen Projekts **Datei**, und klicken Sie dann auf **neues Projekt**. Dadurch wird der erstmaligen Verwendung-Assistent gestartet. Die erste Seite enthält die Schritte, die beim Verwenden des Assistenten:

    * Erstellen einer Datenbank

    * Bereitstellen von Advisor-packs

    * Hinzufügen von Servern zum Liste mit Zielservern

3.  Klicken Sie auf **Weiter**. Die **erstellen Projektdatenbank** Seite werden Sie aufgefordert, den Namen des Microsoft SQL Server-Instanz bereitstellen, in dem Ihre Datenbank zu erstellen möchten. Z. B. wenn es auf dem gleichen Computer wie die Konsole ist, können **"localhost"\\&lt;Ihren SQL Servernamen&gt;**.

    **Beachten Sie** der Standardinstanzname für eine SQL Server 2008 R2 Express-Installation ist SQLExpress. Für eine Instanz von SQL Server 2008 R2 Express, die auf dem lokalen Computer installiert ist, die Datenbank wird in der Regel standardmäßig **"localhost"\\SQLExpress**. Allerdings es möglicherweise während der Installation von SQL Server geändert wurden daher müssen Sie sicherstellen, dass Sie die Namen der richtigen SQL Server-Instanz verwenden.

     

4.  Geben Sie den Datenbanknamen an. Nur Buchstaben, Ziffern und Unterstriche (\_) für einen Datenbanknamen an als gültige Zeichen sind zulässig. Eine angemessene Empfehlung der SPA-Datenbankname wäre **SPA**. Wenn Sie einen ungültigen Namen eingeben, wird ein rotes Fehlersymbol angezeigt. Die zugeordnete QuickInfo gibt den Grund für Fehler bei der Überprüfung.

    **Beachten Sie** es ist wichtig, um den Datenbanknamen und den Server-Instanznamen, denken Sie daran, da dies die einzige Bezeichner für das Projekt sind. Sie müssen diese Informationen bereitstellen, wenn Sie mit dieser Datenbank wechseln möchten.

     

5.  Nachdem Sie den Server-Instanznamen und den Namen angeben, wird beim ersten Verwenden des Assistenten für den Speicherort für die Datenbankdatei generiert.

6.  Auf der **erstellen Projektdatenbank** auf **Weiter**. Beim ersten Verwenden des Assistenten für eine Datenbank erstellt und alle SPA-bezogene Datenbankschema, Funktionen und gespeicherten Prozeduren in der Datenbank generiert. Dieser Schritt kann einige Sekunden, hängt von der Geschwindigkeit Hardware- und Netzwerkkonfiguration dauern.

    **Beachten Sie** , wenn dieser Schritt fehlschlägt, wird eine Fehlermeldung angezeigt. Einige allgemeine Probleme sind: Konsolenverbindung kann nicht mit der SQL Server-Instanz, nicht über ausreichende Berechtigungen zum Erstellen der Datenbank, oder der Name der Datenbank bereits vorhanden ist.

     

7.  Wenn im vorherige Schritt erfolgreich ausgeführt wurde, Sie sehen die **Bereitstellen von Advisor-Pack** Seite. Es listet die Advisor-Packs, die auf Ihrem Computer verfügbar sind. SPA automatisch überprüft den Ordner mit dem Namen **APs** im SPA-Stammverzeichnis. Der vollständige Name, Version und Autor für jedes Advisor Pack aufgeführt.

    **Beachten Sie** finden Sie weitere Informationen zur Verwendung der vollständige Name und Version in der SPA [Verwalten von Advisor-Packs](#bkmk-manageadvisorpacks)

     

8.  Wählen Sie Sie verwenden möchten, stellen Sie in der Datenbank bereit, und klicken Sie dann auf die Advisor-Packs **Weiter**. Sie können auch auf **überspringen** mit dem nächsten Schritt verschieben, ohne die Bereitstellung von Advisor-Packs.

    **Beachten Sie** können Sie Advisor-Packs Sie das Tool verwenden jederzeit bereitstellen. Weitere Informationen finden Sie unter [Verwalten von Advisor-Packs](#bkmk-manageadvisorpacks).

     

9.  Auf der **Hinzufügen von Servern** Seite bei jedem Server werden hinzugefügt, um Liste mit den Zielservern, es gibt zwei Pflichtfelder ausfüllen: **Name des Servers** und **Speicherorts der Dateifreigabe**.

    **Beachten Sie** steht auch eine **Anmerkung** -Feld, das in erster Linie zum Klassifizieren oder suchen Sie nach dem Server verwendet wird. In Fällen, in denen Sie viele Server verfügen, können Sie eine Datei mit kommagetrennten Werten (CSV) importieren, die den Servernamen, Ergebnisordner und optional Anmerkung-Feld enthält. Die **Anmerkung** Feld dient zum Beschreiben des Servers und der Begriff kann verwendet werden, um Server für die Datensammlung zu filtern. Wenn Sie die Server über die CSV-Datei initialisieren, wird ein Analysefehler in der Datei nicht auf die Servern geladen.

     

10. Mehrere Konfigurationen müssen festgelegt werden, um PLA-Datensammlung zu aktivieren, siehe [Einrichten der SPA](#bkmk-setupspa). Die **-Server hinzufügen** Seite enthält eine Testfunktion für die Konfiguration können Sie Konfigurationsprobleme zu beheben. Wählen Sie das Kontrollkästchen, die dem Computer zugeordnet, und klicken Sie dann auf **Testen der Konnektivität**. SPA versucht wird, zum Generieren eines Sammlungssatzes, der auf einem Zielserver, und versucht importieren, die die Ergebnisse in der Datenbank zurück. Wenn alles richtig ist, ist die **Status** zeigt **übergeben**. Wenn ein Fehler auftritt, wird eine QuickInfo angezeigt, die die Ursache des Fehlers beschreibt.

11. Jedem der Server wird automatisch in der Datenbank hinzugefügt werden, selbst wenn den Konfigurationstest nicht erfolgreich ist. Um den Server aus der Liste entfernen möchten, wählen Sie den Namen des Servers ein, und klicken Sie auf **entfernen**.

12. Wenn alles abgeschlossen ist, klicken Sie auf **Fertig stellen** zum ersten Mal verwenden-Assistenten zu schließen. Wenn Sie beim ersten Verwenden des Assistenten für vor dem Beenden es schließen, alle vorherigen Schritte beibehalten und keine von ihnen Rollback automatisch. Sie müssen später Änderungen manuell vornehmen.

## <a name="running-analysis"></a>Ausführen der Analyse


Nach dem Festlegen der Datenbank, können Sie Informationen zur Leistungsanalyse auf den Servern ausführen.

Jedes Mal, wenn die SPA-Konsole gestartet wird, wird das letzte Projekt an, das vom aktuellen Benutzer verwendet wurde automatisch geöffnet. Das Hauptfenster enthält eine Liste von Servern. Jeder Server verfügt über vier Eigenschaften: Servername, Analyseergebnisse, aktuellen Status und Anmerkung.

* **Servername** den Namen des Servers, der Bezeichner für den Server handelt. Es sind keine doppelten Namen zulässig.

* **Analyseergebnisse** standardmäßig es zeigt das Ergebnis der neuesten Leistungsanalyse für den Server ausführen. Wenn keine Leistungsanalyse, die auf dem Server ausführen wurden, wird **kein Bericht**. Es liegt eine Warnung wird ausgelöst, von dem Bericht, zeigt **Warnung** und den Zeitstempel, wenn der aktuelle Bericht generiert wurde. Wenn keine Probleme während der aktuellen Analyse auf dem Server gefunden wurde, wird **OK** und Zeitstempel.

    **Beachten Sie** , wenn Sie kürzlich eine Einstellung geändert, es wird empfohlen, dass Sie die Analyse erneut aus, um die allgemeinen Auswirkungen der Änderung bewerten und erhalten einen aktualisierten Bericht des Systemstatus ausführen. SPA verfolgt keine Änderungen an der Konfiguration auf das getestete System.

     

* **Aktueller Status** zeigt den Status des Performance Analysis-Tasks, die derzeit auf dem Server ausgeführt. Sie können eine ausgeführte Aufgabe abbrechen, indem Sie auf die **Abbrechen** Symbol, das durch ein rotes X gekennzeichnet ist.

* **Anmerkung** beschreibt den aktuellen Zielserver. Beispielsweise können Sie Ihren Server beschreiben, mit der Serverrolle (z. B. SQL Server) oder einen Speicherort (z. B. Kent). SPA verwendet die **Servernamen** und **Anmerkung** zur suchen und den richtigen Server finden kann. Sie können in das Textfeld eingeben. Wenn die **Servernamen** oder **Anmerkung** Spalten enthält, die genaue Zeichenfolge, die Sie in das Suchfeld eingegeben wird der Server in der Serverliste angezeigt.

Außerdem stehen die folgenden Steuerelemente auf der Konsole zur Verfügung:

* **Wiederholen Sie die** , die beschreibt, die Möglichkeit, eine Sammlung regelmäßig wiederholen das Kontrollkästchen auf Grundlage eines bestimmten Zeitintervalls. Bei den meisten Serverinstallationen möchten Sie, wie Sie eine SPA-Sammlung pro Stunde wiederholt werden, um ausreichend-Verlauf für die Analyse verfügen. Wenn Sie die Auflistung nur einmal ausführen möchten, sollten Sie nicht auswählen der **wiederholen** Kontrollkästchen.

* **Entfernen Sie die Wiederholung** eine Schaltfläche, die Ihnen ermöglicht, eine laufende Abbrechen, wiederholen sammlungsauftrag. Die Auflistung mit wiederholen Sie diesen Schritt abgebrochen, aber nicht die aktuelle Auflistung (sofern vorhanden) wird ausgeführt. Diese Option können Sie eine neue, wiederholen Sie diesen Schritt Sammlungsintervall zurücksetzen oder die Sammlung manuell ausführen.

Bevor Sie die Leistungsanalyse starten, wählen Sie die Dauer der Daten-Auflistung. Zwar mehr Daten erfasst ein genaueres Image der Situation Leistung Server bereitstellen hilft, generiert außerdem eine größere Anzahl von Protokollen, und es kann weitere mögliche Auswirkungen haben, auf dem Server. Wählen Sie die richtigen Daten sammlungsdauer basierend auf Ihren Anforderungen. Jedes Advisor Pack definiert die minimale gültige Dauer. Die Dauer der Daten-Auflistung, die Sie auswählen muss länger als die minimale Dauer der ausgewählten Advisor Packs sein.

Um Informationen zur Leistungsanalyse auf Zielservern ausgeführt werden soll, wählen Sie die Servern, die Sie verwenden möchten, führen Sie die Informationen zur Leistungsanalyse für, und klicken Sie auf ** zum Ausführen der Analyse ** ein Dialogfeld angezeigt wird, und fordert Sie auf die Advisor-Packs auf den Servern ausgeführt werden. Die ausgewählten Ratgeber Packs, die gleichzeitig ausgeführt werden. Die Berichte, die generiert werden, basieren auf der Leistungsdaten, die im gleichen Zeitraum gesammelt werden.

**Beachten Sie** , wenn Sie einen Server, die eine sich wiederholenden Leistungsanalyse ausgeführt wird auswählen, verfügt die **Serie entfernen** Schaltfläche können Sie zum Abbrechen der Erfassung von sich wiederholenden. SPA lässt nicht mehrere Data Collection-Sitzungen gleichzeitig auf demselben Computer.

 

## <a href="" id="bkmk-viewingreports"></a>Anzeigen von Berichten


In der SPA gibt es drei Arten von Bericht zur Leistungsanalyse: Berichtsdefinitionssprache "," Seite-an-Seite im Bericht "und" Trend "und" Verlaufsdiagramme ".

Nach ausgeführten Leistungsanalyse wird ein Bericht für jedes der Advisor-Pack führen Sie auf dem Zielcomputer erstellt. Sie können aus der Liste der im Hauptfenster von Server, erweitern **Analyseergebnisse** des Advisor-Packs angezeigt, die auf dem angegebenen Server ausgeführt wurden. Sie können einen Berichtsnamen, um einen einzelnen Bericht anzeigen klicken.

Es gibt drei Symbole neben den Advisor-Pack-Namen, die zeigen, den Status der aktuellen Analyse, die auf dem Server ausführen:

* Die **neueste** Symbol zeigt den Bericht aus, die von der aktuellen Leistungsanalyse auf diesem Server für die Advisor-Pack generiert wurde.

* Die **finden** Symbol zeigt die Liste der Analyseberichte, dadurch können Sie den richtigen Bericht auswählen. Die **Advisor Pack** und **Zielserver** Felder sind mit der aktuellen Serverinformationen der Advisor Pack und das Ziel bereits ausgefüllt. Der Standardbereich für die Zeit auf eine Woche festgelegt ist, und das Enddatum auf heute festgelegt ist. Wenn Sie auf die **Suche** Schaltfläche in der oberen rechten Ecke können Sie eine Liste aller Performance Analysis Berichte abrufen, für das ausgewählte Server und Advisor Pack innerhalb des Zeitbereichs.

* Die **Ansicht Diagramme** Symbol öffnet den Trend und die Verlaufsdiagramm anzeigen.

Die folgende Abbildung zeigt die **neueste**, **finden**, und **Ansicht Diagramme** Symbole nach jedem Advisor Pack:

![Bericht-Symbole](../media/server-performance-advisor/spa-user-manual-report-icons.png)

### <a name="searching-for-and-within-reports"></a>Suche nach und in Berichten

Suchen nach Berichten erfolgt über **Berichts-Explorer**. Dadurch können Sie Berichte nach Datumsbereich, Servername und Advisor Pack suchen. Dies ist die empfohlene Methode zum Suchen eines Berichts von Interesse sind, außer dem letzten Ausführen von Berichten. Die letzten Ausführen von Berichten steht über **View-Bericht** für diesen Server.

Wenn Sie einen bestimmten Bericht anzeigen, können Sie ganz einfach auf den Bericht weiter und zurück navigieren, nach Zeit oder sehen Sie sich einen verknüpften Bericht, wie eine andere AP zur gleichen Zeit ausgeführt. Diese Optionen sind verfügbar unter **Aktionen**.

Es ist auch möglich, in einem Bericht suchen. Eine Anzahl der Berichte ein **finden** Zeichenfolge-Suchfeld für schnelle textzeichenfolgensuche innerhalb des Berichts verfügbar. Um das Textfeld zu entfernen, können Sie es schließen. Um ein Suchfeld (unter Windows, deren Text suchen) zu aktivieren, können Sie die STRG + F Verknüpfung. Die **finden** Feld ermöglicht dem Benutzer, geben Sie die Groß-/ Kleinschreibung nach Bedarf mit der **Groß-/Kleinschreibung beachten** Option.

Die folgende Abbildung zeigt die **finden** Suchfeld, mit der Zeichenfolge **Power** auf die **Bericht** Registerkarte.

![das Suchfeld suchen](../media/server-performance-advisor/spa-user-manual-find-search-box.png)

### <a name="single-report"></a>Berichtsdefinitionssprache

Ein einzelner Bericht zeigt die Leistungsergebnisse für die Analyse von einer einzigen Ausführung des Advisor-Pack auf einem einzelnen Computer. Der Bericht zeigt den Namen des dem Advisor-Pack, die den Namen des Zielservers, die Zeit, die der Bericht generiert und die Dauer für die Sammlung von.

Ein einzelner Bericht enthält einen Abschnitt für die Benachrichtigung und die Datenabschnitte.

### <a name="notification-section"></a>Abschnitt Benachrichtigung

Bereich "Benachrichtigungen" besteht aus einem Satz von Leistungsregeln für die Analyse. Jede Benachrichtigung enthält die einer Datenquelle, einige Schwellenwerte und etwas Geschäftslogik. Beim Ausführen von Leistungsanalyse wertet die Geschäftslogik die Datenquellen mit den Schwellenwerten, um zu bestimmen, ob die Regel oder nicht erfolgreich war. Wenn dies nicht der Fall ist, wird eine Warnung angezeigt wird, informieren Sie über ein mögliches Leistungsproblem. Darüber hinaus Empfehlungen können Sie das Problem zu beheben. Bereich "Benachrichtigungen" ist immer die erste Registerkarte in der Ansicht der einzelnen Bericht.

Bereich "Benachrichtigungen" ist in zwei Teile unterteilt: **Warnung** und **andere Benachrichtigungen**.

Wenn die Datenquelle für eine Regel bestimmte Bedingungen, die auf Grundlage der Einstellungen Logik und Schwellenwerte erfüllt, eine Warnung angezeigt wird, der **Warnung** Bereich. Eine Warnung besteht aus den folgenden Teilen:

* Ein Warnsymbol gibt an, ob ein potenzielles Problem vorhanden ist.

* Der Name der Regel. Z. B. **Netzwerk empfangen Paket löscht** ist ein Link, der auf der Seite Regel Details zeigt, wie in beschrieben [Verwalten von Advisor-Packs](#bkmk-manageadvisorpacks).

* Eine einfache Beschreibung zu dem potenziellen Problem.

* Eine Empfehlung für eine mögliche Lösung für die mögliches Leistungsproblem.

Verschiedene Servern können andere Konfigurations- und Verwendungsmustern, und es ist unmöglich, legen Sie die Schwellenwerte und Regeln, die für alle Server unter allen Umständen gültig sind. SPA bietet die Möglichkeit, um die Schwellenwerte zu ändern. Sie können auch auswählen, um eine Regel zu deaktivieren, wenn die Regel für Ihr Szenario nicht anwendbar ist. Standardmäßig werden alle Regeln aktiviert. Eine deaktivierte Regel ist nicht im Infobereich der Taskleiste angezeigt. Weitere Informationen finden Sie unter [Verwalten von Advisor-Packs](#bkmk-manageadvisorpacks).

Die **andere Benachrichtigungen** Bereich enthält alle anderen Regeln, in denen keine Warnung wird ausgelöst, oder die Regel ist nicht anwendbar. Sie enthält ähnliche Komponenten, wie in der **Warnung** Bereich. Der größte Unterschied ist, dass keine Warnung ausgelöst wird, oder die Regel gilt nicht, in der Regel keine Empfehlung bereitgestellt wird.

### <a name="data-sections"></a>Datenabschnitte

Datenabschnitte enthalten, die Leistungsdaten, die das Advisor-Pack generiert basierend auf den von den Zielservern gesammelten Rohdaten. Datenabschnitte enthalten eine Reihe von Abschnitten auf oberster Ebene und mehrere Ebenen von Unterabschnitte. In den Abschnitten auf oberster Ebene werden als Registerkarten dargestellt. Alle in den Bereichen der obersten Ebene in den Unterabschnitten werden in der erweiterbaren Bereiche angezeigt. Sie können reduzieren oder Erweitern Sie den Abschnitten für eine Fokussierung auf Interessengebiet, wie in der folgenden Abbildung dargestellt.

![Datenabschnitte](../media/server-performance-advisor/spa-user-manual-data-sections.png)

Das Core OS SPA Advisor Pack und die IIS-SPA Advisor Pack enthalten eine **Systemübersicht** Abschnitt. Dieser Abschnitt enthält die Informationen auf oberster Ebene, über die ressourcennutzung und die Konfiguration. Andere Abschnitten auf oberster Ebene stehen für die Bereiche von Leistungsdaten. SPA zeigt Berichtsdaten, es gibt folgende Möglichkeiten:

* **Einzelner Wert** Schlüssel/Wert-Paar. Der Schlüssel ist eine Zeichenfolge, die die Bedeutung des Werts darstellt. Der Wert kann es sich um eine Zeichenfolge, die einen numerischen Wert oder ein boolescher Wert sein. Dies wird häufig verwendet, werden statische Informationen angezeigt, z. B., z. B. die CPU-Konfigurationsarchitektur, die Größe des gesamten Speichers und die BIOS-Version, die nicht im Laufe der Zeit ändern.

* **Auflisten Wert** Dies ist manchmal ein Schlüssel/Wert-Paar, aber der Listenwert kann mehrere Felder enthalten. Das Attribut der CPU kann z. B. in einer Tabelle mit mehreren Spalten und Zeilen angezeigt werden. Jede Zeile stellt eine CPU, und jede Spalte steht für ein Attribut der CPU.

* **Statistiken** kann einen speziellen Typ von den einmaligen Wert betrachtet werden. Es darf nur numerische Daten enthalten. Während des Zeitraums der Datensammlung schwanken, viele der numerischen Datenpunkte bleiben-Konstante. Die CPU-Auslastung ändert sich beispielsweise jedes Mal den PLA der Leistungsindikatoren gesammelt werden. Zeigt nur einen einzelnen Wert kann nicht die Situation Leistung genau wiedergeben. Anstatt nur ein Wert, Mittelwert, Maximum, Minimum und 90 % Wert verwendet werden für solche dynamische numerischen Datenpunkte. Der Wert 90 % stellt Aktivität bei oder über das 90. Perzentil für alle Ereignisse für diesen Indikator in dem Intervall für die angegebene Auflistung dar.

* **In der oberen Liste** enthält in der Regel den größten ressourcenverbrauchern eine bestimmte Ressource oder die obersten Entitäten, die bestimmte Ereignisse auftreten. Z. B. **Top 10 verarbeitet, in Bezug auf die durchschnittliche CPU-Auslastung** die Top 10-Prozesse mit der höchsten durchschnittlichen CPU-Auslastung im Zeitraum der Datensammlung enthält. Da die CPU-Nutzung wird sind auch einen dynamischen numerischen Datenpunkt, anderer Statistiken wie die maximale, minimale und 90 % Wert auch in der Liste aus, um dem Benutzer ein umfassenderes Bild von der CPU-Nutzung enthalten ist.

Wie in den vorherigen Abschnitten erwähnt, hängt der SPA PLA zum Sammeln von ETW-Ablaufverfolgung, WMI-Abfragen, Leistungsindikatoren, Registrierungsschlüssel und Konfigurationsdateien, um den Bericht zu generieren. Es ist wichtig, um die Datenquelle für jeden Datenpunkt im Bericht zu verstehen. SPA bietet solche Informationen über QuickInfos. Sie können auf die wichtige Spalten oder Zeilen an die Datenquelle QuickInfo zeigen. Z. B. **WMI:Win32\_DisDrive: Beschriftung** bedeutet, dass die Datenquelle aus einer WMI-Abfrage, die WMI-Klassennamen Win32\_Laufwerk, und die Eigenschaft ist **Beschriftung**.

### <a href="" id="side-by-side-report-"></a>Seite-an-Seite-Bericht

Einzelne Berichte liefern, Benachrichtigungen und Data-Abschnitt, um die Benutzer suchen mögliche Leistungsprobleme zu helfen, aber häufig ist es schwierig, ein mögliches Leistungsproblem zu identifizieren, indem Sie direkt auf einem einzelnen Bericht ansehen. Ein einzelner Bericht möglicherweise zu viele Datenpunkte enthalten, das macht es schwierig, die potenziellen Probleme zu finden.

Um dieses Problem zu beheben, stellt die SPA die Möglichkeit zum Vergleichen von zwei Berichte bereit. Sie können einen Bericht mit einem potenziellen Problem zu einem geplanten Bericht, um die Unterschiede zu finden, vergleichen.

Seite-an-Seite-Berichte können Start von einem einzelnen-Berichts-Viewer darstellen. Benutzer klicken können **Aktionen**, und klicken Sie dann auf **Berichte vergleichen** die Berichte auswählen. Es ist nur sinnvoll, die Berichte aus dem gleichen Advisor Pack verglichen werden soll. Sie können auswählen, vergleichen Sie den Bericht mit einem vorherigen Bericht, den Bericht für nächste Zeitpunkt, oder einen beliebigen Bericht, der über Suchfunktionen ausgewählt ist. Z. B. um anormales Verhalten zu isolieren, können Sie einen Basisbericht Server zu einem Bericht, der zu einem anderen Zeitpunkt auf dem gleichen Computer generiert wurde, oder zu einem Bericht, der generiert wurde, wird auf einem anderen Computer, die eine ähnliche Serverrolle und zu laden.

Ein Seite-an-Seite-Bericht entspricht weitgehend den einzelnen Bericht. Sie enthält einen Abschnitt für die Benachrichtigung und Datenabschnitte. Sie enthält die gleiche Anzahl von Benachrichtigungen und Datenabschnitte als einzelnen Berichts-Viewer. Der einzige besteht Unterschied darin, dass die Berichte in eine Seite-an-Seite Art und Weise angezeigt werden. Jeder Abschnitt enthält die Daten aus dem Quellbericht (1-Bericht) und des zielberichts (2-Bericht). Die Seite-an-Seite-Bericht zeigt den Namen das Advisor-Pack, den Namen des Zielservers (1 auf der linken Seite) und Bericht 2 auf der rechten Seite aus, die Zeit, die der Bericht generiert wurde, und die Dauer der Datensammlung für jeden Bericht.

Wenn Sie schließen die **finden** im Dialogfeld können Sie es reaktivieren durch Eingabe von STRG + F. Dieses Dialogfeld sucht und hebt Textzeichenfolgen innerhalb des aktuellen Bereichs.

Im Bereich "Benachrichtigungen", wenn keines der beiden Berichte, die verglichen werden die Ergebnisse ist eine Warnung, es finden Sie der **Warnung** Bereich. Andernfalls finden Sie die Ergebnisse in die **andere Benachrichtigungen** Bereich. Da der Schlüssel für eine Seite-an-Seite-Bericht zum Identifizieren von Unterschieden zwischen Berichten, wird keine ausführliche Informationen zu einer Regel angezeigt. Benutzer können den Regelnamen, um die Regel-Detail-Formulars für Weitere Informationen über die Regel anzuzeigen klicken.

In den Abschnitten Daten werden die Daten in einer Weise Seite-an-Seite mit Daten aus dem Bericht 1 auf der linken Seite und die Daten aus 2-Bericht auf der rechten Seite dargestellt. SPA zeigt einzelne Werte aus, in der gleichen Tabelle, jedoch anstelle von Spalten bezeichnen **Wert**, sie sind mit dem Namen **Bericht 1** und **Report 2** bzw. Der Seite-an-Seite-Bericht zeigt alle anderen Formen von Daten in Tabellen mit Seite-an-Seite.

Seite-an-Seite, Berichts-Viewer bietet auch QuickInfos zur Datenquelle.

### <a name="historical-and-trend-charts"></a>Verlauf und Trenddiagramme

Es ist nur sinnvoll, Trend und historische Diagramme für einen bestimmten Server und den bestimmten Advisor Pack angezeigt. Sie müssen den Zeitraum (der Standardwert für die letzte Woche verwendet wird), und klicken Sie auf **OK** , um den Trend und die Verlaufsdiagramm Viewer zu öffnen.

Der Trend und Verlaufsdiagramm Viewer enthält drei Registerkarten: Verlaufsdiagramm, 24-Stunden-Trenddiagramm und Trenddiagramm für 7 Tage.

### <a name="historical-chart"></a>Verlaufsdiagramm

Das Verlaufsdiagramm zeigt eine Reihe von Werten für einen bestimmten numerischen Daten mithilfe des angegebenen Zeitrahmens. Z. B. die **durchschnittliche anforderungswartezeit** für IIS auf einem einzelnen Server für die letzten 15 Tage. Jeder Datenpunkt in einem Verlaufsdiagramm stellt den Wert einer bestimmten Datenquelle, die in einer leistungssitzung Analyse benötigte dar.

Es gibt mehrere Möglichkeiten, ein Verlaufsdiagramm verwenden:

1.  Um Anomalien zu einem bestimmten Zeitpunkt für einen Datenpunkt beispielsweise jeden Tag um 2:00 Uhr zu finden. die **durchschnittliche anforderungswartezeit** von IIS springt von ca. 200 ms bis 500 ms.

2.  Können mehrere Datenpunkte zu korrelieren. Beispielsweise zeigt **durchschnittliche anforderungswartezeit** und **durchschnittliche Anforderungsanzahl** während der letzten 15 Tage zusammen. Der Bericht möglicherweise, die anzeigen, die Wartezeit für Anforderungen und die Anforderung Erhöhung der Anzahl der gleichzeitig erkennen, was darauf hindeuten kann, dass die Latenz Erhöhung der Anforderung durch einen Anstieg der Anforderungsanzahl verursacht wird.

In einem Verlaufsdiagramm können Benutzer Folgendes tun:

* Zeigen Sie mehrere Datenreihen im Diagrammbereich dargestellt. Jede Datenreihe wird als ein Liniendiagramm, in der Berichtanzeige angezeigt. Jedes Liniendiagramm wird automatisch im Berichts-Viewer entsprechend skaliert.

* Fügen Sie hinzu oder entfernen Sie eine Datenreihe aus der Liste am unteren Rand des Viewers Verlaufsdiagramm Reihe.

* Ein- oder Ausblenden einer Datenreihe in der Liste der Reihe. Benutzer können eine spezifische Datenreihe in der Liste, markieren Sie das entsprechende Diagramm der Zeile in den Diagrammbereich klicken.

* Vergrößern Sie sich auf einen bestimmten Zeitraum an, indem Sie die Auswahl des Zeitraums, in der Diagrammfläche. Klicken Sie zum Verkleinern, auf die Schaltfläche, die in der unteren linken Ecke des Diagramms befindet.

* Untersuchen Sie einen einzelnen Bericht durch Doppelklicken auf einen bestimmten Datenpunkt an.

* Kopieren Sie die Daten und für die anderen Programmen wie Microsoft Excel verfügbar gemacht. Dadurch können Sie Microsoft Excel Diagrammfunktionen, bei Bedarf nutzen können.

### <a name="trend-charts"></a>Trenddiagramme

Viele sich wiederholende Leistungsprobleme treten auf, durch periodische Aufgaben, die auf oder mit dem Zielserver ausgeführt wird. Z. B. eine Unterhaltung-oriented-Website erhalten möglicherweise weitere Treffer am Wochenende, oder ein Zeitplan Datenträger-Sicherungstask kann die Leistung eines Servers täglich um 02:00 Uhr heruntergefahren.

Ein Trenddiagramm soll solche Leistungsprobleme zu finden. Leistungsprobleme können in verschiedenen Mustern wiederholt auftreten. Die am häufigsten verwendeten Muster sind tägliche Muster und wöchentlichen Mustern, in denen Leistungsprobleme auftreten, während derselben Stunde eines Tages oder der gleichen Tag einer Woche. Aus diesem Grund bietet die SPA ein 24-Stunden-Trenddiagramm und ein 7-Tage-Trenddiagramm.

Die Trenddiagramm für die Analyse erhalten Sie ausführliche Untersuchung auf einem Satz von Daten und Trends basierend auf der Tageszeit sieht. Festlegen die X-Achse auf einen Zeitraum von 24 Stunden, beginnend mit 0:00 (Mitternacht) und endet um 23:59 Uhr. SPA wird Trends für mehrere Datenreihen zur gleichen Zeit nicht angezeigt werden. Klicken Sie auf **Datenreihe auswählen** , wählen Sie eine Datenreihe anzeigen.

Zum Verarbeiten der Daten, SPA sieht aus, für alle Momentaufnahmen, die zwischen 0:00 und 0:59, die für jede Stunde. SPA bestimmt das Minimum, Maximum, Mittelwert, und Sigma-Werte für die Gruppe von Momentaufnahmen während dieser Stunde, und stellt sie als Kerzendiagramme. SPA wiederholt den Prozess für Momentaufnahmen, die zwischen 1:00 bis 1:59, dann 2:00 bis 2:59 und So weiter. Wenn für die angegebene Stunde keine Momentaufnahmen vorhanden sind, werden SPA wird dieser Stunde im Diagramm leer gelassen und der nächsten Stunde erreicht.

Ein 7-Tage-Trenddiagramm ähnelt sehr der 24-Stunden-Trenddiagramm. Der einzige Unterschied ist, dass sie eine Datenreihe basierend auf dem Tag einer Woche anstelle der Tageszeit gruppiert.

Die Datenreihe, die Sie im Trend und historische Diagramme auswählen, werden als eine benutzereinstellung gespeichert. Das nächste Mal, den Trend und die Verlaufsdiagramm Viewer für das gleiche Advisor Pack geöffnet ist, der gleiche Satz von Datenreihen werden als Standard aufgeführt.

## <a name="managing-reports"></a>Verwalten von Berichten


### <a name="deleting-reports"></a>Löschen der Berichte

Berichte können entfernt werden, um die Anzahl der Berichte zu minimieren, die von SPA verwaltet werden müssen. Es wird empfohlen, abhängig von der Häufigkeit von Berichten und die Anzahl der Server die nicht benötigten Berichte gelöscht. Während der SPA keinen Grenzwert für Berichte verfügt, die sie verwalten können, müssen möglicherweise die zugrunde liegenden Datenbank eine größenbeschränkung.

**Beachten Sie** gelöschten Berichte können nicht wiederhergestellt werden.

 

### <a name="exporting-and-importing-reports"></a>Exportieren und Importieren von Berichten

Berichte können in eine XML-Datei an den Transport an einem anderen SPA-Konsole oder an e-Mail-Adresse, an einen anderen Benutzer exportiert werden. Exportieren des Berichts wird den Bericht nicht gelöscht werden. So exportieren Sie die aktuell angezeigten Berichts aus **Berichts-Viewer**, klicken Sie auf **Aktionen**, und klicken Sie dann auf **exportieren**. So exportieren Sie mehrere Berichte aus **Berichts-Explorer**, klicken Sie auf **aktivieren Mehrfachauswahl**, wählen Sie mehrere Berichte aus dem Auswahlfeld aus, und klicken Sie dann auf **exportieren**. Dadurch wird die Berichte im XML-Format in das ausgewählte Ziel-Verzeichnis exportiert.

Ein exportierter Bericht kann in einseitigen Anwendung angezeigt werden. importierten Berichte werden nicht in die SPA-Datenbank hinzugefügt. Sie sind in erster Linie als eine XML-Viewer-Anwendung für den exportierten Bericht verwendet werden sollen. Der Server für den importierten Bericht muss nicht die gleichen Advisor Packs als der ursprüngliche exportierten Bericht SPA-Konsole installiert haben.

## <a href="" id="bkmk-manageadvisorpacks"></a>Verwalten von Advisor-packs


SPA schließt die Advisor-Packs für die Core-Betriebssystem, Hyper-V, active Directory und IIS. SPA bietet eine offene Architektur für die Entwicklung von Advisor-Packs mithilfe von SQL, daher ist es auch möglich, dass nicht-Microsoft-Entwicklern zum Erstellen von Advisor-Pack-Versionen. Es gibt vier Optionen zum Verwalten von Advisor-Pack: bereitzustellen, anzupassen, zurückzusetzen oder zu entfernen.

### <a name="provision-new-advisor-packs"></a>Bereitstellen des neuen Advisor-packs

Neues Advisor-Packs können von Microsoft oder von nicht-Microsoft-Entwicklern freigegeben werden. Ein Advisor-Pack umfasst eine provisionMetaData.xml und einen Satz von SQL-Skripts, die die Logik zu beschreiben.

**Ein neues Advisor-Pack bereitstellen.**

1.  Kopieren Sie den Inhalt der Advisor-Pack unter der *SpaRoot %*\\APs-Verzeichnis.

2.  Klicken Sie im Hauptfenster auf **Konfiguration**, und klicken Sie dann auf **konfigurieren Advisor Packs**. Die **konfigurieren Advisor Packs** Dialogfeld wird geöffnet.

    **Hinweis** dieses Dialogfeld ist ähnlich wie die **Bereitstellen von Advisor-Pack** Seite zum ersten Mal verwenden-Assistenten. Es zeigt eine Liste von Advisor-Packs, die zur Verwaltung verfügbar sind. Jede in der Liste Advisor-Pack verfügt über Eigenschaften wie Name, installierte Version, Version und Autor. Name ist der vollständige Name des Advisor-Pack, und die installierte Version ist die Version dieses Advisor-Pack, das bereits im Projekt bereitgestellt wurde. Wenn das Advisor-Pack in der aktuellen Datenbank nicht bereitgestellt wurde, zeigt das Textfeld für die installierte Version **unterlassen**. Das Feld "Version" gibt an, die Version dieses Advisor-Pack, die unter dem Advisor-Packs-Ordner abgelegt wird.

     

3.  Wählen Sie das Advisor-Pack aus der Liste aus. Wenn das Advisor-Pack nicht bereitgestellt wurde oder eine neuere Version vorhanden, in den Advisor-Packs-Ordner als dem in der Datenbank ist, die **bereitstellen** Schaltfläche ist aktiviert. Klicken Sie auf die **bereitstellen** Schaltfläche.

4.  Wenn die Bereitstellung abgeschlossen ist, ist die **installierte Version** Feld für das ausgewählte Advisor-Pack die Informationen zur neuen Version enthält.

### <a name="customize-advisor-packs"></a>Anpassen von Advisor-packs

SPA definiert, eine offene Architektur, die Benutzern das Ändern des Advisor-Packs ermöglicht. Benutzer können die Advisor-Pack-Dateien ändern, durch Ändern der Schwellenwerte, Schwellenwerte für die Freigabe und aktivieren oder Deaktivieren von Regeln.

Weitere Informationen zum Ändern und Erstellen von Advisor-Packs finden Sie unter [Server Performance Advisor Pack Development Guide](server-performance-advisor-pack-development-guide.md).

### <a name="changing-thresholds"></a>Ändern der Schwellenwerte

Schwellenwerte werden in einseitigen Anwendung verwendet, um festzustellen, ob der Trigger eine Regel erfüllt wird. Die tatsächliche Schwellenwerte für real Kundenszenarien können unterscheiden sich erheblich aufgrund der arbeitsauslastung, hardwareumgebung, und Ihr Unternehmen benötigt. Die Standardschwellenwerte möglicherweise nicht ordnungsgemäße für den aktuellen Benutzerfall, werden, damit die SPA so ändern Sie den vorhandenen Schwellenwert bietet.

Sie können Schwellenwerte ändern, indem Sie auf den Regelnamen in einem einzelnen oder Seite-an-Seite. Oder um alle Regeln einer bestimmten Advisor Pack zu verwalten, können sie ändern, Schwellenwerte aus den **Konfiguration** Menü.

**Um einen Schwellenwert zu ändern.**

1.  In der **Konfiguration** Menü klicken Sie auf **Advisor-Packs konfigurieren**, klicken Sie auf den Namen der geändert werden, und klicken Sie dann auf die Advisor-Pack **konfigurieren**.

    **Beachten Sie** werden Ihnen eine Liste aller Regeln, die im Advisor Pack enthalten sind. Das Kontrollkästchen links neben der Advisor-Pack-Name Gibt an, ob die Regel aktiviert ist. Wenn eine Regel deaktiviert ist, wird es aus allen Berichten ausgeblendet.

     

2.  Klicken Sie auf die spezielle Regel, die Sie ändern möchten. Die **Regeldetails** bilden, für die ausgewählte Regel wird geöffnet.

Die Regel Detailformular enthält ausführliche Informationen über eine bestimmte Regel. Sie enthält den Namen, Beschreibung, Status, Ergebnisse und Schwellenwerte. SPA unterstützt zwei Arten von Regelergebnissen, **Warnung** und **OK**. Für jeden Typ besteht Empfehlungen Text und die Empfehlung vor.

Einige der Regeln verfügen nicht über die angegebenen Schwellenwerte. Z. B. die **HTTP-Keep-Alive** Regel überprüft eine boolesche Einstellung für IIS. Daher kann die Schwellenwerte-Liste leer sein. Andernfalls alle Schwellenwerte, die von der aktuellen Regel verwendet werden wird aufgeführt. Eine ausführliche Beschreibung zur Verwendung ein Schwellenwerts in der Regel ist als Teil der Beschreibung enthalten.

Wenn die **Regeldetails** Formular gestartet wird die **Konfiguration** im Menü die Schwellenwert-Liste enthält drei Spalten: Name, die ursprüngliche Einstellung und die Einstellung ändern. Wenn sie von einem einzelnen oder Seite-an-Seite gestartet wird, sind die Schwellenwerte, die vom Bericht verwendet werden ebenfalls enthalten sein. Benutzer können die aktuellen Schwellenwerte ändern, durch Ändern des Werts in **ändern Sie Einstellung** Spalte, und klicken Sie dann auf **speichern** zum Speichern der Änderungen in die Datenbank.

Alle Änderungen, die an die Schwellenwerte wird nur angewendet, Berichte, die nach der Änderung der generiert werden. Vorhandene Berichte werden nicht von diesen Änderungen betroffen.

### <a name="sharing-thresholds"></a>Freigeben von Schwellenwerten

Wenn Sie Ihre Server in ähnlichen Situationen verwalten, können Sie mit den gleichen Satz von Schwellenwerte auswählen. Exportieren und importieren Sie die Schwellenwerte für ein bestimmtes Advisor Pack mithilfe der **Konfiguration** Menü. Sie können wählen Sie das spezifische Advisor-Pack, und klicken Sie dann auf **konfigurieren**. Die exportierte Schwellenwert-Datei ist in einem XML-Format.

Wenn Sie einen Schwellenwert zu importieren, SPA überprüft das Format der XML-Datei, und überprüft, ob die Datei auf das ausgewählten Advisor-Pack entspricht. Wenn dies erfolgreich ist, importiert SPA alle Werte aus der Schwellenwert-Datei in die aktuelle Projektdatenbank an. Ähnlich wie beim vorherigen Szenario für veränderliche Schwellenwerte, werden alle Änderungen der Schwellenwert nur Auswirkungen auf Berichte, die in der Zukunft generiert werden. Vorhandene Berichte sind nicht betroffen.

### <a name="enable-or-disable-rules"></a>Aktivieren oder Deaktivieren von Regeln

Eine Regel kann aktiviert oder deaktiviert die **Regeldetails** Formular. Sie müssen auf **speichern** vorgenommenen Änderungen beibehalten werden. Wenn eine Regel deaktiviert ist, ist es nicht auf einen der Berichte angezeigt werden. Aber die zugrunde liegende Geschäftslogik wird ausgelöst, beim Erstellen des Berichts, damit bei der Auswahl, um die Regel erneut zu aktivieren, diese in Berichte erneut wird angezeigt.

### <a name="reset-advisor-packs-to-original-state"></a>Advisor-Packs zum ursprünglichen Zustand zurücksetzen

Sie können eine bereitgestellte Advisor-Pack in der Datenbank zu ändern. Als ändern die Schwellenwerte, können Sie auch die SQL-Skripts ändern. SPA unterstützt ändern Berichtsmetadaten hinzufügen oder Entfernen von Regeln für eine bereitgestellte Advisor-Pack nicht. Manuelles Ändern von Bereichen kann zu unerwartetem Verhalten führen.

Weitere Informationen zum Ändern eines bereitgestellten Advisor Packs finden Sie unter den [Server Performance Advisor Pack Development Guide](server-performance-advisor-pack-development-guide.md).

Wenn Sie ein Rollback vorgenommenen Änderungen auf einem bereitgestellten Advisor Pack möchten, können Sie auswählen, das Advisor-Pack zurücksetzen. Dies überschreibt die SQL-Skripts, die beziehen sich auf dem Advisor-Pack und alle Schwellenwerte Standardwerte zurückgesetzt. Auf diese Weise alle vorhandenen Berichte.

Zurücksetzen der Advisor-Pack können Sie dazu die **konfigurieren Advisor Packs** Formular. Sie müssen auf dem Advisor-Pack zurückgesetzt werden, und klicken Sie dann auf **zurücksetzen**.

### <a name="remove-advisor-packs"></a>Entfernen von Advisor-packs

Wenn ein Advisor-Pack nicht mehr benötigt wird, können Benutzer aus der Datenbank entfernen. Das Advisor-Pack entfernen, wird alles über das Advisor-Pack aus der Datenbank, einschließlich der Regeln und Schwellenwerten, alle SQL-Skripts und alle Berichte entfernt. Keine der Aktionen können ein Rollback ausgeführt werden.

Entfernen das Advisor-Pack können Sie dazu **konfigurieren Advisor Packs** Formular. Sie müssen entfernt werden soll, und klicken Sie dann auf die Advisor-Pack auswählen **Deprovision**.

### <a name="update-existing-advisor-packs"></a>Aktualisieren von vorhandenen Advisor-packs

Aktualisieren von vorhandenen Packs für Advisor ist sehr ähnlich ist, auf das Advisor-Pack in seinen ursprünglichen Zustand zurücksetzen. Um die Advisor-Pack auf eine neuere Version zu aktualisieren, kopieren Sie das neue Advisor-Pack für den Advisor-Pack-Ordner ein. Ein Advisor-Pack ist ein Update für ein vorhandenes Advisor Pack betrachtet, nur, wenn keine Änderung der Bericht. Der Bericht und den Regeln-IDs müssen identisch sein. Andernfalls sollten sie als zwei unterschiedliche Advisor Packs behandelt werden.

Wenn nur Änderungen von Unternehmen, Logik und keine Berichtsserver-Metadaten-Änderungen für eine Advisor-Pack vorhanden sind, sollten sie eine neue Versionsnummer, z. B. von 1.0 auf 2.0 zugewiesen werden. Bei Änderung der Bericht wird das Advisor-Pack einen anderen Namen für die vollständige anzugeben. Beispielsweise könnte die Microsoft.ServerPerformanceAdvisor.IIS.V1 in Microsoft.ServerPerformanceAdvisor.IIS.V2 geändert werden.

Wenn eine neuere Version von Advisor-Pack vorhanden ist, die Liste in der **Advisor-Packs konfigurieren** Formular automatisch ausgefüllt wird, die **Version** Spalte mit der neuesten Version von Advisor Pack. Sie können wählen Sie das Advisor-Pack, und klicken Sie dann auf die **zurücksetzen**. Der Advisor-Pack-Updates mit dem neue Geschäftslogik und Schwellenwerte. Alle Berichte für dieses Advisor Pack werden beibehalten.

## <a name="managing-servers"></a>Verwalten von Servern


SPA bietet grundlegende Funktionen für die Verwaltung von Zielservern. Sie können auch neue Server hinzufügen, um die Liste mit den Zielservern, Server aus der Liste zu entfernen oder ändern die Hinweise für Server.

**Hinzufügen oder Entfernen von Servern aus, oder Ändern von Serverinformationen**

1.  Klicken Sie auf die **Konfiguration** Menü klicken Sie auf **-Server konfigurieren**.

2.  In der Liste der Server, die derzeit in der Datenbank vorhanden ist, ist die letzte Zeile leer. Klicken Sie auf die Zeile, und die Felder auszufüllen. Die **Servernamen** und **Speicherorts der Dateifreigabe** Ordner Felder sind obligatorisch, und der Servername muss eindeutig sein.

3.  Geben Sie andere Serverinformationen in den **Anmerkung** Spalte für jeden Server.

    **Beachten Sie** dieses Feld einem freien Text-Format verwendet, damit Sie sie als ein Feld "Beschreibung" verwenden können. Oder verwenden Sie dieses Feld auf um die Servern zu kennzeichnen, sodass sie problemlos im Hauptfenster oder Gruppe von Servern, z. B. von Speicherort oder die Serverrolle gefunden werden können.

     

4.  Wenn Sie die SPA mit einer großen Anzahl von Servern verwenden möchten, unterstützt SPA eine durch Trennzeichen getrennte (.csv)-Format für den Import an. Die Datei muss mindestens zwei Felder enthalten: **Server** und **Speicherort der Dateifreigabe**. Das dritte Feld **Anmerkung** ist optional, aber es wird empfohlen, die Server zu organisieren. Sie können auch die Liste der Server exportieren, um eine CSV-Datei, um zu bestimmen das geeignete Format aus, oder die Serverkonfiguration sichern.

### <a name="searching-and-filtering"></a>Suchen und Filtern

Wenn Sie mehr als ein paar Server verwalten, bietet SPA basic-Support, um die Server im Hauptfenster von schnell zu finden. Klicken Sie auf die Spalte zu sortieren, anhand der Servername, Analyseergebnisse, aktuellen Aufgabenstatus oder "Hinweise". Sie können auch auswählen, um die Suchfunktion verwenden. In der oberen rechten Ecke der wichtigsten Windows können Sie eine zu suchende Zeichenfolge eingeben. Die **Zielserver** Liste im Hauptfenster von verwendet die Zeichenfolge aus, um die Server zu filtern und zeigt nur auf Servern mit Namen oder die Anmerkung Felder, die die Suchzeichenfolge enthält.

Die folgende Abbildung zeigt, wie die Zeichenfolge **DelL** Server mit der Zeichenfolge entspricht **DelL** oder Server mit **Anmerkung** Feld mit **DelL**.

![Suchen und Beispiel für das Filtern](../media/server-performance-advisor/spa-user-manual-find-search-example.png)

## <a name="advanced-functionality"></a>Erweiterte Funktionen


### <a name="working-with-spa-windows-powershell-cmdlets"></a>Verwenden von SPA-Windows-PowerShell-cmdlets

Die SPA-Konsole verfügt über Unterstützung über die Benutzeroberfläche für die Sammlung von sich wiederholenden. Wenn diese Funktion nicht für Ihre Umgebung ausreichend ist, sind Windows PowerShell-Cmdlets, die ein erweiterten Administrator zum Anpassen der Datensammlung verwenden können. Diese Windows PowerShell-Cmdlets ermöglichen Systemadministratoren automatisch durchführen einer Leistungsanalyse für Zielserver, und Verwenden von SPA für den remote-Kundensupport. Systemadministratoren können z. B. Skripts, die zum Aufrufen von SPA-Cmdlets in bestimmten Zeitintervallen in regelmäßigen Abständen Stichproben für den Namen der leistungsbedingung von Zielservern schreiben.

Es wird empfohlen, schließen Sie die Anwendung SPAConsole.exe vor der Verwendung dieser Cmdlets.

Bevor Sie alle Windows PowerShell-Cmdlets ausführen müssen Sie die Cmdlets auf dem Computer-Konsole registrieren.

**Registrieren Sie die Windows PowerShell-cmdlets**

1.  Geben Sie an einer Windows PowerShell-Eingabeaufforderung **registerSpaCmdlets.cmd**. Die **SPA-Cmdlets wurde erfolgreich registriert** Meldung wird angezeigt.

2.  Führen Sie **SPA-PowerShell.cmd**. Wenn Sie den Pfad zum Windows PowerShell-Skriptdatei übergeben, sie führen Sie die Skripts automatisch. Andernfalls öffnet sie eine Windows PowerShell-Eingabeaufforderung, die wodurch die SPA Windows PowerShell-Cmdlets ausgeführt werden kann.

Die folgende Tabelle beschreibt die SPA Windows PowerShell-Cmdlets:

| Cmdlet-Name | Parameter | Beschreibung |
| ------ | ------- | ------ |
| Start-SpaAnalysis | **– ServerName** Name des Zielservers.<br>**-AdvisorPackName** vollständigen Namen des dem Advisor-Pack auf Server in die Warteschlange gestellt werden. Wenn mehr als eine Pack die gleichzeitige Ausführung geplant ist, sollte der Wert des Parameters als AP1name, AP2name formatiert werden.<br>**-Dauer** Dauer für die Datensammlung.<br>**-Credential** Benutzeranmeldeinformationen für das Konto, das die Datensammlung auf dem Zielserver ausgeführt wird.<br>**-SqlInstanceName** Name der SQL Server-Instanz.<br>**-SqlDatabaseName** Namen der Datenbank ein SPA-Projekt. | Startet eine sammlungssitzung der SPA-Daten auf dem angegebenen Server. |
| Stop-SpaAnalysis | **-SqlInstanceName** Name der SQL Server-Instanz.<br>**-SqlDatabaseName** Namen der Datenbank ein SPA-Projekt.<br>**– ServerName** Name des Zielservers. | Versucht, eine ausgeführte SPA-Sitzung zu beenden. Wenn eine Sitzung bereits abgeschlossen wurde, wird ohne Benutzereingriff zurückgegeben. |
| Get-SpaServer | **-SqlInstanceName** Name der SQL Server-Instanz.<br>**-SqlDatabaseName** Namen der Datenbank ein SPA-Projekt. | Ruft die Liste der Server in der Datenbank ab. Es gibt eine Liste von Objekten, einschließlich der folgenden Eigenschaften: Name, Status, Dateifreigabe und Anmerkung. |
| Get-SpaAdvisorPacks | **-SqlInstanceName** Name der SQL Server-Instanz<br>**-SqlDatabaseName** Namen der Datenbank ein SPA-Projekt | Ruft die Liste der Advisor-Pack in der Datenbank ab. Es gibt eine Liste von Objekten, einschließlich der folgenden Eigenschaften: Name, "DisplayName", Autor und Version. |

Windows PowerShell bietet die Möglichkeit zum Übergeben von Anmeldeinformationen über verschlüsselte Dateien, um Automatisierungsszenarios zu ermöglichen. Weitere Informationen zur Verwendung von verschlüsselter Dateien Anmeldeinformationen an ein Cmdlet übergeben, finden Sie unter [Erstellen von Windows PowerShell-Skripts, Anmeldeinformationen akzeptieren](https://technet.microsoft.com/magazine/ff714574.aspx).

### <a name="automating-spa-report-collection-by-using-windows-powershell"></a>Automatisieren von SPA-berichtsauflistung mithilfe von Windows PowerShell

Die folgenden Verfahren stellen ein Beispiel für eine Auflistung der SPA-Bericht mithilfe der SPA Windows PowerShell-Cmdlets automatisieren.

Anmeldeinformationen des Benutzers können verschlüsselt und über Windows PowerShell zwischengespeichert werden. Diese Anmeldeinformationen werden verwendet, zum Anmelden an Remoteserver. Obwohl nicht spezifisch für die SPA, wird im folgenden Beispiel wird diese Technik veranschaulicht:

``` syntax
$fileName = 'D:\temp\operator.txt'
$userName = 'domainname\operator'
 
# save credential to file
$(Get-Credential).Password | convertFrom-SecureString | Set-Content $fileName
 
# load credential from file
$credential = New-Object System.Management.Automation.PsCredential $userName, $(Get-Content $fileName | convertTo-SecureString)
 
# run command
.\start-SpaAnalysis  ServerName: Server1  Credential: $credential  AdvisorPackName:Microsoft.ServerPerformanceAdvisor.CoreOS.V1 10  Duration:10  SqlInstanceName: .\SQLExpress  SqlDatabaseName:SPA8294
```

Bevor Sie diese Datei ausführen können, müssen Sie ausführen **Set-Executionpolicy RemoteSigned**

Sie können es über eine Batchdatei mit dem folgenden Befehl ausführen:

``` syntax
PowerShell -command "& '.\RunSpa.ps1' "
```

### <a name="use-t-sql-to-generate-reports"></a>Verwenden von T-SQL zum Generieren von Berichten

SPA-Berichtsdaten können extrahiert werden, mithilfe von SQL zum Erstellen von benutzerdefinierter Berichten nicht, die innerhalb der SPAConsole.exe bereitgestellt werden.

Beispielsweise bietet die folgende T-SQL-Befehl eine Top 10-Liste der Server CPU-Nutzung für den Zeitrahmen für den letzten drei Tagen:

``` syntax
select TOP 10
   MachineName,
   AverageCpu
FROM (
   select
      __MachineName MachineName,
      AVG(AverageValue) AverageCpu
   FROM [SPA].[Microsoft.ServerPerformanceAdvisor.CoreOS.V1].vwCpuPerformance
   WHERE __Creationtime > dateadd(DAY, -3, GETUTcdate())
      AND Name = N'% Processor time' AND CpuId = N'_Total'
   GROUP BY __MachineName
) t
OrdER BY t.AverageCpu DESC 
```

### <a name="working-with-multiple-projects"></a>Arbeiten mit mehreren Projekten

In einigen Fällen empfiehlt es sich um SQL Server-Datenbanken zu partitionieren, die von SPA verwendet werden. Dies kann helfen, Verringerung der Datengröße der SQL Server-Datenbank oder Ihnen bei die Server logisch partitioniert. In diesen Fällen unterstützt die SPA-Konsole mehrere Projekte. Sie können eine neue Projektdatenbank erstellen, indem Sie auf **Datei**, und klicken Sie dann auf **neues Projekt**. Der ersten Verwendung angezeigt verwenden-Assistenten, um die neue Projektdatenbank zu erstellen.

Nachdem die Projekte erstellt wurden, können Sie klicken **Datei**, und klicken Sie dann auf **geöffneten Projekt** zwischen Projekten zu wechseln. Die SPA-Konsole lässt sich nicht darauf aus, wechseln von Datenbanken, wenn ausstehende Leistungsanalyse in der aktuell geöffneten Projekt ausgeführt wird. Dadurch wird die Integrität der Leistungsdaten zu schützen.

Wenn Sie eine neue Projektdatenbank erstellen oder öffnen Sie eine anderes Projektdatenbank auswählen, wird das aktuelle Projekt geschlossen. Alle Berichte, die geschlossen werden, wenn das aktuelle Projekt geschlossen wird.

**Beachten Sie** SQL Server 2008 R2 Express ist auf 10 GB-Datenbank beschränkt. Mit mehreren Projekten, können Sie verwenden eine oder mehrere SQL Server-Datenbanken und bleiben unter die Grenze von 10 GB SQLServer 2008 R2 Express.

 

### <a name="logging-and-debugging"></a>Protokollierung und Debuggen

SPA stellt grundlegende Protokollierungsfunktionen bereit. Es kann nur Protokolle in eine Protokolldatei geschrieben werden, die sich im gleichen Ordner wie SPAConsole.exe befindet. Das Benutzerkonto, das die SPA-Konsole ausgeführt wird, muss Schreibberechtigungen für den Ordner verfügen, auf dem SPA installiert wurde, um sicherzustellen, dass die Protokolle in die Protokolldatei geschrieben werden können.

SPA enthält die folgenden gültigen Protokollebenen:

* **Nur zu Informationszwecken** sichert die Protokolle für jede Aktion, nimmt der SPA-Konsole, und es dient in erster Linie für Debugzwecke.

* **Warnung** protokolliert alle Fehler und Ausnahmen, die in der SPA-Konsole geschehen. Einige Fehler sind einfach Überprüfungsfehler, die von der SPA-Konsole verarbeitet werden können.

* **Kritische** protokolliert nur Fehler und Ausnahmen, die von der SPA-Konsole nicht behandelt werden können. In diesen Fällen dazu führen, dass die SPA-Konsole zu einem Absturz. Die Protokolle bieten die Kontextinformationen für solche Fehler.

In der Standardeinstellung die Protokollebene "Warnung" das bedeutet, dass SPA nur protokolliert, Fehlern und Ausnahmen, die in der SPA auftreten und. Die Protokollebene kann geändert werden, durch Bearbeiten der **SpaConsole.exe.config** Datei im gleichen Ordner wie SpaConsole.exe befindet. Alle Protokolle werden in die Datei "log.txt" im gleichen Ordner geschrieben.

SPA enthält auch einige grundlegende Funktionen für das Debuggen. Um für die SPA-Debuggen zu aktivieren, müssen Benutzer die SPA Project-Datenbank manuell zu ändern. Die Einstellung wird in einer Tabelle gespeichert. Benutzer müssen die folgende SQL-Skript, um das SPA-Projekt, um den Debugmodus zu ändern:

``` syntax
UPdate [Configurations] SET Value = N'true' WHERE Name = N'Debugmode'.
```

Im Debugmodus befindet behält die SPA-Framework die temporären Daten, die während der Leistungsanalyse generiert wird, damit Sie Probleme in den Advisor-Packs beheben können. Dieses Skript dient in erster Linie von Advisor-Pack-Entwicklern verwendet werden.

Weitere Informationen zu den Funktionen zum Debuggen in einseitigen Anwendung, finden Sie unter den [Server Performance Advisor Pack Development Guide](server-performance-advisor-pack-development-guide.md).

### <a name="managing-the-database"></a>Verwalten der Datenbank

### <a name="backup-and-restore-the-database"></a>Sichern und Wiederherstellen der Datenbank

Die SPA-Konsole bietet keine Funktionen zum Sichern und Wiederherstellen der SPA-Datenbank. Sie sollten die standard-Microsoft SQL Server-Tools und Skripts verwenden, Sichern und Wiederherstellen von Datenbanken.

### <a name="clean-up-the-database"></a>die Datenbank bereinigen

Die SPA-Projekt-Datenbanken können groß werden, während Weitere Informationen zur Leistungsanalyse ausgeführt wird. Standardmäßig behält SPA alle Berichte. Sie sollten so entfernen Sie alte Berichte, um die Leistung zu verbessern. Sie können Berichte durch Löschen der **Berichts-Explorer** Schnittstelle.

## <a name="privacy-and-security"></a>Datenschutz und Sicherheit


SPA unterstützt nur die Datensammlung vom Zielserver in der SPA-Konsole. Es dient nicht zum Senden von Informationen an Microsoft oder Microsoft-fremden Entwicklern. Weitere Informationen zum SPA-Datenschutz finden Sie in der Microsoft-Software-Lizenzbedingungen für Server Performance Advisor.

Alle Daten, die von SPA gesammelt werden, wird in den Projektdatenbanken gespeichert. Aufgrund der Art eines Teils der ETW-ablaufverfolgungen erfasst SPA u. u. vertraulichen Informationen, der hohe geschäftliche Priorität haben könnte. Sie sollten die potenziellen Risiken im Zusammenhang mit der Freigabe des Zugriffs auf die Datenbanken der SPA-Projekt kennen. Temporäre Dateien werden in den freigegebenen Ordnern gespeichert, die auf jedem Zielcomputer angegeben werden. Obwohl SPA versucht So löschen Sie diese temporäre Log-Dateien nach Abschluss des Datenimports, es gibt keine Garantie, dass diese Protokolldateien werden immer gelöscht werden. Sie sollten sicherstellen, werden, dass die freigegebenen Ordner an sicheren Orten befinden.

Advisor-Packs SPA enthält SQL-Skripts zu analysieren und von Leistungsprotokollen zum Generieren von Leistungsberichten zu analysieren. SPA versucht, die der Berechtigung, diese Skripts ausgeführt beschränken. Es ist jedoch immer noch eine Möglichkeit, dass die Skripts können vertrauliche Informationen über die SPA von Zielservern, sammeln oder Abrufen oder ändern vertrauliche Informationen, die in der gleichen Datenbank der SPA-Projekt gespeichert ist. Sie müssen sicherstellen, dass die Advisor-Packs, die in der SPA-Projektdatenbank bereitgestellt werden von vertrauenswürdigen Quellen stammen.

## <a name="errors-and-troubleshooting"></a>Fehler und Problembehandlung


### <a name="spaconsoleexe-does-not-start-or-write-log-file"></a>SPAConsole.exe nicht starten oder Protokolldatei zu schreiben

Wenn Sie versuchen, SPAConsole.exe zum ersten Mal ausführen, wenn .NET Framework nicht installiert ist, die Anwendung nicht starten oder eine Protokolldatei schreiben. Stellen Sie sicher, die einen compatible.NET, die Framework installiert ist und die Arbeit ordnungsgemäß vor der Installation von SPA.

### <a name="locating-log-information"></a>Suchen von Protokollinformationen

SPA speichert Fehlerinformationen, in der Datei "log.txt" in der SPA-Ordner. detaillierte Fehlermeldungen und Aufruflisteninformationen werden in diesen Ordner geschrieben. Wenn Fehler, die Weitere Informationen zum Interpretieren auftreten, können Sie die Datei um die Fehlerdetails finden Sie unter "log.txt" öffnen.

### <a name="database-size-limitations-for-sql-server-express"></a>Einschränkungen hinsichtlich der Datenbankgröße für SQL Server Express

SQL Server Express hat eine größenbeschränkung von 10 GB für eine Benutzerdatenbank. Diese Größe Datenbank hat die Kapazität zum Speichern von Berichten von 20.000-30.000. Um die Möglichkeit, durch Erreichen dieses Grenzwerts für die Datenbank zu reduzieren, empfehlen wir regelmäßig Löschen von Berichten, bzw. mit einer anderen Version von SQL Server, die nicht über die Beschränkung auf 10 GB Benutzer Datenbank verfügt.

### <a name="sql-server-express-log-size-and-disk-capacity"></a>SQL Server Express Größe und die Datenträger Protokollkapazität

Wenn Sie SQL Server Express verwenden, wird die Benutzerdatenbank auf 10 GB beschränkt ist, aber die entsprechende Protokolldatei kann 70 GB überschreiten. Aus diesen Gründen empfehlen wir mindestens 100 GB an freiem Festplattenspeicher verfügbar für SQL Server Express ein. Dieser Speicherplatz sollte ausreichen, um ungefähr 20.000 zu 30.000 Berichte gespeichert. Diese Datei heißt SPADB\_log.ldf, und es befindet sich **%Program Files%\\Microsoft SQL Server\\MSSQL10. SQLEXPRESS\\MSSQL\\Daten**.

### <a name="failure-to-connect-to-target-server"></a>Fehler beim Verbinden zum Zielserver

Beim Ausführen der Leistungsanalyse auf Zielservern muss das Benutzerkonto, das die SPA-Konsole ausgeführt wird, bestimmte Berechtigungen auf den entsprechenden datensammlersatz, PLA auf den Zielservern in die Warteschlange. Windows-Firewall-Einstellungen müssen auch geändert werden, um PLA Kommunikation zu durchlaufen. Ausführliche konfigurationsanweisungen, finden Sie unter [Einrichten der SPA](#bkmk-setupspa).

### <a name="failure-to-create-pla-data-collection-set-on-the-target-server"></a>Fehler beim Erstellen von PLA Datensammlungssatz auf dem Zielserver

Wenn Sie erhalten eine kann nicht auf Server Zielnachricht erstellen PLA Datensammlungssatz, stellen Sie sicher, dass die folgenden Schritte ausführen:

* Stellen Sie sicher, dass die **Leistungsprotokolle und Warnungen** -Dienst wird ausgeführt

* Die sicherheitseinstellung **Netzwerkzugriff: Speicherung von Kennwörtern und Anmeldeinformationen für die Netzwerkauthentifizierung nicht zulassen** ist deaktiviert. Die sicherheitseinstellung muss deaktiviert sein, da die SPA muss die Anmeldeinformationen des Benutzers zu verwenden, um den Datensammlungssatz auf dem Zielserver erstellen.

### <a href="" id="running-spa-against-the-console-"></a>SPA für die Konsole ausführen

PLA durchläuft einen anderen Kanal aus, wenn der Zielserver die SPA-Konsole identisch ist. Auch wenn das Benutzerkonto, das die SPA-Konsole mit Administratorrechten ausgeführt wird, schlägt die PLA fehl. Wenn die SPA-Konsole auf einem Zielserver installiert ist, müssen Benutzer zum Starten der SPA als Administrator aus, um sicherzustellen, dass die Performance Analysis-Task in der Konsole ausgeführt werden kann.

### <a name="running-multiple-consoles-at-the-same-time"></a>Mehrere Konsolen ausführen zur gleichen Zeit

SPA unterstützt nicht mehrere Konsolen, die für dieselbe Datenbank SPA-Projekt zur gleichen Zeit ausgeführt. SPA bietet auch keine den Sperren und Synchronisierung Mechanismus, um es zu verhindern. Wenn zwei SPA-Konsolen, die zur gleichen Zeit ausgeführt werden, wird die Konsole inkonsistent je nach der Zeit-Sequenz Verhalten, die diese SPA-Konsolen ausgeführt werden. Um dies zu verhindern, sollten alle in der Warteschlange Performance Analysis-Sitzungen aus der Liste entfernt werden, bevor sie von der Konsole verarbeitet wird, die die Analyse wird gestartet.

SPA schützt die Integrität der einzelnen Berichte, die von SPA erfolgreich generiert wird. zur gleichen Zeit garantiert SPA nicht, dass alle in der Warteschlange Analyseaufgaben abgeschlossen sind. Wenn inkonsistenten statusänderungen werden für die Analyse von leistungssitzungen angezeigt, oder Suchen von Fehlern, die den Anspruch können nicht Leistungsprotokolle, die vom datensammlersatz generiert werden, ist es wahrscheinlich über mehrere Instanzen des SPA-Konsole ausgeführt wird, für dieselbe verursacht werden SPA Project-Datenbank.

SPA Windows PowerShell-Cmdlets ausführen kann auch durch eine SPA-Konsole beeinträchtigt werden, die für die gleiche SPA-Datenbank ausgeführt wird. Es wird empfohlen, dass Sie die SPA-Konsole schließen, bevor Sie die SPA Windows PowerShell-Cmdlets ausführen.

### <a name="spaconsoleexe-recurring-collection-is-disrupted"></a>Wiederholte SPAConsole.exe-Sammlung ist unterbrochen.

Beim Ausführen der SPAConsole.exe, und einer sich wiederholenden datenauflistung (z. B. eine stündliche Sammlung verwenden), sollte der Server, der die SPAConsole.exe ausgeführt wird, ihn anzuhalten, kann nicht im Energiesparmodus sein. SPA wird für einen Energiesparmodus über die Richtlinie nicht überprüft werden. Der Erfassung von regulären wiederkehrenden kann diese angehaltene Aktivität unterbrochen werden.

### <a name="lost-etw-events"></a>Verloren gegangene ETW-Ereignisse

Um Auswirkungen auf die minimale Leistung auf einem Zielserver zu erstellen, dient die PLA mit niedriger Priorität ausgeführt wird, während Leistungsdaten gesammelt werden. Wenn der Zielserver ausgelastet ist, kann PLA Löschen einiger der datensammlungsaufgaben, um Aufgaben mit hoher Priorität zu erhalten, die auf Zielservern ausgeführt werden. Sie sollten erwägen, das Einrichten der freigegebene Ordner, in dem die Ereignisse auf einem Datenträger verfügt t verursachen einen Konflikt mit der Workload-s-e/a- oder ein schneller Laufwerk, z. B. ein SSD geschrieben. Wenn Ereignisse gelöscht werden, werden sie in der Berichtsansicht gemeldet, da verloren gegangener Ereignisse, die Zuverlässigkeit der generierten Leistungsmetriken auswirken können.

Bestimmte Berechtigungsprobleme verursachen auch Registry oder WMI-Abfragen, die übersprungen werden. Dies ist jedoch sehr viel weniger wahrscheinlich, als der Verlust von ETW-Ereignisse. Daher werden die Ergebnisse von Data Collector Set manchmal alle Werte keine, die angefordert werden. Sie müssen sicherstellen, dass die Situation von den T-SQL-Skripts für alle Packs für Advisor behandelt wird. Wenn die Daten in das Ergebnis der Data-Auflistung nicht vorhanden ist, wird es als keine Daten in den Berichten gekennzeichnet.

Da der Verlust von ETW-Ereignisse für PLA häufig vorkommt, ist auf der Grundlage von Datenpunkten, die generiert werden einer ETW-Ablaufverfolgungs nicht konsistent mit Datenpunkten, die generiert werden, z. B. Leistungsindikatoren basiert möglicherweise. Beispielsweise ist es möglich, zu sehen, dass die gesamte CPU-Auslastung von IIS über 80 % beträgt (die von Leistungsindikatoren stammt) und den oberen URLs nur 10 % der gesamten CPU-Zeit verwenden (die einen Datenpunkt, der von der ETW-Ablaufverfolgung enthalten ist). In der Regel kann die Datenquelle für einen Datenpunkt über die QuickInfo des Datenpunkts angezeigt werden. Sie sollten die Auswirkungen solcher Datenverlust kennen.

Um den Verlust solcher Ereignisse zu vermeiden, sollte der Ordner "Ergebnis" auf dem Zielserver geschlossen werden.

Wenn die Ergebnisse des Data Collector unvollständige Daten als ETW-Ablaufverfolgung verloren gehen enthält, und der Advisor-Pack-Entwickler haben die Unterstützung für ETW-ereignisbenachrichtigung verloren gehen, eine Informationsleiste sehen Sie zusätzlich zu den einzelnen Bericht zur Benachrichtigung des Benutzers über die potenziell Inkonsistente Bericht zurückzuführen, dass Daten verloren gehen. Ausführliche Informationen zu Datenverlust finden Sie in der Datei "log.txt".

## <a name="glossary"></a>Glossar


Hier sind einige der Begriffe mit SPA verwendet:

* **Advisor-Pack** eine Auflistung von Metadaten und T-SQL-Skripts, die die Leistungsprotokolle zu verarbeiten, die auf dem Zielserver erfasst werden. Das Advisor-Pack generiert dann Berichte über die leistungsprotokolldaten aus. Die Metadaten in das Advisor-Pack definiert die Daten von der Zielserver für Leistungsindikatoren gesammelt werden sollen. Die Metadaten definieren auch den Satz von Regeln, Schwellenwerten und das Format des Berichts. In den meisten Fällen wird ein Advisor-Pack speziell für eine einzige Serverrolle, z. B. Internet Information Services (IIS) geschrieben.

* **SPA-Konsole** SpaConsole.exe, die der zentrale Teil des SPA ist. SPA muss nicht auf dem Zielserver ausgeführt wird, die Sie testen. Die SPA-Konsole enthält die Benutzeroberflächen für SPA vom das Projekt Analyse ausführen und Anzeigen von Berichten einrichten. Standardmäßig ist die SPA eine Anwendung mit zwei Ebenen. Die SPA-Konsole enthält die UI-Ebene und der Teil der Geschäftslogik-Ebene. Die SPA-Konsole plant und Performance Analysis-Anforderungen verarbeitet.

* **SPA-Framework** bietet alle Benutzeroberflächen, protokollverarbeitung Leistung, Konfiguration, Fehlerbehandlung und Prozeduren für Datenbank-APIs und die Verwaltung.

* **SPA-Projekt** eine Datenbank, die alle Informationen zu den Zielservern Advisor-Packs und Leistungsanalyse enthält Berichte, die auf den Zielservern für die Advisor-Packs generiert werden. Sie können vergleichen und Anzeigen von Verlauf und Trend Diagrammen innerhalb des gleichen SPA-Projekts. Sie können mehr als ein Projekt erstellen. Die SPA-Projekte sind voneinander unabhängig, und es sind keine Daten für Projekte freigegeben.

* **Zielserver** der physischen oder virtuellen Computer, die Windows Server mit bestimmten Serverrollen, wie z. B. IIS ausgeführt wird.

* **Data Analysis-Sitzung** dem Systemmonitor Leistungsanalysen an einen bestimmten Zielserver. Eine Data-Analyse-Sitzung kann mehrere Packs für Advisor enthalten. Die Sammlungssätze aus diesen Packs für Advisor werden in einer einzelnen Datensammlergruppe zusammengeführt. Alle Leistungsprotokolle für eine einzelne Analysis-Sitzung werden im gleichen Zeitraum gesammelt werden. Analysieren von Berichten, die von Advisor-Packs ausgeführt wird, in der gleichen Sitzung des Data-Analyse generiert werden, können Benutzer verstehen, die gesamtleistung Situation und Ursachen, um Leistungsprobleme zu identifizieren.

* **Ereignis-Ablaufverfolgung für Windows** eine hohe Leistung, mit geringem Verwaltungsaufwand, skalierbare Ablaufverfolgungssystem, die in Windows bereitgestellt wird. Es bietet die profilerstellung und Debuggen Funktionen, die verwendet werden kann, um eine Vielzahl von Szenarien zu beheben. SPA verwendet ETW-Ereignisse als Datenquelle für das Generieren von die Leistungsberichte. Allgemeine Informationen zu ETW finden Sie unter [verbessertes Debugging und Leistungsoptimierung mit ETW](https://msdn.microsoft.com/magazine/cc163437.aspx).

* **Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI)** der Infrastruktur für die Verwaltungs-Data und Vorgängen in Windows. Sie können WMI-Skripts oder Anwendungen zum Automatisieren administrativer Aufgaben auf Remotecomputern schreiben. WMI bietet auch die Verwaltungsdaten für andere Teile des Betriebssystems und Produkte. SPA verwendet WMI-Klasseninformationen und Datenpunkte als Quellen zum Generieren von Leistungsberichten.

* **Leistungsindikatoren** verwendet, um Informationen über das Betriebssystem oder eine Anwendung, Dienst oder Treiber Leistung bereitzustellen. Die Leistungsindikatordaten können helfen, Engpässe im System festzustellen und System- und Anwendungsleistung zu optimieren. Geben Sie das Betriebssystem, Netzwerk, und Geräte Leistungsindikatordaten, die eine Anwendung nutzen kann, um Benutzern eine grafische Ansicht der Leistung des Systems zur Verfügung stellen. SPA werden Informationen für Leistungsindikatoren und Datenpunkte als Datenquellen verwendet, um Leistungsberichte zu generieren.

* **Leistungsprotokolle und Warnungen (PLA)** sammelt Protokolle und Leistung und führt eine Ablaufverfolgung für leistungswarnungen ausgelöst, wenn es sich bei bestimmten Triggern erfüllt sind. PLA kann zum Sammeln von Leistungsindikatoren, ereignisablaufverfolgung für Windows (ETW), WMI-Abfragen, Registrierungsschlüssel und -Konfiguration Dateien verwendet werden. PLA unterstützt auch die remotedatensammlung über Remoteprozeduraufrufe (RPC). Der Benutzer definiert einen datensammlersatz, der Informationen über die zu sammelnden Daten, die Häufigkeit der Datensammlung, Daten sammlungsdauer, Filter und einen Speicherort zum Speichern der Ergebnisdateien enthält. SPA verwendet PLA, um alle Leistungsdaten von den Zielservern zu sammeln.

* **Einzelne Bericht** ein SPA-Berichten, die generiert wird auf Grundlage einer Data Analysis-Sitzung für eine Advisor-Pack auf einem einzelnen Zielserver. Sie können Benachrichtigungen und die verschiedenen Datenabschnitte enthalten.

* **Seite-an-Seite Bericht** ein SPA-Bericht, in dem zwei einzelne Berichte für das gleiche Advisor Pack verglichen. Die beiden Berichte können von anderen Servern oder aus separaten Performance Analysis ausgeführt wird, auf dem gleichen Zielserver generiert werden. Der Bericht für die Seite-an-Seite erstellt die Funktion zum Vergleichen von zwei Berichte, die Benutzer erkennen nicht normalem Verhalten oder die Einstellungen in einen Bericht zu erleichtern. Ein Seite-an-Seite-Bericht enthält, Benachrichtigungen und die verschiedenen Datenabschnitte. In jedem Abschnitt sind die Daten aus sowohl Berichten aufgelisteten Seite-an-Seite.

* **Trenddiagramm** ein SPA-Bericht, der verwendet wird, um sich wiederholende Muster von Leistungsproblemen zu untersuchen. Viele sich wiederholende Leistungsprobleme werden durch geplante serveränderungen verursacht, auf dem Server oder -Clientcomputern, die auftreten, können täglich oder wöchentlich. SPA bietet ein 24-Stunden-Trenddiagramm und ein Trenddiagramm für 7 Tage um diese Probleme zu identifizieren.

    Wahlweise kann der Benutzer eine oder mehrere Datenreihen zu einem Zeitpunkt, die einen numerischen Wert in den einzelnen Bericht, wie z. B. ist **durchschnittliche CPU-gesamtnutzung**. genauer gesagt ist ein numerischer Wert einen skalaren Wert aus einem einzelnen Server, der durch einen einzelnen Zugriffspunkt an einem bestimmten Zeitpunkt-Instanz generiert wird. SPA gruppiert diese Werte in 24-Gruppen, eine für jede Stunde des Tages (für einen Bericht für 7 Tage, eine für jeden Tag der Woche: sieben). SPA berechnet, Mittelwert, Minimum, Maximum und Standardabweichungen für jede Gruppe.

* **Verlaufsdiagramm** ein SPA-Bericht, der verwendet wird, um Änderungen in bestimmten numerischen anzuzeigen Werte innerhalb der einzelnen Berichte für einen bestimmten Server und Advisor Pack-Paar im Laufe der Zeit. Der Benutzer kann mehrere Datenreihen wählen und gemeinsam im das Verlaufsdiagramm zu die Korrelation zwischen unterschiedliche Datenreihen anzeigen.

* **Datenreihe** numerische Daten, die von der gleichen Datenquelle über einen Zeitraum gesammelt werden. Die gleiche Quelle bedeutet, dass die Daten aus dem gleichen Zielserver, z. B. die durchschnittliche Länge der Anforderungswarteschlange für IIS auf einem Server stammen.

* **Regeln** Kombinationen von Logik-, Schwellenwerte und Beschreibungen. Sie stellen ein mögliches Leistungsproblem dar. Jedes Advisor Pack enthält mehrere Regeln. Jede Regel wird durch die Verarbeitung eines Berichts Generation ausgelöst. Eine Regel gilt die Logik und die Schwellenwerte auf die Daten in den einzelnen Bericht. Wenn die Kriterien erfüllt sind, wird eine Benachrichtigung für eine Warnung ausgelöst. Wenn nicht, die Benachrichtigung, um festgelegt ist die **OK** Zustand. Wenn nicht die Regel gilt, wird die Benachrichtigung, die nicht anwendbar festgelegt (**NA**) Zustand.

* **Benachrichtigungen** Informationen, die eine Regel für Benutzer angezeigt. Es enthält den Status der Regel (**OK**, **NA**, oder ein **Warnung**), wird der Name der Regeln und möglichen Empfehlungen, um die Leistungsprobleme zu beheben.
