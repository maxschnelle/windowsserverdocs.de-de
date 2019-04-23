---
title: Anzeigen und Verwalten von Updates
description: Windows Server Update Service (WSUS)-Thema – anzeigen und Verwalten von Updates in der WSUS-Konsole
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac70192b-0309-4385-b697-2e8eda51911c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cd517be0de3ba6ca97ca11f4bbe8f59111a01216
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870951"
---
# <a name="viewing-and-managing-updates"></a>Anzeigen und Verwalten von Updates

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Sie können die WSUS-Konsole anzeigen und Verwalten von Updates verwenden.

## <a name="viewing-updates"></a>Anzeigen von Updates
Auf der **Updates** Seite können Sie Folgendes tun:

-   Updates anzeigen. Übersicht über die Updates zeigt Updates, die von der Updatequelle mit Ihrem WSUS-Server synchronisiert wurden und zur Genehmigung verfügbar sind.

-   Updates zu filtern. In der Standardansicht können Sie Updates, Genehmigungsstatus und Installationsstatus filtern. Die Standardeinstellung ist für die nicht genehmigte Updates, die von einigen Clients benötigt werden oder hatten, die in einigen Clients Fehler bei der Installation. Sie können diese Ansicht ändern, indem Filter die Genehmigung für Status und Installationspfad zu ändern, und klicken Sie dann auf **aktualisieren**.

-   Erstellen Sie neue Updateansichten. In der **Aktionen** Bereich, klicken Sie auf **neue Updateansicht**. Sie können Updates nach Klassifizierung, Produkt, die Gruppe, die für die sie genehmigt wurde und Datum filtern. Sie können die Liste sortieren, indem Sie auf die entsprechende Spaltenüberschrift in der Titelleiste angezeigt.

-   Suchen Sie nach Updates. Sie können nach Titel, Beschreibung, Knowledge Base-Artikel oder die Microsoft Security Response Center-Anzahl für das Update für ein individuelles Update oder eine Gruppe von Updates suchen.

-   Details zum Status und Verlauf für jedes Update.

-   Genehmigen und Ablehnen von Updates.

#### <a name="to-view-updates"></a>Zum Anzeigen von updates

1.  Klicken Sie in der WSUS-Verwaltungskonsole erweitern Sie Knoten "Updates", und klicken Sie dann auf alle Updates.

2.  Standardmäßig werden Updates mit ihren Titel, Klassifizierung, installiert/nicht anwendbar Prozentsatz und Genehmigungsstatus angezeigt. Wenn Sie mehr bzw. andere Updateeigenschaften anzeigen möchten, mit der rechten Maustaste in die Leiste der Spaltenüberschriften, und wählen Sie die entsprechenden Spalten.

3.  Klicken Sie auf die entsprechende Spaltenüberschrift, um nach verschiedenen Kriterien wie z. B. Uploadstatus, Titel, Klassifizierung, Veröffentlichungsdatum oder Genehmigungsstatus, zu sortieren.

#### <a name="to-filter-the-list-of-updates-displayed-on-the-updates-page"></a>Zum Filtern der Liste der Updates, die auf der Seite "Updates" angezeigt

1.  Erweitern Sie in der WSUS-Verwaltungskonsole **Updates**, und klicken Sie dann auf **alle Updates**.

2.  Im mittleren Bereich neben **Genehmigung**, wählen Sie die gewünschten Genehmigungsstatus und neben **Status** wählen Sie den Status der gewünschten Installation. Klicken Sie auf **Refresh**.

#### <a name="to-create-a-new-update-view-on-wsus"></a>Erstellen Sie eine neue Updateansicht in WSUS

1.  Erweitern Sie in der WSUS-Verwaltungskonsole **Updates**, und klicken Sie dann auf **alle Updates**.

2.  In der **Aktionen** Bereich, klicken Sie auf **neue Updateansicht**.

