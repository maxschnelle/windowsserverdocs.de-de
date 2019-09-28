---
title: Anzeigen und Verwalten von Updates
description: 'Thema zu Windows Server Update Service (WSUS): anzeigen und Verwalten von Updates in der WSUS-Konsole'
ms.prod: windows-server
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
ms.openlocfilehash: de2d12ad34ba11f948baa390546747a6bf4b635c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361491"
---
# <a name="viewing-and-managing-updates"></a>Anzeigen und Verwalten von Updates

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie können die WSUS-Konsole verwenden, um Updates anzuzeigen und zu verwalten.

## <a name="viewing-updates"></a>Anzeigen von Updates
Auf der Seite **Updates** können Sie folgende Aufgaben ausführen:

-   Anzeigen von Updates. In der Update Übersicht werden Updates angezeigt, die von der Update Quelle mit dem WSUS-Server synchronisiert wurden und für die Genehmigung verfügbar sind.

-   Updates filtern. In der Standardansicht können Sie Updates nach Genehmigungs Status und Installationsstatus filtern. Die Standardeinstellung ist für nicht genehmigte Updates, die von einigen Clients benötigt werden oder bei denen bei einigen Clients Installationsfehler aufgetreten sind. Sie können diese Ansicht ändern, indem Sie die Filter für den Genehmigungs Status und den Installationsstatus ändern und dann auf **Aktualisieren**klicken.

-   Erstellen Sie neue Update Sichten. Klicken Sie im **Aktions** Bereich auf **neue Update Ansicht**. Sie können Updates nach Klassifizierung, Produkt, der Gruppe, für die Sie genehmigt wurden, und dem Synchronisierungs Datum filtern. Sie können die Liste sortieren, indem Sie in der Titelleiste auf die entsprechende Spaltenüberschrift klicken.

-   Suchen Sie nach Updates. Sie können nach einem einzelnen Update oder Satz von Updates nach Titel, Beschreibung, Knowledge Base-Artikel oder der Microsoft Security Response Center-Nummer für das Update suchen.

-   Details, Status und Revisions Verlauf für jedes Update anzeigen.

-   Genehmigen und ablehnen von Updates.

#### <a name="to-view-updates"></a>Anzeigen von Updates

1.  Erweitern Sie in der WSUS-Verwaltungskonsole den Knoten Updates, und klicken Sie dann auf alle Updates.

2.  Standardmäßig werden Updates mit dem Titel, der Klassifizierung, dem installierten/nicht anwendbaren Prozentsatz und dem Genehmigungs Status angezeigt. Wenn Sie weitere oder andere Update Eigenschaften anzeigen möchten, klicken Sie mit der rechten Maustaste auf die Spaltenüberschriften Leiste, und wählen Sie die entsprechenden Spalten aus.

3.  Klicken Sie auf die entsprechende Spaltenüberschrift, um nach verschiedenen Kriterien zu sortieren, z. b. Download Status, Titel, Klassifizierung, Veröffentlichungsdatum oder Genehmigungs Status.

#### <a name="to-filter-the-list-of-updates-displayed-on-the-updates-page"></a>So filtern Sie die Liste der Updates, die auf der Seite Updates angezeigt werden

1.  Erweitern Sie in der WSUS-Verwaltungskonsole den Knoten **Updates**, und klicken Sie dann auf **alle Updates**.

2.  Wählen Sie im mittleren Bereich neben **Genehmigung**den gewünschten Genehmigungs Status aus, und wählen Sie neben **Status** den gewünschten Installationsstatus aus. Klicken Sie auf **Aktualisieren**.

#### <a name="to-create-a-new-update-view-on-wsus"></a>So erstellen Sie eine neue Update Ansicht in WSUS

1.  Erweitern Sie in der WSUS-Verwaltungskonsole den Knoten **Updates**, und klicken Sie dann auf **alle Updates**.

2.  Klicken Sie im **Aktions** Bereich auf **neue Update Ansicht**.

