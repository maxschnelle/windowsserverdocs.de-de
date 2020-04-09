---
title: Einrichten einer AD FS-Bereitstellung mit AlwaysOn-Verfügbarkeitsgruppen
author: billmath
ms.author: billmath
manager: daveba
ms.date: 01/20/2020
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ddec398be56aba6d354b1863a98c8d641831415c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816093"
---
# <a name="setting-up-an-ad-fs-deployment-with-alwayson-availability-groups"></a>Einrichten einer AD FS-Bereitstellung mit AlwaysOn-Verfügbarkeitsgruppen
Eine hochverfügbare georedunverteilte Topologie bietet Folgendes:
* Beseitigung eines Single Point of Failure: Dank der Failoverfunktionen können Sie eine hochverfügbare AD FS-Infrastruktur erreichen, auch wenn eines der Rechenzentren in einem Teil einer Welt ausfällt.
* Verbesserte Leistung: Sie können die vorgeschlagene Bereitstellung zum Bereitstellen einer hochleistungsfähigen ADFS-Infrastruktur verwenden.

AD FS kann für ein hochverfügbares georedunverteiltes Szenario konfiguriert werden.
Das folgende Handbuch führt Sie durch eine Übersicht über AD FS mit SQL Always on-Verfügbarkeits Gruppen und Überlegungen zur Bereitstellung und Anleitungen.

## <a name="overview---alwayson-availability-groups"></a>Übersicht-AlwaysOn-Verfügbarkeitsgruppen