3.  In der **aktualisieren Ansicht hinzufügen** Fenster unter **Schritt 1: Wählen Sie Eigenschaften**, wählen Sie die Eigenschaften, die Sie filtern die Aktualisierungsansicht müssen:

    -   Auf Updates sind in einer bestimmten Klassifizierung aus, um nach Updates, gehören zu filtern, auf einen oder mehrere Klassifizierungen zu aktualisieren.

    -   Wählen Sie Updates sind für ein bestimmtes Produkt aus, um nach Updates für eine oder mehrere Produkte und Produktfamilien zu filtern.

    -   Wählen Sie genehmigte Updates für eine bestimmte Gruppe zum Filtern nach Updates für eine oder mehrere Computergruppen genehmigt sind.

    -   Wählen Sie in einem bestimmten Zeitraum zum Filtern nach einem bestimmten Zeitpunkt synchronisierte Updates synchronisiert wurden.

    -   Wählen Sie Updates sind WSUS-Updates auf WSUS-Updates zu filtern.

4.  Klicken Sie unter **Schritt2: Bearbeiten Sie die Eigenschaften**, klicken Sie auf die unterstrichenen Wörter ein, um die Werte auswählen, werden sollen.

5.  Klicken Sie unter **Schritt 3: Geben Sie einen Namen**, benennen Sie der neuen Ansicht.

6.  Klicken Sie auf **OK**.

Die neue Ansicht wird in der Strukturansicht unter Updates angezeigt. Es wird angezeigt werden wie die Standardansichten, in der Mitte, wenn Sie diese Option auswählen.

#### <a name="to-search-for-an-update"></a>Um nach einem Update zu suchen.

1.  Wählen Sie die **Updates** Knotens (oder auf jedem Knoten).

2.  In der **Aktionen** Bereich, klicken Sie auf **Suche**.

3.  In der **Suche** Fenster auf die **Updates** Registerkarte, geben Sie die Suchkriterien. Können Sie Text aus der **Titel**, **Beschreibung**, und **Microsoft Knowledge Base (KB)-Artikelnummer** Felder. Jedes dieser Elemente ist eine Eigenschaft, die aufgelistet werden, auf die **Details** Registerkarte in den Updateeigenschaften.

#### <a name="to-view-the-properties-for-an-update"></a>Anzeigen die Eigenschaften für ein update

1.  Erweitern Sie in der WSUS-Verwaltungskonsole **Updates**, und klicken Sie dann auf **alle Updates**.

2.  Klicken Sie in der Liste der Updates auf das Update aus, die, das Sie anzeigen möchten.

3.  Im unteren Bereich wird die andere Eigenschaftenabschnitte angezeigt:

    -   Die Titelleiste wird des Titels des Updates; Beispiel: Security Update für Windows Media Player 9 (KB911565).

    -   Der Status-Abschnitt zeigt den Installationsstatus des Updates (der Computer, auf denen er installiert werden muss, Computer, auf denen sie mit Fehlern installiert wurde, Computer, auf denen er installiert wurde, oder ist nicht anwendbar, und Computer, die nicht Bericht erstattet haben Status für das Update), sowie allgemeine Informationen (KB und MSRC Veröffentlichungsdatum für Zahlen, usw.).

    -   Der Abschnitt "Beschreibung" zeigt eine kurze Beschreibung des Updates.

    -   Der Abschnitt zusätzliche Details zeigt die folgenden Informationen an:

        -   Das Verhalten bei der Installation des Updates (unabhängig davon, ob er kann entfernt werden, fordert einen Neustart, eine Benutzereingabe erfordert oder muss ausschließlich installiert werden).

        -   Unabhängig davon, ob das Update für Microsoft Software License Terms enthält

        -   Die Produkte, für die das Update gilt

        -   Die Updates, die dieses Update abgelöst wird

        -   Die Updates, die durch dieses Update abgelöst werden.

        -   Die vom Update unterstützten Sprachen

        -   Die Update-ID

Beachten Sie, dass Sie dieses Verfahren auf nur eine Aktualisierung zu einem Zeitpunkt ausführen können. Wenn Sie mehrere Updates auswählen, wird nur das erste Update in der Liste angezeigt werden, der **Eigenschaften** Bereich.

## <a name="managing-updates-with-wsus"></a>Verwalten von Updates mit WSUS
Updates werden zum Aktualisieren oder da Sie einen vollständigen Ersatz für Software, die auf einem Computer installiert ist. Jedes Update, das auf Microsoft Update verfügbar ist besteht aus zwei Komponenten:

-   Metadata: Enthält Informationen zu dem Update. Beispielsweise liefert Metadaten Informationen für die Eigenschaften eines Updates, sodass Sie herausfinden, welche das Update nützlich ist. Metadaten umfassen auch die Microsoft Software-Lizenzbedingungen. Für ein Update heruntergeladene Metadatenpaket ist in der Regel viel kleiner ist als das eigentliche Updatedateipaket.

-   Updatedateien: Die tatsächlichen Dateien erforderlich, um ein Update auf einem Computer installieren.

Beim Synchronisieren von Updates auf den WSUS-Server werden die Metadaten- und Updatedateien an zwei separaten Speicherorten gespeichert. Metadaten werden in der WSUS-Datenbank gespeichert. Updatedateien können gespeichert werden, entweder auf dem WSUS-Server oder auf Microsoft Update-Servern, je nachdem, wie Sie Ihre Optionen für die Synchronisierung konfiguriert haben. Wenn Sie entscheiden, Updatedateien auf Microsoft Update-Servern zu speichern, wird nur die Metadaten zum Zeitpunkt der Synchronisierung heruntergeladen. Sie genehmigen der Updates über die WSUS-Verwaltungskonsole, und klicken Sie dann Clientcomputer erhalten die aktualisierten Dateien direkt von Microsoft Update zum Zeitpunkt der Installation. Weitere Informationen zu den Optionen zum Speichern von Updates finden Sie im Abschnitt [1.3. Wählen Sie eine WSUS-Speicherstrategie](../plan/plan-your-wsus-deployment.md#BKMK_1.3.) von Schritt 1: Vorbereiten der WSUS-Bereitstellung, im Bereitstellungshandbuch für WSUS.

Sie werden das Einrichten und Hinzufügen von Computern und Computergruppen und Bereitstellung von Updates in regelmäßigen Abständen Synchronisierungen ausführen. Die folgende Liste enthält Beispiele für allgemeine Aufgaben, die Sie möglicherweise bei der Aktualisierung von Computern mit WSUS ausführt.

-   Bestimmen Sie ein Update Management Gesamtplan basierend auf Ihrer Netzwerktopologie und die Bandbreite, die Anforderungen des Unternehmens und die Organisationsstruktur.

    -   Gibt an, ob Sie eine Hierarchie von WSUS-Servern und wie die Hierarchie strukturiert werden soll.

    -   Welche Computergruppen, die zum Erstellen und Zuweisen von Computern zu werden (serverseitige oder clientseitige Zielgruppenadressierung).

    -   Welche Datenbank für die Softwareupdate-Metadaten (z. B. Windows Internal Database, SQL Server) verwendet.

    -   Gibt an, ob Updates automatisch und zu welchem Zeitpunkt synchronisiert werden sollen.

-   Synchronisierungsoptionen, z. B. die Quelle für das Produkt und die updateklassifizierung, Sprache, Verbindungseinstellungen, Speicherort und Synchronisierungszeitplan festgelegt.

-   Abrufen der Updates und zugehörigen Metadaten auf dem WSUS-Server über die Synchronisierung von Microsoft Update oder WSUS-Upstreamserver.

-   Genehmigen oder ablehnen von Updates. Sie haben die Möglichkeit, sodass Benutzer die Updates selbst installiert (Wenn sie lokale Administratoren auf ihren Clientcomputern befinden).

-   Konfigurieren Sie automatische Genehmigungen. Sie können auch konfigurieren, ob Sie aktivieren die automatischen Genehmigung von Revisionen für vorhandene Updates oder Änderungen manuell genehmigen möchten. Wenn Sie zum manuellen Genehmigen von Revisionen auswählen, wird Ihr WSUS-Server mit der älteren Version, bis Sie die neue Revision manuell genehmigen fortgesetzt.

-   Überprüfen Sie den Status von Updates. Sie können Updatestatus anzeigen, Drucken einen Bericht oder Konfigurieren von E-mail für reguläre Statusberichte.

## <a name="update-products-and-classifications"></a>Update-Produkte und Klassifizierungen
Auf Microsoft Update verfügbaren Updates unterscheiden sich von Produkt (oder -Produktfamilie) und Klassifizierung.

Ein Produkt ist eine bestimmte Edition eines Betriebssystems oder einer Anwendung, z. B. Windows Server 2012. Eine Produktfamilie ist das Basisbetriebssystem oder die Anwendung, von dem die einzelnen Produkte abgeleitet sind. Ein Beispiel für eine Produktfamilie ist Microsoft Windows, von denen Windows Server 2012 Mitglied ist. Sie können auswählen, die Produkte und Produktfamilien, die für die Sie Ihren Server, um Updates zu synchronisieren möchten. Sie können eine Produktfamilie oder einzelne Produkte innerhalb der Produktfamilie angeben. Auswählen von jedem Produkt oder Produktfamilie erhalten Updates für den aktuellen und zukünftigen Versionen des Produkts.

Updateklassifizierungen darstellen, den Typ des Updates. Für ein bestimmtes Produkt oder Produktfamilie möglicherweise Updates unter mehreren updateklassifizierungen (z. B. Windows 7-Produktfamilie kritische Updates und Sicherheitsupdates) verfügbar. Die folgende Tabelle enthält die Aktualisierung von Klassifizierungen.

| Updateklassifizierungen  | Beschreibung   |
|--|--|
|Wichtige Updates|Publikum freigegeben Korrekturen für bestimmte Probleme wichtiger, nicht sicherheitsrelevanter damit zusammenhängenden Fehler.|
|Definitionsupdates|Updates für Viren- oder andere Definitionsdateien.|
|Treiber|Softwarekomponenten auf neue Hardware unterstützen.|
|Feature packs|Releases neuer Features, die in der Regel in Produkte auf die nächste Version ausgeführt wird.|
|Sicherheitsupdates|Allgemein veröffentlichten Updates für bestimmte Produkte, Behandeln von Sicherheitsproblemen.|
|Service Packs|Kumulative Sätze aller Hotfixes, Sicherheitsupdates, Kritischer Updates und Updates, die seit der Veröffentlichung des Produkts erstellt. Servicepacks können auch eine begrenzte Anzahl von Kunden angeforderter Designänderungen oder Features enthalten.|
|Tools|Dienstprogramme oder Funktionen, die bei der Erledigung einer oder mehrerer Aufgaben.|
|Updaterollups|Einen kumulativen Satz von Hotfixes, Sicherheitsupdates, kritische Updates und andere Updates, die zur Vereinfachung der Bereitstellung gebündelt sind. Ein Rollup bezieht sich im Allgemeinen einen bestimmten Bereich, z. B. Sicherheit oder eine bestimmte Komponente, z. B. Internet Information Services (IIS).|
|Updates|Publikum freigegeben Korrekturen für bestimmte Probleme unkritische, nicht sicherheitsrelevanter damit zusammenhängenden Fehler.|

## <a name="icons-used-for-updates-in-windows-server-update-services"></a>Symbole für Updates in Windows Server Update Services verwendet wird
 Updates in WSUS werden durch eines der folgenden Symbole dargestellt.  
 Um diese Symbole anzuzeigen, müssen Sie die Ablösung-Spalte in der Update Services-Konsole aktivieren.
 
### <a name="no-icon"></a>Symbol "keine"
 Das Update enthält keine ablösungsbeziehung mit alle anderen Updates.

 **Einsatzbedenken:**  

 Keine Einsatzbedenken.  
 
### <a name="superseding-icon"></a>Ersetzen das Symbol
 ![Symbol](../../media/wsus/wsus-superseding.png) Dieses Update ersetzt andere Updates.

 **Einsatzbedenken:**  

 Keine Einsatzbedenken.  

### <a name="superseded--superseding-icon"></a>Symbol für Abgelöstes & Ablösenden
 ![Symbol](../../media/wsus/wsus-superseded.png) Dieses Update wird durch ein anderes Update abgelöst und ersetzt andere Updates.

 **Einsatzbedenken:**  

 Ersetzen Sie diese Updates mit den ersetzenden Updates, wenn möglich.
 
### <a name="superseded-icon"></a>Symbol „Abgelöst“
 ![Symbol](../../media/wsus/wsus-superseded-leaf.png) Dieses Update wird durch ein anderes Update ersetzt.

 **Einsatzbedenken:**  

 Ersetzen Sie diese Updates mit den ersetzenden Updates, wenn möglich.
