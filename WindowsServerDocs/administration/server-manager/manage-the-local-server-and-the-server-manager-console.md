---
title: Verwalten des lokalen Servers und der Server-Manager-Konsole
description: Server-Manager
ms.topic: article
ms.assetid: eeb32f65-d588-4ed5-82ba-1ca37f517139
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7892ec8f4102c8baadd8cded8982b6b92702afa8
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895742"
---
# <a name="manage-the-local-server-and-the-server-manager-console"></a>Verwalten des lokalen Servers und der Server-Manager-Konsole

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In Windows Server können Sie mit Server-Manager sowohl den lokalen Server (wenn Sie Server-Manager auf Windows Server ausführen, nicht auf einem Windows-basierten Client Betriebssystem) als auch Remote Server verwalten, auf denen Windows Server 2008 und neuere Versionen des Windows Server-Betriebssystems ausgeführt werden.

Auf der Seite **lokaler Server** in Server-Manager werden Server Eigenschaften, Ereignisse, Dienst-und Leistungsdaten und Best Practices Analyzer Ergebnisse (BPA) für den lokalen Server angezeigt. Die Kacheln "Ereignis", "Dienst", "BPA" und "Leistung" funktionieren wie auf den Rollen- und Servergruppenseiten. Weitere Informationen zum Konfigurieren der Daten, die auf diesen Kacheln angezeigt werden, finden Sie unter [anzeigen und Konfigurieren von Leistungs-, Ereignis-und Dienst Daten](view-and-configure-performance-event-and-service-data.md) und [Ausführen Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](run-best-practices-analyzer-scans-and-manage-scan-results.md).

Menübefehle und Einstellungen in den Überschriften leisten der Server-Manager-Konsole werden global auf alle Server im Server Pool angewendet, und Sie können mit Server-Manager den gesamten Server Pool verwalten.

Dieses Thema enthält folgende Abschnitte:

-   [Herunterfahren des lokalen Servers](#BKMK_shutdown)

-   [Konfigurieren von Server-Manager-Eigenschaften](#BKMK_props)

-   [Verwalten der Server-Manager-Konsole](#BKMK_managesm)

-   [Anpassen von Tools, die im Menü "Extras" angezeigt werden](#BKMK_tools)

-   [Verwalten von Rollen auf Rollen-Homepages](#BKMK_roles)

## <a name="shut-down-the-local-server"></a><a name=BKMK_shutdown></a>Herunterfahren des lokalen Servers
Im Menü **Aufgaben** auf der Kachel **Eigenschaften** des lokalen Servers können Sie eine Windows PowerShell-Sitzung auf dem lokalen Server starten, das MMC-Snap-in " **Computer Verwaltung** " öffnen oder MMC-Snap-Ins für Rollen oder Features öffnen, die auf dem lokalen Server installiert sind. Zudem kann der lokale Server mithilfe des Befehls **Lokalen Server herunterfahren** im Menü **Aufgaben** heruntergefahren werden. Der Befehl **Lokalen Server herunterfahren** ist für den lokalen Server auch auf der Kachel **Server** auf der Seite **Alle Server** oder auf einer Rollen- oder Gruppenseite verfügbar, auf der der lokale Server dargestellt wird.

Beim Herunterfahren des lokalen Servers mit dieser Methode wird im Gegensatz zum Herunterfahren von Windows Server 2016 über den **Start** Bildschirm das Dialogfeld **Windows herunter** fahren geöffnet, in dem Sie die Gründe für das Herunterfahren im Bereich **Ereignis** Protokollierung Herunterfahren angeben können.

> [!NOTE]
> Nur Mitglieder der Gruppe "Administratoren" können einen Server herunterfahren oder neu starten. Standardbenutzer können einen Server weder herunterfahren noch neu starten. Wenn Sie auf den Befehl **Lokalen Server herunterfahren** klicken, werden Standardbenutzer von Serversitzungen abgemeldet. Dies entspricht der Erfahrung eines Standardbenutzers, der den Befehl **Alt+F4** zum Herunterfahren über den Server-Desktop ausführt.

## <a name="configure-server-manager-properties"></a><a name=BKMK_props></a>Konfigurieren von Server-Manager-Eigenschaften
Auf der Kachel **Eigenschaften** auf der Seite **Lokaler Server** können Sie die folgenden Einstellungen anzeigen oder ändern. Um den Wert einer Einstellung zu ändern, klicken Sie auf den Hypertext-Wert der Einstellung.

> [!NOTE]
> Die auf der Kachel **Eigenschaften** des lokalen Servers angezeigten Eigenschaften können normalerweise nur auf dem lokalen Server geändert werden. Die Eigenschaften des lokalen Servers können nicht von einem Remote Computer mithilfe von Server-Manager geändert werden, da auf der Kachel **Eigenschaften** nur Informationen zum lokalen Computer, nicht für Remote Computer, angezeigt werden können.
>
> Da viele Eigenschaften, die auf der Kachel **Eigenschaften** angezeigt werden, über Tools gesteuert werden, die nicht Teil Server-Manager sind (z. b. die Systemsteuerung), werden Änderungen an den **Eigenschaften** Einstellungen nicht immer sofort in der Kachel **Eigenschaften** angezeigt. Die Daten auf der Kachel **Eigenschaften** werden standardmäßig alle zwei Minuten aktualisiert. Um die Daten der Kachel **Eigenschaften** sofort zu aktualisieren, klicken Sie in der Server-Manager Adressleiste auf **Aktualisieren** .

|Einstellung|BESCHREIBUNG|
|------|--------|
|Computername|Zeigt den anzeigen amen des Computers an, und öffnet das Dialogfeld **System Eigenschaften** , in dem Sie den Namen des Servers, die Domänen Mitgliedschaft und andere System Einstellungen wie z. b. Benutzerprofile ändern können.|
|Domäne (oder Arbeitsgruppe, wenn der Server keiner Domäne angehört)|Zeigt die Domäne oder Arbeitsgruppe an, der der Server angehört. Öffnet das Dialogfeld **System Eigenschaften** , in dem Sie den Namen des Servers, die Domänen Mitgliedschaft und andere System Einstellungen wie z. b. Benutzerprofile ändern können.|
|Windows-Firewall|Zeigt den Status der Windows-Firewall für den lokalen Server an. Öffnet **Systemsteuerung\System und Sicherheit\Windows-Firewall**. Weitere Informationen zum Konfigurieren der Windows-Firewall finden Sie unter [Windows-Firewall mit erweiterter Sicherheit und IPsec](https://go.microsoft.com/fwlink/?LinkId=253465).|
|Remoteverwaltung|Zeigt Server-Manager und den Windows PowerShell-Remote Verwaltungsstatus an. Öffnet das Dialogfeld **Remote Verwaltung konfigurieren** . Weitere Informationen zur Remote Verwaltung finden Sie unter [Konfigurieren der Remote Verwaltung in Server-Manager](configure-remote-management-in-server-manager.md).|
|Remotedesktop|Zeigt an, ob Benutzer mithilfe von Remotedesktopsitzungen eine Remoteverbindung mit dem Server herstellen können. Öffnet die Registerkarte **Remote** im Dialogfeld **System Eigenschaften** .|
|NIC-Teamvorgang|Zeigt an, ob der lokale Server am NIC-Teamvorgang teilnimmt. Öffnet das Dialogfeld **NIC-Teamvorgang**. Wenn Sie möchten, können Sie hier den lokalen Server einem NIC-Team hinzufügen. Weitere Informationen zum NIC-Teamvorgang finden Sie im [Whitepaper zum NIC-Teamvorgang](https://go.microsoft.com/fwlink/?LinkID=253449).|
|Ethernet|Zeigt den Netzwerkstatus des Servers an. Öffnet **Systemsteuerung\Netzwerk und Internet\Netzwerkverbindungen**.|
|Betriebssystemversion|In diesem schreibgeschützten Feld wird die Versionsnummer des Windows-Betriebssystems angezeigt, das auf dem lokalen Server ausgeführt wird.|
|Hardwareinformationen|In diesem schreibgeschützten Feld werden Hersteller, Modellname und -nummer der Serverhardware angezeigt.|
|Zuletzt installierte Updates|Zeigt den Tag und die Uhrzeit der letzten Installation von Windows-Updates an. Öffnet **Systemsteuerung\System und Sicherheit\Windows Update**.|
|Windows-Update|Zeigt die Windows Update-Einstellungen für den lokalen Server an. Öffnet **Systemsteuerung\System und Sicherheit\Windows Update**.|
|Zuletzt auf Updates geprüft|Zeigt den Tag und die Uhrzeit der letzten Überprüfung des Servers auf verfügbare Windows-Updates an. Öffnet **Systemsteuerung\System und Sicherheit\Windows Update**.|
|Windows-Fehlerberichterstattung|Zeigt den den Anmeldestatus der Windows-Fehlerberichterstattung an. Öffnet das Dialogfeld **Windows-Fehlerberichterstattungs-Konfiguration**. Weitere Informationen zur Windows-Fehlerberichterstattung, zu den Vorteilen, Datenschutzbestimmungen und Anmeldeeinstellungen finden Sie unter [Windows-Fehlerberichterstattung](https://go.microsoft.com/fwlink/?LinkID=245991).|
|Programm zur Verbesserung der Benutzerfreundlichkeit|Zeigt den Anmeldestatus des Programms zur Verbesserung der Benutzerfreundlichkeit von Windows an. Öffnet das Dialogfeld **Konfiguration des Programms zur Verbesserung der Benutzerfreundlichkeit**. Weitere Informationen zum Programm zur Verbesserung der Benutzerfreundlichkeit von Windows, zu den Vorteilen und Anmeldeeinstellungen finden Sie unter [Programm zur Verbesserung der Benutzerfreundlichkeit von Windows](https://go.microsoft.com/fwlink/?LinkID=245992).|
|Verstärkte Sicherheitskonfiguration für Internet Explorer (IE)|Zeigt, ob die Verstärkte Sicherheitskonfiguration für IE (auch als IE Hardening oder IE ESC bezeichnet) aktiviert oder deaktiviert ist. Öffnet das Dialogfeld **Verstärkte Sicherheitskonfiguration für Internet Explorer**. Die verstärkte Sicherheitskonfiguration für IE ist eine Sicherheitsmaßnahme für Server, mit der verhindert wird, dass Webseiten in Internet Explorer geöffnet werden. Weitere Informationen zur verstärkten Sicherheitskonfiguration für Internet Explorer, zu den Vorteilen und Einstellungen finden Sie unter [Verstärkte Sicherheitskonfiguration  für Internet Explorer](https://go.microsoft.com/fwlink/?LinkId=253461).|
|Zeitzone|Zeigt die Zeitzone des lokalen Servers an. Öffnet das Dialogfeld **Datum und Uhrzeit** .|
|Product ID|Zeigt den Status der Windows-Aktivierung und die Produkt-ID (sofern Windows aktiviert wurde) des Betriebssystems Windows Server 2016 an. Hierbei handelt es sich nicht um den Windows-Product Key. Öffnet das Dialogfeld **Windows-Aktivierung**.|
|Prozessoren|In diesem schreibgeschützten Feld werden Hersteller, Modellname und Geschwindigkeitsinformationen zu den Prozessoren des lokalen Servers angezeigt.|
|Installierter Arbeitsspeicher (RAM)|In diesem schreibgeschützten Feld wird die Größe des verfügbaren Arbeitsspeichers in Gigabyte angezeigt.|
|Speicherplatz insgesamt|In diesem schreibgeschützten Feld wird die Größe des verfügbaren Festplattenspeichers in Gigabyte angezeigt.|

## <a name="manage-the-server-manager-console"></a><a name=BKMK_managesm></a>Verwalten der Server-Manager-Konsole
Globale Einstellungen, die für die gesamte Server-Manager-Konsole gelten, sowie für alle Remote Server, die dem Server-Manager-Server Pool hinzugefügt wurden, befinden sich in den Überschriften leisten oben im Server-Manager Konsolenfenster.

### <a name="add-servers-to-server-manager"></a>Server zu Server-Manager hinzufügen
Mit dem Befehl, mit dem das Dialogfeld **Server hinzufügen** geöffnet wird und Sie dem Server-Manager Server-Pool physische oder virtuelle Remote Server hinzufügen können, befindet sich im Menü **Verwalten** der Server-Manager Konsole. Ausführliche Informationen zum Hinzufügen von Servern finden Sie unter [Hinzufügen von Servern zu Server-Manager](add-servers-to-server-manager.md).

### <a name="refresh-data-that-is-displayed-in-server-manager"></a>Aktualisieren von Daten, die in Server-Manager angezeigt werden
Sie können das Aktualisierungs Intervall für Daten konfigurieren, die in Server-Manager im Dialogfeld **Server-Manager Eigenschaften** angezeigt werden, das Sie über das Menü **Verwalten** öffnen.

##### <a name="to-configure-the-refresh-interval-in-server-manager"></a>So konfigurieren Sie das Aktualisierungsintervall in Server-Manager

1.  Klicken Sie in der Server-Manager Konsole im Menü **Verwalten** auf **Server-Manager Eigenschaften**.

2.  Geben Sie im Dialogfeld **Eigenschaften von Server-Manager** einen Zeitraum (in Minuten) für die verstrichene Zeit in Minuten zwischen den Aktualisierungen der in Server-Manager angezeigten Daten an. Standardwert: 10 Minuten. Klicken Sie anschließend auf "OK".

#### <a name="refresh-limitations"></a>Aktualisierungsbeschränkungen
Die Aktualisierung gilt global für Daten von allen Servern, die Sie dem Server-Manager-Server Pool hinzugefügt haben. Es können keine Daten für einzelne Server, Rollen und Gruppen aktualisiert oder für einzelne Server, Rollen und Gruppen unterschiedliche Aktualisierungsintervalle konfiguriert werden.

Wenn Server, die sich in einem Cluster befinden, Server-Manager hinzugefügt werden, und zwar unabhängig davon, ob es sich um physische oder virtuelle Computer handelt, kann bei der ersten Datenaktualisierung ein Fehler auftreten, oder es werden nur Daten für den Host Server für Cluster Objekte angezeigt. Bei nachfolgenden Aktualisierungen werden die genauen Daten für physische oder virtuelle Server in einem Servercluster angezeigt.

Daten, die auf den Startseiten der Rolle in Server-Manager für Remotedesktopdienste, die IP-Adressverwaltung und die Datei-und Speicherdienste angezeigt werden, werden nicht automatisch aktualisiert. Aktualisieren Sie die auf diesen Seiten angezeigten Daten manuell, indem Sie **F5** drücken oder in der Server-Manager-Konsolen Überschrift auf **Aktualisieren** klicken, während Sie sich auf diesen Seiten befinden.

### <a name="add-or-remove-roles-or-features"></a>Rollen oder Features hinzufügen oder entfernen
Die Befehle, mit denen der Assistent zum Hinzufügen von Rollen und Features und der Assistent zum Entfernen von Rollen und Features geöffnet werden, und das Hinzufügen oder Entfernen von Rollen, Rollen Diensten und Features zu Servern in Ihrem Server Pool finden Sie im Menü **Verwalten** der Server-Manager-Konsole und im Menü **Aufgaben** der Kachel **Rollen und Features** auf Rollen-oder Gruppen Seiten. Ausführlichere Informationen zum Hinzufügen oder Entfernen von Rollen oder Features finden Sie unter [Installieren oder Deinstallieren von Rollen, Rollendiensten oder Features](install-or-uninstall-roles-role-services-or-features.md).

In Server-Manager werden Rollen-und Featuredaten in der Basis Sprache des Systems, auch als "System Default GUI Language" bezeichnet, oder der während der Installation des Betriebssystems ausgewählten Sprache angezeigt.

### <a name="create-server-groups"></a>Erstellen von Server Gruppen
Der Befehl, mit dem das Dialogfeld **Server Gruppe erstellen** geöffnet wird, in dem Sie benutzerdefinierte Server Gruppen erstellen können, befindet sich im Menü **Verwalten** der Server-Manager Konsole. Ausführliche Informationen zum Erstellen von Server Gruppen finden Sie unter [Erstellen und Verwalten von Server Gruppen](create-and-manage-server-groups.md).

### <a name="prevent-server-manager-from-opening-automatically-at-logon"></a>Verhindern, dass Server-Manager beim Anmelden automatisch geöffnet wird
Mit dem Kontrollkästchen **Server-Manager nicht automatisch bei der Anmeldung starten** im Dialogfeld **Server-Manager Eigenschaften** wird gesteuert, ob Server-Manager bei der Anmeldung für Mitglieder der Gruppe "Administratoren" auf einem lokalen Server automatisch geöffnet wird. Diese Einstellung wirkt sich nicht auf das Server-Manager Verhalten aus, wenn es unter Windows 10 als Teil Remoteserver-Verwaltungstools ausgeführt wird. Weitere Informationen zum Konfigurieren dieser Einstellung finden Sie unter [Server-Manager](server-manager.md).

### <a name="zoom-in-or-out"></a>Vergrößern oder Verkleinern
Wenn Sie die Ansicht der Server-Manager Konsole vergrößern oder verkleinern möchten, können Sie entweder die **Zoom** -Befehle im Menü **Ansicht** verwenden oder **Strg + Plus (+)** drücken, um zu vergrößern und **STRG + minus (-)** zu verkleinern.

## <a name="customize-tools-that-are-displayed-in-the-tools-menu"></a><a name=BKMK_tools></a>Anpassen von Tools, die im Menü "Extras" angezeigt werden
Das **Menü Extras** in Server-Manager enthält weiche Links zu Verknüpfungen im Ordner **Verwaltung** unter **Systemsteuerung/System und Sicherheit**. Der Ordner **Verwaltung** enthält eine Liste mit Verknüpfungen oder LNK-Dateien zu verfügbaren Verwaltungs Tools wie MMC-Snap-Ins. Server-Manager füllt das **Menü Extras** mit Links zu diesen Verknüpfungen auf und **kopiert die Ordner** Struktur des Ordners **Verwaltung** in das Menü Extras. Die Tools im Ordner "Verwaltung" werden standardmäßig in einer flachen Liste angeordnet und nach Typ und nach Name sortiert. Im**Menü Server-Manager** Extras werden Elemente nur nach Name, nicht nach Typ sortiert.

Wenn Sie das Menü **Tools** anpassen möchten, kopieren Sie die gewünschten Tool- oder Skriptverknüpfungen in den Ordner **Verwaltung**. Sie können Ihre Verknüpfungen auch in Ordnern organisieren, die im Menü **Tools** hierarchische Menüs bilden. Wenn Sie den Zugriff auf die benutzerdefinierten Tools **im Menü Extras** einschränken möchten, können Sie außerdem Benutzer Zugriffsrechte für Ihre benutzerdefinierten Tool Ordner in "Verwaltung" oder direkt auf dem ursprünglichen Tool bzw. in den Skriptdateien festlegen.

Es wird empfohlen, System- und Verwaltungstools sowie Rollen und Features zugeordnete Verwaltungstools, die auf dem lokalen Server installiert sind, nicht neu zu organisieren. Wenn Verwaltungstools von Rollen und Features verschoben werden, können sie bei Bedarf möglicherweise nicht deinstalliert werden. Nach der Deinstallation einer Rolle oder eines Features bleibt möglicherweise ein defekter Link zu einem Tool, dessen Verknüpfung verschoben wurde, im Menü **Tools** zurück. Beim erneuten Installieren der Rolle wird im Menü **Tools** ein doppelter Link zum selben Tool erstellt, aber einer der Links ist defekt.

Rollen- und Featuretools, die als Teil der Remoteserver-Verwaltungstools auf einem clientbasierten Windows-Computer installiert werden, können jedoch in benutzerdefinierten Ordnern organisiert werden. Das Deinstallieren der übergeordneten Rolle oder des übergeordneten Features hat keine Auswirkungen auf die Tool Verknüpfungen, die auf einem Remote Computer unter Windows 10 verfügbar sind.

Im folgenden Verfahren wird beschrieben, wie ein Beispiel Ordner mit dem Namen *mytools*erstellt und Verknüpfungen für zwei Windows PowerShell-Skripts in den Ordner verschoben werden, auf den dann über das Menü Server-Manager Tools zugegriffen werden kann.

#### <a name="to-customize-the-tools-menu-by-adding-shortcuts-in-administrative-tools"></a>So passen Sie das Menü "Extras" durch Hinzufügen von Verknüpfungen in "Verwaltung" an

1.  Erstellen Sie einen neuen Ordner mit dem Namen *mytools* an einem geeigneten Speicherort.

    > [!NOTE]
    > Aufgrund von restriktiven Zugriffsrechten für den Ordner **Verwaltung** dürfen Sie keinen Ordner direkt im Ordner **Verwaltung** erstellen. Sie müssen einen neuen Ordner an einem anderen Speicherort (z. B. auf dem Desktop) erstellen und ihn anschließend in den Ordner **Verwaltung** kopieren.

2.  Verschieben oder kopieren Sie *mytools* in **Systemsteuerung/System und Sicherheit/Verwaltungs Tools**. Sie müssen Mitglied der Gruppe "Administratoren" auf dem Computer sein, um Änderungen am Ordner **Verwaltung** vornehmen zu können.

3.  Wenn Sie die Benutzer Zugriffsrechte für Ihre benutzerdefinierten Tool Verknüpfungen nicht einschränken müssen, fahren Sie mit Schritt 6 fort. Andernfalls klicken Sie mit der rechten Maustaste auf die Tooldatei (oder den Ordner *MeineTools*), und klicken Sie dann auf **Eigenschaften**.

4.  Klicken Sie im Dialogfeld **Eigenschaften** der Datei auf der Registerkarte **Sicherheit** auf **Bearbeiten**.

5.  Deaktivieren Sie für Benutzer, für die Sie den Zugriff auf das Tool einschränken möchten, die Kontrollkästchen für **Lese & Berechtigungen ausführen**, **Lesen**und **Schreiben** . Diese Berechtigungen werden von der Toolverknüpfung im Ordner **Verwaltung** übernommen.

    Wenn Sie die Zugriffsrechte eines Benutzers bearbeiten, während der Benutzer Server-Manager verwendet (oder wenn Server-Manager geöffnet ist), werden Ihre Änderungen **im Menü Extras** erst angezeigt, wenn der Benutzer Server-Manager neu startet.

    > [!NOTE]
    > Wenn Sie den Zugriff auf einen vollständigen Ordner beschränken, den Sie in "Verwaltung" kopiert haben, können Benutzer mit eingeschränkten Berechtigungen weder den Ordner noch dessen Inhalt im Menü Server-Manager**Tools** anzeigen.
    >
    > Bearbeiten Sie die Berechtigungen für den Ordner im Ordner **Verwaltung** . Da ausgeblendete Dateien und Ordner in "Verwaltung" immer im Menü "Server-Manager**Tools** " angezeigt werden, verwenden Sie die Einstellung **ausgeblendet** im Dialogfeld **Eigenschaften** einer Datei oder eines Ordners nicht, um den Benutzer Zugriff auf Ihre benutzerdefinierten Tool Verknüpfungen einzuschränken.
    >
    > Mit der Berechtigung **Verweigern** wird die Berechtigung **Zulassen** immer überschrieben.

6.  Klicken Sie **mit der rechten** Maustaste auf das ursprüngliche Tool, das Skript oder die ausführbare Datei, für das Sie im Menü Extras Einträge hinzufügen möchten, und klicken Sie dann auf **Verknüpfung erstellen**.

7.  Verschieben Sie die Verknüpfung in den Ordner " *mytools* " unter "Verwaltung".

8.  Wenn erforderlich, können Sie Server-Manager aktualisieren oder neu starten, um die Verknüpfung des Benutzer **definierten Tools im Menü Extras** anzuzeigen.

## <a name="manage-roles-on-role-home-pages"></a><a name=BKMK_roles></a>Verwalten von Rollen auf Rollen-Homepages
Nachdem Sie dem Server-Manager Server Pool Server hinzugefügt haben und Server-Manager Inventur Daten zu Servern in Ihrem Pool sammelt, werden dem Navigationsbereich von Server-Manager Seiten für Rollen hinzugefügt, die auf verwalteten Servern erkannt werden. Auf der Kachel **Server** auf Rollenseiten werden verwaltete Server aufgelistet, von denen die Rolle ausgeführt wird. Standardmäßig werden auf den Kacheln **Ereignisse**, **Best Practices Analyzer**, **Dienste** und **Leistung** Daten für alle Server angezeigt, von denen die Rolle ausgeführt wird. Durch Auswahl bestimmter Server auf der Kachel **Server** wird der Bereich von Ereignissen, Diensten, Leistungsindikatoren und BPA-Ergebnissen auf die ausgewählten Server eingeschränkt. Verwaltungs Tools sind in der Regel im Menü "Server-Manager-Konsolen **Tools** " verfügbar, nachdem eine Rolle oder ein Feature auf einem verwalteten Server installiert oder erkannt wurde. Sie können auf der Kachel **Server** für eine Rolle oder Gruppe mit der rechten Maustaste auf Servereinträge klicken und dann das gewünschte Verwaltungstool starten.

In Windows Server 2016 verfügen die folgenden Rollen und Features über Verwaltungs Tools, die in Server-Manager-Konsole als Seiten integriert sind.

-   **Datei- und Speicherdienste.** Die Seiten für Datei- und Speicherdienste enthalten benutzerdefinierte Kacheln und Befehle zum Verwalten von Volumes, Freigaben, virtuellen iSCSI-Datenträgern und Speicherpools. Wenn Sie die Startseite der Rolle "Datei-und Speicherdienste" in Server-Manager öffnen, wird ein zurücknahmebereich geöffnet, in dem benutzerdefinierte Verwaltungs Seiten für Datei-und Speicherdienste angezeigt werden. Weitere Informationen zum Bereitstellen und Verwalten von Datei- und Speicherdiensten finden Sie unter [Datei- und Speicherdienste](https://go.microsoft.com/fwlink/p/?LinkId=241530).

-   **Remotedesktopdienste.** Die Seiten für Remotedesktopdienste enthalten benutzerdefinierte Kacheln und Befehle zum Verwalten von Sitzungen, Lizenzen, Gateways und virtuellen Desktops. Weitere Informationen zum Bereitstellen und Verwalten von Remotedesktopdienste finden Sie unter [Remotedesktopdienste (rdS)](https://go.microsoft.com/fwlink/p/?LinkId=241532).

-   **IP-Adressverwaltung (IP Address Management, IPAM)** Die Rollenseite für die IP-Adressverwaltung enthält die benutzerdefinierte Kachel **Willkommen** mit Links zu allgemeinen IPAM-Konfigurations- und IPAM-Verwaltungsaufgaben, inklusive eines Assistenten zum Bereitstellen eines IPAM-Servers. Die IPAM-Homepage enthält zudem Kacheln zum Anzeigen des verwalteten Netzwerks, einer Übersicht über die Konfiguration sowie geplanter Aufgaben.

    Es gibt einige Einschränkungen für die IPAM-Verwaltung in Server-Manager. Im Gegensatz zu anderen Rollen- und Gruppenseiten befinden sich auf der IPAM-Seite keine Kacheln für **Server**, **Ereignisse**, **Leistung**, **Best Practices Analyzer** und **Dienste**. Für IPAM ist kein Best Practices Analyzer Modell verfügbar. Best Practices Analyzer Scans in IPAM werden nicht unterstützt. Wenn Sie auf Server in Ihrem Serverpool zugreifen möchten, auf denen IPAM ausgeführt wird, erstellen Sie eine benutzerdefinierte Gruppe mit diesen Servern, und greifen Sie über die Kachel **Server** auf der benutzerdefinierten Gruppenseite auf die Serverliste zu. Sie können auf IPAM-Server auch über die Kachel **Server** auf der Gruppenseite **Alle Server** zugreifen.

    In Miniaturansichten im Dashboard wird im Vergleich zu Miniaturansichten für andere Rollen und Gruppen nur eine begrenzte Anzahl Zeilen für IPAM angezeigt. Wenn Sie auf die Zeile mit IPAM-Miniaturansichten klicken, können Sie Ereignisse, Leistungsdaten und Verwaltbarkeitsstatuswarnungen für Server anzeigen, auf denen IPAM ausgeführt wird. IPAM-bezogene Dienste können über Seiten für Servergruppen verwaltet werden, die IPAM-Server enthalten, wie die Seite für die Gruppe **Alle Server**.

    Weitere Informationen zum Bereitstellen und Verwalten von IPAM finden Sie unter [IP Address Management (IPAM)](https://go.microsoft.com/fwlink/p/?LinkId=241533).

## <a name="see-also"></a>Weitere Informationen
[Server-Manager](server-manager.md) 
 [Server zu Server-Manager](add-servers-to-server-manager.md) 
 Hinzufügen [Erstellen und Verwalten von Server Gruppen](create-and-manage-server-groups.md) 
 [Anzeigen und Konfigurieren von Leistungs-, Ereignis-und Dienst Daten](view-and-configure-performance-event-and-service-data.md) 
 [Datei-und Speicherdienste](https://go.microsoft.com/fwlink/p/?LinkId=241530) 
 [Remotedesktopdienste (rdS)](https://go.microsoft.com/fwlink/p/?LinkId=241532) 
 [IP-Adressverwaltung (IP Address Management, IPAM)](https://go.microsoft.com/fwlink/p/?LinkId=241533)