Weitere Informationen zu AlwaysOn-Verfügbarkeits Gruppen finden Sie unter [Übersicht über AlwaysOn-Verfügbarkeitsgruppen (SQL Server)](https://technet.microsoft.com/library/ff877884.aspx) .

Aus Sicht der Knoten einer AD FS SQL Server Farm ersetzt die AlwaysOn-Verfügbarkeits Gruppe die einzelne SQL Server Instanz als die Richtlinie/artefaktdatenbank.  Der verfügbarkeitsgruppenlistener verwendet den Client (der AD FS Sicherheitstokendienst) zum Herstellen einer Verbindung mit SQL.
Das folgende Diagramm zeigt eine AD FS SQL Server Farm mit AlwaysOn-Verfügbarkeits Gruppe.

![Serverfarm mit SQL](media/ad-fs-always-on/SQLoverview.png)

Eine Always on Verfügbarkeits Gruppe (Availability Group, AG) ist eine oder mehrere Benutzer Datenbanken, für die ein Failover ausgeführt wird. Eine Verfügbarkeits Gruppe besteht aus einem primären Verfügbarkeits Replikat und einem bis vier sekundären Replikaten, die durch SQL Server Protokoll basierten Daten Verschiebung für den Datenschutz ohne freigegebenen Speicher verwaltet werden. Jedes Replikat wird von einer Instanz von SQL Server auf einem anderen wsfc-Knoten gehostet. Die Verfügbarkeits Gruppe und ein entsprechender virtueller Netzwerkname werden als Ressourcen im wsfc-Cluster registriert.

Ein verfügbarkeitsgruppenlistener im Knoten des primären Replikats antwortet auf eingehende Client Anforderungen zum Herstellen einer Verbindung mit dem virtuellen Netzwerknamen. basierend auf Attributen in der Verbindungs Zeichenfolge wird jede Anforderung an die entsprechende SQL Server Instanz umgeleitet.
Wenn bei einem Failover der Besitz von freigegebenen physischen Ressourcen nicht auf einen anderen Knoten übertragen wird, wird wsfc genutzt, um ein sekundäres Replikat auf einer anderen SQL Server Instanz neu zu konfigurieren, um das primäre Replikat der Verfügbarkeits Gruppe zu werden. Die virtuelle Netzwerknamen Ressource der Verfügbarkeits Gruppe wird dann auf diese Instanz übertragen.
Zu einem beliebigen Zeitpunkt kann nur eine einzelne SQL Server Instanz das primäre Replikat der Datenbanken einer Verfügbarkeits Gruppe hosten. alle zugeordneten sekundären Replikate müssen sich jeweils auf einer separaten Instanz befinden, und jede Instanz muss sich auf separaten physischen Knoten befinden.

> [!NOTE] 
> Wenn Computer in Azure ausgeführt werden, richten Sie die virtuellen Azure-Computer ein, um die Listenerkonfiguration für die Kommunikation mit AlwaysOn-Verfügbarkeits Gruppen zu aktivieren. Weitere Informationen [Virtual Machines: SQL Always on Listener](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener).

Eine weitere Übersicht über AlwaysOn-Verfügbarkeitsgruppen finden Sie unter [Übersicht über Always on Verfügbarkeits Gruppen (SQL Server)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-ver15).

> [!NOTE] 
> Wenn die Organisation ein Failover über mehrere Daten Center hinweg erfordert, empfiehlt es sich, in jedem Daten Center eine artefaktdatenbank zu erstellen und einen Hintergrund Cache zu aktivieren, der die Latenzzeit während der Anforderungs Verarbeitung reduziert. Befolgen Sie die Anweisungen für die [Feinabstimmung von SQL und die Reduzierung der Latenz](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/adfs-sql-latency)Zeit.

## <a name="deployment-guidance"></a>Leitfaden zur Bereitstellung

1. <b>Beachten Sie die richtige Datenbank für die Ziele der AD FS Bereitstellung.</b> In AD FS wird eine Datenbank zum Speichern der Konfiguration und in einigen Fällen Transaktionsdaten verwendet, die sich auf die Verbunddienst beziehen. Sie können mit AD FS Software entweder die interne Windows-Datenbank (WID) oder Microsoft SQL Server 2008 oder höher auswählen, um die Daten im Verbund Dienst zu speichern.
In der folgenden Tabelle werden die Unterschiede in den unterstützten Funktionen zwischen einer wid und einer SQL-Datenbank beschrieben.


| Kategorie      | Feature       | Unterstützt von wid  | Von SQL unterstützt |
| ------------------ |:-------------:| :---:|:---: |
| AD FS Features     | Bereitstellung einer Verbundserverfarm | Ja  | Ja |
| AD FS Features     | SAML-artefaktauflösung. Hinweis: Dies ist für SAML-Anwendungen nicht üblich.     |   Nein | Nein  |
| AD FS Features | Wiedergabe Erkennung für SAML/WS-Verbund Token. Hinweis: Dies ist nur erforderlich, wenn AD FS Token von externen IDPs empfängt. Dies ist nicht erforderlich, wenn AD FS nicht als IDP fungiert.      |    Nein  | Ja |
| Datenbankfunktionen     |   Grundlegende Daten Bank Redundanz mithilfe der Pull-Replikation, bei der ein oder mehrere Server, die eine schreibgeschützte Kopie der Datenbank hosten, Änderungen anfordern, die auf einem Quell Server eine Lese-/Schreibkopie der Datenbank durchgeführt haben.    |   Nein | Nein  |
| Datenbankfunktionen | Daten Bank Redundanz mithilfe von Lösungen für Hochverfügbarkeit, z. b. Clustering oder Spiegelung (auf Datenbankebene)      |    Nein  | Ja |

Wenn Sie ein großes Unternehmen mit mehr als 100 Vertrauens Stellungen sind, die sowohl interne als auch externe Benutzer mit einmaligem Anmelden für Verbund Anwendungen oder-Dienste bereitstellen müssen, ist SQL die empfohlene Option.

Wenn Sie eine Organisation mit 100 oder weniger konfigurierten Vertrauens Stellungen sind, bietet wid eine Redundanz für Daten-und Verbund Dienste (wobei jeder Verbund Serveränderungen auf anderen Verbund Servern in derselben Farm repliziert). WID unterstützt keine Erkennung von tokenwiederholungen oder artefaktauflösung und hat ein Limit von 30 Verbund Servern.
Weitere Informationen zum Planen der Bereitstellung finden Sie [hier](https://docs.microsoft.com/windows-server/identity/ad-fs/design/planning-your-deployment).

## <a name="sql-server-high-availability-solutions"></a>SQL Server Lösungen mit hoher Verfügbarkeit
Wenn Sie SQL Server als AD FS Konfigurations Datenbank verwenden, können Sie mithilfe SQL Server Replikation georedundanz für Ihre AD FS Farm einrichten. Georedundante Redundanz repliziert Daten zwischen zwei geografisch entfernten Standorten, sodass Anwendungen von einem Standort zu einem anderen wechseln können. Auf diese Weise können Sie bei einem Ausfall eines Standorts weiterhin alle Konfigurationsdaten am zweiten Standort verfügbar haben. 
Wenn SQL die geeignete Datenbank für Ihre Bereitstellungs Ziele ist, fahren Sie mit diesem Bereitstellungs Handbuch fort.

In diesem Handbuch werden die folgenden Schritte erläutert:
* AD FS bereitstellen
* Konfigurieren von AD FS für die Verwendung einer AlwaysOn-Verfügbarkeitsgruppen
* Installieren der Rolle "Failoverclustering"
* Ausführen von Cluster Validierungs Tests
* Always on Verfügbarkeits Gruppen aktivieren
* Sichern von AD FS-Datenbanken
* Erstellen von AlwaysOn-Verfügbarkeits Gruppen
* Datenbanken auf dem zweiten Knoten hinzufügen
* Verknüpfen eines Verfügbarkeits Replikats mit Verfügbarkeits Gruppen
* Aktualisieren der SQL-Verbindungs Zeichenfolge

## <a name="deploy-ad-fs"></a>AD FS bereitstellen

> [!NOTE] 
> Wenn Computer in Azure ausgeführt werden, muss die Virtual Machines auf eine bestimmte Art und Weise konfiguriert werden, damit der Listener mit der Always on Verfügbarkeits Gruppe kommunizieren kann. Weitere Informationen zur Konfiguration finden Sie unter [Konfigurieren eines Load Balancers für eine Verfügbarkeits Gruppe in Azure SQL Server VMS](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener) .


In diesem Bereitstellungs Handbuch wird eine zwei-Knoten-Farm mit zwei SQL-Servern als Beispiel angezeigt.
Befolgen Sie zum Bereitstellen AD FS die folgenden Links, um den AD FS-Rollen Dienst zu installieren. Zum Konfigurieren von für eine AOA-Gruppe müssen zusätzliche Schritte für die Rolle ausgeführt werden.
-   [Hinzufügen eines Computers zu einer Domäne](https://docs.microsoft.com/windows-server/identity/ad-fs/deployment/join-a-computer-to-a-domain)
-   [Registrieren eines SSL-Zertifikats für AD FS](https://docs.microsoft.com/windows-server/identity/ad-fs/deployment/enroll-an-ssl-certificate-for-ad-fs)
-   [Installieren des AD FS-Rollendiensts](https://docs.microsoft.com/windows-server/identity/ad-fs/deployment/install-the-ad-fs-role-service)


## <a name="configuring-ad-fs-to-use-an-alwayson-availability-group"></a>Konfigurieren von AD FS für die Verwendung einer AlwaysOn-Verfügbarkeits Gruppe

Das Konfigurieren einer AD FS-Farm mit AlwaysOn-Verfügbarkeits Gruppen erfordert eine geringfügige Änderung am AD FS Bereitstellungs Verfahren. Stellen Sie sicher, dass auf allen Server Instanzen dieselbe Version von SQL ausgeführt wird. Die vollständige Liste der Voraussetzungen, Einschränkungen und Empfehlungen für Always on-Verfügbarkeitsgruppen finden Sie [hier](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability?view=sql-server-2017#PrerequisitesForDbs).

1.  Die Datenbanken, die Sie sichern möchten, müssen erstellt werden, bevor die AlwaysOn-Verfügbarkeits Gruppen konfiguriert werden können.  AD FS erstellt seine Datenbanken im Rahmen der Einrichtung und Erstkonfiguration des ersten Verbund Dienst Knotens einer neuen AD FS SQL Server Farm.  Geben Sie den Daten bankhostnamen für die vorhandene Farm mithilfe von SQL Server an. Als Teil der AD FS Konfiguration müssen Sie eine SQL-Verbindungs Zeichenfolge angeben. Daher müssen Sie die erste AD FS Farm so konfigurieren, dass eine direkte Verbindung mit einer SQL-Instanz hergestellt wird (Dies ist nur temporär). Spezifische Anleitungen zum Konfigurieren einer AD FS-Farm, einschließlich der Konfiguration eines AD FS Farm Knotens mit einer SQL Server-Verbindungs Zeichenfolge, finden Sie unter [Konfigurieren eines Verbund Servers](https://docs.microsoft.com/windows-server/identity/ad-fs/deployment/configure-a-federation-server).

![Farm angeben](media/ad-fs-always-on/deploymentSpecifyFarm.png)

2.  Überprüfen Sie die Verbindung mit der Datenbank mithilfe von SSMS, und stellen Sie dann eine Verbindung mit dem Zielhostnamen der Wenn Sie der Verbund Farm einen weiteren Knoten hinzufügen, stellen Sie eine Verbindung mit der Zieldatenbank her.
3.  Geben Sie das SSL-Zertifikat für die AD FS-Farm an.

![SSL-Zertifikat angeben](media/ad-fs-always-on/deploymentSpecifySSL.png)

4.  Verbinden Sie die Farm mit einem Dienst Konto oder GMSA.

![Dienst Konto angeben](media/ad-fs-always-on/deploymentSpecifyServiceAccount.png)

5.  Schließen Sie die Konfiguration und Installation der AD FS Farm ab.

> [!NOTE] 
> SQL Server müssen unter einem Domänen Konto für die Installation von Always on Verfügbarkeits Gruppen ausgeführt werden. Standardmäßig wird es als lokales System ausgeführt.

## <a name="install-the-failover-clustering-role"></a>Installieren der Rolle "Failoverclustering"
In der Windows Server-Failoverclusterrolle finden Sie weitere Informationen zu Windows Server-Failoverclustern.
1.  Starten Sie den Server-Manager.
2.  Wählen Sie im Menü verwalten die Option Rollen und Features hinzufügen aus.
3.  Wählen Sie auf der Seite Vorbereitung die Option weiter aus.
4.  Wählen Sie auf der Seite Installationstyp auswählen die Option rollenbasierte oder featurebasierte Installation aus, und klicken Sie dann auf Weiter.
5.  Wählen Sie auf der Seite Zielserver auswählen den SQL-Server aus, auf dem Sie das Feature installieren möchten, und klicken Sie dann auf Weiter.

![Zielserver](media/ad-fs-always-on/clusteringDestinationServer.png)

6.  Wählen Sie auf der Seite Server Rollen auswählen die Option weiter aus.
7.  Aktivieren Sie auf der Seite Features auswählen das Kontrollkästchen Failoverclustering.

![Clustering-Feature auswählen](media/ad-fs-always-on/clusteringFeature.png)

8.  Wählen Sie auf der Seite Installations Auswahl bestätigen die Option installieren aus.
Ein Neustart des Servers ist für das Failoverclusteringfeature nicht erforderlich.
9.  Wenn die Installation abgeschlossen ist, wählen Sie schließen aus.
10. Wiederholen Sie diesen Vorgang auf jedem Server, den Sie als Failoverclusterknoten hinzufügen möchten.

## <a name="run-cluster-validation-tests"></a>Ausführen von Cluster Validierungs Tests
1.  Starten Sie den Failovercluster-Manager auf einem Computer, auf dem die Verwaltungstools für Failovercluster über die Remoteserver-Verwaltungstools installiert wurden, oder auf einem Server, auf dem Sie das Failoverclusteringfeature installiert haben. Um dies auf einem Server zu erreichen, starten Sie Server-Manager, und wählen Sie dann im Menü Extras die Option Failovercluster-Manager aus.
2.  Klicken Sie im Failovercluster-Manager Bereich unter Verwaltung auf Konfiguration überprüfen.
3.  Wählen Sie auf der Seite Vorbereitung die Option weiter aus.
4.  Geben Sie auf der Seite Server oder Cluster auswählen in das Feld Name eingeben den NetBIOS-Namen oder den voll qualifizierten Domänen Namen eines Servers ein, den Sie als Failoverclusterknoten hinzufügen möchten, und klicken Sie dann auf hinzufügen. Wiederholen Sie diesen Schritt für alle weiteren Server, die Sie hinzufügen möchten. Wenn Sie mehrere Server gleichzeitig hinzufügen möchten, trennen Sie die Namen durch ein Komma oder Semikolon. Geben Sie die Namen z. B. im Format server1.contoso.com, server2.contoso.com ein. Wenn Sie fertig sind, wählen Sie weiter aus.

![Bild auswählen (Server)](media/ad-fs-always-on/clusterValidationServers.png)

5. Wählen Sie auf der Seite Test Optionen die Option Alle Tests ausführen (empfohlen) aus, und klicken Sie dann auf Weiter.
6. Wählen Sie auf der Seite Bestätigung die Option weiter aus.
Auf der Seite zur Ausführung der Überprüfung wird der Status der aktiven Tests angezeigt.
7. Führen Sie auf der Seite Zusammenfassung eine der folgenden Aktionen aus:
- Wenn die Ergebnisse auf eine erfolgreiche Ausführung der Tests hinweisen und die Konfiguration für das Clustering geeignet ist und Sie den Cluster sofort erstellen möchten, stellen Sie sicher, dass das Kontrollkästchen Cluster jetzt mit den überprüften Knoten erstellen aktiviert ist, und klicken Sie dann auf Fertigstellen. Fahren Sie anschließend mit Schritt 4 des [Verfahrens erstellen des Failoverclusters](https://docs.microsoft.com/windows-server/failover-clustering/create-failover-cluster#create-the-failover-cluster)fort.

![Konfigurations Bild überprüfen](media/ad-fs-always-on/clusterValidationResults.png)

-   Wenn die Ergebnisse darauf hindeuten, dass Warnungen oder Fehler aufgetreten sind, wählen Sie Bericht anzeigen aus, um die Details anzuzeigen und zu ermitteln, welche Probleme korrigiert werden müssen. Beachten Sie, dass eine Warnung für einen bestimmten Validierungstest darauf hinweist, dass dieser Aspekt des Failoverclusters zwar unterstützt werden kann, er aber möglicherweise nicht den empfohlenen bewährten Methoden entspricht.

> [!NOTE]
> Wenn Sie eine Warnung für den Test "Permanente Reservierung für Speicherplatz überprüfen" erhalten, finden Sie weitere Informationen im Blogbeitrag [Windows Failover Cluster validation warning indicates your disks don't support the persistent reservations for Storage Spaces](https://blogs.msdn.microsoft.com/clustering/2013/05/24/validate-storage-spaces-persistent-reservation-test-results-with-warning/) .
> Weitere Informationen zu Hardwarevalidierungstests finden Sie unter [Überprüfen der Hardware für einen Failovercluster](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v%3dws.11)).

## <a name="create-the-failover-cluster"></a>Erstellen des Failoverclusters

Stellen Sie zum Abschließen dieses Schritts sicher, dass das Benutzerkonto, mit dem Sie sich anmelden, den im Abschnitt [Überprüfen der Voraussetzungen](https://docs.microsoft.com/windows-server/failover-clustering/create-failover-cluster#verify-the-prerequisites) dieses Themas angegebenen Anforderungen entspricht.
1.  Starten Sie den Server-Manager.
2.  Wählen Sie im Menü Extras die Option Failovercluster-Manager aus.
3.  Klicken Sie im Failovercluster-Manager Bereich unter Verwaltung auf Cluster erstellen.
Der Clustererstellungs-Assistent wird geöffnet.
4.  Wählen Sie auf der Seite Vorbereitung die Option weiter aus.
5.  Wenn die Seite Server auswählen angezeigt wird, geben Sie in das Feld Name eingeben den NetBIOS-Namen oder den voll qualifizierten Domänen Namen eines Servers ein, den Sie als Failoverclusterknoten hinzufügen möchten, und klicken Sie dann auf hinzufügen. Wiederholen Sie diesen Schritt für alle weiteren Server, die Sie hinzufügen möchten. Wenn Sie mehrere Server gleichzeitig hinzufügen möchten, trennen Sie die Namen durch ein Komma oder Semikolon. Geben Sie die Namen z. B. im Format server1.contoso.com; server2.contoso.com ein. Wenn Sie fertig sind, wählen Sie weiter aus.

![Cluster erstellen und Server auswählen](media/ad-fs-always-on/createClusterServers.png)

> [!NOTE]
> Wenn Sie den Cluster sofort nach dem Ausführen der Überprüfung im [Konfigurations Überprüfungsverfahren](https://docs.microsoft.com/windows-server/failover-clustering/create-failover-cluster#validate-the-configuration)erstellt haben, wird die Seite Server auswählen nicht angezeigt. Die überprüften Knoten werden automatisch zum Clustererstellungs-Assistenten hinzugefügt, damit Sie diese nicht erneut eingeben müssen.

6.  Wenn Sie die Validierung zuvor übersprungen haben, wird eine Seite mit einer Validierungswarnung angezeigt. Es wird dringend empfohlen, die Clustervalidierung auszuführen. Nur Cluster, die alle Validierungstests bestehen, werden von Microsoft unterstützt. Um die Validierungstests auszuführen, wählen Sie ja aus, und klicken Sie dann auf Weiter. Führen Sie den Konfigurationsüberprüfungs-Assistenten wie unter Überprüfen [der Konfiguration](https://docs.microsoft.com/windows-server/failover-clustering/create-failover-cluster#validate-the-configuration)beschrieben aus.
7.  Gehen Sie auf der Seite Zugriffspunkt für die Clusterverwaltung wie folgt vor:
-   Geben Sie in das Feld Clustername den Namen ein, über den Sie den Cluster verwalten möchten. Überprüfen Sie zuvor die folgenden Informationen:
 -  Während der Cluster Erstellung wird dieser Name als Cluster Computer Objekt (auch als Cluster Namen Objekt oder CNO bezeichnet) in AD DS registriert. Wenn Sie einen NetBIOS-Namen für den Cluster angeben, wird das Clustercomputerobjekt (CNO) am gleichen Speicherort erstellt, an dem sich die Computerobjekte für die Clusterknoten befinden. Hierbei kann es sich um den Standardcontainer des Computers oder um eine Organisationseinheit (OU) handeln.
 -  Wenn Sie einen anderen Speicherort für das CNO angeben möchten, können Sie den Distinguished Name einer Organisationseinheit im Feld Clustername eingeben. Beispiel: CN = Cluster Name, ou = Clusters, DC =%% amp; quot; DC = com.
 -  Wenn ein Domänenadministrator das CNO in einer anderen Organisationseinheit vorab bereitgestellt hat, in der sich die Clusterknoten nicht befinden, geben Sie den Distinguished Name an, der vom Domänenadministrator bereitgestellt wird.
- Wenn der Server nicht über einen für DHCP konfigurierten Netzwerkadapter verfügt, müssen Sie mindestens eine statische IP-Adresse für den Failovercluster konfigurieren. Aktivieren Sie das Kontrollkästchen neben den jeweiligen Netzwerkadaptern, die Sie für die Clusterverwaltung verwenden möchten. Wählen Sie das Feld Adresse neben einem ausgewählten Netzwerk aus, und geben Sie dann die IP-Adresse ein, die Sie dem Cluster zuweisen möchten. Diese IP-Adresse (oder Adressen) wird dem Clusternamen im Domain Name System zugeordnet.
- Wenn Sie fertig sind, wählen Sie weiter aus.

8.  Überprüfen Sie auf der Seite Bestätigung die Einstellungen. Das Kontrollkästchen Der gesamte geeignete Speicher soll dem Cluster hinzugefügt werden ist standardmäßig aktiviert. Deaktivieren Sie dieses Kontrollkästchen, wenn Sie eine der folgenden Optionen ausführen möchten:
-   Sie möchten den Speicher später konfigurieren.
-   Sie planen die Erstellung von Clusterspeicherplätzen über den Failovercluster-Manager oder mithilfe von Windows PowerShell-Cmdlets für Failoverclustering und haben bisher keine Speicherplätze in den Datei- und Speicherdiensten erstellt. Weitere Informationen finden Sie unter [Bereitstellen von Clusterspeicherplätzen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11)).
9.  Wählen Sie weiter aus, um den Failovercluster zu erstellen.
10. Bestätigen Sie auf der Seite Zusammenfassung die erfolgreiche Erstellung des Failoverclusters. Wenn Warnungen oder Fehler aufgetreten sind, zeigen Sie die Ausgabe der Zusammenfassung an, oder wählen Sie Bericht anzeigen aus, um den vollständigen Bericht anzuzeigen. Wählen Sie Fertig stellen aus.
11. Überprüfen Sie, ob der Clustername in der Navigationsstruktur unter Failovercluster-Manager aufgeführt ist, um die Erstellung des Clusters zu bestätigen. Sie können den Cluster Namen erweitern und dann unter Knoten, Speicher oder Netzwerke Elemente auswählen, um die zugeordneten Ressourcen anzuzeigen.
Beachten Sie, dass es einen Moment dauern kann, bevor der Clustername im DNS erfolgreich repliziert wird. Wenn Sie nach der erfolgreichen DNS-Registrierung und-Replikation alle Server in Server-Manager ausgewählt haben, sollte der Cluster Name als Server mit dem verwaltbarkeitsstatus Online aufgeführt werden.

![Cluster Erstellung ist beendet](media/ad-fs-always-on/createClusterComplete.png)

## <a name="enable-always-on-availability-groups-with-sql-server-configuration-manager"></a>Aktivieren von Always on-Verfügbarkeits Gruppen mit SQL Server-Konfigurations-Manager

1.  Stellen Sie eine Verbindung mit dem wsfc-Knoten (Windows Server Failover Cluster) her, der die SQL Server Instanz hostet, auf der Sie Always on Verfügbarkeits Gruppen aktivieren möchten.
2.  Zeigen Sie im Menü Start auf alle Programme, zeigen Sie auf Microsoft SQL Server, zeigen Sie auf Konfigurationstools, und klicken Sie auf SQL Server-Konfigurations-Manager.
3.  Klicken Sie in SQL Server-Konfigurations-Manager auf SQL Server Services, klicken Sie mit der rechten Maustaste auf SQL Server (<instance name>), wobei <instance name> der Name einer lokalen Server Instanz ist, für die Sie Always on Verfügbarkeits Gruppen aktivieren möchten, und klicken Sie auf Eigenschaften.
4.  Wählen Sie die Registerkarte Always on Hochverfügbarkeit aus.
5.  Überprüfen Sie, ob das Feld Name des Windows-Failoverclusters den Namen des lokalen Failoverclusters enthält. Wenn dieses Feld leer ist, unterstützt diese Serverinstanz derzeit keine Always on-Verfügbarkeitsgruppen. Entweder der lokale Computer ist kein Cluster Knoten, der wsfc-Cluster wurde heruntergefahren, oder diese Edition von SQL Server, die Always on-Verfügbarkeitsgruppen nicht unterstützt.
6.  Aktivieren Sie das Kontrollkästchen Always on Verfügbarkeits Gruppen aktivieren, und klicken Sie auf OK.
Der SQL Server-Konfigurations-Manager speichert die Änderung. Dann müssen Sie den SQL Server-Dienst manuell neu starten. Auf diese Weise können Sie eine Neustartzeit auswählen, die für Ihre Geschäftsanforderungen am besten geeignet ist. Wenn der SQL Server-Dienst neu gestartet wird, wird Always on aktiviert, und die ishadrenabled-Server Eigenschaft wird auf 1 festgelegt.

![Aktivieren von AOA](media/ad-fs-always-on/enableAoAGroup.png)

## <a name="back-up-ad-fs-databases"></a>Sichern von AD FS-Datenbanken
Sichern Sie die AD FS Konfigurations-und artefaktdatenbanken mit den vollständigen Transaktions Protokollen. Legen Sie die Sicherungskopie im ausgewählten Ziel ab.
Sichern Sie das AD FS-artefaktverzeichnis und die Konfigurations Datenbanken.
- Tasks > Sicherung > voll > zu einer Sicherungsdatei hinzufügen > OK zum Erstellen

![Server sichern](media/ad-fs-always-on/backUpADFS.png)

## <a name="create-new-availability-group"></a>Neue Verfügbarkeits Gruppe erstellen

1.  Stellen Sie in Objekt-Explorer eine Verbindung mit der Serverinstanz her, die das primäre Replikat hostet
2.  Erweitern Sie den Knoten Always on Hochverfügbarkeit und den Knoten Verfügbarkeits Gruppen.
3.  Um den Assistenten für neue Verfügbarkeitsgruppen zu starten, wählen Sie den Befehl Assistent für neue Verfügbarkeitsgruppen aus.
4.  Wenn Sie den Assistenten zum ersten Mal ausführen, wird eine Einführungsseite angezeigt. Damit diese Seite in Zukunft nicht mehr angezeigt wird, klicken Sie auf Diese Seite nicht mehr anzeigen. Nachdem Sie diese Seite gelesen haben, klicken Sie auf Weiter.
5.  Geben Sie auf der Seite Optionen für die Verfügbarkeits Gruppe angeben den Namen der neuen Verfügbarkeits Gruppe in das Feld Name der Verfügbarkeits Gruppe ein. Dieser Name muss ein gültiger SQL Server Bezeichner sein, der im Cluster und in Ihrer Domäne als Ganzes eindeutig ist. Die maximale Länge für einen Verfügbarkeits Gruppennamen beträgt 128 Zeichen. e
6.  Geben Sie als nächstes den Clustertyp an. Die möglichen Cluster Typen hängen von der SQL Server Version und dem Betriebssystem ab. Wählen Sie entweder wsfc, extern oder None aus. Weitere Informationen finden Sie unter [angeben der Name der Verfügbarkeits Gruppe](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/specify-availability-group-name-page?view=sql-server-ver15)

![Name der Gruppe "AOA" und Cluster](media/ad-fs-always-on/createAoAName.png)

7.  Auf der Seite Datenbanken auswählen sind im Raster die Benutzerdatenbanken auf der verbundenen Serverinstanz aufgeführt, die Verfügbarkeitsdatenbanken werden können. Wählen Sie mindestens eine der aufgelisteten Datenbanken aus, die an der neuen Verfügbarkeits Gruppe teilnehmen sollen. Diese Datenbanken sind anfänglich die ursprünglichen primären Datenbanken.
Für jede aufgelistete Datenbank zeigt die Spalte Größe die Datenbankgröße an (wenn bekannt). In der Spalte Status wird angegeben, ob eine bestimmte Datenbank die [Voraussetzungen](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability?view=sql-server-ver15) für Verfügbarkeits Datenbanken erfüllt. Die Voraussetzungen sind nicht erfüllt, eine kurze Statusbeschreibung gibt den Grund an, warum die Datenbank nicht geeignet ist. Dies ist beispielsweise der Fall, wenn das vollständige Wiederherstellungs Modell nicht verwendet wird. Klicken Sie auf die Statusbeschreibung, um weitere Informationen zu erhalten.
Wenn Sie eine Datenbank so ändern, dass sie verwendet werden kann, klicken Sie auf Aktualisieren, um das Raster für die Datenbanken zu aktualisieren.
Wenn die Datenbank einen Datenbank-Hauptschlüssel enthält, geben Sie das Kennwort für den Datenbank-Hauptschlüssel in die Spalte Kennwort ein.

![Datenbanken für AOA auswählen](media/ad-fs-always-on/createAoASelectDb.png)

8. Geben Sie auf der Seite Replikate angeben mindestens ein Replikat für die neue Verfügbarkeits Gruppe an, und konfigurieren Sie es. Diese Seite enthält vier Registerkarten. In der folgenden Tabelle werden diese Registerkarten vorgestellt. Weitere Informationen finden Sie auf der [Seite Replikate angeben (Assistent für neue Verfügbarkeits Gruppen: Assistent zum Hinzufügen von Replikaten)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard?view=sql-server-ver15) .

| TAB      | Kurzbeschreibung       |
| ------------------ |:-------------:|
| Replikate     | Auf dieser Registerkarte können Sie jede Instanz von SQL Server angeben, die ein sekundäres Replikat hostet. Beachten Sie, dass die Serverinstanz, mit der Sie gerade verbunden sind, das primäre Replikat hosten muss. |
| Endpunkte     | Verwenden Sie diese Registerkarte, um vorhandene Datenbankspiegelungs-Endpunkte zu überprüfen und auch, wenn dieser Endpunkt auf einer Serverinstanz fehlt, deren Dienst Konten die Windows-Authentifizierung verwenden, um den Endpunkt automatisch zu erstellen.|
| Sicherungseinstellungen | Verwenden Sie diese Registerkarte, um die Sicherungs Einstellung für die Verfügbarkeits Gruppe als Ganzes und die Sicherungs Prioritäten für die einzelnen Verfügbarkeits Replikate anzugeben.      |
| Listener     | Mithilfe dieser Registerkarte können Sie einen verfügbarkeitsgruppenlistener erstellen. Standardmäßig erstellt der Assistent keinen Listener.      |

![Replikat Details angeben](media/ad-fs-always-on/createAoAchooseReplica.png)

9. Wählen Sie auf der Seite Anfängliche Datensynchronisierung auswählen aus, wie die neuen sekundären Datenbanken erstellt und mit der Verfügbarkeitsgruppe verknüpft werden sollen. Wählen Sie eine der folgenden Optionen aus:
-   Automatisches Seeding
 - SQL Server erstellt automatisch die sekundären Replikate für jede Datenbank in der Gruppe. Das automatische Seeding erfordert, dass die Daten-und Protokolldatei Pfade auf jeder SQL Server-Instanz, die Teil der Gruppe ist, identisch sind. Verfügbar auf SQL Server 2016 (13. x) und höher. Siehe [Automatisches Initialisieren von Always on Verfügbarkeits Gruppen](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group?view=sql-server-ver15).
- Vollständige Datenbank-und Protokoll Sicherung
 - Wählen Sie diese Option aus, wenn Ihre Umgebung die Anforderungen zum automatischen Starten der anfänglichen Datensynchronisierung erfüllt (Weitere Informationen finden Sie unter [Voraussetzungen, Einschränkungen und Empfehlungen weiter oben in diesem Thema)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio?view=sql-server-ver15#Prerequisites).
Wenn Sie Vollständig auswählen, werden vom Assistenten nach der Erstellung der Verfügbarkeitsgruppe alle primären Datenbanken und ihre Transaktionsprotokolle auf einer Netzwerkfreigabe gesichert und die Sicherungen auf allen Serverinstanzen wiederhergestellt, die ein sekundäres Replikat hosten. Anschließend wird jede sekundäre Datenbank mit der Verfügbarkeits Gruppe verknüpft.
Legen Sie im Feld zum Angeben eines freigegebenen Netzwerkspeicherorts, auf den von allen Replikaten zugegriffen werden kann, eine Sicherungsfreigabe fest, für die alle Serverinstanzen, die Replikate hosten, Lese-/Schreibzugriff besitzen. Weitere Informationen finden Sie weiter oben in diesem Thema unter Voraussetzungen. Im Überprüfungs Schritt führt der Assistent einen Test aus, um sicherzustellen, dass der angegebene Netzwerkort gültig ist. der Test erstellt eine Datenbank auf dem primären Replikat mit dem Namen "BackupLocDb_" gefolgt von einer GUID und führt eine Sicherung am angegebenen Netzwerkort aus und stellt Sie dann auf den sekundären Replikaten wieder her. Es ist sicher, diese Datenbank zusammen mit dem Sicherungs Verlauf und der Sicherungsdatei zu löschen, falls Sie vom Assistenten nicht gelöscht werden konnte.
- Nur verknüpfen
 - Wenn Sie sekundäre Datenbanken auf den Server Instanzen, die die sekundären Replikate hosten werden, manuell vorbereitet haben, können Sie diese Option auswählen. Der Assistent verknüpft die vorhandenen sekundären Datenbanken mit der Verfügbarkeits Gruppe.
- Ursprüngliche Datensynchronisierung überspringen
 - Wählen Sie diese Option aus, wenn Sie eigene Datenbank-und Protokoll Sicherungen der primären Datenbanken verwenden möchten. Weitere Informationen finden Sie unter [Start Data Movement on a Always on secondary Database (SQL Server)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server?view=sql-server-ver15).

![Option "Datensynchronisierung auswählen"](media/ad-fs-always-on/createAoADataSync.png)

9.  Auf der Seite Überprüfung wird überprüft, ob die in diesem Assistenten angegebenen Werte die Anforderungen des Assistenten für neue Verfügbarkeitsgruppen erfüllen. Um eine Änderung vorzunehmen, klicken Sie auf Zurück, um zu einer vorherigen Assistentenseite zurückzukehren und Werte zu ändern. Klicken Sie anschließend auf Weiter, um auf die Seite Überprüfung zurückzukehren, und klicken Sie auf Überprüfung erneut ausführen.

10. Überprüfen Sie auf der Seite Zusammenfassung die Optionen für die neue Verfügbarkeitsgruppe. Um eine Änderung vorzunehmen, klicken Sie auf Zurück, um zu der relevanten Seite zurückzukehren. Nachdem Sie die Änderung vorgenommen haben, klicken Sie auf Weiter, um zur Seite Zusammenfassung zurückzukehren.

> [!NOTE] 
> Wenn das SQL Server-Dienst Konto einer Server Instanz, die ein neues Verfügbarkeits Replikat hostet, noch nicht als Anmelde Name vorhanden ist, muss der Anmelde Name vom Assistenten für neue Verfügbarkeits Gruppen erstellt werden. Auf der Seite Zusammenfassung des Assistenten werden die Informationen für den zu erstellenden Anmeldenamen angezeigt. Wenn Sie auf Fertig stellen klicken, erstellt der Assistent diesen Anmeldenamen für das SQL Server-Dienstkonto und erteilt ihm die CONNECT-Berechtigung.
> Wenn Sie mit der Auswahl zufrieden sind, können Sie optional auf Skript klicken, um ein Skript der Schritte zu erstellen, die der Assistent ausführt. Klicken Sie dann zum Erstellen und Konfigurieren der neuen Verfügbarkeitsgruppe auf Fertig stellen.

11. Auf der Seite Status wird der Status der Schritte zum Erstellen der Verfügbarkeitsgruppe angezeigt (Konfigurieren von Endpunkten, Erstellen der Verfügbarkeitsgruppe und Hinzufügen des sekundären Replikats zu der Gruppe).
12. Wenn diese Schritte abgeschlossen sind, wird auf der Seite Ergebnisse das Ergebnis der einzelnen Schritte angezeigt. Wenn alle diese Schritte erfolgreich ausgeführt wurden, wird die neue Verfügbarkeits Gruppe vollständig konfiguriert. Wenn einer der Schritte zu einem Fehler führt, müssen Sie die Konfiguration möglicherweise manuell ausführen oder einen Assistenten für den fehlerhaften Schritt verwenden. Klicken Sie in der Spalte Ergebnis auf den zugehörigen Fehlerlink, um weitere Informationen zur Ursache eines bestimmten Fehlers zu erhalten.
Klicken Sie nach Abschluss des Assistenten auf Schließen, um den Assistenten zu beenden.

![Validierung ist beendet](media/ad-fs-always-on/createAoAValidation.png)

## <a name="add-databases-on-secondary-node"></a>Datenbanken auf Sekundär Knoten hinzufügen

1.  Stellen Sie die artefaktdatenbank über die Benutzeroberfläche auf dem sekundären Knoten mithilfe der erstellten Sicherungsdateien wieder her.
![Wiederherstellung über die Benutzeroberfläche](media/ad-fs-always-on/restoreDB.png)

2. Stellen Sie die Datenbank im Zustand "nicht wieder hergestellt" wieder her.
![Restore with Non Recovery](media/ad-fs-always-on/restoreNonRecovery.png)

3. Wiederholen Sie den Prozess zum Wiederherstellen der Konfigurations Datenbank.

## <a name="join-availability-replica-to-an-availability-group"></a>Verknüpfen eines Verfügbarkeits Replikats mit einer Verfügbarkeits Gruppe

1.  Stellen Sie in Objekt-Explorer eine Verbindung mit der Serverinstanz her, auf der das sekundäre Replikat gehostet wird, und klicken Sie auf den Servernamen, um die Serverstruktur
2.  Erweitern Sie den Knoten Always on Hochverfügbarkeit und den Knoten Verfügbarkeits Gruppen.
3.  Wählen Sie die Verfügbarkeits Gruppe des sekundären Replikats aus, mit dem Sie verbunden sind.
4.  Klicken Sie mit der rechten Maustaste auf das sekundäre Replikat, und klicken Sie auf Verfügbarkeitsgruppe beitreten.
5.  Das Dialogfeld Replikat mit Verfügbarkeitsgruppe verknüpfen wird geöffnet.
6.  Klicken Sie auf OK, um das sekundäre Replikat mit der Verfügbarkeitsgruppe zu verknüpfen.

![sekundäre Replikat verknüpfen](media/ad-fs-always-on/jointoAoA.png)

## <a name="update-the-sql-connection-string"></a>Aktualisieren der SQL-Verbindungs Zeichenfolge
Verwenden Sie abschließend PowerShell zum Bearbeiten der AD FS Eigenschaften, um die SQL-Verbindungs Zeichenfolge so zu aktualisieren, dass Sie die DNS-Adresse des Listener der AlwaysOn-Verfügbarkeits Gruppe verwendet.
Führen Sie die Änderung der Konfigurations Datenbank auf jedem Knoten aus, und starten Sie den ADFS-Dienst auf allen AD FS-Knoten neu. Der anfängliche Katalogwert ändert sich basierend auf der Farm Version.

```
PS:\>$temp= Get-WmiObject -namespace root/ADFS -class SecurityTokenService
PS:\>$temp.ConfigurationdatabaseConnectionstring=”data source=<SQLCluster\SQLInstance>; initial catalog=adfsconfiguration;integrated security=true”
PS:\>$temp.put()
PS:\> Set-AdfsProperties –artifactdbconnection ”Data source=<SQLCluster\SQLInstance >;Initial Catalog=AdfsArtifactStore;Integrated Security=True”
```
