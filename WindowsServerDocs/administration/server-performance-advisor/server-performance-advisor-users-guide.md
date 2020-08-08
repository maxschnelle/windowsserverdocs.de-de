---
title: Server Performance Advisor-Benutzerhandbuch
description: Server Performance Advisor-Benutzerhandbuch
ms.assetid: be99a5a9-b9c0-436b-912c-e5c5839a533d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.topic: article
ms.openlocfilehash: 1a7ea3b902793f281156930a8e666c1d32d05cbe
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87993118"
---
# <a name="server-performance-advisor-users-guide"></a>Server Performance Advisor-Benutzerhandbuch

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10, Windows 8

Dieses Benutzerhandbuch für Microsoft Server Performance Advisor (Spa) enthält Richtlinien für die Verwendung von Spa, um Leistungsengpässe in Systemen zu identifizieren, die in verschiedenen Server Rollen bereitgestellt werden.

Spa kann Ihnen Folgendes helfen:

* Verwalten Sie die Serverleistung, und beheben Sie Probleme mit der Serverleistung.

* Stellen Sie Daten Berichte und Empfehlungen zu häufigen Konfigurations-und Leistungsproblemen bereit.

* Geben Sie Empfehlungen zu bewährten Methoden auf Grundlage der gesammelten Daten an.

> [!NOTE]
> Die Spa-Konsole nimmt keine Änderungen an den Servern vor.

Weitere Informationen zum Entwickeln von Spa Advisor-Paketen finden Sie im [Entwicklungs Handbuch zum Server Performance Advisor Pack](server-performance-advisor-pack-development-guide.md).

## <a name="server-performance-advisor-overview"></a>Übersicht über den Server Performance Advisor


In diesem Abschnitt wird der Verlauf der Spa erläutert, die Zielgruppe und die Zielgruppe beschrieben und eine architektonische Übersicht über das Tool vorgestellt.

### <a name="history-of-spa"></a>Verlauf der Spa

Die ursprüngliche Version von Microsoft Server Performance Advisor (Spa) wurde in 2005-2006 veröffentlicht. Dabei handelt es sich hauptsächlich um Windows Server 2003, einschließlich der wichtigsten Betriebssystem-und Server Rollen wie Internetinformationsdienste (IIS) und Active Directory. Das Tool soll Ihnen helfen, die Serverleistung zu bewerten und Probleme mit der Serverleistung zu beheben.

Spa bietet Daten Berichte und Empfehlungen für Systemadministratoren zu häufigen Konfigurations-und Leistungsproblemen. Spa sammelt leistungsbezogene Daten aus verschiedenen Quellen auf Servern, z. b. Leistungsindikatoren, Registrierungs Schlüsseln, WMI-Abfragen, Konfigurationsdateien und Ereignis Ablauf Verfolgung für Windows (ETW). Basierend auf den erfassten Server Leistungsdaten bietet Spa eine ausführliche Betrachtung der aktuellen Serverleistung und gibt Empfehlungen dazu, was verbessert werden kann.

Das Original-Spa-Tool hat mehr als 1 Million Downloads und unterstützt viele Systemadministratoren dabei, die Leistung Ihrer Server zu verwalten. Es handelt sich um ein sehr erfolgreiches Tool zur Problembehandlung bei der Leistung.

Seit der Veröffentlichung der ursprünglichen Spa gibt es einige wesentliche Änderungen in der Server Leistungs Welt. Insbesondere das Release von Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008 mit neuen Versionen der entsprechenden Server Rollen wie Internetinformationsdienste (IIS) 8,5. Neuere Versionen von Server Performance Advisor erweitern die Funktionalität der ursprünglichen Spa auf die neuesten Server Betriebssysteme und Server Rollen.

Obwohl Spa 3,1 die gleichen Entwurfs Ziele und Leistungsanalyse Paradigma wie das ursprüngliche Tool nutzt, wurde es mit der neuesten Technologie umgeschrieben. Außerdem bietet es die folgenden wichtigen Verbesserungen:

* Kann Analysen für Server ausführen, auf denen Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008 ausgeführt wird.

* Unterstützt die Remote Analysefunktion, die es Spa 3,1 ermöglicht, Daten aus einer zentralen Konsole zu erfassen und zu analysieren, ohne dass Code auf den zu analysierenden Servern installiert werden muss.

* Verwendet einen Microsoft SQL Server für die Datenanalyse und den Speicher, der die Verarbeitung und Speicherung großer Datenmengen ermöglicht.

* Trennt das Tool von den Advisor-Paketen. Die Leistungsanalyse Logik für jede Server Rolle wird in Form eines Advisor-Pakets freigegeben, das getrennt vom Tool veröffentlicht oder aktualisiert werden kann.

* Stellt Advisor-Pakete bereit, die in SQL-Skripts mit einer offenen Architektur entwickelt wurden. Parteien, die nicht von Microsoft sind, können Advisor Packs entwickeln oder die vorhandenen Advisor Packs von Microsoft erweitern, um besondere Anforderungen zu erfüllen.

* Unterstützt neue Features wie parallele Vergleichsberichte und Trend-und Vergangenheits Diagramme, die Ihnen bei der Suche nach Anomalien helfen.

* Bietet Features wie z. b. die Schwellenwerte zum ändern, importieren und exportieren, mit denen Sie die Berichte und Benachrichtigungen optimieren und diese für andere Spa-Benutzer freigeben können.

* Unterstützt mehrere-Projekte, die zum Gruppieren von Ziel Servern verwendet werden können.

* Ermöglicht die wiederholte Erfassung von Daten in der Spa-Konsole.

* Aktiviert benutzerdefinierte Abfragen und die Generierung von Berichten mithilfe von Microsoft SQL Server (für fortgeschrittene Benutzer).

* Angepasste Windows PowerShell-Cmdlets sind für die Verwendung mit Spa verfügbar.

* Abwärts kompatibel zum Importieren und Anzeigen von Berichten aus einer Spa 3,0-Datenbank

### <a name="target-audience"></a>Zielgruppe

Das Spa-Tool ist hauptsächlich für Systemadministratoren konzipiert, die weniger als 100 Server in verschiedenen Server Rollen verwalten. Es kann auch von Support Technikern verwendet werden, um Leistungsdaten zu erfassen und Leistungsprobleme für Kunden zu beheben.

Spa bietet Empfehlungen, mit denen Sie Leistungsprobleme beheben können. Es basiert jedoch auf Annahmen, die möglicherweise nicht auf Ihre bestimmte Serverumgebung anwendbar sind. Die Empfehlungen, die über Spa angeboten werden, sollten als Vorschläge angesehen werden. Wir gehen davon aus, dass Spa-Benutzer ein gutes Verständnis der Systemkonfiguration, der Anwendungsfälle und der Auswirkungen der Systemoptimierung auf das gesamte Systemverhalten haben. System Administratoren sollten entscheiden, ob die Spa-Empfehlungen auf Ihre Umgebung angewendet werden sollen.

### <a name="what-s-new-in-spa-31"></a><a href="" id="what-s-new-in-spa-3-1-"></a>Welche Neuerungen gibt es in Spa 3,1?

Die folgenden Features und Verbesserungen wurden in Spa 3,1 hinzugefügt:

* Das Active Directory Advisor Pack hilft bei der Analyse der allgemeinen Leistung der Server Rolle "Active Directory-Domänen Dienste" des Servers.

* Unterstützung für Entwickler zum Hinzufügen verlorener ETW-Ereignis Benachrichtigungs Warnungen in den Advisor Packs und zum Anzeigen der Warnung, wenn ein Bericht generiert wurde und Ereignisse aufgrund der Häufigkeit der Protokollierung auf einem langsamen oder stark in Konflikt befindlichen Datenträger verloren gegangen sind

### <a name="target-scenarios"></a>Ziel Szenarien

Im folgenden sind die Ziel Szenarien für Spa aufgeführt:

* **Server Umgebung**

    Spa ist so konzipiert, dass es problemlos eingerichtet und gewartet werden kann. Dies gilt für Serverumgebungen, die 1 bis 100 Server verwenden. Spa ist nicht gut skalierbar, wenn Sie versuchen, die Leistung für mehr als 100 Server zu verwalten. Für größere oder anspruchsvollere Umgebungen sollten Sie die Verwendung von System Center Operations Manager in Erwägung gezogen.

* **Behandlung von Leistungsproblemen**

    Sie können Spa als Tool zur Leistungsproblem Behandlung verwenden. Er bietet die Möglichkeit, Leistungsdaten auf hoher Ebene zu erfassen. er führt eine gründliche Verarbeitung der Daten durch, um Ihnen ein besseres Verständnis für das gesamte Systemverhalten zu bieten, und Kenn gibt jegliche Anomalien. Wenn ein Kunde von einem Leistungsproblem vermutet wird, können Sie die Spa verwenden, um Leistungsdaten vom Server zu erfassen und zu analysieren.

    Spa generiert einen Bericht, den Sie anzeigen können. Spa-Berichte bieten eine Benachrichtigungsliste, die mögliche Probleme hervorhebt, und einen Daten Abschnitt, der verschiedene Leistungsindizes, Konfigurationen und Einstellungen für den Server enthält. Mithilfe dieses Berichts können Sie das spezifische Leistungsproblem identifizieren und die Empfehlungen verwenden, um Lösungen für das Problem zu finden. Berichte können mit anderen Berichten verglichen werden, die zu einem anderen Zeitpunkt oder von einem anderen Server generiert wurden. Mit diesem parallelen Vergleich können Sie Unterschiede zwischen der normalen Baseline und dem normalen Verhalten ermitteln.

    **Hinweis** Spa ist nicht als Debuggen oder Messungs Tool konzipiert. Außerdem kann Sie aus der Perspektive der Server als Schreib geschütztes Tool angesehen werden, und die Serverkonfigurationen werden nicht geändert.



* **Leistungsindex Überwachung**

    Sie können Spa verwenden, um den Leistungsindex von-Servern zu überwachen. Sie können festlegen, dass Spa regelmäßig auf Servern ausgeführt werden soll, um Leistungsdaten zu erfassen, und dann ein Trend Diagramm oder ein Verlaufs Diagramm ausführen, um die Anomalien zu erkennen. Sie können den Bericht für eine bestimmte Analyse anzeigen, weitere Informationen zum Leistungsproblem anzeigen und dann die Empfehlungen oder andere Berichtsdaten verwenden, um das Problem zu beheben.

### <a name="spa-architecture"></a>Spa-Architektur

Die Spa-Daten Sammlungs Logik basiert auf einem Protokoll in Windows namens Leistungsprotokolle und-Warnungen (PLA). Mithilfe von Pla können Programme Leistungsdaten von lokalen Servern oder Remote Servern erfassen, wie z. b. Leistungsindikatoren, WMI-Abfragen, etw-Ablauf Verfolgungen, Registrierungs Schlüsseln und Konfigurationsdateien. Wenn das Spa eine Leistungsanalyse auf einem Zielserver ausführt, erstellt es einen Pla-Datensammler Satz, der auf dem von Ihnen ausgewählten Spa Advisor-Paket basiert. Das Advisor-Paket enthält die zu sammelnde Datenquelle und die Dateifreigabe, in der die Protokolle gespeichert werden sollen. Bei der Spa-Datensammlung wird nur ein einzelnes Benutzerkonto gespeichert. das gleiche Benutzerkonto, das von Pla verwendet wird, wird auch verwendet, um die Protokolle zu schreiben.

Spa verwendet eine SQL Server Datenbank, um die Leistungs Protokolle zu speichern, die von den Ziel Servern gesammelt werden. Spa importiert alle Leistungs Protokolle aus der Dateifreigabe in die Datenbank und verwendet dann die Datenanalyse Logik innerhalb jedes Advisor-Pakets, um die Daten zu verarbeiten und die Berichte zu generieren. Ein Advisor-Paket analysiert die Leistungsdaten, die von den Ziel Servern gesammelt wurden, und generiert die Spa-Berichte. Weitere Informationen zum Aufbau eines Advisor-Pakets finden Sie im [Entwicklungs Handbuch zum Server Performance Advisor Pack](server-performance-advisor-pack-development-guide.md).

Die Benutzeroberflächen und Interaktionen der Spa-Konsole werden als Teil des SPAConsole.exe erstellt. Sie können die-Konsole verwenden, um eine Datenbank zu erstellen, Advisor-Pakete hinzuzufügen oder zu entfernen, Zielserver zu verwalten, Leistungsanalysen auszuführen und Leistungsberichte anzuzeigen.

Die Spa-Konsole kann unter den folgenden Betriebssystemen ausgeführt werden:

* Windows 8.1

* Windows 8

* Windows 7

* Windows Server 2012 R2

* Windows Server 2012

* Windows Server 2008 R2

* WindowsServer 2008

In einer typischen Geschäftsanwendung gibt es drei Ebenen: die Präsentationsschicht, die Geschäftslogik Schicht und die Speicher Ebene. Spa ist als ein zweistufiges Produkt der-Konsole und der-Datenbank konzipiert. Die-Konsole fungiert als Präsentationsschicht mit bestimmter prozessbezogener Logik, und die-Datenbank fungiert als Speicherschicht und Geschäftslogik Schicht. Die-Konsole erfasst Benutzereingaben und steuert die Schritte für die Datensammlung, die Datenverarbeitung und die Bericht Generierung. Spa ist nicht von den Windows-System Diensten abhängig.

