---
title: Verwalten des lokalen Servers und der Server-Manager-Konsole
description: Server-Manager
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eeb32f65-d588-4ed5-82ba-1ca37f517139
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1f22578cc54a22464fe5d9208731fe681be30481
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832981"
---
# <a name="manage-the-local-server-and-the-server-manager-console"></a>Verwalten des lokalen Servers und der Server-Manager-Konsole

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

In Windows Server, Server-Manager können Sie sowohl den lokalen Server verwalten, (Wenn Sie Server-Manager unter Windows Server und nicht auf einem Windows-basierten Client-Betriebssystem ausgeführt werden) und Remoteservern, auf denen Windows Server 2008 und neueren Versionen von dem Windows ausgeführt werden Server-Betriebssystem.

Die **lokalen Server** Seite im Server-Manager zeigt die Server-Eigenschaften, Ereignisse, Dienst und Leistungsindikatordaten sowie Best Practices Analyzer (BPA) für den lokalen Server führt. Die Kacheln "Ereignis", "Dienst", "BPA" und "Leistung" funktionieren wie auf den Rollen- und Servergruppenseiten. Weitere Informationen zum Konfigurieren der Daten, die auf diesen Kacheln angezeigt werden, finden Sie unter [Anzeigen und Konfigurieren von Leistungs-, Ereignis- und Dienstdaten](view-and-configure-performance-event-and-service-data.md) und unter [Ausführen von Best Practices Analyzer-Überprüfungen und Verwalten der Überprüfungsergebnisse](run-best-practices-analyzer-scans-and-manage-scan-results.md).

Menübefehle und Einstellungen in den überschriftenleisten der Server-Manager-Konsole global auf allen Servern im Serverpool angewendet, und können Sie Server-Manager, die zum Verwalten des gesamten Serverpools verwenden.

Dieses Thema enthält die folgenden Abschnitte:

-   [Herunterfahren des lokalen Servers](#BKMK_shutdown)

-   [Konfigurieren Sie Server-Manager-Eigenschaften](#BKMK_props)

-   [Verwalten der Server-Manager-Konsole](#BKMK_managesm)

-   [Anpassen von Tools, die Sie im Menü Extras angezeigt werden](#BKMK_tools)

-   [Verwalten von Rollen auf Rollen-Homepages](#BKMK_roles)

## <a name="BKMK_shutdown"></a>Herunterfahren des lokalen Servers
Die **Aufgaben** im Menü auf dem lokalen Server **Eigenschaften** Kachel können Sie eine Windows PowerShell-Sitzung starten, auf dem lokalen Server, öffnen Sie die **Computer Management** Mmc-Snap-in, oder öffnen MMC-Snap-ins für Rollen oder Features, die auf dem lokalen Server installiert sind. Zudem kann der lokale Server mithilfe des Befehls **Lokalen Server herunterfahren** im Menü **Aufgaben** heruntergefahren werden. Der Befehl **Lokalen Server herunterfahren** ist für den lokalen Server auch auf der Kachel **Server** auf der Seite **Alle Server** oder auf einer Rollen- oder Gruppenseite verfügbar, auf der der lokale Server dargestellt wird.

Mit dieser Methode wird im Gegensatz zum Herunterfahren von Windows Server 2016 aus dem lokalen Server Herunterfahren der **starten** Startbildschirm die **schließen Sie Windows** Dialogfeld Sie die Gründe für das Herunterfahren angeben können in der **Shutdown Event Tracker** Bereich.

> [!NOTE]
> Nur Mitglieder der Gruppe "Administratoren" können einen Server herunterfahren oder neu starten. Standardbenutzer können einen Server weder herunterfahren noch neu starten. Wenn Sie auf den Befehl **Lokalen Server herunterfahren** klicken, werden Standardbenutzer von Serversitzungen abgemeldet. Dies entspricht der Erfahrung eines Standardbenutzers, der den Befehl **Alt+F4** zum Herunterfahren über den Server-Desktop ausführt.

## <a name="BKMK_props"></a>Konfigurieren Sie Server-Manager-Eigenschaften
Auf der Kachel **Eigenschaften** auf der Seite **Lokaler Server** können Sie die folgenden Einstellungen anzeigen oder ändern. Klicken Sie zum Ändern eines Einstellungswerts auf den hypertextwert der Einstellung.

> [!NOTE]
> Die auf der Kachel **Eigenschaften** des lokalen Servers angezeigten Eigenschaften können normalerweise nur auf dem lokalen Server geändert werden. Sie können keine Eigenschaften des lokalen Servers von einem Remotecomputer aus ändern, indem Sie mit Server-Manager aus, da die **Eigenschaften** Kachel kann nur Informationen über den lokalen Computer, die nicht von Remotecomputern abgerufen werden.
> 
> Da viele Eigenschaften, in angezeigt der **Eigenschaften** Kachel sind über Tools gesteuert werden, die nicht Teil des Server-Managers (Systemsteuerung, z. B.), sind Änderungen an **Eigenschaften** Einstellungen sind nicht immer angezeigt der **Eigenschaften** sofort Kachel. Die Daten auf der Kachel **Eigenschaften** werden standardmäßig alle zwei Minuten aktualisiert. Aktualisieren **Eigenschaften** direkt Daten der Kachel, klicken Sie auf **aktualisieren** in der Adressleiste des Server-Manager.

|Einstellung|Beschreibung|
|------|--------|
|Name des Computers|Zeigt den Anzeigenamen für die Computer, und öffnet die **Systemeigenschaften** Dialogfeld, in dem Sie den Namen des Servers, Domänenmitgliedschaft und andere Systemeigenschaften wie Benutzerprofile ändern kann.|
|Domäne (oder Arbeitsgruppe, wenn der Server keiner Domäne angehört)|Zeigt die Domäne oder Arbeitsgruppe an, der der Server angehört. Öffnet die **Systemeigenschaften** Dialogfeld, in dem Sie den Namen des Servers, Domänenmitgliedschaft und andere Systemeigenschaften wie Benutzerprofile ändern kann.|
|Windows-Firewall|Zeigt den Status der Windows-Firewall für den lokalen Server an. Öffnet **Systemsteuerung\System und Sicherheit\Windows-Firewall**. Weitere Informationen zum Konfigurieren der Windows-Firewall finden Sie unter [Windows-Firewall mit erweiterter Sicherheit und IPsec](https://go.microsoft.com/fwlink/?LinkId=253465).|
|Remoteverwaltung|Zeigt den Status von Server-Manager und Windows PowerShell-Remoteverwaltung. Öffnet die **Konfigurieren der Remoteverwaltung** Dialogfeld. Weitere Informationen zur Remoteverwaltung finden Sie unter [Konfigurieren der Remoteverwaltung im Server-Manager](configure-remote-management-in-server-manager.md).|
|Remotedesktop|Zeigt an, ob Benutzer mithilfe von Remotedesktopsitzungen eine Remoteverbindung mit dem Server herstellen können. Öffnet die **remote** Registerkarte die **Systemeigenschaften** Dialogfeld.|
|NIC-Teamvorgang|Zeigt an, ob der lokale Server am NIC-Teamvorgang teilnimmt. Öffnet das Dialogfeld **NIC-Teamvorgang** . Wenn Sie möchten, können Sie hier den lokalen Server einem NIC-Team hinzufügen. Weitere Informationen zum NIC-Teamvorgang finden Sie im [Whitepaper zum NIC-Teamvorgang](https://go.microsoft.com/fwlink/?LinkID=253449).|
|Ethernet|Zeigt den Netzwerkstatus des Servers an. Öffnet **Systemsteuerung\Netzwerk und Internet\Netzwerkverbindungen**.|
|Version des Betriebssystems|In diesem schreibgeschützten Feld wird die Versionsnummer des Windows-Betriebssystems angezeigt, das auf dem lokalen Server ausgeführt wird.|
|Hardwareinformationen|In diesem schreibgeschützten Feld werden Hersteller, Modellname und -nummer der Serverhardware angezeigt.|
|Zuletzt installierte Updates|Zeigt den Tag und die Uhrzeit der letzten Installation von Windows-Updates an. Öffnet **Systemsteuerung\System und Sicherheit\Windows Update**.|
|Windows Update|Zeigt die Windows Update-Einstellungen für den lokalen Server an. Öffnet **Systemsteuerung\System und Sicherheit\Windows Update**.|
|Zuletzt auf Updates geprüft|Zeigt den Tag und die Uhrzeit der letzten Überprüfung des Servers auf verfügbare Windows-Updates an. Öffnet **Systemsteuerung\System und Sicherheit\Windows Update**.|
|Windows-Fehlerberichterstattung|Zeigt den den Anmeldestatus der Windows-Fehlerberichterstattung an. Öffnet das Dialogfeld **Windows-Fehlerberichterstattungs-Konfiguration** . Weitere Informationen zur Windows-Fehlerberichterstattung, zu den Vorteilen, Datenschutzbestimmungen und Anmeldeeinstellungen finden Sie unter [Windows-Fehlerberichterstattung](https://go.microsoft.com/fwlink/?LinkID=245991).|
|Programm zur Verbesserung der Benutzerfreundlichkeit|Zeigt den Anmeldestatus des Programms zur Verbesserung der Benutzerfreundlichkeit von Windows an. Öffnet das Dialogfeld **Konfiguration des Programms zur Verbesserung der Benutzerfreundlichkeit** . Weitere Informationen zum Programm zur Verbesserung der Benutzerfreundlichkeit von Windows, zu den Vorteilen und Anmeldeeinstellungen finden Sie unter [Programm zur Verbesserung der Benutzerfreundlichkeit von Windows](https://go.microsoft.com/fwlink/?LinkID=245992).|
|Verstärkte Sicherheitskonfiguration für Internet Explorer (IE)|Zeigt, ob die Verstärkte Sicherheitskonfiguration für IE (auch als IE Hardening oder IE ESC bezeichnet) aktiviert oder deaktiviert ist. Öffnet das Dialogfeld **Verstärkte Sicherheitskonfiguration für Internet Explorer**. Die verstärkte Sicherheitskonfiguration für IE ist eine Sicherheitsmaßnahme für Server, mit der verhindert wird, dass Webseiten in Internet Explorer geöffnet werden. Weitere Informationen zur Verstärkten Sicherheitskonfiguration, die Vorteile und Einstellungen finden Sie unter [Internet Explorer: Verstärkte Sicherheitskonfiguration für](https://go.microsoft.com/fwlink/?LinkId=253461).|
|Zeitzone|Zeigt die Zeitzone des lokalen Servers. Öffnet die **Datums- /** Dialogfeld.|
|Produkt-ID|Zeigt die Windows-Aktivierung Status und Produkt-ID (sofern Windows aktiviert wurde) des Betriebssystems Windows Server 2016. Hierbei handelt es sich nicht um den Windows-Product Key. Öffnet das Dialogfeld **Windows-Aktivierung** .|
|Prozessoren|Dieses schreibgeschützte Feld werden Hersteller, Modellname und Geschwindigkeitsinformationen zu Prozessoren für den lokalen Server angezeigt.|
|Installierter Arbeitsspeicher (RAM)|In diesem schreibgeschützten Feld wird die Größe des verfügbaren Arbeitsspeichers in Gigabyte angezeigt.|
|Speicherplatz insgesamt|In diesem schreibgeschützten Feld wird die Größe des verfügbaren Festplattenspeichers in Gigabyte angezeigt.|

## <a name="BKMK_managesm"></a>Verwalten der Server-Manager-Konsole
Globale Einstellungen, die gelten, in der gesamten Server-Manager-Konsole, und klicken Sie auf allen Remoteservern, die dem Serverpool des Server-Manager hinzugefügt wurden, werden in den überschriftenleisten oben im Fenster der Server-Manager-Konsole gefunden.

### <a name="add-servers-to-server-manager"></a>Hinzufügen von Servern zu Server-Manager
Der Befehl, der geöffnet wird die **Hinzufügen von Servern** im Dialogfeld und können Sie dem Serverpool des Server-Manager physische und virtuelle Remoteserver hinzufügen, wird die **verwalten** im Menü der Server-Manager-Konsole. Ausführliche Informationen zum Hinzufügen von Servern finden Sie unter [Hinzufügen von Servern zu Server Manager](add-servers-to-server-manager.md).

### <a name="refresh-data-that-is-displayed-in-server-manager"></a>Aktualisieren von Daten, die in Server-Manager angezeigt werden
Sie können konfigurieren, dass das Aktualisierungsintervall für Daten, die im Server-Manager angezeigt wird, auf die **Server-Manager-Eigenschaften** Dialogfeld, das Sie öffnen die **verwalten** Menü.

##### <a name="to-configure-the-refresh-interval-in-server-manager"></a>So konfigurieren Sie das Aktualisierungsintervall in Server-Manager

1.  Auf der **verwalten** in der Server-Manager-Konsole, klicken Sie anschließend auf **Server-Manager-Eigenschaften**.

2.  In der **Server-Manager-Eigenschaften** Dialogfeld geben einen Zeitraum in Minuten an, für die Menge an Zeit, die zwischen den Aktualisierungen der Daten, die im Server-Manager angezeigt werden. Der Standardwert ist 10 Minuten. Klicken Sie anschließend auf "OK".

#### <a name="refresh-limitations"></a>Aktualisierungsbeschränkungen
Aktualisierung wirkt sich Global auf Daten von allen Servern, die Sie dem Serverpool des Server-Manager hinzugefügt haben. Es können keine Daten für einzelne Server, Rollen und Gruppen aktualisiert oder für einzelne Server, Rollen und Gruppen unterschiedliche Aktualisierungsintervalle konfiguriert werden.

Beim Hinzufügen von Servern, die in einem Cluster Server-Manager, ob sie physische oder virtuelle Computer sind kann der ersten datenaktualisierung fehlschlagen, angezeigt oder Daten nur für den Hostserver für die gruppierten Objekte. Bei nachfolgenden Aktualisierungen werden die genauen Daten für physische oder virtuelle Server in einem Servercluster angezeigt.

Daten, die im Rollen-Homepages im Server-Manager für Remote Desktop Services, IP-Adresse, Verwaltung, und die Datei- und Speicherdienste angezeigt werden, werden nicht automatisch aktualisiert. Aktualisieren Sie die auf diesen Seiten angezeigten Daten manuell, durch Drücken von ist **F5** oder durch Klicken auf **aktualisieren** in den Server-Manager-Konsolenüberschrift auf diesen Seiten möchten.

### <a name="add-or-remove-roles-or-features"></a>Hinzufügen oder Entfernen von Rollen oder features
Die Befehle, die das Hinzufügen von Rollen und Features-Assistenten zu öffnen, und Entfernen von Rollen und Features-Assistenten und ermöglichen, die Sie hinzufügen oder Entfernen von Rollen, Rollendienste und Features auf Servern im Serverpool, befinden sich in der **verwalten** im Menü des Server-Managers Konsole und die **Aufgaben** im Menü der **Rollen und Features** Kachel auf Rollen- oder Gruppenseiten. Ausführliche Informationen zum Hinzufügen oder Entfernen von Rollen oder Features finden Sie unter [installieren oder Deinstallieren von Rollen, Rollendienste oder Features](install-or-uninstall-roles-role-services-or-features.md).

Im Server-Manager wird die Rollen-und Featuredaten in der Basissprache des Systems, auch als GUI-Standardsprache des Systems oder der während der Installation des Betriebssystems ausgewählten Sprache angezeigt.

### <a name="create-server-groups"></a>Erstellen von Servergruppen
Der Befehl, der geöffnet wird die **Servergruppe erstellen** im Dialogfeld und mit dem Sie benutzerdefinierte Servergruppen zu erstellen, befindet sich in der **verwalten** im Menü der Server-Manager-Konsole. Ausführliche Informationen über das Erstellen von Servergruppen finden Sie unter [erstellen und Verwalten von Servergruppen](create-and-manage-server-groups.md).

### <a name="prevent-server-manager-from-opening-automatically-at-logon"></a>Verhindern, dass Server-Manager beim Anmelden automatisch geöffnet wird
Die **Server-Manager beim Anmelden nicht automatisch starten** Kontrollkästchen in der **Server-Manager-Eigenschaften** Dialogfeld steuert, ob es sich bei Server-Manager beim Anmelden für Mitglieder der öffnet automatisch die Gruppe "Administratoren" auf einem lokalen Server. Server-Manager-Verhalten wird von dieser Einstellung nicht beeinflusst werden, wenn es als Teil der Remoteserver-Verwaltungstools unter Windows 10 ausgeführt wird. Weitere Informationen zum Konfigurieren dieser Einstellung finden Sie unter [Server-Manager](server-manager.md).

### <a name="zoom-in-or-out"></a>Vergrößern oder Verkleinern
Um die Ansicht der Server-Manager-Konsole vergrößern oder zu vergrößern, können Sie entweder die **Zoom** von Befehlen auf die **Ansicht** Menü, oder drücken Sie **STRG + Plus (+)** zum Verkleinern die Tasten und **STRG + Minus (-)** verkleinern.

## <a name="BKMK_tools"></a>Anpassen von Tools, die Sie im Menü Extras angezeigt werden
Die **Tools** Menü im Server-Manager enthält weiche Links zu Verknüpfungen im der **Verwaltung** Ordner **Systemsteuerung/System und Sicherheit**. Die **Verwaltung** Ordner enthält eine Liste mit Verknüpfungen oder LNK-Dateien zu verfügbaren Verwaltungstools wie Mmc-Snap-ins. Server-Manager füllt die **Tools** Menü mit Links zu diesen Verknüpfungen und kopiert die Ordnerstruktur des der **Verwaltung** Ordner, um die **Tools** Menü. Die Tools im Ordner "Verwaltung" werden standardmäßig in einer flachen Liste angeordnet und nach Typ und nach Name sortiert. Im Server-Manager**Tools** Menü Elemente werden nur nach Name, nicht nach Typ sortiert.

Wenn Sie das Menü **Extras** anpassen möchten, kopieren Sie die gewünschten Tool- oder Skriptverknüpfungen in den Ordner **Verwaltung** . Sie können Ihre Verknüpfungen auch in Ordnern organisieren, die im Menü **Extras** hierarchische Menüs bilden. Darüber hinaus sollten Sie den Zugriff auf die benutzerdefinierten Tools zu beschränken, auf die **Tools** Menü können Sie Zugriffsrechte für Benutzer festlegen, für die Ordner benutzerdefiniertes Tool in der Verwaltung oder direkt in der ursprünglichen Tool- oder Skriptdatei.

Es wird empfohlen, System- und Verwaltungstools sowie Rollen und Features zugeordnete Verwaltungstools, die auf dem lokalen Server installiert sind, nicht neu zu organisieren. Wenn Verwaltungstools von Rollen und Features verschoben werden, können sie bei Bedarf möglicherweise nicht deinstalliert werden. Nach der Deinstallation einer Rolle oder eines Features bleibt möglicherweise ein defekter Link zu einem Tool, dessen Verknüpfung verschoben wurde, im Menü **Extras** zurück. Beim erneuten Installieren der Rolle wird im Menü **Extras** ein doppelter Link zum selben Tool erstellt, aber einer der Links ist defekt.

Rollen- und Featuretools, die als Teil der Remoteserver-Verwaltungstools auf einem clientbasierten Windows-Computer installiert werden, können jedoch in benutzerdefinierten Ordnern organisiert werden. Deinstallation der übergeordneten Rolle oder Feature hat keine Auswirkungen auf die toolverknüpfungen, die auf einem Remotecomputer verfügbar sind, auf denen Windows 10 ausgeführt wird.

Das folgende Verfahren beschreibt, wie ein Beispielordner mit dem Namen erstellt *Meinetools*, und verschieben Sie die Verknüpfungen für zwei Windows PowerShell-Skripts in den Ordner, der dann über das Menü "Server-Manager" zugegriffen werden kann.

#### <a name="to-customize-the-tools-menu-by-adding-shortcuts-in-administrative-tools"></a>So passen Sie das Menü "Extras" durch Hinzufügen von Verknüpfungen in "Verwaltung" an

1.  Erstellen Sie einen neuen Ordner namens *Meinetools* an einem geeigneten Speicherort.

    > [!NOTE]
    > Aufgrund von restriktiven Zugriffsrechten für den Ordner **Verwaltung** dürfen Sie keinen Ordner direkt im Ordner **Verwaltung** erstellen. Sie müssen einen neuen Ordner an einem anderen Speicherort (z. B. auf dem Desktop) erstellen und ihn anschließend in den Ordner **Verwaltung** kopieren.

2.  Verschieben oder kopieren Sie *Meinetools* zu **Systemsteuerung/System und Sicherheit/Verwaltung**. Sie müssen Mitglied der Gruppe "Administratoren" auf dem Computer sein, um Änderungen am Ordner **Verwaltung** vornehmen zu können.

3.  Wenn Sie nicht benötigen, um Benutzer über die Zugriffsrechte für Ihre benutzerdefinierten toolverknüpfungen zu beschränken, fahren Sie mit Schritt 6 fort. Andernfalls klicken Sie mit der rechten Maustaste auf die Tooldatei (oder den Ordner *MeineTools*), und klicken Sie dann auf **Eigenschaften**.

4.  Auf der **Sicherheit** Registerkarte der Datei **Eigenschaften** Dialogfeld klicken Sie auf **bearbeiten**.

5.  für Benutzer, die für die Sie Zugriff auf Tools einschränken möchten, deaktivieren Sie die Kontrollkästchen für **Lesen & ausführen**, **lesen**, und **schreiben** Berechtigungen. Diese Berechtigungen werden von der Toolverknüpfung im Ordner **Verwaltung** übernommen.

    Wenn Sie die Zugriffsrechte eines Benutzers bearbeiten, während der Benutzer den Server-Manager verwendet wird (oder Server-Manager öffnen), und klicken Sie dann Ihre Änderungen nicht, in angezeigt werden der **Tools** Menü, bis der Benutzer die Server-Manager neu gestartet wird.

    > [!NOTE]
    > Wenn Sie den Zugriff auf einen ganzen Ordner, die Sie auf Verwaltung kopiert haben einschränken, sehen Benutzer mit eingeschränkte rechten weder den Ordner noch dessen Inhalt im Server-Manager**Tools** Menü.
    > 
    > Bearbeiten Sie die Berechtigungen für den Ordner, in der **Verwaltung** Ordner. Da ausgeblendete Dateien und Ordner in der Verwaltung immer im Server-Manager angezeigt werden**Tools** Menü verwenden Sie nicht die **Hidden** festlegen auf eine Datei oder eines Ordners **Eigenschaften** Einschränken des Benutzerzugriffs auf Ihre benutzerdefinierten toolverknüpfungen im Dialogfeld.
    > 
    > Mit der Berechtigung **Verweigern** wird die Berechtigung **Zulassen** immer überschrieben.

6.  Mit der rechten Maustaste das ursprüngliche Tool, Skript oder ausführbare Datei, die für die Einträge hinzufügen sollen die **Tools** , und klicken Sie dann auf **Verknüpfung erstellen**.

7.  Verschieben Sie die Verknüpfung in die *Meinetools* Ordner in der Verwaltung.

8.  Aktualisieren oder Server-Manager neu starten, bei Bedarf, um Ihre benutzerdefinierten toolverknüpfungen der **Tools** Menü.

## <a name="BKMK_roles"></a>Verwalten von Rollen auf Rollen-Homepages
Nachdem Sie dem Serverpool des Server-Manager-Server hinzufügen und die Server-Manager Bestandsdaten über Server in Ihrem Pool erfasst, mit Server-Manager im Navigationsbereich für Rollen, die auf verwalteten Servern erkannt werden Seiten hinzugefügt. Auf der Kachel **Server** auf Rollenseiten werden verwaltete Server aufgelistet, von denen die Rolle ausgeführt wird. Standardmäßig werden auf den Kacheln **Ereignisse**, **Best Practices Analyzer**, **Dienste**und **Leistung** Daten für alle Server angezeigt, von denen die Rolle ausgeführt wird. Durch Auswahl bestimmter Server auf der Kachel **Server** wird der Bereich von Ereignissen, Diensten, Leistungsindikatoren und BPA-Ergebnissen auf die ausgewählten Server eingeschränkt. Verwaltungstools sind in der Regel in der Server-Manager-Konsole verfügbar **Tools** Menü, nachdem eine Rolle oder Feature installiert oder auf einem verwalteten Server ermittelt wurde. Sie können auf der Kachel **Server** für eine Rolle oder Gruppe mit der rechten Maustaste auf Servereinträge klicken und dann das gewünschte Verwaltungstool starten.

In Windows Server 2016 verfügen die folgenden Rollen und Features über Verwaltungstools, die in Server-Manager-Konsole als Seiten integriert sind.

-   **Datei- und Speicherdienste.** Die Seiten für Datei- und Speicherdienste enthalten benutzerdefinierte Kacheln und Befehle zum Verwalten von Volumes, Freigaben, virtuellen iSCSI-Datenträgern und Speicherpools. Wenn Sie die Datei öffnen und die Rollenhomepage für Speicherdienste im Server-Manager ein zurücknahmebereich geöffnet, die werden benutzerdefinierte Verwaltungsseiten für Datei- und Speicherdienste angezeigt. Weitere Informationen zum Bereitstellen und Verwalten von Datei- und Speicherdiensten finden Sie unter [Datei- und Speicherdienste](https://go.microsoft.com/fwlink/p/?LinkId=241530).

-   **Remotedesktopdienste.** Die Seiten für Remotedesktopdienste enthalten benutzerdefinierte Kacheln und Befehle zum Verwalten von Sitzungen, Lizenzen, Gateways und virtuellen Desktops. Weitere Informationen zum Bereitstellen und Verwalten von Remotedesktopdiensten finden Sie unter [Remote Desktop Services (RdS)](https://go.microsoft.com/fwlink/p/?LinkId=241532).

-   **IP-Adresse (Management, IPAM).** Die Rollenseite für die IP-Adressverwaltung enthält die benutzerdefinierte Kachel **Willkommen** mit Links zu allgemeinen IPAM-Konfigurations- und IPAM-Verwaltungsaufgaben, inklusive eines Assistenten zum Bereitstellen eines IPAM-Servers. Die IPAM-Homepage enthält zudem Kacheln zum Anzeigen des verwalteten Netzwerks, einer Übersicht über die Konfiguration sowie geplanter Aufgaben.

    Es gibt einige Einschränkungen, die IPAM-Verwaltung in Server-Manager. Im Gegensatz zu anderen Rollen- und Gruppenseiten befinden sich auf der IPAM-Seite keine Kacheln für **Server**, **Ereignisse**, **Leistung**, **Best Practices Analyzer** und **Dienste**. Es ist kein Best Practices Analyzer-Modell für IPAM verfügbar. Best Practices Analyzer-Scans in IPAM werden nicht unterstützt. Wenn Sie auf Server in Ihrem Serverpool zugreifen möchten, auf denen IPAM ausgeführt wird, erstellen Sie eine benutzerdefinierte Gruppe mit diesen Servern, und greifen Sie über die Kachel **Server** auf der benutzerdefinierten Gruppenseite auf die Serverliste zu. Sie können auf IPAM-Server auch über die Kachel **Server** auf der Gruppenseite **Alle Server** zugreifen.

    In Miniaturansichten im Dashboard wird im Vergleich zu Miniaturansichten für andere Rollen und Gruppen nur eine begrenzte Anzahl Zeilen für IPAM angezeigt. Wenn Sie auf die Zeile mit IPAM-Miniaturansichten klicken, können Sie Ereignisse, Leistungsdaten und Verwaltbarkeitsstatuswarnungen für Server anzeigen, auf denen IPAM ausgeführt wird. IPAM-bezogene Dienste können über Seiten für Servergruppen verwaltet werden, die IPAM-Server enthalten, wie die Seite für die Gruppe **Alle Server** .

    Weitere Informationen zum Bereitstellen und Verwalten von IPAM finden Sie unter [IP-Adresse (Management, IPAM)](https://go.microsoft.com/fwlink/p/?LinkId=241533).

## <a name="see-also"></a>Siehe auch
[Server-Manager](server-manager.md)
[Hinzufügen von Servern zu Server Manager](add-servers-to-server-manager.md)
[erstellen und Verwalten von Servergruppen](create-and-manage-server-groups.md)
[anzeigen "und" Konfigurieren Leistungs-, Ereignis- und Dienstdaten](view-and-configure-performance-event-and-service-data.md)
[Datei- und Speicherdienste](https://go.microsoft.com/fwlink/p/?LinkId=241530)
[Remote Desktop Services (RdS)](https://go.microsoft.com/fwlink/p/?LinkId=241532) 
 [ IP-Adresse (Management, IPAM)](https://go.microsoft.com/fwlink/p/?LinkId=241533)