3.  Wählen Sie im Fenster " **Update Ansicht hinzufügen** " unter **Schritt 1: Eigenschaften auswählen**die Eigenschaften aus, die zum Filtern der Update Ansicht erforderlich sind:

    -   SELECT-Updates sind in einer bestimmten Klassifizierung, um nach Updates zu filtern, die zu einer oder mehreren Update Klassifizierungen gehören.

    -   SELECT-Updates sind für ein bestimmtes Produkt, das nach Updates für ein oder mehrere Produkte oder Produktfamilien gefiltert werden soll.

    -   SELECT Updates werden für eine bestimmte Gruppe genehmigt, um nach Updates zu filtern, die für mindestens eine Computergruppe genehmigt wurden.

    -   SELECT-Updates wurden innerhalb eines bestimmten Zeitraums synchronisiert, um nach Updates zu filtern, die zu einem bestimmten Zeitpunkt synchronisiert wurden.

    -   SELECT Updates sind WSUS-Updates zum Filtern von WSUS-Updates.

4.  Klicken Sie unter **Schritt 2: Bearbeiten der Eigenschaften**auf die unterstrichenen Wörter, um die gewünschten Werte auszuwählen.

5.  Unter **Schritt 3: Geben Sie den Namen @ no__t-0 an, und geben Sie der neuen Ansicht einen Namen.

6.  Klicken Sie auf **OK**.

Die neue Ansicht wird im Struktur Ansichts Bereich unter Updates angezeigt. Sie wird wie die Standardansichten im mittleren Bereich angezeigt, wenn Sie Sie auswählen.

#### <a name="to-search-for-an-update"></a>So suchen Sie nach einem Update

1.  Wählen Sie den Knoten **Updates** aus (oder einen beliebigen Knoten darunter).

2.  Klicken Sie im Bereich **Aktionen** auf **Suchen**.

3.  Geben Sie im **Such** Fenster auf der Registerkarte **Updates** Ihre Suchkriterien ein. Sie können Text aus den Feldern **Titel**, **Beschreibung**und **Artikelnummer der Microsoft Knowledge Base (KB)** verwenden. Jedes dieser Elemente ist eine Eigenschaft, die in den Update Eigenschaften auf der Registerkarte **Details** aufgeführt ist.

#### <a name="to-view-the-properties-for-an-update"></a>So zeigen Sie die Eigenschaften für ein Update an

1.  Erweitern Sie in der WSUS-Verwaltungskonsole den Knoten **Updates**, und klicken Sie dann auf **alle Updates**.

2.  Klicken Sie in der Liste der Updates auf das Update, das Sie anzeigen möchten.

3.  Im unteren Bereich werden die unterschiedlichen Eigenschaften Abschnitte angezeigt:

    -   In der Titelleiste wird der Titel des Updates angezeigt. Beispiel: Sicherheits Update für Windows Media Player 9 (KB911565).

    -   Der Abschnitt Status zeigt den Installations Status des Updates an (die Computer, auf denen er installiert werden muss, Computer, auf denen er mit Fehlern installiert wurde, Computer, auf denen er installiert wurde oder nicht anwendbar ist) und Computer, die nicht gemeldet wurden. Status für das Update) sowie allgemeine Informationen (das Veröffentlichungsdatum für KB und MSRC-Nummern usw.).

    -   Im Abschnitt Beschreibung wird eine kurze Beschreibung des Updates angezeigt.

    -   Im Abschnitt Weitere Details werden die folgenden Informationen angezeigt:

        -   Das Installations Verhalten des Updates (unabhängig davon, ob es sich um einen Wechsel handelt, fordert einen Neustart an, erfordert eine Benutzereingabe oder muss exklusiv installiert werden).

        -   Gibt an, ob das Update Microsoft-Software-Lizenzbedingungen enthält.

        -   Die Produkte, für die das Update gilt

        -   Updates, durch die dieses Update abgelöst wird

        -   Die Updates, die durch dieses Update abgelöst werden

        -   Die vom Update unterstützten Sprachen

        -   Die Update-ID

Beachten Sie, dass Sie diese Prozedur nur auf jeweils einem Update ausführen können. Wenn Sie mehrere Updates auswählen, wird nur das erste Update in der Liste im Bereich " **Eigenschaften** " angezeigt.

## <a name="managing-updates-with-wsus"></a>Verwalten von Updates mit WSUS
Updates werden für die Aktualisierung oder die Bereitstellung einer vollständigen Datei Ersetzung für Software verwendet, die auf einem Computer installiert ist. Jedes Update, das auf Microsoft Update verfügbar ist, besteht aus zwei Komponenten:

-   Benötigten Stellt Informationen zum Update bereit. Metadaten liefern z. b. Informationen für die Eigenschaften eines Updates, sodass Sie ermitteln können, was das Update nützlich ist. Metadaten enthalten auch die Microsoft-Software-Lizenzbedingungen. Das für ein Update heruntergeladene Metadatenpaket ist in der Regel viel kleiner als das tatsächliche Update Dateipaket.

-   Aktualisieren von Dateien: Die eigentlichen Dateien, die zum Installieren eines Updates auf einem Computer erforderlich sind.

Beim Synchronisieren von Updates auf den WSUS-Server werden die Metadaten- und Updatedateien an zwei separaten Speicherorten gespeichert. Metadaten werden in der WSUS-Datenbank gespeichert. Update Dateien können entweder auf dem WSUS-Server oder auf Microsoft Update Servern gespeichert werden, je nachdem, wie Sie die Synchronisierungs Optionen konfiguriert haben. Wenn Sie Update Dateien auf Microsoft Update Servern speichern möchten, werden zum Zeitpunkt der Synchronisierung nur Metadaten heruntergeladen. die Updates werden über die WSUS-Konsole genehmigt, und die Update Dateien werden von den Client Computern zum Zeitpunkt der Installation direkt aus dem Microsoft Update. Weitere Informationen zu den Optionen zum Speichern von Updates finden Sie im Abschnitt [1,3. Wählen Sie eine WSUS-Speicherstrategie @ no__t-0 von Schritt 1: Vorbereiten der WSUS-Bereitstellung im WSUS-Bereitstellungs Handbuch.

Sie werden die Synchronisierung einrichten und ausführen, Computer und Computer Gruppen hinzufügen und Updates regelmäßig bereitstellen. Die folgende Liste enthält Beispiele für allgemeine Aufgaben, die Sie beim Aktualisieren von Computern mit WSUS durchführen können.

-   Bestimmen Sie einen allgemeinen Update Verwaltungsplan basierend auf der Netzwerktopologie und-Bandbreite, den Unternehmensanforderungen und der Organisationsstruktur.

    -   Gibt an, ob eine Hierarchie von WSUS-Servern eingerichtet werden soll und wie die Hierarchie strukturiert werden soll.

    -   Welche Computer Gruppen erstellt werden sollen, und wie Sie Ihnen Computer zuweisen (serverseitige oder Client seitige Zielgruppen).

    -   Welche Datenbank für Update Metadaten verwendet werden soll (z. b. interne Windows-Datenbank, SQL Server).

    -   Gibt an, ob Updates automatisch und zu welchem Zeitpunkt synchronisiert werden sollen.

-   Legen Sie Synchronisierungs Optionen wie Update Quelle, Produkt-und Update Klassifizierung, Sprache, Verbindungseinstellungen, Speicherort und Synchronisierungs Zeitplan fest.

-   Sie erhalten die Updates und zugeordneten Metadaten auf dem WSUS-Server, indem Sie die Synchronisierung von Microsoft Update oder einem WSUS-Upstream-Server ausführen.

-   Genehmigen oder ablehnen von Updates. Sie haben die Möglichkeit, Benutzern die Installation der Updates selbst zu gestatten (wenn es sich um lokale Administratoren auf Ihren Client Computern handelt).

-   Konfigurieren Sie automatische Genehmigungen. Sie können auch konfigurieren, ob Sie die automatische Genehmigung von Revisionen vorhandener Updates aktivieren oder Revisionen manuell genehmigen möchten. Wenn Sie Änderungen manuell genehmigen möchten, verwendet der WSUS-Server weiterhin die ältere Version, bis Sie die neue Revision manuell genehmigen.

-   Überprüfen Sie den Status von Updates. Sie können den Update Status anzeigen, einen Statusbericht drucken oder e-Mail für reguläre Statusberichte konfigurieren.

## <a name="update-products-and-classifications"></a>Aktualisieren von Produkten und Klassifizierungen
Die auf Microsoft Update verfügbaren Updates unterscheiden sich anhand des Produkts (oder der Produktfamilie) und der Klassifizierung.

Ein Produkt ist eine bestimmte Edition eines Betriebssystems oder einer Anwendung, z. b. Windows Server 2012. Eine Produktfamilie ist das Basis Betriebssystem bzw. die Basisanwendung, von dem die einzelnen Produkte abgeleitet werden. Ein Beispiel für eine Produktfamilie ist Microsoft Windows, von dem Windows Server 2012 ein Mitglied ist. Sie können die Produkte oder Produktfamilien auswählen, für die der Server Updates synchronisieren soll. Sie können eine Produktfamilie oder einzelne Produkte innerhalb der Familie angeben. Wenn Sie ein Produkt oder eine Produktfamilie auswählen, erhalten Sie Updates für die aktuelle und zukünftige Version des Produkts.

Update Klassifizierungen stellen den Typ des Updates dar. Für ein bestimmtes Produkt oder eine Produktfamilie können Updates unter mehreren Update Klassifizierungen verfügbar sein (z. b. wichtige Updates und Sicherheitsupdates der Windows 7-Familie). In der folgenden Tabelle sind die Update Klassifizierungen aufgeführt.

| Updateklassifizierungen  | Beschreibung   |
|--|--|
|Wichtige Updates|Im großen und ganzen finden Sie Korrekturen für bestimmte Probleme, die kritische, nicht sicherheitsrelevante Fehler behandeln.|
|Definitions Updates|Updates für Viren-oder andere Definitions Dateien.|
|Treiber|Software Komponenten, die zur Unterstützung neuer Hardware entwickelt wurden.|
|Feature Packs|Neue featurereleases, die normalerweise in der nächsten Version in Produkte eingeführt werden.|
|Sicherheitsupdates|Allgemein veröffentlichte Korrekturen für bestimmte Produkte, die Sicherheitsprobleme behandeln.|
|Service Packs|Kumulative Sätze aller Hotfixes, Sicherheitsupdates, kritischer Updates und Updates, die seit der Veröffentlichung des Produkts erstellt wurden. Service Packs können auch eine begrenzte Anzahl von vom Kunden angeforderten Entwurfs Änderungen oder-Features enthalten.|
|Tools|Hilfsprogramme oder Funktionen, die bei der Ausführung einer Aufgabe oder einer Gruppe von Aufgaben helfen.|
|Updaterollups|Einen kumulativen Satz von Hotfixes, Sicherheitsupdates, kritischen Updates und anderen Updates, die zur einfachen Bereitstellung zusammengepackt werden. Ein Rollup bezieht sich in der Regel auf einen bestimmten Bereich, z. b. Sicherheit oder eine bestimmte Komponente, wie z. b. Internetinformationsdienste (IIS).|
|Updates|Allgemein veröffentlichte Korrekturen für bestimmte Probleme, die auf nicht kritische, nicht sicherheitsrelevante Fehler hinweisen.|

## <a name="icons-used-for-updates-in-windows-server-update-services"></a>Symbole, die für Updates in Windows Server Update Services verwendet werden
 Updates in WSUS werden durch eines der folgenden Symbole dargestellt.  
 Um diese Symbole anzuzeigen, müssen Sie die ablösungs Spalte in der Update Services-Konsole aktivieren.
 
### <a name="no-icon"></a>Kein Symbol
 Das Update hat keine ablösungs Beziehung zu anderen Updates.

 **Betriebliche Bedenken:**  

 Keine Einsatzbedenken.  
 
### <a name="superseding-icon"></a>Symbol "abgelöst"
 ![Symbol](../../media/wsus/wsus-superseding.png) Dieses Update ersetzt andere Updates.

 **Betriebliche Bedenken:**  

 Keine Einsatzbedenken.  

### <a name="superseded--superseding-icon"></a>Abgelöst & abgelöst-Symbol
 ![Symbol](../../media/wsus/wsus-superseded.png) Dieses Update wird durch ein anderes Update abgelöst und ersetzt andere Updates.

 **Betriebliche Bedenken:**  

 Ersetzen Sie diese Updates, wenn möglich, durch die ersetzenden Updates.
 
### <a name="superseded-icon"></a>Symbol „Abgelöst“
 ![Symbol](../../media/wsus/wsus-superseded-leaf.png) Dieses Update wird durch ein anderes Update abgelöst.

 **Betriebliche Bedenken:**  

 Ersetzen Sie diese Updates, wenn möglich, durch die ersetzenden Updates.