Das folgende Diagramm zeigt die allgemeine Architektur des Spa-Systems. Der Prozess lautet wie folgt:

1.  In der Spa-Konsole führen Sie die Leistungsanalyse auf den angegebenen Servern aus.

2.  Wenn die Leistungsdaten gesammelt werden, werden die Protokolle von Pla auf den Ziel Servern zurück in die Dateifreigabe geschrieben, die durch den Datensammler Satz angegeben wird.

3.  Nachdem die Datensammlung auf einem Bereitstellungs Zielcomputer fertiggestellt wurde, importiert die Spa-Konsole die Protokolle in die SQL Server Datenbank.

4.  Die-Konsole Ruft die Datenverarbeitungs Logik eines bestimmten Advisor-Pakets auf.

5.  Das Advisor Pack verarbeitet die Daten und ruft Spa-APIs auf, um Datensätze in die vom Spa-Framework definierten System Berichts Tabellen einzufügen.

6.  Sie können den Bericht-Viewer in der-Konsole verwenden, um die generierten Berichte anzuzeigen. Um Ihnen bei der Behebung von Leistungsproblemen zu helfen, bietet Spa drei Arten von Berichten: einzelne Berichte, parallele Berichte und Trend-oder Vergangenheits Diagramme. Weitere Informationen zu Berichten finden Sie unter [Anzeigen von Berichten](#bkmk-viewingreports).

![Spa-Architektur](../media/server-performance-advisor/spa-user-manual-architecture.png)

## <a name="getting-started-with-spa"></a>Einstieg in die Spa


### <a name="requirements"></a>Anforderungen

Die Spa-Konsole kann auf Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008 installiert werden. Das Ausführen von Spa unter früheren Versionen des Windows Server-Betriebssystems wird nicht unterstützt. Spa wird auf x86 oder x64 ausgeführt, unterstützt jedoch keine ia64-oder ARM-Architekturen.

Spa basiert auf Windows Presentation Foundation (WPF) 2,0, das Teil von Microsoft .NET Framework 4 ist, sodass .NET Framework 4 erforderlich ist.

Außerdem müssen Sie SQL Server 2008 R2 Express auf demselben Computer installieren, auf dem Spa installiert ist. SQL Server 2008 R2 Express ist eine kostenlose Datenbank-Engine, die von Microsoft veröffentlicht wird. Sie können Microsoft SQL Server 2008 R2 Express aus dem Microsoft Download Center herunterladen. Obwohl wir SQL Server 2008 R2 Express vorschlagen, können neuere Versionen von SQL Server auch mit Spa kompatibel sein.

**Hinweis** Das Spa umfasst weder SQL Server noch die .NET Framework als Teil des Installationspakets. Nach der Installation von Microsoft SQL Server 2008 R2 und .NET Framework 4,0 empfiehlt es sich, vor der Installation von Spa Windows Update auszuführen.



Da Benutzerdaten Banken mit Spa erstellen und verwalten können, muss das Benutzerkonto, das zum Ausführen von Spa verwendet wird, über dieselben Administratorrechte wie SQL Server verfügen.

### <a name="setting-up-spa"></a><a href="" id="bkmk-setupspa"></a>Einrichten von Spa

Spa ist als CAB-Datei verpackt, die alle Binärdateien für das Spa-Framework, die Windows PowerShell-Cmdlets, die in erweiterten Szenarien verwendet werden, und die folgenden Advisor-Pakete enthält: Core OS, Hyper-V, Active Directory und IIS. Nachdem Sie die CAB-Datei in einen Ordner extrahiert haben, ist keine weitere Installation erforderlich. Zum Ausführen von Spa müssen Sie die Datensammlung auf den Ziel Servern jedoch wie folgt aktivieren:

* Zum Ausführen der Pla-Datensammlung muss das Benutzerkonto, das Sie zum Ausführen der Spa-Konsole verwenden, der Sicherheitsgruppe "Administratoren" auf dem Zielserver angehören. Wenn sich der Zielserver und die-Konsole in derselben Domäne befinden, muss das Domänen Benutzerkonto Teil der Sicherheitsgruppe Administratoren auf dem Zielserver sein. Wenn sich der Zielserver und die-Konsole nicht in derselben Domäne befinden, erstellen Sie ein Administrator Konto auf dem Zielserver mit demselben Benutzernamen und Kennwort wie das Benutzerkonto, das Sie zum Ausführen der Spa-Konsole verwenden.

* Erstellen Sie einen freigegebenen Ordner für die Ergebnisse auf dem Server.

* Stellen Sie sicher, dass das Benutzerkonto, das Sie zum Ausführen der Spa-Konsole verwenden, über Lese-und Schreibberechtigungen für den freigegebenen Ordner verfügt. Mit diesem Konto werden von Pla Protokolle in den Ordner geschrieben.
Die Spa-Konsole verwendet dasselbe Konto, um Protokolle zu lesen und in die-Datenbank zu importieren.

    **Hinweis** Etw implementiert einen Zirkel Puffer zum Speichern der Ablauf Verfolgung und verschiebt Sie nach Möglichkeit in den freigegebenen Ordner. Wenn der Server ausgelastet ist oder der Schreibvorgang langsam ist, löscht etw die Ablauf Verfolgungen, wenn der Puffer voll ist. Es ist wichtig, dass sich der freigegebene Ordner auf einem Server befindet, der überschnellen e/a-Zugriff verfügt. Es wird empfohlen, dass jeder Zielserver über einen freigegebenen Ordner verfügt, um Datenverluste zu minimieren, die durch langsame Datei-e/a



* Legen Sie für die Windows-Firewall für den Zugriff auf Zielserver mit der Windows-Firewall den Zugriff auf Remote Leistungsprotokolle und-Warnungen auf Ziel Servern fest. Die Pla verwendet den TCP-Port 139.

* Stellen Sie sicher, dass die **Leistungs Protokolle &** Warnungs Dienst ausgeführt werden.

* Wenn sich die Konsole und der Zielserver in unterschiedlichen Subnetzen befinden, müssen Sie auch das Feld Remote-IP-Adresse in den Regeln für die eingehende Firewall in den **Bereichs** Einstellungen auf der Seite **Leistungsprotokolle und-Warnungen** festlegen, wie hier gezeigt.

    ![Pla-Eigenschaften](../media/server-performance-advisor/spa-user-manual-pla-firewall.png)

* Aktivieren Sie die Netzwerk Ermittlung in der-Konsole und auf jedem der Zielserver.

* Wenn der Zielserver keiner Domäne hinzugefügt wird, aktivieren Sie die folgende Registrierungs Einstellung: **HKLM \\ Software \\ Microsoft \\ Windows \\ CurrentVersion \\ Policies \\ System \\ localaccountdekenfilterpolicy**.

**Hinweis** Standardmäßig schreibt Spa Diagnoseprotokolle in den Ordner, in dem sich SpaConsole.exe befindet. Wenn die Spa im Ordner "Programme" installiert ist, kann die Spa nur das Protokoll schreiben, wenn SpaConsole.exe als Administrator ausgeführt wird.

Wenn Sie die Datenanalyse auf dem Computer mit der-Konsole ausführen möchten, müssen Sie Spa als Administrator ausführen. Die Pla durchläuft einen anderen Codepfad, wenn Sie auf einem lokalen Computer ausgeführt wird, für den Administratorrechte erforderlich sind.

Wenn Sie das IIS Spa Advisor Pack für Ihre Server ausführen möchten, müssen Sie die WMI-Abfrage und die ETW-Ablauf Verfolgung für den IIS-Server aktivieren. Hierzu können Sie die Ablauf **Verfolgung** unter dem Integritäts **-und Diagnose** Rollen Dienst und die **IIS-Verwaltungs Skripts und-Tools** unter **Verwaltungs Tools** der Server Rolle " **Webserver (IIS)** " aktivieren.



### <a name="creating-your-first-project"></a>Erstellen Ihres ersten Projekts

Nachdem alles eingerichtet wurde, können Sie Ihr erstes Spa-Projekt erstellen. Wie im vorherigen Abschnitt beschrieben, speichert Spa alle Elemente, die sich auf die Analyse von Leistungsdaten in einer Datenbank beziehen. Jedes Spa-Projekt entspricht einer einzelnen Datenbank. Der **Assistent zum ersten Mal** führt Sie durch die folgenden Schritte:

**So erstellen Sie ein Spa-Projekt**

1.  Starten Sie SpaConsole.exe. Die Konsole wechselt in einen getrennten Modus, in dem die Spa nicht mit einer Datenbank verbunden ist und das Hauptfenster leer ist.

2.  Um ein neues Projekt zu erstellen, klicken Sie auf **Datei**und dann auf **Neues Projekt**. Hiermit wird der Assistent zum ersten Mal verwendet. Auf der ersten Seite werden die Schritte angezeigt, die Sie bei der Verwendung des Assistenten befolgen:

    * Erstellen einer Datenbank

    * Advisor-Pakete bereitstellen

    * Hinzufügen von Servern zur Zielserver Liste

3.  Klicken Sie auf **Weiter**. Auf der Seite **Projektdatenbank erstellen** werden Sie aufgefordert, den Namen der Microsoft SQL Server Instanz anzugeben, in der Sie die Datenbank erstellen möchten. Wenn Sie sich z. b. auf dem gleichen Computer wie die-Konsole befindet, können Sie **localhost als \\ &lt; SQL &gt; Server-Namen**verwenden.

    **Hinweis** Der Standardinstanzname für eine SQL Server 2008 R2 Express-Installation lautet SQLExpress. Bei einer Instanz von SQL Server 2008 R2 Express, die auf dem lokalen Computer installiert ist, wird in der Regel standardmäßig **localhost \\ SQLExpress**für die Datenbank festgelegt. Es wurde jedoch möglicherweise während SQL Server Installation geändert, daher müssen Sie sicherstellen, dass Sie den richtigen SQL Server Instanznamen verwenden.



4.  Geben Sie den Datenbanknamen an. Es sind nur Buchstaben, Ziffern und Unterstriche ( \_ ) als gültige Zeichen für einen Datenbanknamen zulässig. Ein angemessener Vorschlag für den Namen der Spa-Datenbank wäre " **Spa**". Wenn Sie einen ungültigen Namen eingeben, wird ein rotes Fehler Symbol angezeigt. Die zugehörige QuickInfo gibt den Grund für den Überprüfungs Fehler aus.

    **Hinweis** Es ist wichtig, den Datenbanknamen und den Serverinstanznamen zu merken, da dies die einzigen Bezeichner für Ihr Projekt sind. Sie müssen diese Informationen angeben, wenn Sie zu dieser Datenbank wechseln möchten.



5.  Nachdem Sie den Serverinstanznamen und den Datenbanknamen bereitgestellt haben, generiert der Assistent zum ersten Mal den Speicherort für die Datenbankdatei.

6.  Klicken Sie auf der Seite " **Projektdatenbank erstellen** " auf " **weiter**". Beim ersten Mal erstellt der Assistent eine Datenbank und generiert alle Spa-bezogenen Datenbankschemas, Funktionen und gespeicherten Prozeduren in der Datenbank. Dieser Schritt kann je nach Hardware-und Netzwerkgeschwindigkeit einige Sekunden in Anspruch nehmen.

    **Hinweis** wenn dieser Schritt fehlschlägt, wird eine Fehlermeldung angezeigt. Einige häufige Probleme sind: die-Konsole kann keine Verbindung mit der SQL Server-Instanz herstellen, unzureichende Berechtigungen zum Erstellen einer Datenbank, oder der Datenbankname ist bereits vorhanden.



7.  Wenn der vorherige Schritt erfolgreich ausgeführt wurde, wird die Seite " **Advisor-Paket bereit** stellen" angezeigt. Sie listet alle Advisor-Pakete auf, die auf Ihrem Computer verfügbar sind. Spa scannt den Ordner mit dem Namen **APS** automatisch unter dem Spa-Stammverzeichnis. Sie listet den vollständigen Namen, die Version und den Autor für jedes Advisor Pack auf.

    **Hinweis** Weitere Informationen zur Verwendung des vollständigen Namens und der Version in der Spa finden Sie unter [Verwalten von Advisor Packs](#bkmk-manageadvisorpacks) .



8.  Wählen Sie aus, welche Ratgeber Pakete Sie in der Projektdatenbank bereitstellen möchten, und klicken Sie dann auf **weiter**. Sie können auch auf über **springen** klicken, um zum nächsten Schritt zu wechseln, ohne Advisor-Pakete bereitzustellen.

    **Hinweis** Sie können Ratgeber Pakete jederzeit bereitstellen, wenn Sie das Tool verwenden. Weitere Informationen finden Sie unter [Verwalten von Advisor Packs](#bkmk-manageadvisorpacks).



9.  Auf der Seite **Server hinzufügen** müssen für jeden Server, der der Liste Zielserver hinzugefügt werden soll, zwei Pflichtfelder ausgefüllt werden: **Name des Servers und der** **Dateifreigabe**.

    **Hinweis** Es gibt auch ein Feld für die **Anmerkung** , das hauptsächlich zum Klassifizieren oder Suchen des Servers verwendet wird. In Fällen, in denen Sie viele Server haben, können Sie eine Datei mit Komma getrennten Werten (CSV-Datei) importieren, die den Servernamen, den Ergebnis Ordner und das optionale Feld für die Anmerkung enthält. Das Feld " **Anmerkung** " wird verwendet, um den Server zu beschreiben, und der Begriff kann zum Filtern von Servern für die Datensammlung verwendet werden. Wenn Sie die Server über die CSV-Datei initialisieren, werden die Server durch einen Fehler beim fehl geschachtelungs Fehler in der Datei nicht geladen.



10. Es müssen mehrere Konfigurationen festgelegt werden, um die Pla-Datensammlung zu aktivieren, wie unter [Einrichten von Spa](#bkmk-setupspa)beschrieben. Die Seite **Server hinzufügen** bietet eine Test Konfigurationsfunktion, mit der Sie Konfigurationsprobleme beheben können. Aktivieren Sie das Kontrollkästchen, das dem Computer zugeordnet ist, und klicken Sie dann auf **Verbindung testen**. Spa versucht, einen Datensammler Satz auf Ziel Servern zu generieren, und versucht, die Ergebnisse zurück in die Datenbank zu importieren. Wenn alles richtig ist, zeigt der **Status** " **Pass**" an. Wenn ein Fehler auftritt, wird eine QuickInfo angezeigt, die den Grund für den Fehler beschreibt.

11. Jeder Server wird der Datenbank automatisch hinzugefügt, auch wenn er den Konfigurations Test nicht bestanden hat. Wenn Sie Server aus der Liste entfernen möchten, wählen Sie den Servernamen aus, und klicken Sie auf **Entfernen**.

12. Wenn alles abgeschlossen ist, klicken Sie auf **Fertig** stellen, um den Assistenten zum ersten Mal zu schließen. Wenn Sie den Assistenten zum ersten Mal verwenden, bevor Sie ihn abschließen, werden alle vorherigen Schritte beibehalten, und für keinen wird automatisch ein Rollback ausgeführt. Sie müssen zukünftige Änderungen manuell vornehmen.

## <a name="running-analysis"></a>Analyse wird ausgeführt


Nachdem Sie die Datenbank eingerichtet haben, können Sie die Leistungsanalyse auf den Servern ausführen.

Jedes Mal, wenn die Spa-Konsole gestartet wird, wird das letzte Projekt, das vom aktuellen Benutzer verwendet wurde, automatisch geöffnet. Das Hauptfenster enthält eine Liste von Servern. Jeder Server verfügt über vier Eigenschaften: Server Name, Analyseergebnis, aktueller Status und Hinweis.

* **Server Name** Der Name des Servers, der der Bezeichner für den Server ist. Doppelte Namen sind nicht zulässig.

* **Analyseergebnis** Standardmäßig wird das Ergebnis der aktuellen Leistungsanalyse angezeigt, die auf dem Server ausgeführt wird. Wenn keine Leistungsanalyse auf dem Server ausgeführt wurde, wird **kein Bericht**angezeigt. Wenn vom Bericht eine Warnung ausgelöst wird, wird eine **Warnung** und der Zeitstempel angezeigt, wenn der aktuelle Bericht generiert wurde. Wenn während der letzten Analyse auf dem Server kein Problem gefunden wurde, wird die Meldung " **OK** " und der Zeitstempel angezeigt.

    **Hinweis** Wenn Sie vor kurzem eine Systemeinstellung geändert haben, empfiehlt es sich, die Analyse erneut auszuführen, um die allgemeinen Auswirkungen der Änderung zu evaluieren und einen aktualisierten Bericht zum Systemstatus zu erhalten. Spa verfolgt keine Konfigurationsänderungen am getesteten System nach.



* **Aktueller Status** Zeigt den Status von Leistungsanalyse Tasks an, die zurzeit auf dem Server ausgeführt werden. Sie können eine laufende Aufgabe abbrechen, indem Sie auf das Symbol " **Abbrechen** " klicken, das durch ein rotes X gekennzeichnet ist.

* **Anmerkung** Beschreibt den aktuellen Zielserver. Beispielsweise können Sie den Server mithilfe der Server Rolle (z. b. SQL Server) oder eines Speicher Orts (z. b. Kent) beschreiben. Spa verwendet den **Servernamen** und die- **Anmerkung** , um die Suche nach dem richtigen Server zu unterstützen. Sie können in das Textfeld Suchen eingeben. Wenn die Spalten **Servername** oder **Anmerkung** die genaue Zeichenfolge enthält, die Sie im Suchfeld eingegeben haben, wird der Server in der Liste Server angezeigt.

Die folgenden Steuerelemente sind auch in der-Konsole verfügbar:

* **Wiederholen** Ein Kontrollkästchen, das die Möglichkeit beschreibt, eine Auflistung basierend auf einem Zeitintervall regelmäßig zu wiederholen. Bei den meisten Serverinstallationen sollten Sie eine Spa-Sammlung stündlich wiederholen, um für die Analyse ausreichend Verlauf zu haben. Wenn Sie die Sammlung nur einmal ausführen möchten, sollten Sie das Kontrollkästchen **wiederholen** nicht aktivieren.

* **Wiederholung entfernen** Eine Schaltfläche, die es Ihnen ermöglicht, einen laufenden Wiederholungs Sammlungs Auftrag abzubrechen. Die Wiederholungs Auflistung wird abgebrochen, aber nicht die aktuelle Auflistung (sofern vorhanden). Mit dieser Option können Sie ein neues Wiederholungs Sammlungs Intervall zurücksetzen oder die Auflistung manuell ausführen.

Bevor Sie mit der Leistungsanalyse beginnen, wählen Sie die Dauer der Datensammlung aus. Obwohl durch das Erfassen von mehr Daten eine genauere Darstellung der Server leistungssituation erzielt werden kann, wird auch eine größere Anzahl von Protokollen generiert, und es kann eine größere Auswirkung auf den Server haben. Wählen Sie die richtige Daten Sammlungs Dauer basierend auf Ihrem speziellen Bedarf aus. Jedes Advisor-Paket definiert eine minimale gültige Dauer. Die von Ihnen gewählte Dauer für die Datensammlung muss länger sein als die minimale Dauer der ausgewählten Advisor Packs.

Wenn Sie die Leistungsanalyse auf Ziel Servern ausführen möchten, wählen Sie die Server aus, für die Sie die Leistungsanalyse ausführen möchten, und klicken Sie auf **Analyse ausführen** A. Daraufhin werden Sie aufgefordert, die Advisor Packs auszuwählen, die auf den Servern ausgeführt werden sollen. Die ausgewählten Advisor Packs werden gleichzeitig ausgeführt. Die generierten Berichte basieren auf den Leistungsdaten, die während des gleichen Zeitraums gesammelt werden.

**Hinweis** Wenn Sie einen Server auswählen, auf dem eine wiederkehrende Leistungsanalyse ausgeführt wird, können Sie mit der Schaltfläche **Wiederholung entfernen** die wiederkehrende Datensammlung abbrechen. Die Spa lässt nicht mehrere Daten Sammlungs Sitzungen gleichzeitig auf demselben Computer zu.



## <a name="viewing-reports"></a><a href="" id="bkmk-viewingreports"></a>Anzeigen von Berichten


In Spa gibt es drei Typen von Leistungsanalyse Berichten: einzelner Bericht, paralleler Bericht und Trend-und Verlaufs Diagramme.

Nach dem Ausführen der Leistungsanalyse wird für jedes Advisor-Paket, das auf dem Bereitstellungs Zielcomputer ausgeführt wird, ein Bericht generiert. Aus der Serverliste im Hauptfenster können Sie das **Analyseergebnis** erweitern, um alle Advisor-Pakete anzuzeigen, die auf dem jeweiligen Server ausgeführt wurden. Sie können auf einen Berichts Namen klicken, um einen einzelnen Bericht anzuzeigen.

Neben dem Namen des Advisor-Pakets sind drei Symbole vorhanden, die den Status der letzten Analyse anzeigen, die auf dem Server ausgeführt wird:

* Das **neueste** Symbol zeigt den Bericht, der von der aktuellen Leistungsanalyse auf diesem Server für das Advisor Pack generiert wurde.

* Das Symbol **Suchen** zeigt die Liste der Leistungsanalyse Berichte an, mit deren Hilfe Sie den richtigen Bericht auswählen können. Die Felder **Advisor Pack** und **Zielserver** sind mit dem aktuellen Advisor Pack und den Zielserver Informationen vorab gefüllt. Der Standardzeit Bereich ist auf eine Woche festgelegt, und das Enddatum wird auf heute festgelegt. Wenn Sie in der oberen rechten Ecke auf die Schaltfläche **Suchen** klicken, können Sie eine Liste aller Leistungsanalyse Berichte für den ausgewählten Server und das Advisor-Paket im Zeitbereich erhalten.

* Das Symbol **Diagramme anzeigen** öffnet die Diagramm Ansicht Trend und Vergangenheits Diagramm.

In der folgenden Abbildung werden die Symbole für das **neueste**, das **Suchen**und **Anzeigen von Diagrammen** nach den einzelnen Advisor-Paketen angezeigt:

![Berichts Symbole](../media/server-performance-advisor/spa-user-manual-report-icons.png)

### <a name="searching-for-and-within-reports"></a>Suchen nach und innerhalb von Berichten

Die Suche nach Berichten erfolgt über den **Berichts-Explorer**. Dies ermöglicht es Ihnen, nach dem Datumsbereich, dem Servernamen und dem Advisor-Paket nach Berichten zu suchen. Dies ist die empfohlene Vorgehensweise, um einen anderen Bericht als den letzten Bericht zu finden. Der letzte Testlauf ist über **Bericht anzeigen** für diesen Server verfügbar.

Wenn Sie einen bestimmten Bericht anzeigen, können Sie ganz einfach zum nächsten und vorherigen Bericht navigieren, oder Sie können sich einen verknüpften Bericht ansehen, z. b. eine andere, gleichzeitig laufende Zugriffspunkt-app. Diese Optionen sind unter **Aktionen**verfügbar.

Es ist auch möglich, in einem Bericht zu suchen. Für eine Reihe von Berichten ist das Suchfeld **Such Zeichenfolge für** die schnelle Text Zeichenfolgen-Suche im Bericht verfügbar. Um das Textfeld zu entfernen, können Sie es verwerfen. Wenn Sie ein Suchfeld (in Fenstern mit Text Suche) aktivieren möchten, können Sie die Verknüpfung Steuerelement + F verwenden. Das **Feld Suchen** ermöglicht dem Benutzer die Angabe der Groß-/Kleinschreibung bei der Suche nach Bedarf mit der Option Groß-/Kleinschreibung **.**

In der folgenden Abbildung wird **das Suchfeld suchen mit** der Zeichenfolge **Power** auf der Registerkarte **Bericht** angezeigt.

![Suchfeld suchen](../media/server-performance-advisor/spa-user-manual-find-search-box.png)

### <a name="single-report"></a>Einzelner Bericht

Ein einzelner Bericht zeigt die Ergebnisse der Leistungsanalyse aus einer einzelnen Ausführung eines Advisor-Pakets auf einem einzelnen Computer an. Der Bericht zeigt den Namen des Advisor-Pakets, den Namen des Zielservers, den Zeitpunkt, zu dem der Bericht generiert wurde, und die Dauer für die Datensammlung an.

Ein einzelner Bericht enthält einen Benachrichtigungs Abschnitt und die Datenabschnitte.

### <a name="notification-section"></a>Benachrichtigungs Abschnitt

Der Benachrichtigungs Abschnitt besteht aus einer Reihe von Leistungsanalyse Regeln. Jede Benachrichtigung enthält einige Datenquellen, einige Schwellenwerte und einige Geschäftslogik. Wenn Sie die Leistungsanalyse ausführen, wertet die Geschäftslogik die Datenquellen anhand der Schwellenwerte aus, um zu bestimmen, ob die Regel weitergeleitet wird. Wenn dies nicht der Fall ist, wird eine Warnung angezeigt, um Sie über ein mögliches Leistungsproblem zu informieren. Außerdem finden Sie hier Empfehlungen, die Ihnen helfen, das Problem zu beheben. Der Benachrichtigungs Abschnitt ist immer die erste Registerkarte in der einzelnen Berichtsansicht.

Der Benachrichtigungs Abschnitt ist in zwei Teile unterteilt: **Warnung** und **andere Benachrichtigungen**.

Wenn die Datenquelle für eine Regel bestimmte Bedingungen basierend auf den Logik-und Schwellenwert Einstellungen erfüllt, wird im **Warnungs** Bereich eine Warnung angezeigt. Eine Warnung umfasst die folgenden Teile:

* Ein Warnsymbol gibt das vorhanden sein eines potenziellen Problems an.

* Der Name der Regel. Beispielsweise ist das **Netzwerk Empfangs Paket Drop** ein Link, der auf die Regel Detailseite zeigt, wie unter [Verwalten von Advisor Packs](#bkmk-manageadvisorpacks)beschrieben.

* Eine einfache Beschreibung des potenziellen Problems.

* Eine Empfehlung für eine mögliche Lösung für das potenzielle Leistungsproblem.

Unterschiedliche Server können die Konfiguration und die Verwendungs Muster erheblich unterscheiden, und es ist nicht möglich, die Schwellenwerte und Regeln festzulegen, die für alle Server unter allen Bedingungen gelten. Spa bietet die Möglichkeit, die Schwellenwerte zu ändern. Sie können eine Regel auch deaktivieren, wenn die Regel nicht für Ihr Szenario gilt. Standardmäßig sind alle Regeln aktiviert. Eine deaktivierte Regel wird nicht im Benachrichtigungsbereich angezeigt. Weitere Informationen finden Sie unter [Managing Advisor Packs](#bkmk-manageadvisorpacks).

Der **andere Benachrichtigungs** Bereich enthält alle anderen Regeln, bei denen keine Warnung ausgelöst oder die Regel nicht anwendbar ist. Sie enthält ähnliche Teile wie im **Warnungs** Bereich. Der größte Unterschied besteht darin, dass, wenn keine Warnung ausgelöst wird oder die Regel nicht anwendbar ist, normalerweise keine Empfehlung bereitgestellt wird.

### <a name="data-sections"></a>Datenabschnitte

Datenabschnitte enthalten die Leistungsdaten, die vom Advisor-Paket basierend auf den von den Ziel Servern gesammelten Rohdaten generiert werden. Datenabschnitte enthalten eine Reihe von Abschnitten der obersten Ebene und mehrere Ebenen von Unterabschnitten. Die Abschnitte der obersten Ebene werden als Registerkarten dargestellt. Alle Unterabschnitte in den Abschnitten der obersten Ebene werden in erweiterbaren Bereichen angezeigt. Sie können die einzelnen Abschnitte reduzieren oder erweitern, um den Fokus auf den Interessenbereich zu setzen, wie in der folgenden Abbildung dargestellt.

![Datenabschnitte](../media/server-performance-advisor/spa-user-manual-data-sections.png)

Das Core OS Spa Advisor Pack und das IIS Spa Advisor Pack enthalten einen Abschnitt **System Übersicht** . Dieser Abschnitt enthält die Informationen der obersten Ebene zur Ressourcenverwendung und-Konfiguration. Andere Abschnitte der obersten Ebene stellen Bereiche von Leistungsdaten dar. Spa zeigt Berichtsdaten auf folgende Weise an:

* **Einzelner Wert** Ein Schlüssel-Wert-Paar. Der Schlüssel ist eine Zeichenfolge, die die Bedeutung des Werts darstellt. Der Wert kann eine Zeichenfolge, ein numerischer Wert oder ein boolescher Wert sein. Dies wird häufig verwendet, um statische Informationen wie z. b. die CPU-Architektur, die Gesamtgröße des Arbeitsspeichers und die BIOS-Version anzuzeigen, die sich im Laufe der Zeit nicht ändern.

* **Listen Wert** Manchmal handelt es sich um ein Schlüssel-Wert-Paar, aber der Listen Wert kann mehrere Felder enthalten. Beispielsweise kann das-Attribut der CPU in einer Tabelle mit mehreren Spalten und mehreren Zeilen angezeigt werden. Jede Zeile stellt eine CPU dar, und jede Spalte stellt ein Attribut der CPU dar.

* **Statistik** Kann als spezieller Typ eines einzelnen Werts angesehen werden. Er darf nur numerische Daten enthalten. Während der Datensammlung schwanken viele der numerischen Datenpunkte und bleiben nicht konstant. Beispielsweise ändert sich die CPU-Auslastung bei jeder Erfassung des Leistungs Zählers durch das Pla. Die Anzeige nur eines einzelnen Werts kann die leistungssituation nicht exakt widerspiegeln. Anstatt nur einen Wert, den Mittelwert, den Höchstwert, den Minimalwert und den Wert von 90% für solche dynamischen numerischen Datenpunkte anzuzeigen. Der Wert 90% stellt eine Aktivität bei oder oberhalb des 90. Perzentils für alle Ereignisse dieses Zählers in diesem angegebenen Sammlungs Intervall dar.

* **Obere Liste** Enthält normalerweise die häufigsten Consumer einer bestimmten Ressource oder die obersten Entitäten, für die bestimmte Ereignisse auftreten. Die **10 wichtigsten Prozesse in Bezug auf die durchschnittliche CPU-Auslastung** umfassen beispielsweise die zehn wichtigsten Prozesse mit der höchsten durchschnittlichen CPU-Auslastung während der Datensammlung. Da die CPU-Auslastung auch ein dynamischer numerischer Datenpunkt ist, sind andere Statistiken wie Maximum, minimal und 90% ebenfalls in der Liste enthalten, um dem Benutzer ein ausführlichere Bild der CPU-Auslastung zu verschaffen.

Wie in den vorherigen Abschnitten erwähnt, baut Spa auf der Erstellung der etw-Ablauf Verfolgung, WMI-Abfragen, Leistungsindikatoren, Registrierungsschlüssel und Konfigurationsdateien auf, um den Bericht zu generieren. Es ist wichtig, dass Sie die Datenquelle hinter den einzelnen Datenpunkten im Bericht verstehen. Spa stellt Informationen über Quick Infos bereit. Sie können mit dem Mauszeiger auf die Schlüssel Spalten oder Zeilen zeigen, um die QuickInfo für die Datenquelle anzuzeigen. Beispielsweise bedeutet **WMI: Win32 \_ disdrive: Caption** , dass die Datenquelle aus einer WMI-Abfrage, der WMI-Klassenname Win32 \_ diskdrive und die Eigenschaft **Beschriftung**ist.

### <a name="side-by-side-report"></a><a href="" id="side-by-side-report-"></a>Paralleler Bericht

Einzelne Berichte stellen Benachrichtigungen und einen Daten Abschnitt bereit, um den Benutzer bei der Suche nach potenziellen Leistungsproblemen zu unterstützen. es ist jedoch oft schwierig, ein mögliches Leistungsproblem zu erkennen, indem Sie einen einzelnen Bericht direkt betrachten. Ein einzelner Bericht kann zu viele Datenpunkte enthalten, wodurch es schwierig wird, potenzielle Probleme zu finden.

Um dieses Problem zu beheben, bietet Spa die Möglichkeit, zwei Berichte zu vergleichen. Sie können einen Bericht mit einem potenziellen Problem mit einem Basisbericht vergleichen, um die Unterschiede zu ermitteln.

Parallele Berichte können von einem Einzel Bericht-Viewer aus gestartet werden. Benutzer können auf **Aktionen**klicken und dann auf **Berichte vergleichen** klicken, um die Berichte auszuwählen. Es ist nur sinnvoll, Berichte desselben Advisor-Pakets zu vergleichen. Sie können den Bericht mit einem vorherigen Bericht in der Zeit, dem nächsten Bericht in der Zeit oder einem beliebigen Bericht vergleichen, der über Suchfunktionen ausgewählt wird. Um z. b. nicht normales Verhalten zu isolieren, können Sie einen Baseline-Server Bericht mit einem Bericht vergleichen, der auf demselben Computer zu einem anderen Zeitpunkt generiert wurde, oder auf einem Bericht, der auf einem anderen Computer mit einer ähnlichen Server Rolle und Last generiert wurde.

Ein paralleler Bericht sieht in etwa wie der einzige Bericht aus. Sie enthält einen Benachrichtigungs Abschnitt und Datenabschnitte. Sie enthält die gleiche Anzahl von Benachrichtigungen und Daten Abschnitten wie die einzelne Bericht Anzeige. Der einzige Unterschied besteht darin, dass die Berichte nebeneinander angezeigt werden. Jeder Abschnitt enthält die Daten aus dem Quell Bericht (Bericht 1) und dem Ziel Bericht (Bericht 2). Der parallele Bericht zeigt den Namen des Advisor-Pakets, den Namen des Zielservers (auf der linken Seite und den Bericht 2 auf der rechten Seite), den Zeitpunkt, zu dem der Bericht generiert wurde, und die Dauer der Datensammlung für die einzelnen Berichte an.

Wenn Sie das Dialogfeld **Suchen** schließen, können Sie es reaktivieren, indem Sie Steuerelement + F eingeben. In diesem Dialogfeld werden Text Zeichenfolgen im aktuellen Abschnitt gefunden und hervorgehoben.

Wenn im Abschnitt Benachrichtigung eine der Ergebnisse aus den zwei verglichenen Berichten eine Warnung ist, wird Sie im **Warnungs** Bereich aufgelistet. Andernfalls werden die Ergebnisse im Bereich **andere Benachrichtigungen** aufgeführt. Da der Schlüssel für einen parallelen Bericht darin besteht, Unterschiede Zwischenberichten zu identifizieren, werden keine detaillierten Informationen zu einer Regel angezeigt. Benutzer können auf den Regel Namen klicken, um das Regel Detail Formular für weitere Informationen zur Regel anzuzeigen.

In den Daten Abschnitten werden die Daten nebeneinander und Daten aus Bericht 1 auf der linken Seite und Daten aus Bericht 2 auf der rechten Seite angezeigt. Spa zeigt einzelne Werte in derselben Tabelle an. statt jedoch den Spalten **Wert**zu bezeichnen, werden Sie als " **Report 1** " bzw. " **Report 2** " bezeichnet. Der parallele Bericht zeigt alle anderen Formen von Daten in parallelen Tabellen an.

Die Seite-an-Seite-Bericht Anzeige bietet auch Quick Infos zur Datenquelle.

### <a name="historical-and-trend-charts"></a>Vergangenheits-und Trenddiagramme

Es ist nur sinnvoll, Trend-und Vergangenheits Diagramme für einen bestimmten Server und ein bestimmtes Advisor-Pack anzuzeigen. Sie müssen den Zeitbereich auswählen (der Standardwert für die letzte Woche ist), und dann auf **OK** klicken, um den Trend und den Verlaufs Diagramm-Viewer anzuzeigen.

Der Trend-und Verlaufs Diagramm-Viewer enthält drei Registerkarten: das Verlaufs Diagramm, das 24-Stunden-Trend Diagramm und das 7-tägige Trend Diagramm.

### <a name="historical-chart"></a>Verlaufs Diagramm

Das Verlaufs Diagramm zeigt eine Reihe von Werten für einen numerischen Datenpunkt über den angegebenen Zeitrahmen an. Beispielsweise die **durchschnittliche Anforderungs** Wartezeit für IIS auf einem einzelnen Server während der letzten 15 Tage. Jeder Datenpunkt in einem Verlaufs Diagramm stellt den Wert einer bestimmten Datenquelle dar, die in einer Leistungsanalyse Sitzung erstellt wurde.

Es gibt mehrere Möglichkeiten, ein Verlaufs Diagramm zu verwenden:

1.  Die **durchschnittliche Anforderungs Latenz** von IIS springt von ungefähr 200 ms auf 500 ms, um zu einem bestimmten Zeitpunkt bei einem Daten 2:00 Punkt nach Anomalien zu suchen.

2.  Zum Korrelieren mehrerer Datenpunkte. Beispielsweise werden die **durchschnittliche Anforderungs Latenz** und die **durchschnittliche Anforderungs Anzahl** in den letzten 15 Tagen angezeigt. Der Bericht zeigt möglicherweise an, dass die Anforderungs Latenz und die Anzahl der Anforderungen zum gleichen Zeitpunkt zunehmen, was darauf hindeuten kann, dass die Erhöhung der Anforderungs Latenz durch eine Erhöhung der Anforderungs Anzahl verursacht wird.

In einem Verlaufs Diagramm können Benutzer folgende Aktionen ausführen:

* Zeigen Sie mehrere Datenreihen in der Diagrammbereich an. Jede Datenreihe wird als Liniendiagramm im Berichts-Viewer angezeigt. Jedes Liniendiagramm wird automatisch so skaliert, dass es in den Berichts-Viewer passt.

* Fügen Sie der Datenreihen Liste unten im Verlaufs Diagramm-Viewer eine Datenreihe hinzu, oder entfernen Sie Sie.

* Ein-oder Ausblenden von Datenreihen in der Datenreihen Liste. Benutzer können auf eine bestimmte Datenreihe in der Liste klicken, um das entsprechende Liniendiagramm im Diagrammbereich hervorzuheben.

* Vergrößern Sie einen bestimmten Zeitraum, indem Sie den Zeitraum in der Diagramm Fläche auswählen. Zum Verkleinern klicken Sie auf die Schaltfläche, die sich in der unteren linken Ecke des Diagramms befindet.

* Untersuchen Sie einen einzelnen Bericht, indem Sie auf einen bestimmten Datenpunkt doppelklicken.

* Kopieren Sie die Daten, und stellen Sie Sie für andere Programme (z. b. Microsoft Excel) zur Verfügung. Dies ermöglicht es Ihnen, bei Bedarf Microsoft Excel-Diagramm Funktionen zu nutzen.

### <a name="trend-charts"></a>Trenddiagramme

Viele wiederkehrende Leistungsprobleme werden dadurch verursacht, dass regelmäßige Tasks auf oder auf Ziel Servern ausgeführt werden. Beispielsweise kann eine Unterhaltungs orientierte Website während des Wochenendes mehr Treffer erhalten, oder ein Task "Datenträger Sicherung planen" kann die Leistung eines Servers täglich um 2:00 Uhr senken.

Ein Trend Diagramm ist so konzipiert, dass Sie derartige Leistungsprobleme finden. Leistungsprobleme können wiederholt in verschiedenen Mustern auftreten. Bei den gängigsten Mustern handelt es sich um tägliche Muster und wöchentliche Muster, bei denen Leistungsprobleme während der gleichen Stunde eines Tages oder desselben Tags auftreten. Daher bietet Spa ein 24-Stunden-Trend Diagramm und ein 7-Tage-Trend Diagramm.

Das Trendanalyse Diagramm bietet einen tieferen Grad an Untersuchung zu einem Satz von Daten und sucht nach Trends basierend auf der Tageszeit. Die X-Achse wird auf einen 24-Stunden-Zeitraum festgelegt, beginnend um 0:00 Uhr (Mitternacht) und endet bei 23:59. Spa zeigt nicht gleichzeitig Trends für mehrere Datenreihen an. Sie können auf **Datenreihe auswählen** klicken, um eine Datenreihe zum anzeigen auszuwählen.

Um die Daten zu verarbeiten, sucht Spa nach allen Momentaufnahmen, die für jede Stunde zwischen 0:00 und 0:59 erstellt wurden. Spa bestimmt die minimalen, maximalen, durchschnittlichen und Sigma-Werte für den Satz von Momentaufnahmen, die während dieser Stunde erstellt wurden, und zeigt Diagramme als Kerzen Diagramme an. Spa wiederholt den Prozess für Momentaufnahmen, die zwischen 1:00 und 1:59, dann 2:00 bis 2:59 usw. erstellt wurden. Wenn für die angegebene Stunde keine Momentaufnahmen vorhanden sind, bleibt diese Stunde im Diagramm leer und fährt mit der nächsten Stunde fort.

Ein 7-Tage-Trend Diagramm ähnelt dem 24-Stunden-Trend Diagramm. Der einzige Unterschied besteht darin, dass eine Datenreihe auf der Grundlage des Wochentags und nicht der Stunde des Tages gruppiert wird.

Die Datenreihen, die Sie in Trend-und Vergangenheits Diagrammen auswählen, werden als Benutzereinstellung gespeichert. Wenn der Trend-und Verlaufs Diagramm-Viewer das nächste Mal für das gleiche Advisor-Pack geöffnet wird, wird derselbe Satz von Datenreihen als Standard aufgeführt.

## <a name="managing-reports"></a>Verwalten von Berichten


### <a name="deleting-reports"></a>Löschen der Berichte

Berichte können entfernt werden, um die Anzahl von Berichten zu minimieren, die von Spa verwaltet werden müssen. Abhängig von der Häufigkeit der Berichte und der Anzahl der Server wird empfohlen, unnötige Berichte zu löschen. Obwohl die Spa nicht über eine Beschränkung für Berichte verfügt, die Sie verwalten kann, kann die zugrunde liegende Datenbank eine Größenbeschränkung aufweisen.

**Hinweis** gelöschte Berichte können nicht wieder hergestellt werden.



### <a name="exporting-and-importing-reports"></a>Exportieren und Importieren von Berichten

Berichte können in eine XML-Datei exportiert werden, um Sie in eine andere Spa-Konsole zu transportieren oder an einen anderen Benutzer zu senden. Wenn Sie den Bericht exportieren, wird der Bericht nicht gelöscht. Klicken Sie zum Exportieren des aktuell angezeigten Berichts in der **Berichts**Anzeige auf **Aktionen**, und klicken Sie dann auf **exportieren**. Wenn Sie mehrere Berichte exportieren möchten, klicken Sie im **Berichts-Explorer**auf **Mehrfachauswahl aktivieren**, wählen Sie im Auswahlfeld mehrere Berichte aus, und klicken Sie dann auf **exportieren**. Dadurch werden die Berichte im XML-Format in das ausgewählte Zielverzeichnis exportiert.

Ein exportierter Bericht kann in Spa angezeigt werden. importierte Berichte werden der Spa-Datenbank nicht hinzugefügt. Sie sind in erster Linie als XML-Viewer-Anwendung für den exportierten Bericht zu fungieren. Auf dem Server für den importierten Bericht müssen nicht dieselben Advisor-Pakete installiert sein wie die Original-Konsole des exportierten Berichts.

## <a name="managing-advisor-packs"></a><a href="" id="bkmk-manageadvisorpacks"></a>Verwalten von Advisor-Paketen


Spa umfasst Advisor-Pakete für das Haupt Betriebssystem, Hyper-V, Active Directory und IIS. Spa bietet eine offene Architektur zum Entwickeln von Advisor-Paketen mithilfe von SQL. Daher ist es auch für Entwickler von Drittanbietern möglich, Versionen von Advisor Packs zu erstellen. Es gibt vier Optionen zum Verwalten eines Advisor-Pakets: bereitstellen, anpassen, zurücksetzen oder entfernen.

### <a name="provision-new-advisor-packs"></a>Neue Ratgeber Pakete bereitstellen

Neue Ratgeber Pakete können von Microsoft oder von Entwicklern, die nicht von Microsoft sind, veröffentlicht werden. Ein Advisor-Pack enthält eine provisionMetaData.xml und einen Satz von SQL-Skripts, die die Logik beschreiben.

**So stellen Sie ein neues Advisor Pack bereit**

1.  Kopieren Sie den gesamten Inhalt des Advisor-Pakets in das Verzeichnis *% sparoot%* \\ APS.

2.  Klicken Sie im Hauptfenster auf **Konfiguration**, und klicken Sie dann auf **Advisor Packs konfigurieren**. Das Dialogfeld **Advisor-Pakete konfigurieren** wird geöffnet.

    **Hinweis** Dieses Dialogfeld ähnelt der Seite des Assistenten zum Bereitstellen von **Advisor-Paketen** . Es wird eine Liste von Advisor-Paketen angezeigt, die zur Verwaltung verfügbar sind. Jedes Advisor-Paket in der Liste verfügt über Eigenschaften wie Name, installierte Version, Version und Autor. Name ist der vollständige Name des Advisor-Pakets, und die installierte Version ist die Version dieses Advisor-Pakets, das bereits im Projekt bereitgestellt wurde. Wenn das Advisor-Pack nicht in der aktuellen Datenbank bereitgestellt wird, wird im Textfeld installierte Version **nicht installiert**angezeigt. Das Feld Version gibt die Version dieses Advisor-Pakets an, das unter dem Advisor Packs-Ordner abgelegt wird.



3.  Wählen Sie das Advisor-Pack aus der Liste aus. Wenn das Advisor-Paket nicht bereitgestellt wurde oder eine neuere Version im Advisor Packs-Ordner als der in der Datenbank vorhanden ist, wird die Schaltfläche **bereit** stellen aktiviert. Klicken Sie auf " **bereit** stellen".

4.  Wenn die Bereitstellung vollständig ist, enthält das Feld **installierte Version** des ausgewählten Advisor-Pakets die neuen Versionsinformationen.

### <a name="customize-advisor-packs"></a>Anpassen von Advisor-Paketen

Spa definiert eine offene Architektur, mit der Benutzer die Advisor-Pakete ändern können. Benutzer können die Advisor Pack-Dateien ändern, indem Sie Schwellenwerte ändern, Schwellenwerte freigeben und Regeln aktivieren bzw. deaktivieren.

Weitere Informationen zum Ändern und Erstellen von Advisor-Paketen finden Sie im [Entwicklungs Handbuch zum Server Performance Advisor Pack](server-performance-advisor-pack-development-guide.md).

### <a name="changing-thresholds"></a>Ändern von Schwellenwerten

In Spa werden Schwellenwerte verwendet, um zu bestimmen, ob die Auslöserbedingung einer Regel erfüllt ist. Die tatsächlichen Schwellenwerte für echte Kunden Szenarien können aufgrund der Arbeitsauslastung, der Hardware Umgebung und der geschäftlichen Anforderungen erheblich variieren. Die Standard Schwellenwerte sind für den aktuellen Benutzer Fall möglicherweise nicht richtig, sodass Spa die Möglichkeit bietet, den vorhandenen Schwellenwert zu ändern.

Sie können Schwellenwerte ändern, indem Sie auf den Regel Namen in einem einzelnen oder einem parallelen Bericht klicken. Oder um alle Regeln eines bestimmten Advisor-Pakets zu verwalten, können Sie die Schwellenwerte im **Konfigurations** Menü ändern.

**So ändern Sie einen Schwellenwert**

1.  Klicken Sie im Menü **Konfiguration** auf **Advisor Packs konfigurieren**, klicken Sie auf den Namen des Advisor-Pakets, das geändert werden soll, und klicken Sie dann auf **Konfigurieren**.

    **Hinweis** Ihnen wird eine Liste aller Regeln angezeigt, die im Advisor-Paket enthalten sind. Das Kontrollkästchen links neben dem Advisor-Paketnamen gibt an, ob die Regel aktiviert ist. Wenn eine Regel deaktiviert ist, wird Sie in allen Berichten ausgeblendet.



2.  Klicken Sie auf die jeweilige Regel, die Sie ändern möchten. Das Formular " **Regel Details** " für die ausgewählte Regel wird geöffnet.

Das Formular "Regel Details" enthält ausführliche Informationen zu einer bestimmten Regel. Sie enthält den Namen, die Beschreibung, den Status, mögliche Ergebnisse und Schwellenwerte. Spa unterstützt zwei Arten von Regel Ergebnissen: **Warnung** und **OK**. Für jeden Typ gibt es Empfehlungs Text und eine Empfehlung.

Für einige Regeln sind keine Schwellenwerte definiert. Beispielsweise prüft die **HTTP Keep-Alive** -Regel, ob eine boolesche Einstellung für IIS festgelegt ist. Daher ist die Liste der Schwellenwerte möglicherweise leer. Andernfalls werden alle Schwellenwerte aufgelistet, die von der aktuellen Regel verwendet werden. Eine ausführliche Beschreibung, wie ein Schwellenwert in der Regel verwendet wird, ist als Teil der Beschreibung enthalten.

Wenn das Formular " **Regel Details** " im **Konfigurations** Menü gestartet wird, enthält die Schwellenwert Liste drei Spalten: Name, ursprüngliche Einstellung und Änderungs Einstellung. Wenn Sie über einen einzelnen oder einen parallelen Bericht gestartet wird, werden die Schwellenwerte, die vom Bericht verwendet werden, ebenfalls eingeschlossen. Benutzer können die aktuellen Schwellenwerte ändern, indem Sie den Wert in der Spalte **Änderungs Einstellung** ändern und dann auf **Speichern** klicken, um die Änderungen in der Datenbank zu speichern.

Alle Änderungen, die an Schwellenwerten vorgenommen werden, werden nur auf Berichte angewendet, die nach den Änderungen generiert werden. Vorhandene Berichte sind von diesen Änderungen nicht betroffen.

### <a name="sharing-thresholds"></a>Freigabe Schwellenwerte

Wenn Sie Ihre Server in ähnlichen Situationen verwalten, können Sie auch denselben Satz von Schwellenwerten verwenden. Mithilfe des **Konfigurations** Menüs können Sie Schwellenwerte für ein bestimmtes Advisor Pack exportieren und importieren. Sie können das jeweilige Advisor-Paket auswählen und dann auf **Konfigurieren**klicken. Die exportierte Schwellenwert Datei hat ein XML-Format.

Beim Importieren eines Schwellenwerts überprüft Spa das XML-Dateiformat und überprüft, ob die Datei mit dem ausgewählten Advisor Pack übereinstimmt. Wenn dies erfolgreich ist, importiert Spa alle Werte aus der Schwellenwert Datei in die aktuelle Projektdatenbank. Ähnlich wie beim vorherigen Szenario mit veränderlichen Schwellenwerten werden alle Schwellenwert Änderungen nur für Berichte wirksam, die in Zukunft generiert werden. Vorhandene Berichte sind nicht betroffen.

### <a name="enable-or-disable-rules"></a>Aktivieren oder Deaktivieren von Regeln

Eine Regel kann im Formular " **Regel Details** " aktiviert oder deaktiviert werden. Sie müssen auf **Speichern** klicken, um die vorgenommenen Änderungen beizubehalten. Wenn eine Regel deaktiviert ist, kann Sie nicht in einem der Berichte angezeigt werden. Die zugrunde liegende Geschäftslogik wird jedoch beim Erstellen des Berichts ausgelöst. Wenn Sie also die Regel erneut aktivieren, wird Sie erneut in Berichten angezeigt.

### <a name="reset-advisor-packs-to-original-state"></a>Zurücksetzen von Advisor Packs in den ursprünglichen Zustand

Sie können ein bereitgestelltes Advisor-Paket in der-Datenbank ändern. Mit Ausnahme der Änderung der Schwellenwerte können Sie auch die SQL-Skripts ändern. Spa unterstützt das Ändern von Berichts Metadaten oder das Hinzufügen oder Entfernen von Regeln für ein bereitgestelltes Advisor Pack nicht. Das manuelle Ändern dieser Bereiche kann zu unerwartetem Verhalten führen.

Weitere Informationen zum Ändern eines bereitgestellten Advisor-Pakets finden Sie im [Entwicklungs Handbuch zum Server Performance Advisor Pack](server-performance-advisor-pack-development-guide.md).

Wenn Sie Änderungen zurücksetzen möchten, die an einem bereitgestellten Advisor-Paket vorgenommen wurden, können Sie das Advisor-Paket zurücksetzen. Dies überschreibt alle SQL-Skripts, die mit dem Advisor-Paket verknüpft sind, und setzt alle Standard Schwellenwerte zurück. Dadurch werden alle vorhandenen Berichte beibehalten.

zum Zurücksetzen des Advisor-Pakets können Sie das Formular **Advisor Packs konfigurieren** verwenden. Sie müssen das Advisor-Paket auswählen, das zurückgesetzt werden soll, und dann auf **Zurücksetzen**klicken.

### <a name="remove-advisor-packs"></a>Advisor-Pakete entfernen

Wenn ein Advisor-Pack nicht mehr benötigt wird, können Benutzer es aus der Datenbank entfernen. Wenn Sie das Advisor-Paket entfernen, werden alle Informationen über das Advisor-Pack aus der Datenbank entfernt, einschließlich der Regeln und Schwellenwerte, aller SQL-Skripts und sämtlicher Berichte. Für keine der Aktionen kann ein Rollback ausgeführt werden.

zum Entfernen des Advisor-Pakets können Sie das Formular **Advisor Packs konfigurieren** verwenden. Wählen Sie das zu entfernende Advisor-Paket aus, und klicken Sie dann auf Aufhebung der **Bereitstellung**.

### <a name="update-existing-advisor-packs"></a>Aktualisieren vorhandener Advisor-Pakete

Das Aktualisieren vorhandener Advisor Packs ähnelt dem Zurücksetzen des Advisor-Pakets auf seinen ursprünglichen Zustand. Wenn Sie das Advisor Pack auf eine neuere Version aktualisieren möchten, kopieren Sie das neue Advisor-Paket in den Advisor Pack-Ordner. Ein Advisor-Pack gilt nur dann als Update für ein vorhandenes Advisor Pack, wenn keine Änderung der Berichts Metadaten vorliegt. Der Bericht und die Regel-IDs müssen identisch sein. Andernfalls sollten Sie als zwei verschiedene Advisor-Packs behandelt werden.

Wenn nur Änderungen an der Geschäftslogik und keine Änderungen an der Berichts Metadaten für ein Advisor-Paket vorgenommen werden, sollte eine neue Versionsnummer angegeben werden, z. b. von 1,0 bis 2,0. Wenn sich die Änderung der Berichts Metadaten ändert, sollte dem Advisor-Paket ein anderer vollständiger Name zugewiesen werden. Beispielsweise könnte Microsoft. serverperformanceadvisor. IIS. v1 in Microsoft. serverperformanceadvisor. IIS. v2 geändert werden.

Wenn eine neuere Version des Advisor-Pakets vorhanden ist, füllt die Liste im Formular **Advisor-Pakete konfigurieren** automatisch die **Versions** Spalte mit der neuesten Version des Advisor-Pakets aus. Sie können das Advisor-Paket auswählen und dann auf **Zurücksetzen**klicken. Das Advisor Pack wird mit der neuen Geschäftslogik und den Schwellenwerten aktualisiert. Alle Berichte für dieses Advisor Pack werden beibehalten.

## <a name="managing-servers"></a>Verwalten von Servern


Spa stellt grundlegende Funktionen für die Verwaltung von Ziel Servern bereit. Sie können auswählen, ob Sie der Liste der Zielserver neue Server hinzufügen, Server aus der Liste entfernen oder die Hinweise für Server ändern möchten.

**So können Sie Server hinzufügen oder entfernen oder Server Informationen ändern**

1.  Klicken Sie auf das Menü **Konfiguration** , und klicken Sie auf **Server konfigurieren**.

2.  In der Liste der Server, die zurzeit in der Projektdatenbank vorhanden sind, ist die letzte Zeile leer. Klicken Sie auf die Zeile, und füllen Sie die Felder aus. Die Felder **Servername** und **Dateifreigabe Speicherort** Ordner sind obligatorisch, und der Servername muss eindeutig sein.

3.  Geben Sie für jeden Server in der Spalte " **Anmerkung** " weitere Server Informationen ein.

    **Hinweis** In diesem Feld wird ein kostenloses Textformat verwendet, sodass Sie es als Beschreibungsfeld verwenden können. Oder verwenden Sie dieses Feld, um die Server zu markieren, damit Sie im Hauptfenster problemlos gefunden werden können, oder zum Gruppieren von Servern, z. b. nach Standort oder Server Rolle.



4.  Wenn Sie Spa mit einer großen Anzahl von Servern verwenden möchten, unterstützt Spa ein durch Kommas getrenntes Format (. CSV) für den Import. Die Datei muss mindestens zwei Felder enthalten: **Server** -und **Dateifreigabe Speicherort**. Das dritte Feld, " **Anmerkung** ", ist optional, aber es wird empfohlen, die Server zu organisieren. Sie können die Serverliste auch in eine CSV-Datei exportieren, um das entsprechende Format zu ermitteln oder die Serverkonfiguration zu sichern.

### <a name="searching-and-filtering"></a>Suchen und Filtern

Wenn Sie mehr als ein paar Server verwalten, bietet Spa grundlegende Unterstützung für die schnelle Suche der Server im Hauptfenster. Sie können auf die Spaltenüberschrift klicken, um Sie basierend auf dem Servernamen, den Analyseergebnissen, dem aktuellen Task Status oder den Anmerkungen zu sortieren. Sie können auch die Suchfunktion verwenden. In der oberen rechten Ecke des Hauptfenster können Sie eine Zeichenfolge eingeben, nach der gesucht werden soll. Die Liste der **Zielserver** im Hauptfenster verwendet die Zeichenfolge zum Filtern der Server und zum Anzeigen von Servern mit den Feldern "Name" und "Anmerkung", die die Such Zeichenfolge enthalten.

In der folgenden Abbildung wird gezeigt, wie die Zeichenfolge **Dell** Server mit der Zeichenfolge **Dell** oder Servern mit dem Feld " **Anmerkung** " vergleicht, das **delL**enthält.

![Beispiel für suchen und Filtern](../media/server-performance-advisor/spa-user-manual-find-search-example.png)

## <a name="advanced-functionality"></a>Erweiterte Funktionalität


### <a name="working-with-spa-windows-powershell-cmdlets"></a>Arbeiten mit Windows PowerShell-Cmdlets für Spa

Die Spa-Konsole unterstützt die Benutzeroberfläche für die wiederholte Datensammlung. Wenn diese Funktionalität für Ihre Umgebung nicht ausreicht, gibt es Windows PowerShell-Cmdlets, mit denen ein erweiterter Administrator die Datensammlung anpassen kann. Diese Windows PowerShell-Cmdlets ermöglichen Systemadministratoren das automatische Ausführen von Leistungsanalysen auf Ziel Servern und die Verwendung von Spa für den Remote Kundensupport. Systemadministratoren können z. b. Skripts zum Aufrufen von Spa-Cmdlets in bestimmten Zeitintervallen schreiben, um die Leistung der Zielserver in regelmäßigen Abständen zu testen.

Es wird empfohlen, die SPAConsole.exe Anwendung zu schließen, bevor Sie diese Cmdlets verwenden.

Bevor Sie Windows PowerShell-Cmdlets ausführen, müssen Sie die Cmdlets auf dem Konsolen Computer registrieren.

**So registrieren Sie die Windows PowerShell-Cmdlets**

1.  Geben Sie an einer Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten den Befehl **registerspacmdlets. cmd**ein. Die Meldung zum **Registrieren von Spa-Cmdlets** wird angezeigt.

2.  Führen Sie **Spa-PowerShell. cmd**aus. Wenn Sie den Pfad an eine Windows PowerShell-Skriptdatei übergeben, führen Sie die Skripts automatisch aus. Andernfalls wird eine Windows PowerShell-Eingabeaufforderung geöffnet, die zum Ausführen von Windows PowerShell-Cmdlets für das Spa bereit ist.

In der folgenden Tabelle werden die Windows PowerShell-Cmdlets für Spa beschrieben:

| Cmdlet-Name | Parameter | BESCHREIBUNG |
| ------ | ------- | ------ |
| Start-spaanalysis | **-Servername** Der Name des Zielservers.<br>**-Advisorpackname** Vollständiger Name des Advisor-Pakets, das auf dem Server in die Warteschlange gestellt werden soll Wenn mehrere Pakete zur gleichen Zeit ausgeführt werden sollen, muss der Wert des-Parameters als AP1name, AP2name formatiert werden.<br>**-Dauer** Dauer für die Datensammlung.<br>**-Credential** Benutzer Anmelde Informationen für das Konto, mit dem die Datensammlung auf dem Zielserver ausgeführt wird.<br>**-SqlInstanceName** Der Name der SQL Server Instanz.<br>**-SQLDatabaseName** Der Name der Spa-Projektdatenbank. | Startet eine Spa-Daten Sammlungs Sitzung auf dem angegebenen Server. |
| "Ende-spaanalysis" | **-SqlInstanceName** Der Name der SQL Server Instanz.<br>**-SQLDatabaseName** Der Name der Spa-Projektdatenbank.<br>**-Servername** Der Name des Zielservers. | Versucht, eine laufende Spa-Sitzung zu verhindern. Wenn eine Sitzung bereits beendet ist, wird Sie zurückgegeben, ohne etwas zu tun. |
| Get-spaserver | **-SqlInstanceName** Der Name der SQL Server Instanz.<br>**-SQLDatabaseName** Der Name der Spa-Projektdatenbank. | Ruft die Serverliste in der Datenbank ab. Sie gibt eine Liste von-Objekten zurück, einschließlich der folgenden Eigenschaften: Name, Status, Dateifreigabe und Anmerkung. |
| Get-spaadvisorpacks | **-SqlInstanceName** Name der SQL Server Instanz<br>**-SQLDatabaseName** Name der Spa-Projektdatenbank | Ruft die Advisor Pack-Liste in der Datenbank ab. Sie gibt eine Liste von-Objekten zurück, einschließlich der folgenden Eigenschaften: Name, Display Name, Author und Version. |

Windows PowerShell bietet die Möglichkeit, Anmelde Informationen über verschlüsselte Dateien zu übergeben, um Automatisierungs Szenarios zu ermöglichen. Weitere Informationen zur Verwendung verschlüsselter Dateien zum Übergeben von Anmelde Informationen an ein Cmdlet finden Sie unter [Erstellen von Windows PowerShell-Skripts, die Anmelde Informationen akzeptieren](/previous-versions/technet-magazine/ff714574(v=msdn.10)).

### <a name="automating-spa-report-collection-by-using-windows-powershell"></a>Automatisieren der Spa-Bericht Sammlung mithilfe von Windows PowerShell

Die folgenden Prozeduren stellen ein Beispiel für das Automatisieren einer Spa-Bericht Sammlung mithilfe der Windows PowerShell-Cmdlets für Spa dar.

Benutzer Anmelde Informationen können mithilfe von Windows PowerShell verschlüsselt und zwischengespeichert werden. Diese Anmelde Informationen werden verwendet, um sich bei Remote Servern anzumelden. Obwohl es sich nicht um die Spa handelt, wird im folgenden Beispiel dieses Verfahren veranschaulicht:

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

Bevor Sie diese Datei ausführen können, müssen Sie **Set-ExecutionPolicy RemoteSigned** ausführen.

Sie können Sie mithilfe des folgenden Befehls aus einer Batchdatei ausführen:

``` syntax
PowerShell -command "& '.\RunSpa.ps1' "
```

### <a name="use-t-sql-to-generate-reports"></a>Verwenden von T-SQL zum Generieren von Berichten

Spa-Berichtsdaten können mithilfe von SQL extrahiert werden, um benutzerdefinierte Berichte zu erstellen, die nicht innerhalb der SPAConsole.exe bereitgestellt werden.

der folgende T-SQL-Befehl stellt z. b. eine Top 10-Liste der Server nach CPU für den Zeitraum bereit, der die letzten drei Tage umfasst:

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

In einigen Fällen möchten Sie möglicherweise die von Spa verwendeten SQL Server Datenbanken partitionieren. Dies kann dazu beitragen, die Datengröße der SQL Server Datenbank zu reduzieren oder die Server logisch zu partitionieren. In diesen Fällen werden von der Spa-Konsole mehrere Projekte unterstützt. Sie können eine neue Projektdatenbank erstellen, indem Sie auf **Datei**und dann auf **Neues Projekt**klicken. Der Assistent zum ersten Mal wird zum Erstellen der neuen Projektdatenbank angezeigt.

Nachdem die Projekte erstellt wurden, können Sie auf **Datei**und dann auf **Projekt öffnen** klicken, um zwischen Projekten zu wechseln. Die Spa-Konsole lässt das Wechseln von Datenbanken nicht zu, wenn eine ausstehende Leistungsanalyse innerhalb des aktuell geöffneten Projekts ausgeführt wird. Dies dient zum Schutz der Integrität der Leistungsdaten.

Wenn Sie eine neue Projektdatenbank erstellen oder eine andere Projektdatenbank öffnen, wird das aktuelle Projekt geschlossen. Alle geöffneten Berichte werden geschlossen, wenn das aktuelle Projekt geschlossen wird.

**Hinweis** SQL Server 2008 R2 Express hat eine Daten Bank Beschränkung von 10 GB. Wenn Sie mehrere Projekte verwenden, können Sie eine oder mehrere SQL Server Datenbanken verwenden und unter dem Limit von 10 GB SQL Server 2008 R2 Express bleiben.



### <a name="logging-and-debugging"></a>Protokollierung und Debugging

Spa stellt grundlegende Protokollierungsfunktionen bereit. Es können nur Protokolle in eine Protokolldatei geschrieben werden, die sich im selben Ordner wie SPAConsole.exe befindet. Das Benutzerkonto, in dem die Spa-Konsole ausgeführt wird, muss über die Berechtigung Schreiben für den Ordner verfügen, in dem Spa installiert wurde, um sicherzustellen, dass die Protokolle in die Protokolldatei geschrieben werden können.

Spa enthält die folgenden gültigen Protokoll Ebenen:

* **Information** Sichert Protokolle für jede Aktion, die von der Spa-Konsole ausgeführt wird, und ist in erster Linie für Debugzwecke konzipiert.

* **Warnung** Protokolliert alle Fehler und Ausnahmen, die innerhalb der Spa-Konsole auftreten. Einige der Fehler sind einfach Validierungs Fehler, die von der Spa-Konsole behandelt werden können.

* **Kritisch** Protokolliert nur Fehler und Ausnahmen, die von der Spa-Konsole nicht behandelt werden können. Diese Fehler verursachen einen Absturz der Spa-Konsole. Die Protokolle stellen die Kontextinformationen zu solchen Fehlern bereit.

Standardmäßig ist die Protokollebene "Warnung", was bedeutet, dass die Spa nur Fehler und Ausnahmen protokolliert, die in Spa auftreten. Die Protokollebene kann geändert werden, indem Sie die **SpaConsole.exe.config** Datei im selben Ordner bearbeiten, in dem sich SpaConsole.exe befindet. Alle Protokolle werden in log.txt Datei im selben Ordner geschrieben.

Spa bietet auch einige grundlegende Funktionen für das Debuggen. Um das Debuggen für Spa zu aktivieren, müssen Benutzer die Spa-Projektdatenbank manuell ändern. Die Einstellung wird in einer Konfigurations Tabelle gespeichert. Der Benutzer muss das folgende SQL-Skript ausführen, um das Spa-Projekt in den Debugmodus zu ändern:

``` syntax
UPdate [Configurations] SET Value = N'true' WHERE Name = N'Debugmode'.
```

Im Debugmodus behält das Spa-Framework alle temporären Daten bei, die während der Leistungsanalyse generiert werden, damit Sie Probleme in den Advisor-Paketen beheben können. Dieses Skript ist hauptsächlich für die Verwendung durch Advisor Pack-Entwickler konzipiert.

Weitere Informationen zu den Debuggingfunktionen in Spa finden Sie im [Entwicklungs Handbuch zum Server Performance Advisor Pack](server-performance-advisor-pack-development-guide.md).

### <a name="managing-the-database"></a>Verwalten der Datenbank

### <a name="backup-and-restore-the-database"></a>Sichern und Wiederherstellen der Datenbank

Die Spa-Konsole stellt keine Funktionen zum Sichern und Wiederherstellen der Spa-Datenbank bereit. Zum Sichern und Wiederherstellen von Datenbanken sollten Sie standardmäßige Microsoft SQL Server Tools und Skripts verwenden.

### <a name="clean-up-the-database"></a>Bereinigen der Datenbank

Die Größe der Spa-Projekt Datenbanken kann zunehmen, wenn eine höhere Leistungsanalyse ausgeführt wird. Standardmäßig speichert Spa alle Berichte. Möglicherweise möchten Sie alte Berichte entfernen, um die Leistung zu verbessern. Berichte können über die Benutzeroberfläche des **Berichts-Explorers** gelöscht werden.

## <a name="privacy-and-security"></a>Datenschutz und -sicherheit


Spa unterstützt nur die Datensammlung von Ziel Servern zur Spa-Konsole. Es ist nicht darauf ausgelegt, Informationen an Microsoft-oder nicht-Microsoft-Entwickler zu senden. Weitere Informationen zum Datenschutz in Spa finden Sie in den Microsoft-Software-Lizenzbedingungen für den Server Performance Advisor.

Alle Daten, die von Spa gesammelt werden, werden in den Projekt Datenbanken gespeichert. Aufgrund der Art einiger etw-Ablauf Verfolgungen kann Spa vertrauliche Informationen erfassen, die eine hohe geschäftliche Wichtigkeit aufweisen können. Sie sollten sich über das potenzielle Risiko im Zusammenhang mit der Freigabe des Zugriffs auf die Spa-Projekt Datenbanken im klaren sein. Temporäre Protokolldateien werden in den freigegebenen Ordnern gespeichert, die auf den einzelnen Bereitstellungs Ziel Computern angegeben werden. Obwohl Spa versucht, diese temporären Protokolldateien zu löschen, wenn der Datenimport abgeschlossen ist, gibt es keine Garantie dafür, dass diese Protokolldateien immer gelöscht werden. Stellen Sie sicher, dass sich die freigegebenen Ordner an sicheren Orten befinden.

Spa Advisor Packs enthalten SQL-Skripts zum Analysieren und Analysieren von Leistungs Berichten zum Generieren von Leistungs Berichten. Spa versucht, die Berechtigung einzuschränken, unter der diese Skripts ausgeführt werden. Es besteht jedoch weiterhin die Möglichkeit, dass die Skripts vertrauliche Informationen über die Spa von den Ziel Servern sammeln oder vertrauliche Informationen abrufen oder ändern können, die in derselben Spa-Projektdatenbank gespeichert sind. Sie müssen sicherstellen, dass alle Advisor-Pakete, die in der Spa-Projektdatenbank bereitgestellt werden, aus vertrauenswürdigen Quellen stammen.

## <a name="errors-and-troubleshooting"></a>Fehler und Troubleshooting


### <a name="spaconsoleexe-does-not-start-or-write-log-file"></a>Die Protokolldatei wird von SPAConsole.exe nicht gestartet oder geschrieben.

Wenn Sie versuchen, SPAConsole.exe zum ersten Mal auszuführen, wenn die .NET Framework nicht installiert ist, wird von der Anwendung keine Protokolldatei gestartet oder geschrieben. Stellen Sie sicher, dass ein compatible.NET-Framework installiert ist und ordnungsgemäß funktioniert, bevor Sie Spa starten.

### <a name="locating-log-information"></a>Suchen von Protokollinformationen

Spa speichert Fehlerinformationen in der log.txt-Datei im Ordner "Spa". ausführliche Fehlermeldungen und Informationen zur aufrufsstapel werden in diesen Ordner geschrieben. Wenn Fehler auftreten, die weitere Informationen zur Interpretation benötigen, können Sie log.txt Datei öffnen, um die Fehlerdetails anzuzeigen.

### <a name="database-size-limitations-for-sql-server-express"></a>Einschränkungen der Datenbankgröße für SQL Server Express

SQL Server Express hat für eine Benutzerdatenbank eine Größenbeschränkung von 10 GB. Diese Datenbankgröße verfügt über die Kapazität, 20.000 30.000 Berichte zu speichern. Um die Wahrscheinlichkeit zu verringern, dass das Daten Bank Limit erreicht wird, empfiehlt es sich, Berichte regelmäßig zu löschen und/oder eine andere Version von SQL Server zu verwenden, die nicht die 10-GB-Einschränkung der Benutzerdatenbank

### <a name="sql-server-express-log-size-and-disk-capacity"></a>SQL Server Express Protokoll Größe und Datenträger Kapazität

Wenn Sie SQL Server Express verwenden, ist die Benutzerdatenbank auf 10 GB beschränkt, aber die zugehörige Protokolldatei kann 70 GB überschreiten. Aus diesen Gründen empfehlen wir 100 GB oder mehr freien Speicherplatz für SQL Server Express. Dieser Speicherplatz muss ausreichen, um ca. 20.000 bis 30.000 Berichte zu speichern. Diese Protokolldatei hat den Namen spadb \_ Log. ldf und befindet sich unter **% Program Files% \\ Microsoft SQL Server \\ MSSQL10. SQLExpress- \\ MSSQL- \\ Daten**.

### <a name="failure-to-connect-to-target-server"></a>Fehler beim Herstellen einer Verbindung mit dem Zielserver.

Wenn Sie die Leistungsanalyse auf Ziel Servern ausführen, benötigt das Benutzerkonto, unter dem die Spa-Konsole ausgeführt wird, bestimmte Berechtigungen, um den Datensammler auf den Ziel Servern in die Warteschlange des Datensammler Satzes zu setzen. Die Windows-Firewall-Einstellungen müssen auch geändert werden, damit die Pla-Kommunikation durchlaufen werden kann. Ausführliche Konfigurations Anweisungen finden Sie unter [Einrichten von Spa](#bkmk-setupspa).

### <a name="failure-to-create-pla-data-collection-set-on-the-target-server"></a>Fehler beim Erstellen des Pla-Daten Sammlungs Satzes auf dem Zielserver.

Wenn Sie die Meldung zum Erstellen eines Daten Sammlungs Satzes auf dem Zielserver nicht erstellen können, stellen Sie sicher, dass Sie die folgenden Schritte ausführen:

* Stellen Sie sicher, dass die **Leistungs Protokolle &** Warnungs Dienst ausgeführt werden.

* Die Sicherheitseinstellung **Netzwerk Zugriff: keine Speicherung von Kenn Wörtern und Anmelde Informationen für die Netzwerk Authentifizierung zulassen** ist deaktiviert. Die Sicherheitseinstellung muss deaktiviert werden, da Spa die Benutzer Anmelde Informationen verwenden muss, um den Daten Sammlungs Satz auf dem Zielserver zu erstellen.

### <a name="running-spa-against-the-console"></a><a href="" id="running-spa-against-the-console-"></a>Ausführen von Spa mit der Konsole

Die Pla durchläuft einen anderen Channel, wenn der Zielserver mit der Spa-Konsole identisch ist. Auch wenn für das Benutzerkonto die Spa-Konsole mit Administratorrechten ausgeführt wird, schlägt die Ausführung von Pla fehl. Wenn die Spa-Konsole auf einem Zielserver installiert ist, müssen die Benutzer die Spa als Administrator starten, um sicherzustellen, dass die Leistungsanalyse Aufgabe in der Konsole ausgeführt werden kann.

### <a name="running-multiple-consoles-at-the-same-time"></a>Gleich zeidas Ausführen mehrerer Konsolen

Spa unterstützt nicht mehrere Konsolen, die gleichzeitig für dieselbe Spa-Projektdatenbank ausgeführt werden. Spa bietet auch keine Sperr-und Synchronisierungs Mechanismen, um die Ausführung zu verhindern. Wenn zwei Spa-Konsolen gleichzeitig ausgeführt werden, verhält sich die Konsole in Abhängigkeit von der Zeitsequenz, in der diese Spa-Konsolen ausgeführt werden, inkonsistent. Um dies zu verhindern, sollten alle in der Warteschlange befindlichen Leistungsanalyse Sitzungen aus der Liste entfernt werden, bevor Sie von der-Konsole verarbeitet werden, die die Analyse startet.

Spa schützt die Integrität der einzelnen Berichte, die von Spa erfolgreich generiert wurden. Gleichzeitig garantiert Spa nicht, dass alle in der Warteschlange befindlichen Analyseaufgaben abgeschlossen sind. Wenn inkonsistente Statusänderungen für Leistungsanalyse Sitzungen oder Fehler angezeigt werden, die behaupten, dass das System keine Leistungs Protokolle finden kann, die vom Datensammler Satz generiert werden, wird es wahrscheinlich durch mehrere Spa-Konsolen Instanzen verursacht, die für dieselbe Spa-Projektdatenbank ausgeführt werden.

Das Ausführen von Windows PowerShell-Cmdlets für Spa kann auch von einer Spa-Konsole beeinflusst werden, die für dieselbe Spa-Datenbank ausgeführt wird. Es wird empfohlen, dass Sie die Spa-Konsole schließen, bevor Sie die Windows PowerShell-Cmdlets für Spa ausführen.

### <a name="spaconsoleexe-recurring-collection-is-disrupted"></a>SPAConsole.exe wiederkehrende Sammlung wird unterbrochen.

Wenn Sie die SPAConsole.exe ausführen und eine wiederholte Datensammlung (z. b. eine stündliche Sammlung) verwenden, sollte sich der Server, auf dem die SPAConsole.exe ausgeführt wird, nicht im Energiesparmodus befinden, sodass er angehalten werden kann. Spa prüft nicht, ob eine Energiespar Richtlinie verwendet wird. Diese angehaltene Aktivität kann die reguläre wiederkehrende Datensammlung stören.

### <a name="lost-etw-events"></a>Verlorene ETW-Ereignisse

Um minimale Auswirkungen auf die Leistung auf Ziel Servern zu erzielen, ist die Ausführung von Pla mit niedriger Priorität geplant, während Leistungsinformationen gesammelt werden. Wenn der Zielserver ausgelastet ist, können Sie einige der Daten Sammlungs Tasks löschen, um Sie für Aufgaben mit hoher Priorität, die auf Ziel Servern ausgeführt werden, zu erzielen. Sie sollten das Einrichten des freigegebenen Ordners in Erwägung nehmen, in dem die Ereignisse auf einem Datenträger geschrieben werden, der keinen Konflikt mit der e/a-Auslastung der Arbeitsauslastung oder einem schnelleren Laufwerk (z. b. SSD) hat. Wenn Ereignisse gelöscht werden, werden Sie in der Berichtsansicht angezeigt, da verlorene Ereignisse die Zuverlässigkeit der generierten Leistungsmetriken beeinträchtigen können.

Bestimmte Berechtigungsprobleme können auch bewirken, dass Registrierungs-oder WMI-Abfragen übersprungen werden. Dies ist jedoch weitaus weniger wahrscheinlich als bei einem ETW-Ereignis Verlust. Folglich enthalten die Ergebnisse des Datensammler Satzes manchmal nicht alle angeforderten Werte. Sie müssen sicherstellen, dass die Situation von den T-SQL-Skripts für alle Advisor Packs behandelt wird. Wenn die Daten im Daten Sammlungs Ergebnis nicht vorhanden sind, werden Sie in den Berichten als keine Daten gekennzeichnet.

Da der ETW-Ereignis Verlust bei Pla häufig auftritt, sind Datenpunkte, die basierend auf einer etw-Ablauf Verfolgung generiert werden, möglicherweise nicht konsistent mit Datenpunkten, die basierend auf, z. b. Leistungsindikatoren, generiert werden. Beispielsweise ist es möglich, zu sehen, dass die CPU-Gesamtauslastung durch IIS 80% beträgt (was aus Leistungsindikatoren stammt) und dass die Top-URLs nur 10% der gesamten CPU-Zeit (ein Datenpunkt, der aus der etw-Ablauf Verfolgung stammt) verwenden. Normalerweise kann die Datenquelle für einen Datenpunkt über die QuickInfo des Daten Punkts angezeigt werden. Sie sollten sich über die Auswirkungen dieses Daten Verlusts im klaren sein.

Um derartige Ereignis Verluste zu vermeiden, sollte der Ergebnis Ordner auf dem Zielserver geschlossen werden.

Wenn die Ergebnisse des Daten Sammlers unvollständige Daten als etw-Ablauf Verfolgungs Verlust enthalten und der Advisor Pack-Entwickler Unterstützung für die Benachrichtigung über etw-Ereignis Verlust hinzugefügt hat, wird eine Informationsleiste oberhalb des einzelnen Berichts angezeigt, um den Benutzer über den potenziell inkonsistenten Bericht zu benachrichtigen, der durch Datenverlust verursacht wurde. Ausführliche Informationen zum Datenverlust finden Sie in der log.txt-Datei.

## <a name="glossary"></a>Glossar


Im folgenden finden Sie einige der in Spa verwendeten Begriffe:

* **Advisor-Pack** Eine Auflistung von Metadaten und T-SQL-Skripts, mit denen die vom Zielserver gesammelten Leistungs Protokolle verarbeitet werden. Das Advisor-Pack generiert dann Berichte aus den Leistungs Protokolldaten. Die Metadaten im Advisor-Pack definieren die Daten, die vom Zielserver für Leistungsmessungen gesammelt werden sollen. Die Metadaten definieren auch den Satz von Regeln, die Schwellenwerte und das Berichtsformat. In den meisten Fällen wird ein Advisor-Pack speziell für eine einzelne Server Rolle geschrieben, z. b. Internetinformationsdienste (IIS).

* Die **Spa-Konsole** SpaConsole.exe, die der zentrale Teil der Spa ist. Die Spa muss nicht auf dem Zielserver ausgeführt werden, den Sie testen. Die Spa-Konsole enthält alle Benutzeroberflächen für Spa, von der Einrichtung des Projekts bis hin zur Ausführung von Analysen und Anzeigen von Berichten. Das Spa ist eine Anwendung mit zwei Ebenen. Die Spa-Konsole enthält die UI-Schicht und einen Teil der Geschäftslogik Ebene. Die Spa-Konsole plant und verarbeitet Leistungsanalyse Anforderungen.

* **Spa-Framework** Bietet alle Benutzeroberflächen, die Verarbeitung von Leistungs Protokollen, die Konfiguration, die Fehlerbehandlung und Datenbank-APIs sowie Verwaltungs Prozeduren.

* **Spa-Projekt** Eine Datenbank, die alle Informationen zu den Ziel Servern, Advisor Packs und Leistungsanalyse Berichten enthält, die auf den Ziel Servern für die Advisor-Pakete generiert werden. Sie können Verlaufs-und Trenddiagramme innerhalb desselben Spa-Projekts vergleichen und anzeigen. Sie können mehr als ein Projekt erstellen. Die Spa-Projekte sind voneinander unabhängig, und es gibt keine Daten, die von allen Projekten gemeinsam genutzt werden.

* **Zielserver** Der physische oder virtuelle Computer, auf dem Windows Server mit bestimmten Server Rollen (z. b. IIS) ausgeführt wird.

* **Datenanalyse Sitzung** Eine Leistungsanalyse auf einem bestimmten Zielserver. Eine Datenanalyse Sitzung kann mehrere Advisor-Pakete enthalten. Die Datensammler Sätze aus diesen Advisor-Paketen werden zu einem einzelnen Datensammler Satz zusammengeführt. Alle Leistungs Protokolle für eine einzelne Datenanalyse Sitzung werden innerhalb desselben Zeitraums gesammelt. Das Analysieren von Berichten, die von Advisor-Paketen generiert werden, die in derselben Datenanalyse Sitzung ausgeführt werden, kann Benutzern helfen, die Gesamtleistung zu verstehen und die Ursachen für Leistungsprobleme zu identifizieren.

* **Ereignis Ablauf Verfolgung für Windows** Ein leistungsfähiges, skalierbares, skalierbares Ablauf Verfolgungssystem, das in Windows bereitgestellt wird. Es bietet Profil Erstellungs-und Debuggingfunktionen, die zur Problembehandlung für eine Vielzahl von Szenarien verwendet werden können. Spa verwendet ETW-Ereignisse als Datenquelle zum Erstellen von Leistungs Berichten. Allgemeine Informationen zu etw finden Sie unter verbessertes [Debugging und Leistungsoptimierung mit etw](/archive/msdn-magazine/2007/april/event-tracing-improve-debugging-and-performance-tuning-with-etw).

* **Windows-Verwaltungsinstrumentation (WMI)** Die Infrastruktur für Verwaltungsdaten und-Vorgänge in Windows. Sie können WMI-Skripts oder-Anwendungen schreiben, um administrative Aufgaben auf Remote Computern zu automatisieren. WMI stellt auch Verwaltungsdaten für andere Teile des Betriebssystems und für Produkte bereit. Spa verwendet WMI-Klassen Informationen und Datenpunkte als Quellen zum Erstellen von Leistungs Berichten.

* **Leistungsindikatoren** Wird verwendet, um Informationen darüber bereitzustellen, wie gut das Betriebssystem, die Anwendung, der Dienst oder der Treiber ausgeführt wird. Die Leistungsdaten können Ihnen helfen, Engpässe im System zu ermitteln und die System-und Anwendungsleistung zu optimieren. Das Betriebssystem, das Netzwerk und die Geräte bieten Leistungsdaten, die von einer Anwendung genutzt werden können, um Benutzern eine grafische Ansicht der Leistung des Systems zu bieten. Die Spa verwendet Leistungsdaten und Datenpunkte als Quellen zum Generieren von Leistungs Berichten.

* **Leistungsprotokolle und-Warnungen (PLA)** Sammelt Leistungs Protokolle und Ablauf Verfolgungen und löst Leistungs Warnungen aus, wenn bestimmte Trigger erfüllt sind. Mithilfe von Pla können Leistungsindikatoren, Ereignis Ablauf Verfolgung für Windows (ETW), WMI-Abfragen, Registrierungsschlüssel und Konfigurationsdateien erfasst werden. Außerdem unterstützt die Verwendung von Remote Prozedur aufrufen (RPC) die Remote Datensammlung. Der Benutzer definiert einen Datensammler Satz, der Informationen über die zu sammelnden Daten, die Häufigkeit der Datensammlung, die Dauer der Datenerfassung, Filter und einen Speicherort zum Speichern der Ergebnisdateien enthält. Spa sammelt mithilfe von PLA alle Leistungsdaten von den Ziel Servern.

* **Einzelner Bericht** Ein Spa-Bericht, der auf der Grundlage einer Datenanalyse Sitzung für ein Advisor Pack auf einem einzelnen Zielserver generiert wird. Es kann Benachrichtigungen und verschiedene Datenabschnitte enthalten.

* Paralleler **Bericht** Ein Spa-Bericht, in dem zwei einzelne Berichte für dasselbe Advisor Pack verglichen werden. Die beiden Berichte können von verschiedenen Ziel Servern oder von separaten Leistungsanalysen auf demselben Zielserver generiert werden. Der parallele Bericht erstellt die Funktion zum Vergleichen von zwei Berichten, damit Benutzer ungewöhnliche Verhalten oder Einstellungen in einem der Berichte identifizieren können. Ein paralleler Bericht enthält Benachrichtigungen und verschiedene Datenabschnitte. In jedem Abschnitt werden die Daten aus beiden Berichten nebeneinander aufgelistet.

* **Trend Diagramm** Ein Spa-Bericht, der verwendet wird, um wiederkehrende Muster von Leistungsproblemen zu untersuchen. Viele sich wiederholende Leistungsprobleme werden durch geplante Server Lade Änderungen vom Server oder von Client Computern verursacht, die täglich oder wöchentlich auftreten können. Spa bietet ein 24-Stunden-Trend Diagramm und ein 7-Tage-Trend Diagramm, um diese Probleme zu identifizieren.

    Der Benutzer kann eine oder mehrere Datenreihen gleichzeitig auswählen, wobei es sich um einen numerischen Wert innerhalb des einzelnen Berichts handelt, z. b. die **durchschnittliche CPU-Gesamtauslastung**. genauer gesagt handelt es sich bei einem numerischen Wert um einen skalaren Wert von einem einzelnen Server, der von einem einzelnen AP-Wert zu einer bestimmten Zeit Instanz generiert wird. Spa gruppiert diese Werte in 24 Gruppen, eine für jede Stunde des Tages (sieben für einen 7-tägigen Bericht, eine für jeden Tag der Woche). Spa berechnet durchschnittliche, minimale, maximale und standardmäßige Abweichungen für jede Gruppe.

* Verlaufs **Diagramm** Ein Spa-Bericht, der verwendet wird, um Änderungen an bestimmten numerischen Werten in einzelnen Berichten für ein bestimmtes Server-und Advisor Pack-Paar im Zeitverlauf anzuzeigen. Der Benutzer kann mehrere Datenreihen auswählen und diese zusammen im Verlaufs Diagramm anzeigen, um die Korrelation zwischen verschiedenen Datenreihen nachzuvollziehen.

* **Datenreihe** Numerische Daten, die über einen bestimmten Zeitraum aus derselben Datenquelle gesammelt werden. Dieselbe Quelle bedeutet, dass die Daten vom gleichen Zielserver stammen müssen, z. b. die durchschnittliche Länge der Anforderungs Warteschlange für IIS auf einem Server.

* **Regeln** Kombinationen aus Logik, Schwellenwerten und Beschreibungen. Sie stellen ein mögliches Leistungsproblem dar. Jedes Advisor-Paket enthält mehrere Regeln. Jede Regel wird durch einen Bericht Generierungsprozess ausgelöst. Eine Regel wendet die Logik und die Schwellenwerte auf die Daten in einem einzelnen Bericht an. Wenn die Kriterien erfüllt sind, wird eine Warnmeldung ausgelöst. Wenn dies nicht der Wert ist, wird die Benachrichtigung auf den Status **OK** festgelegt. Wenn die Regel nicht angewendet wird, wird die Benachrichtigung auf den Status nicht zutreffend (**na**) festgelegt.

* **Benachrichtigungen** Informationen, die von einer Regel für Benutzer angezeigt werden. Sie enthält den Status der Regel (**OK**, **na**oder eine **Warnung**), den Namen der Regel und mögliche Empfehlungen, um die Leistungsprobleme zu beheben.