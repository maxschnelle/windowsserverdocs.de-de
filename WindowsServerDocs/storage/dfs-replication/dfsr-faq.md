---
Title: 'DFS-Replikation: Häufig gestellte Fragen'
ms.date: 06/18/2014
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 00bb3dfd79096e28f9752053152571ea9919edcf
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284266"
---
# <a name="dfs-replication-frequently-asked-questions-faq"></a>DFS-Replikation: Häufig gestellte Fragen


Aktualisiert: 30 April 2019

Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Diese häufig gestellten Fragen beantwortet Fragen zur Distributed File System (DFS)-Replikation (auch bekannt als DFS-R oder DFSR) für Windows Server.

Informationen zu DFS-Namespaces finden Sie unter [DFS-Namespaces: Häufig gestellte Fragen](https://technet.microsoft.com/library/ee404780).

Informationen zu den neuerungen Neues bei DFS-Replikation finden Sie unter den folgenden Themen:

  - [DFS-Namespaces and DFS Replication Overview](https://technet.microsoft.com/library/jj127250) (unter WindowsServer 2012)  
      
  - [Neuigkeiten in Distributed File System](https://technet.microsoft.com/library/ee307957) Thema [Änderungen an der Funktionalität von Windows Server 2008 und Windows Server 2008 R2](https://technet.microsoft.com/library/dd391932)  
      
  - [Verteiltes Dateisystem](https://technet.microsoft.com/library/cc753479) Thema [Änderungen an der Funktionalität von Windows Server 2003 mit SP1 und Windows Server 2008](https://technet.microsoft.com/library/cc753208)  
      

Eine Liste der zuletzt vorgenommenen Änderungen an diesem Thema finden Sie im Abschnitt [Änderungsverlauf](#change-history) dieses Themas.

      

## <a name="interoperability"></a>Interoperabilität

### <a name="can-dfs-replication-communicate-with-frs"></a>Werden DFS-Replikation kann mit dem Dateireplikationsdienst (FRS) kommunizieren?

Nein. DFS-Replikation kommuniziert nicht mit der Windows-Verwaltungsinstrumentation (File Replication Service, FRS). DFS-Replikation und Dateireplikationsdienst (FRS) können gleichzeitig auf demselben Server ausführen, aber sie müssen nie um die gleichen Ordner oder Unterordner repliziert werden, da dies Datenverlust führen kann konfiguriert werden.

### <a name="can-dfs-replication-replace-frs-for-sysvol-replication"></a>Die DFS-Replikation kann für SYSVOL-Replikation Dateireplikationsdienst (FRS) ersetzen

Ja, können die DFS-Replikation Dateireplikationsdienst (FRS) für die Replikation von SYSVOL auf Servern unter Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ersetzen. Servern, die mit Windows Server 2003 R2 wird nicht unterstützt, mithilfe von DFS-Replikation zum Replizieren von SYSVOL-Ordners.

Weitere Informationen über die Replikation von SYSVOL mit DFS-Replikation finden Sie unter den [Anleitung zur SYSVOL-Replikationsmigration: FRS-zu DFS-Replikation](https://technet.microsoft.com/library/dd640019).

### <a name="can-i-upgrade-from-frs-to-dfs-replication-without-losing-configuration-settings"></a>Kann ich von der FRS-zur DFS-Replikation aktualisieren ohne Verlust von Konfigurationseinstellungen?

Ja. Um die Replikation von der FRS-zur DFS-Replikation zu migrieren, finden Sie in den folgenden Dokumenten:

  - Um die Replikation von Ordnern als dem SYSVOL-Ordner zu migrieren, finden Sie unter [DFS-Betriebshandbuch: Migration von der FRS-zur DFS-Replikation](http://go.microsoft.com/fwlink/?linkid=192776) und [FRS2DFSR – ein FRS-zu DFS-Migrationsdienstprogramm](http://go.microsoft.com/fwlink/?linkid=195437) (http://go.microsoft.com/fwlink/?LinkID=195437).  
      
  - Um die Replikation von SYSVOL-Ordners zur DFS-Replikation zu migrieren, finden Sie unter [Anleitung zur SYSVOL-Replikationsmigration: FRS-zu DFS-Replikation](https://technet.microsoft.com/library/dd640019).  
      

### <a name="can-i-use-dfs-replication-in-a-mixed-windowsunix-environment"></a>Kann ich die DFS-Replikation in einer gemischten Windows/UNIX-Umgebung verwenden?

Ja. Obwohl DFS-Replikation nur Replizieren von Inhalten zwischen Servern mit Windows Server unterstützt, können die UNIX-Clients Dateifreigaben auf den Windows-Servern zugreifen. Hierzu installieren Sie Dienste für Network File Systems (NFS) auf dem Server für die DFS-Replikation.

Sie können auch die SMB/CIFS-Clientfunktion, die in vielen UNIX-Clients direkt zugreifen, die die Windows-Dateifreigaben, obwohl diese Funktionalität oft begrenzt sein oder Änderungen an der Windows-Umgebung (z. B. das Deaktivieren von mithilfe von SMB-Signaturen erfordert, enthalten Die Gruppenrichtlinie).

DFS-Replikation interagiert mit NFS auf einem Server mit einem Windows-Betriebssystem, aber eine NFS-Bereitstellungspunkt können nicht repliziert werden.

### <a name="can-i-use-the-volume-shadow-copy-service-with-dfs-replication"></a>Kann ich den Volumeschattenkopie-Dienst mit DFS-Replikation verwenden?

Ja. DFS-Replikation wird auf Volumes mit Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) unterstützt, und frühere Momentaufnahmen mit dem Client mit vorherigen Versionen wurde erfolgreich wiederhergestellt werden können.

### <a name="can-i-use-windowsbackup-ntbackupexe-to-remotely-back-up-a-replicated-folder"></a>Kann ich Windows Backup (Ntbackup.exe) verwenden, Remote, um zu einem replizierten Ordner sichern?

Nein, wird mithilfe von Windows Backup (Ntbackup.exe) auf einem Computer unter Windows Server 2003 oder früher So sichern Sie den Inhalt eines replizierten Ordners auf einem Computer unter Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 nicht unterstützt.

Verwenden Sie Windows Server-Sicherung oder Microsoft® System Center Data Protection Manager, um Dateien zu sichern, die in einem replizierten Ordner gespeichert sind. Weitere Informationen zu Sicherungs- und Wiederherstellungsfunktionalität in Windows Server 2008 R2 und Windows Server 2008, finden Sie unter [Sicherung und Wiederherstellung](https://technet.microsoft.com/library/Cc754097). Weitere Informationen finden Sie unter [System Center Data Protection Manager](http://go.microsoft.com/fwlink/?linkid=182261) (http://go.microsoft.com/fwlink/?LinkId=182261).

### <a name="do-file-system-policies-impact-dfs-replication"></a>Wirken sich die Richtlinien für das Dateisystem auf DFS-Replikation aus?

Ja. Konfigurieren Sie Richtlinien für das Dateisystem nicht für replizierte Ordner. Die Dateirichtlinie für das System wendet die NTFS-Berechtigungen auf alle Gruppenrichtlinien-Aktualisierungsintervall erneut an. Dies kann dazu führen freigabeverletzungen, da eine geöffnete Datei nicht repliziert werden, bis die Datei geschlossen wird.

### <a name="does-dfs-replication-replicate-mailboxes-hosted-on-microsoft-exchange-server"></a>Repliziert die DFS-Replikation Postfächer, die auf Microsoft Exchange Server gehostet?

Nein. DFS-Replikation kann nicht verwendet werden, repliziert der Postfächer, die auf Microsoft Exchange Server gehostet wird.

### <a name="does-dfs-replication-support-file-screens-created-by-file-server-resource-manager"></a>Unterstützt DFS-Replikation dateiprüfungen erstellt durch File Server Resource Manager?

Ja. Allerdings muss die screening-Einstellungen (File Server Resource Manager, FSRM)-Datei auf beiden Seiten der Replikation übereinstimmen. DFS-Replikation hat außerdem einen eigenen Filtermechanismus für Dateien und Ordner, die Sie verwenden können, um bestimmte Dateien und Dateitypen von der Replikation auszuschließen.

Es folgen bewährte Methoden für die Implementierung von dateiprüfungen oder Kontingente:

  - Die ausgeblendete Ordner DfsrPrivate darf nicht gelten Kontingente oder dateiprüfungen sein.  
      
  - Überprüfte Dateien müssen in einem replizierten Ordner nicht vorhanden, vor die Screening aktiviert ist.  
      
  - Keine Ordner möglicherweise das Kontingent überschreiten, bevor das Kontingent aktiviert wird.  
      
  - Sie müssen die festen Kontingente mit Vorsicht verwenden. Es ist möglich, für einzelne Mitglieder einer Replikationsgruppe innerhalb eines Kontingents vor der Replikation zu bleiben, aber die überschritten werden, wenn Dateien repliziert werden. Z. B. wenn ein Benutzer eine 10 Megabyte (MB)-Datei auf Server A (die Sie dann auf die harte Grenze) kopiert, und ein anderer Benutzer kopiert eine 5 MB-Datei auf Server B aus, bei die nächste Replikation, überschreiten beide Server das Kontingent von 5 MB. Dies kann dazu führen, dass die DFS-Replikation kontinuierlich wiederholt Replizieren der Dateien, die Lücken in den Versionsvektor und mögliche Leistungsprobleme verursachen.  
      

### <a name="is-dfs-replication-cluster-aware"></a>Beachtet die DFS-Replikation-Cluster?

Ja, umfasst die DFS-Replikation unter Windows Server 2012 R2, Windows Server 2012 und Windows Server 2008 R2 die Möglichkeit, einen Failovercluster als Mitglied einer Replikationsgruppe hinzuzufügen. Weitere Informationen finden Sie unter [Hinzufügen eines Failoverclusters zu einer Replikationsgruppe](http://go.microsoft.com/fwlink/?linkid=155085) (http://go.microsoft.com/fwlink/?LinkId=155085). Der DFS-Replikationsdienst in Versionen von Windows vor Windows Server 2008 R2 dient nicht zur Koordinierung mit einem Failovercluster, und der Dienst wird nicht ein Failover auf einen anderen Knoten.


> [!NOTE]
> DFS-Replikation unterstützt keine Replikation Dateien auf freigegebenen Clustervolumes. 
<br>


### <a name="is-dfs-replication-compatible-with-data-deduplication"></a>Ist DFS-Replikation wird mit der Datendeduplizierung kompatibel?

Ja, können die DFS-Replikation Ordnern auf Datenträgern replizieren, die die Datendeduplizierung in Windows Server verwenden.

### <a name="is-dfs-replication-compatible-with-ris-and-wds"></a>Ist Sie DFS-Replikation mit RIS und WDS kompatibel?

Ja. DFS-Replikation repliziert Volumes, die für die Single Instance Storage (SIS) aktiviert ist. SIS wird durch Remoteinstallationsdienste (RIS), Windows-Verwaltungsinstrumentation (Windows Deployment Services, WDS) und Windows Storage Server verwendet.

### <a name="is-it-possible-to-use-dfs-replication-with-offline-files"></a>Ist es möglich, die DFS-Replikation mit Offlinedateien verwenden?

Sie können bedenkenlos einsetzen DFS-Replikation und Offlinedateien zusammen in Szenarien bei nur einem Benutzer zu einem Zeitpunkt, zu den Dateien schreibt. Dies ist nützlich für Benutzer, die zwischen zwei Filialen übertragen und möchten, können Zugriff auf ihre Dateien auf jeden Branch oder während offline. Offlinedateien speichert die Dateien lokal für die Offlineverwendung und DFS-Replikation repliziert die Daten zwischen jede Zweigstelle.

Verwenden Sie nicht die DFS-Replikation mit Offlinedateien in einer mehrbenutzerumgebung da DFS-Replikation keine verteilten Mechanismus zum Sperren oder die Datei Auschecken-Funktion bietet. Wenn zwei Benutzer die gleiche Datei zur gleichen Zeit auf verschiedenen Servern ändern, verschiebt DFS-Replikation die ältere Datei, in der DfsrPrivate\\ConflictandDeleted-Ordner (befindet sich unter dem lokalen Pfad des replizierten Ordners) während der nächsten Replikation.

### <a name="what-antivirus-applications-are-compatible-with-dfs-replication"></a>Welche Antiviren-Anwendungen mit DFS-Replikation kompatibel sind?

Antivirus-Anwendungen können übermäßige Replikation führen, wenn die Überprüfungen Aktivitäten, die Dateien in einem replizierten Ordner ändern. Weitere Informationen [Testen von Antivirus-Anwendungsinteroperabilität mit DFS-Replikation](http://go.microsoft.com/fwlink/?linkid=73990) (http://go.microsoft.com/fwlink/?LinkId=73990).

### <a name="what-are-the-benefits-of-using-dfs-replication-instead-of-windows-sharepoint-services"></a>Was sind die Vorteile der Verwendung von DFS-Replikation anstelle von Windows SharePoint Services?

Windows® SharePoint® Services bietet eine enge Kohärenz in Form von Datei Auschecken Funktionalität, die DFS-Replikation nicht der Fall ist. Wenn Sie Bedenken bezüglich eines mehrere Personen, die die gleiche Datei zu bearbeiten sind, empfehlen wir die Verwendung von Windows SharePoint Services. Windows SharePoint Services 2.0 mit Service Pack 2 finden Sie im Rahmen von Windows Server 2003 R2. Windows SharePoint Services können von der Microsoft-Website heruntergeladen werden. Es ist nicht in neueren Versionen von Windows Server enthalten. Wenn Sie Daten über mehrere Standorte repliziert werden, und Benutzer werden nicht die gleichen Dateien zur gleichen Zeit bearbeiten, bietet die DFS-Replikation jedoch mehr Bandbreite und einfachere Verwaltung.

## <a name="limitations-and-requirements"></a>Einschränkungen und Anforderungen

### <a name="can-dfs-replication-replicate-between-branch-offices-without-a-vpn-connection"></a>Werden DFS-Replikation zwischen Zweigstellen ohne eine VPN-Verbindung können repliziert?

Ja – vorausgesetzt, dass ein private Wide Area Network (WAN) Link (nicht über das Internet), das Herstellen einer Verbindung die Zweigstellen besteht. Allerdings müssen Sie die richtigen Ports in externe Firewalls öffnen. DFS-Replikation verwendet den RPC-Endpunktzuordnung (Port 135) und einen zufällig zugewiesenen kurzlebigen Port über 1024. Sie können die **Dfsrdiag** -Befehlszeilentool, um einen statischen Port anstelle der kurzlebigen Port anzugeben. Weitere Informationen zur Vorgehensweise beim Angeben der RPC-Endpunktzuordnung finden Sie unter [Artikel 154596](http://go.microsoft.com/fwlink/?linkid=73991) in der Microsoft Knowledge Base (http://go.microsoft.com/fwlink/?LinkId=73991).

### <a name="can-dfs-replication-replicate-files-encrypted-with-the-encrypting-file-system"></a>Werden DFS-Replikation mit EFS verschlüsselte Dateien können repliziert?

Nein. DFS-Replikation wird nicht repliziert, Dateien oder Ordnern, die mit der Encrypting File System (EFS) verschlüsselt werden. Wenn ein Benutzer eine Datei, die zuvor repliziert wurde verschlüsselt, löscht der DFS-Replikation die Datei von allen anderen Mitgliedern der Replikationsgruppe. Dadurch wird sichergestellt, dass die einzige verfügbare Kopie der Datei, die verschlüsselte Version auf dem Server ist.

### <a name="can-dfs-replication-replicate-outlook-pst-or-microsoft-office-access-database-files"></a>Werden DFS-Replikation können Outlook PST oder Microsoft Office Access-Datenbankdateien repliziert?

DFS-Replikation können problemlos replizieren (Microsoft Outlook Persönliche Ordnerdateien PST) und Microsoft Access-Dateien nur dann, wenn zu Archivierungszwecken gespeichert sind, und nicht über das Netzwerk erfolgt mit einem Client wie Outlook oder Zugriff (PST- oder Access öffnen Dateien zuerst kopieren die Dateien auf einem Gerät des lokalen Speichers). Die Gründe hierfür lauten wie folgt aus:

  - Öffnen von PST-Dateien über Netzwerkverbindungen kann zur Beschädigung von Daten in PST-Dateien führen. Weitere Informationen dazu, warum PST-Dateien sicher aus über ein Netzwerk zugegriffen werden können, finden Sie unter [Artikel 297019](http://go.microsoft.com/fwlink/?linkid=125363) in der Microsoft Knowledge Base (http://go.microsoft.com/fwlink/?LinkId=125363).  
      
  - PST-Datei und den Zugriff auf Dateien meist für längere Zeit beim Zugriff auf einen Client wie Outlook oder Office Access geöffnet bleibt. Dadurch wird verhindert, dass die DFS-Replikation replizieren diese Dateien aus, bis sie geschlossen werden.  
      

### <a name="can-i-use-dfs-replication-in-a-workgroup"></a>Kann ich die DFS-Replikation in einer Arbeitsgruppe verwenden?

Nein. DFS-Replikation, abhängig von Active Directory® Domain Services für die Konfiguration ab. Es funktioniert nur in einer Domäne.

### <a name="can-more-than-one-folder-be-replicated-on-a-single-server"></a>Kann mehr als einen Ordner auf einem einzelnen Server werden repliziert?

Ja. DFS-Replikation können zahlreiche Ordner zwischen Servern replizieren. Sicherstellen, dass jeden replizierten Ordner einen eindeutigen verfügt root-Pfad und der, dass Sie sich nicht überlappen. Z. B. "d:"\\für Vertrieb und "d:"\\Buchhaltung möglich die Stammpfade für zwei replizierte Ordner, aber "d:"\\für Vertrieb und "d:"\\Sales\\Berichte nicht die Stammpfade für zwei replizierten Ordner.

### <a name="does-dfs-replication-require-dfs-namespaces"></a>Ist die DFS-Replikation, DFS-Namespaces erforderlich?

Nein. DFS-Replikation und DFS-Namespaces können separat oder zusammen verwendet werden. Darüber hinaus die DFS-Replikation dient auch zum eigenständigen DFS-Namespaces zu replizieren, was nicht mit den Dateireplikationsdienst.

### <a name="does-dfs-replication-require-time-synchronization-between-servers"></a>Ist der zeitsynchronisierung zwischen Servern für DFS-Replikation erforderlich?

Nein. DFS-Replikation erfordert explizit keine Synchronisierung zwischen Servern. DFS-Replikation erfordert jedoch, dass die Uhren genau übereinstimmen. Die Uhren müssen innerhalb von fünf Minuten voneinander abweichen (standardmäßig) für Kerberos-Authentifizierung ordnungsgemäß festgelegt werden. DFS-Replikation verwendet z. B. Zeitstempel, um zu bestimmen, welche Datei im Falle von Widersprüchen Vorrang. Genau wie oft sind auch wichtig für die automatische speicherbereinigung, Zeitpläne und andere Funktionen.

### <a name="does-dfs-replication-support-replicating-an-entire-volume"></a>Unterstützt DFS-Replikation ein ganzes Volume replizieren?

Ja. Allerdings müssen Sie zuerst Windows Server 2003 Service Pack 2 oder den Hotfix installieren. Weitere Informationen finden Sie unter [Artikel 920335](http://go.microsoft.com/fwlink/?linkid=76776) in der Microsoft Knowledge Base (http://go.microsoft.com/fwlink/?LinkId=76776). Darüber hinaus kann ein ganzes Volume Replikation die folgenden Probleme verursachen:

  - Wenn das Volume auf eine Windows-Auslagerungsdatei enthält, werden Replikation ein Fehler auftritt und 4312 DFSR-Ereignis im Systemereignisprotokoll protokolliert.  
      
  - DFS-Replikation wird das System "und" Hidden-Attribut für den replizierten Ordner auf den Ziel-Servern. Dies tritt auf, da Windows das System "und" Hidden-Attribut in den Stammordner des Volume in der Standardeinstellung gilt. Wenn der lokale Pfad des replizierten Ordners auf den Ziel-Servern auch Stamm eines Volumes ist, erfolgen keine weiteren Änderungen für die Ordnerattribute.  
      
  - Bei der Replikation von einem Volume, das die Windows-Systemordner enthält, werden DFS-Replikation erkennt der Ordner % WINDIR % und werden nicht repliziert. DFS-Replikation werden jedoch von Microsoft-fremden Anwendungen, die die Anwendungen nicht auf den Ziel-Servern verursachen kann, wenn die Anwendungen Interoperabilitätsprobleme mit DFS-Replikation verwendeten Ordner repliziert.  
      

### <a name="does-dfs-replication-support-rpc-over-http"></a>Unterstützt DFS-Replikation RPC über HTTP?

Nein.

### <a name="does-dfs-replication-work-across-wireless-networks"></a>Funktioniert die DFS-Replikation in drahtlosen Netzwerken?

Ja. DFS-Replikation ist unabhängig von den Verbindungstyp.

### <a name="does-dfs-replication-work-on-refs-or-fat-volumes"></a>Funktioniert die DFS-Replikation unter ReFS oder FAT-Volumes?

Nein. DFS-Replikation unterstützt nur das NTFS-Dateisystem formatierte Volumes. das robuste Dateisystem (ReFS) und das FAT-Dateisystem werden nicht unterstützt. DFS-Replikation ist NTFS erforderlich, da er das Änderungsjournal NTFS verwendet und andere Funktionen des NTFS-Dateisystem.

### <a name="does-dfs-replication-work-with-sparse-files"></a>Funktioniert die DFS-Replikation mit Dateien mit geringer Dichte?

Ja. Sie können Dateien mit geringer Dichte replizieren. Die **Sparse** Attribut wird auf dem empfangenden Mitglied beibehalten.

### <a name="do-i-need-to-log-in-as-administrator-to-replicate-files"></a>Muss ich für die Anmeldung als Administrator, um Dateien zu replizieren?

Nein. DFS-Replikation ist ein Dienst, der unter dem Konto Lokales System ausgeführt wird, benötigen Sie nicht für die Anmeldung als Administrator, um zu replizieren. Allerdings müssen Sie ein Domänenadministrator oder lokale Administratorrechte für die betroffenen Dateiserver, um Änderungen an der Konfiguration der DFS-Replikation vorzunehmen sein.

Weitere Informationen finden Sie unter "sicherheitsanforderungen für die DFS-Replikation und Delegierung" in der [Delegieren der Fähigkeit zum Verwalten von DFS-Replikation](http://go.microsoft.com/fwlink/?linkid=182294) (http://go.microsoft.com/fwlink/?LinkId=182294).

### <a name="how-can-i-upgrade-or-replace-a-dfs-replication-member"></a>Wie kann ich ein upgrade oder ersetzt ein Element der DFS-Replikation?

Zum Aktualisieren oder ersetzen Mitglied DFS-Replikation finden Sie unter diesem Blog auf die Fragen der Directory Services Team-Blog-Beitrag: [Ersetzen DFSR Member Hardware or OS](http://blogs.technet.com/b/askds/archive/2010/09/10/series-wrap-up-and-downloads-replacing-dfsr-member-hardware-or-os.aspx).

### <a name="is-dfs-replication-suitable-for-replicating-roaming-profiles"></a>Eignet DFS-Replikation zum Replizieren von servergespeicherter Profiles?

Ja. Bestimmte Szenarien werden unterstützt, wenn servergespeicherte Benutzerprofile replizieren. Weitere Informationen zu den unterstützten Szenarien finden Sie unter [von Microsoft Support-Anweisung um repliziert Benutzerprofildaten](http://go.microsoft.com/fwlink/?linkid=201282) (http://go.microsoft.com/fwlink/?LinkId=201282).

### <a name="is-there-a-file-character-limit-or-limit-to-the-folder-depth"></a>Gibt es eine zeichenbeschränkung von Datei oder die Beschränkung der Ordnertiefe?

Windows und DFS-Replikation unterstützt Ordnerpfade mit bis zu 32 Tausend Zeichen auf. DFS-Replikation ist nicht auf Ordnerpfaden 260 Zeichen beschränkt.

### <a name="must-members-of-a-replication-group-reside-in-the-same-domain"></a>Müssen Mitglied einer Replikationsgruppe in der gleichen Domäne befinden?

Nein. Replikationsgruppen können zwischen Domänen innerhalb einer einzelnen Gesamtstruktur aber nicht über verschiedene Gesamtstrukturen hinweg erstrecken.

### <a name="what-are-the-supported-limits-of-dfs-replication"></a>Was sind die unterstützten Grenzwerte der DFS-Replikation?

Die folgende Liste enthält eine Reihe von Skalierbarkeitsrichtlinien, die auf Windows Server 2012 R2 von Microsoft getestet wurden:

  - Die Größe aller replizierten Dateien auf einem Server: 100 TB.  
      
  - Anzahl der replizierten Dateien auf einem Volume: mehr als 70 Millionen.  
      
  - Maximale Dateigröße: 250 GB.  
      


> [!IMPORTANT]
> Beim Erstellen von Replikationsgruppen mit einer großen Anzahl oder Größe von Dateien empfohlen, einen Datenbankklon exportieren und vorab-seeding-Verfahren verwenden, um die Dauer der ersten Replikation zu minimieren. Weitere Informationen finden Sie unter <A href="http://blogs.technet.com/b/filecab/archive/2013/08/21/dfs-replication-initial-sync-in-windows-server-2012-r2-attack-of-the-clones.aspx">DFS-Replikation anfängliche Synchronisierung in Windows Server 2012 R2: Angriff der Klonkrieger</A>. 
<br>


Die folgende Liste enthält eine Reihe von Skalierbarkeitsrichtlinien, die auf Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008 von Microsoft getestet wurden:

  - Die Größe aller replizierten Dateien auf einem Server: 10 TB.  
      
  - Anzahl der replizierten Dateien auf einem Volume: 11 Millionen.  
      
  - Maximale Dateigröße: 64 GB.  
      


> [!NOTE]
> Es ist nicht mehr begrenzt die Anzahl der Replikationsgruppen, replizierte Ordner, Verbindungen oder Mitgliedern der Replikationsgruppe. 
<br>


Eine Liste der Skalierbarkeitsrichtlinien, die von Microsoft für Windows Server 2003 R2 getestet wurden, finden Sie unter [DFS-Replikation Skalierbarkeitsrichtlinien](http://go.microsoft.com/fwlink/?linkid=75043) (http://go.microsoft.com/fwlink/?LinkId=75043).

### <a name="when-should-i-not-use-dfs-replication"></a>Wann sollte ich DFS-Replikation nicht verwenden?

Verwenden Sie die DFS-Replikation nicht in einer Umgebung, in denen mehrere Benutzer zu aktualisieren oder ändern Sie die gleichen Dateien auf verschiedenen Servern gleichzeitig. Auf diese Weise kann dazu führen, dass DFS-Replikation in Konflikt stehende Kopien der Dateien in den verborgenen DfsrPrivate verschieben\\ConflictandDeleted-Ordner.

Wenn mehrere Benutzer die gleichen Dateien zur gleichen Zeit auf verschiedenen Servern ändern müssen, verwenden Sie die Datei Auschecken-Funktion von Windows SharePoint Services, stellen Sie sicher, dass nur ein Benutzer auf eine Datei ausgeführt wird. Windows SharePoint Services 2.0 mit Service Pack 2 finden Sie im Rahmen von Windows Server 2003 R2. Windows SharePoint Services können von der Microsoft-Website heruntergeladen werden. Es ist nicht in neueren Versionen von Windows Server enthalten.

### <a name="why-is-a-schema-update-required-for-dfs-replication"></a>Warum ist eine schemaaktualisierung für die DFS-Replikation erforderlich?

DFS-Replikation verwendet neue Objekte in Domänen-Namenskontext des Active Directory Domain Services, um Konfigurationsinformationen zu speichern. Diese Objekte werden erstellt, wenn Sie das Schema der Active Directory-Domänendienste aktualisieren. Weitere Informationen finden Sie unter [Überprüfen von Anforderungen für DFS-Replikation](http://go.microsoft.com/fwlink/?linkid=182264) (http://go.microsoft.com/fwlink/?LinkId=182264).

## <a name="monitoring-and-management-tools"></a>Überwachungs- und Verwaltungstools

### <a name="can-i-automate-the-health-report-to-receive-warnings"></a>Kann ich den Integritätsbericht zum Empfangen von Warnungen automatisieren?

Ja. Es gibt drei Möglichkeiten, um Integritätsberichte zu automatisieren:

  - Verwenden Sie das DFSR Windows PowerShell-Modul in Windows Server 2012 R2 oder DfsrAdmin.exe in Verbindung mit geplanten Tasks enthalten, um Integritätsberichte regelmäßig zu generieren. Weitere Informationen finden Sie unter [Automatisieren von DFS-Replikation-Integritätsberichte](http://go.microsoft.com/fwlink/?linkid=74010) (http://go.microsoft.com/fwlink/?LinkId=74010).  
      
  - Verwenden Sie die DFS-Replikation Management Pack für System Center Operations Manager zum Erstellen von Warnungen, die auf den angegebenen Bedingungen basieren.  
      
  - Verwenden Sie die WMI-Anbieter, um Skripts für Warnungen.  
      

### <a name="can-i-use-microsoft-system-center-operations-manager-to-monitor-dfs-replication"></a>Kann ich Microsoft System Center Operations Manager zum Überwachen von DFS-Replikation verwenden?

Ja. Weitere Informationen finden Sie unter den [DFS Replication-Management Pack für System Center Operations Manager 2007](http://go.microsoft.com/fwlink/?linkid=182265) im Microsoft Download Center (http://go.microsoft.com/fwlink/?LinkId=182265).

### <a name="does-dfs-replication-support-remote-management"></a>Werden die Remoteverwaltung von DFS-Replikation unterstützt?

Ja. DFS-Replikation unterstützt die Remoteverwaltung, die mithilfe der DFS-Verwaltungskonsole und die **Replikationsgruppe hinzufügen** Befehl. Auf Server A, können Sie z. B. zu einer Replikationsgruppe in der Gesamtstruktur mit Server A und B als Member definiert verbinden.

DFS-Verwaltung ist im Lieferumfang von Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 und Windows Server 2003 R2. Um die DFS-Replikation aus anderen Versionen von Windows zu verwalten, verwenden Sie Remotedesktop oder die [Remote Server Administration Tools for Windows 7](https://technet.microsoft.com/library/Ee449475).


> [!IMPORTANT]
> Zum Anzeigen oder Verwalten von Replikationsgruppen, die schreibgeschützten replizierten Ordnern oder Elementen, die Failovercluster sind enthalten, müssen Sie die Version der DFS-Verwaltung, die mit Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, die istverwenden<a href="http://go.microsoft.com/fwlink/p/?linkid=238560">Remoteserver-Verwaltungstools für Windows 8</a>, oder die <a href="https://technet.microsoft.com/library/ee449475">Remoteserver-Verwaltungstools für Windows 7</a>. 
<br>


### <a name="do-ultrasound-and-sonar-work-with-dfs-replication"></a>Funktionieren Ultrasound und Sonar mit DFS-Replikation?

Nein. DFS-Replikation verfügt über einen eigenen Satz von Tools für die Überwachung und Diagnose. Ultrasound und Sonar sind nur FRS überwacht werden können

### <a name="how-can-files-be-recovered-from-the-conflictanddeleted-or-preexisting-folders"></a>Wie können Dateien aus den Ordnern ConflictAndDeleted oder PreExisting werden wiederhergestellt?

Zum Wiederherstellen verloren gegangener Dateien wiederherstellen der Dateien aus der Dateisystemordner oder freigegebenen Ordner mithilfe der Dateien aus dem Verlauf der **Vorgängerversionen wiederherstellen** Befehl im Datei-Explorer oder durch die Dateien aus einer Sicherung wiederherstellen. Verwenden Sie zum Wiederherstellen von Dateien direkt aus dem ConflictAndDeleted "oder" PreExisting "die `Get-DfsrPreservedFiles` und `Restore-DfsrPreservedFiles` (in der DFSR-Modul in Windows Server 2012 R2 enthalten), Windows PowerShell-Cmdlets oder die [RestoreDFSR](http://code.msdn.microsoft.com/restoredfsr) Beispielskript zum Abrufen von der MSDN Code Gallery. Dieses Skript ist nur für die Wiederherstellung im Notfall vorgesehen und wird bereitgestellt, AS-besehen und ohne GEWÄHRLEISTUNGEN.

### <a name="is-there-a-way-to-know-the-state-of-replication"></a>Gibt es eine Möglichkeit, den Status der Replikation wissen?

Ja. Es gibt eine Reihe von Möglichkeiten zur Überwachung der Replikation:

  - DFS-Replikation hat ein Management Pack für System Center Operations Manager, die proaktive Überwachung bereitstellt.  
      
  - DFS-Verwaltung ist eine integrierte Diagnosebericht für den Replikationsrückstand Replikationseffizienz und die Anzahl der Dateien und Ordner in einer bestimmten Gruppe.  
      
  - Die DFSR-Windows-PowerShell-Modul in Windows Server 2012 R2 enthält Cmdlets für die Weitergabe Tests starten und das Schreiben von Verteilung und Integritätsberichte. Weitere Informationen finden Sie unter [Distributed Datei System Replikations-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/dn296601.aspx).  
      
  - Dfsrdiag.exe ist ein Befehlszeilentool, das eine Backlog-Anzahl oder ein Trigger einen Test für die Weitergabe generieren kann. Beide zeigen den Status der Replikation. Weitergabe zeigt an, ob Dateien auf allen Knoten repliziert werden. Backlog wird gezeigt, wie viele Dateien dennoch nicht repliziert werden, bevor zwei Computer übereinstimmen. Die Anzahl der Backlog ist die Anzahl der Updates, die Mitglied einer Replikation nicht verarbeitet wurde. Auf Computern unter Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 können Dfsrdiag.exe auch die Updates anzeigen, die derzeit die DFS-Replikation repliziert wird.  
      
  - Skripts können WMI verwenden, um die Backlog-Informationen sammeln – manuell oder mithilfe von MOM.  
      

## <a name="performance"></a>Leistung

### <a name="does-dfs-replication-support-dial-up-connections"></a>Unterstützt DFS-Replikation DFÜ-Verbindungen?

Aber DFS-Replikation bei DFÜ-Geschwindigkeiten funktionieren, sie können im Rückstand erhalten treten zahlreicher Änderungen repliziert werden. Wenn Sie kleine Änderungen an vorhandenen Dateien vorgenommen werden, bieten DFS-Replikation mit Remote Differential Compression (RDC) einen wesentlich höheren Leistung als die Datei direkt kopieren.

### <a name="does-dfs-replication-perform-bandwidth-sensing"></a>Führt die DFS-Replikation die Bandbreite ermitteln?

Nein. DFS-Replikation führt keine Bandbreite zu ermitteln. Sie können DFS-Replikation, um eine begrenzte Menge an Bandbreite pro Verbindung (Drosselung der Bandbreite) zu verwenden, konfigurieren. Allerdings verringert DFS-Replikation weitere Nutzung der Netzwerkbandbreite nicht die Sättigung der Netzwerkschnittstelle aus, und die DFS-Replikation können den Link für einen kurzen Zeitraum auslasten. Für die bandbreitenbeschränkung mit DFS-Replikation ist nicht hundertprozentig genau, da es sich bei DFS-Replikation von Einschränkungen beim RPC-Aufrufe die Bandbreite drosselt. Daher können verschiedene Puffer auf niedrigeren Ebenen des Netzwerkstapels (einschließlich RPC) auswirken, verursacht der Anstieg des Netzwerkverkehrs.

### <a name="does-dfs-replication-throttle-bandwidth-per-schedule-per-server-or-per-connection"></a>Einschränken die DFS-Replikation, die Bandbreite gemäß Zeitplan, pro Server oder pro Verbindung?

Wenn Sie konfigurieren die Drosselung der Bandbreite, wenn Sie den Zeitplan angeben, werden alle Verbindungen für die Replikationsgruppe, Einstellung für die Drosselung der Bandbreite verwenden. Drosselung der Bandbreite kann auch als eine Einstellung auf Verbindungsebene, die mithilfe von DFS-Verwaltung festgelegt werden.

### <a name="does-dfs-replication-use-active-directory-domain-services-to-calculate-site-links-and-connection-costs"></a>Verwendet DFS-Replikation Active Directory Domain Services, standortverknüpfungen und die Verbindungskosten für die berechnen?

Nein. DFS-Replikation verwendet die Topologie definiert, vom Administrator, der von Active Directory Domain Services Standortkosten unabhängig ist.

### <a name="how-can-i-improve-replication-performance"></a>Wie kann ich die replikationsleistung verbessern?

Informationen zu verschiedenen Methoden der Optimierung der Leistung der Replikation finden Sie unter [Optimieren der Leistung von Replikation bei DFSR](http://blogs.technet.com/b/askds/archive/2010/03/31/tuning-replication-performance-in-dfsr-especially-on-win2008-r2.aspx) auf die [bitten Sie das Directory Services Team Blog](http://blogs.technet.com/b/askds/).

### <a name="how-does-dfs-replication-avoid-saturating-a-connection"></a>Wie komplettauslastung die DFS-Replikation eine Verbindung?

Bei der DFS-Replikation legen Sie die maximale Bandbreite, die Sie für eine Verbindung verwenden möchten, und dieser Ebene der Netzwerkverwendung, behält der Dienst. Dies unterscheidet sich von der BITS Background Intelligent Transfer Service (), und die DFS-Replikation wird die Verbindung nicht auslasten, wenn Sie sie entsprechend festlegen.

Dennoch die Drosselung der Bandbreite nicht 100 % genau und DFS-Replikation können den Link für kurze Zeit auslasten. Dies ist da DFS-Replikation von Einschränkungen beim RPC-Aufrufe die Bandbreite drosselt. Da dieser Prozess verschiedene Puffer auf niedrigeren Ebenen des Netzwerkstapels verwendet, einschließlich RPC und ist der Replikationsdatenverkehr schubweise übertragen, die gelegentlich die Netzwerkverbindungen vollständig beanspruchen kann.

DFS-Replikation unter Windows Server 2008 beinhaltet mehrere leistungsverbesserungen, siehe [Distributed File System](https://technet.microsoft.com/library/Cc753479), ein Thema in der [Änderungen an der Funktionalität von Windows Server 2003 mit SP1 und Windows Server 2008](https://technet.microsoft.com/library/cc753208).

### <a name="how-does-dfs-replication-performance-compare-with-frs"></a>Wie lässt sich die DFS-Replikation-Leistung mit dem Dateireplikationsdienst (FRS) vergleichen?

DFS-Replikation ist wesentlich schneller als Dateireplikationsdienst (FRS), insbesondere dann, wenn kleine an großen Dateien Änderungen und RDC aktiviert ist. Z. B. mit RDC, eine kleine Änderung an einer 2 MB PowerPoint®-Präsentation kann dazu führen nur 60 Kilobyte (KB), die über das Netzwerk gesendet werden – eine Einsparung von 97 Prozent in übertragenen Bytes.

RDC wird keine Dateien unter 64 KB und möglicherweise nicht auf schnelle LANs vorteilhaft, in dem die Netzwerkbandbreite nicht Konflikten. RDC kann mit der DFS-Verwaltung für pro Verbindung deaktiviert werden.

### <a name="how-frequently-does-dfs-replication-replicate-data"></a>Replizieren DFS-Replikation wie häufig Daten?

Daten werden gemäß dem festgelegten Zeitplan repliziert. Beispielsweise können Sie den Zeitplan um 15-Minuten-Intervallen, sieben Tage die Woche festlegen. Während diese Intervalle wird die Replikation aktiviert. Replikation wird gestartet, sobald eine dateiänderung, (in der Regel in Sekunden erkannt wird).

Der Replikationszeitplan für die Gruppe kann in Coordinated Universal Time koordinieren (UTC) festgelegt werden, während der Verbindungszeitplan auf der lokalen Zeit des Empfangendes Mitglied festgelegt wird. Dies berücksichtigt, wenn die Replikationsgruppe aus verschiedenen Zeitzonen umfasst. Lokale Zeit bedeutet, dass die Zeit des Elements, das die eingehende Verbindung gehostet. Der angezeigten Zeitplan der eingehenden Verbindung und die entsprechenden ausgehende Verbindung Zeitzonenunterschiede wider, wenn der Zeitplan in Ortszeit festgelegt ist.

### <a name="how-much-of-my-servers-system-resources-will-dfs-replication-consume"></a>Wie viel meines Servers Systemressourcen verbraucht die DFS-Replikation wird?

Der Datenträger, Arbeitsspeicher und CPU-Ressourcen, die von der DFS-Replikation hängt von einer Reihe von Faktoren, z.B. Anzahl und Größe der Dateien, Änderungsrate ändern, Anzahl von Mitgliedern der Replikationsgruppe und Anzahl der replizierten Ordner. Darüber hinaus sind einige Ressourcen schwieriger zu schätzen. Beispielsweise kann die Extensible Storage Engine (ESE)-Technologie, die für die Datenbank die DFS-Replikation verwendet einen großen Prozentsatz der verfügbaren Arbeitsspeicher nutzen, die sie bei Bedarf freigibt. Andere Anwendungen als DFS-Replikation können auf dem gleichen Server abhängig von der Serverkonfiguration gehostet werden. Jedoch wenn Sie mehrere Anwendungen oder Serverrollen auf einem einzelnen Server zu hosten, unbedingt müssen, dass Sie diese Konfiguration vor der Implementierung in einer produktionsumgebung testen.

### <a name="what-happens-if-a-wan-link-fails-during-replication"></a>Was geschieht, wenn eine WAN-Verbindung während der Replikation ein Fehler auftritt?

Wenn die Verbindung ausfällt, DFS-Replikation wir versuchen es weiter repliziert werden, während der Zeitplan geöffnet ist. Es werden auch Verbindungsfehler im Ereignisprotokoll DFS-Replikation, das mithilfe von MOM (proaktiv über Warnungen) und der Bericht zur Integrität von DFS-Replikation (reaktiv, z. B. wenn ein Administrator es ausgeführt wird) abgegriffen werden können.

## <a name="remote-differential-compression-details"></a>Remote Differential Compression-details

### <a name="are-changes-compressed-before-being-replicated"></a>Werden Änderungen werden komprimiert, bevor Sie repliziert werden?

Ja. Geänderte Teile der Dateien werden komprimiert, bevor Sie gesendet werden, für alle außer den folgenden Dateitypen (die bereits komprimiert sind): .wma, .wmv, ZIP-, JPG, .mpg, .mpeg,. m1v, MP2, MP3, .mpa, CAB, WAV-, .snd, .au, .asf,. WM, .avi, ...z, GZ, TGZ, und FRx. Standardeinstellungen für die Komprimierung für diese Dateitypen sind nicht konfigurierbar, in Windows Server 2003 R2.

### <a name="can-an-administrator-turn-off-rdc-or-change-the-threshold"></a>Kann ein Administrator RDC deaktivieren oder ändern den Schwellenwert?

Ja. Sie können über die Eigenschaftenseite einer bestimmten Verbindung RDC deaktivieren. Deaktivieren von RDC reduzieren CPU-Auslastung und die Replikation Latenz auf schnellen Local Area Network (LAN) Links, die keine bandbreiteneinschränkungen oder Replikationsgruppen, die in erster Linie von Dateien, die kleiner als 64 KB umfassen. Wenn Sie die Remotedifferenzialkomprimierung für eine Verbindung zu deaktivieren möchten, testen Sie die Replikationseffizienz vor und nach der Änderung aus, um sicherzustellen, dass die Leistung verbessert werden können.

Sie können die RDC-Schwellenwert für die Datenbankgröße ändern, indem Sie mit der **Dfsradmin Verbindung festgelegt** Befehl den WMI-Anbieter DFS-Replikation, oder durch manuelles Bearbeiten der Konfigurations-XML-Datei.

### <a name="does-rdc-work-on-all-file-types"></a>Werden RDC auf alle Dateitypen verwendet?

Ja. RDC berechnet die Unterschiede auf Blockebene unabhängig von der Datei-Datentyp. RDC funktioniert jedoch effizienter auf bestimmte Dateitypen wie z. B. Word-Dokumentation, PST-Dateien und VHD-Images.

### <a name="how-does-rdc-work-on-a-compressed-file"></a>Wie funktioniert die Remotedifferenzialkomprimierung für eine komprimierte Datei?

DFS-Replikation mithilfe von RDC, die die Blöcke in der Datei, die geändert wurden, und sendet über das Netzwerk nur die Blöcke, berechnet. DFS-Replikation muss nicht den Inhalt der Datei vertraut sind, nur die Blöcke geändert haben.

### <a name="is-cross-file-rdc-enabled-when-upgrading-to-windows-server-enterprise-edition-or-datacenter-edition"></a>Wird die Dateiübergreifende Remotedifferenzialkomprimierung aktiviert, wenn ein Upgrade auf Windows Server Enterprise Edition oder Datacenter Edition durchführen?

Der Standard-Editionen von Windows Server unterstützen nicht die Dateiübergreifende Remotedifferenzialkomprimierung. Allerdings wird es automatisch aktiviert, beim upgrade auf eine Edition, unterstützt die RDC Dateiübergreifende, oder wenn ein Mitglied der replikationsverbindung eine unterstützte Edition ausgeführt wird. Eine Liste der Editionen, Unterstützung RDC Dateiübergreifende finden Sie unter die Editionen der Windows-Betriebssystem-Unterstützung RDC Dateiübergreifende?

### <a name="is-rdc-true-block-level-replication"></a>Ist die RDC-Replikation für "true" auf Blockebene?

Nein. RDC ist ein allgemeiner-Protokoll für die Übertragung von Dateien komprimiert. DFS-Replikation mithilfe von RDC auf Blöcke auf Dateiebene, nicht auf der Ebene des Datenträger-Block. RDC ist eine Datei in Blöcke unterteilt. Für jeden Block in einer Datei berechnet es eine Signatur, die eine kleine Anzahl von Bytes ist, die den größeren Block darstellen kann. Der Satz von Signaturen wird vom Server zum Client übertragen. Der Client vergleicht die Signaturen Server bis zum eigenen. Der Client dann Anforderungen sendet der Server nur die Daten für Signaturen, die auf dem Client noch nicht vorhanden sind.

### <a name="what-happens-if-i-rename-a-file"></a>Was geschieht, wenn ich eine Datei umbenenne?

DFS-Replikation wird die Datei auf allen anderen Mitgliedern der Replikationsgruppe während der nächsten Replikation. Dateien sind nachverfolgte mit einer eindeutigen ID, also das Umbenennen einer Datei und verschieben, dass die Datei in das Replikat keine Auswirkungen auf die Möglichkeit der DFS-Replikation zum Replizieren einer Datei hat.

### <a name="what-is-cross-file-rdc"></a>Was ist die Dateiübergreifende Remotedifferenzialkomprimierung?

Die Dateiübergreifende Remotedifferenzialkomprimierung ermöglicht die DFS-Replikation RDC auch verwenden, wenn eine Datei mit dem gleichen Namen auf der Clientseite nicht vorhanden ist. Die Dateiübergreifende Remotedifferenzialkomprimierung wird eine Heuristik verwendet, um Dateien zu ermitteln, die in der Datei ähnlich sind, die repliziert werden muss, und verwendet Blöcke ähnlich wie Dateien, die identisch mit der Datei replizieren, um die Menge der Daten zu minimieren, die über das WAN übertragen. Die Dateiübergreifende Remotedifferenzialkomprimierung können Blöcke von bis zu fünf ähnliche Dateien in diesem Prozess.

Verwendet die Dateiübergreifende Remotedifferenzialkomprimierung, ein Mitglied der replikationsverbindung muss einer Edition von Windows, unterstützt die RDC Dateiübergreifende ausgeführt werden. Eine Liste der Editionen, Unterstützung RDC Dateiübergreifende finden Sie unter die Editionen der Windows-Betriebssystem-Unterstützung RDC Dateiübergreifende?

### <a name="what-is-rdc"></a>Was ist die RDC?

Remotedifferenzialkomprimierung (RDC) ist eine Client / Server-Protokoll, das verwendet werden kann, um Dateien über ein Netzwerk mit begrenzter Bandbreite effizient zu aktualisieren. Die Remotedifferenzialkomprimierung erkennt einfügungen, entfernungen und neuanordnungen von Daten in Dateien, aktivieren die DFS-Replikation nur die Änderungen repliziert werden, wenn Dateien aktualisiert werden. RDC wird verwendet, nur für Dateien, die 64 KB oder höher standardmäßig. RDC können eine ältere Version einer Datei mit dem gleichen Namen in den replizierten Ordner oder in der DfsrPrivate\\ConflictandDeleted-Ordner (befindet sich unter dem lokalen Pfad des replizierten Ordners).

### <a name="when-is-rdc-used-for-replication"></a>Wann wird die Remotedifferenzialkomprimierung für die Replikation verwendet?

RDC wird verwendet, wenn die Datei einen Schwellenwert für die minimale Größe überschreitet. Dieser Schwellenwert für die Datenbankgröße beträgt 64 KB wird standardmäßig an. Nach eine Datei, die beim Überschreiten dieses Schwellenwerts repliziert wurde, mithilfe von aktualisierten Versionen der Datei immer RDC, es sei denn, die ein großer Teil der Datei geändert wird, oder RDC ist deaktiviert.

### <a name="which-editions-of-the-windows-operating-system-support-cross-file-rdc"></a>Welche Editionen von der Windows-Betriebssystem-Unterstützung die Dateiübergreifende Remotedifferenzialkomprimierung?

Verwendet die Dateiübergreifende Remotedifferenzialkomprimierung, ein Mitglied der replikationsverbindung muss einer Edition des Windows-Betriebssystems, unterstützt die RDC Dateiübergreifende ausgeführt werden. Die folgende Tabelle zeigt, welche Editionen von Windows-Betriebssystem unterstützen, die Dateiübergreifende Remotedifferenzialkomprimierung.

### <a name="cross-file-rdc-availability-in-editions-of-the-windows-operating-system"></a>Die Dateiübergreifende Remotedifferenzialkomprimierung-Verfügbarkeit in den Editionen des Windows-Betriebssystems

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Betriebssystemversion</th>
<th>Standard Edition</th>
<th>Enterprise</th>
<th>Datacenter Edition</th>
</tr>
</thead>
<tbody>
<tr class="even">
<td><p>Windows Server 2012 R2</p></td>
<td><p>"Ja"<em></p></td>
<td><p>Nicht verfügbar</p></td>
<td><p>Ja</em></p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012</p></td>
<td><p>Ja</p></td>
<td><p>Nicht verfügbar</p></td>
<td><p>Ja</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 R2</p></td>
<td><p>Nein</p></td>
<td><p>Ja</p></td>
<td><p>Ja</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008</p></td>
<td><p>Nein</p></td>
<td><p>Ja</p></td>
<td><p>Nein</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2003 R2</p></td>
<td><p>Nein</p></td>
<td><p>Ja</p></td>
<td><p>Nein</p></td>
</tr>
</tbody>
</table>

\* Sie können optional deaktivieren dateiübergreifenden Remotedifferenzialkomprimierung für Windows Server 2012 R2.

## <a name="replication-details"></a>Replikationsdetails

### <a name="can-i-change-the-path-for-a-replicated-folder-after-it-is-created"></a>Kann ich ändern den Pfad für einen replizierten Ordner nach der Erstellung?

Nein. Wenn Sie den Pfad eines replizierten Ordners ändern müssen, müssen Sie löschen Sie sie in der DFS-Verwaltung und fügen Sie es wieder als einen neu replizierten Ordner. DFS-Replikation verwendet (Remote Differential Compression, RDC), um eine Synchronisierung durchführen, die bestimmt, ob die Daten auf dem sendenden und empfangenden Mitgliedern identisch ist. Es werden alle Daten in den Ordner nicht erneut repliziert.

### <a name="can-i-configure-which-file-attributes-are-replicated"></a>Kann ich konfigurieren, welche Attribute der Datei repliziert werden?

Sie können nicht nicht, welche Attribute der Datei konfigurieren, die DFS-Replikation repliziert.

Eine Liste der Attributwerte und deren Beschreibungen finden Sie [Dateiattribute](http://go.microsoft.com/fwlink/?linkid=182268) auf MSDN (http://go.microsoft.com/fwlink/?LinkId=182268).

Die folgenden Attributwerte werden festgelegt, mit der `SetFileAttributes dwFileAttributes` -Funktion, und sie werden von der DFS-Replikation repliziert. Änderungen an diese Attributwerte-Replikation der Attribute an. Der Inhalt der Datei werden nicht repliziert werden, es sei denn, Sie auch den Inhalt zu ändern. Weitere Informationen finden Sie unter [SetFileAttributes Funktion](http://go.microsoft.com/fwlink/?linkid=182269) in der MSDN Library (http://go.microsoft.com/fwlink/?LinkId=182269).

  - DATEI\_ATTRIBUT\_AUSGEBLENDET  
      
  - DATEI\_ATTRIBUT\_READONLY  
      
  - DATEI\_ATTRIBUT\_SYSTEM  
      
  - DATEI\_ATTRIBUT\_NICHT\_CONTENT\_INDIZIERT  
      
  - DATEI\_ATTRIBUT\_OFFLINE  
      

Die folgenden Attributwerte werden von der DFS-Replikation repliziert, aber sie lösen keine Replikation aus.

  - DATEI\_ATTRIBUT\_ARCHIV  
      
  - DATEI\_ATTRIBUT\_– NORMAL  
      

Die folgenden Attributwerte für die Datei auch Replikation auslösen, auch wenn sie mithilfe von festgelegt werden, können nicht die `SetFileAttributes` Funktion (verwenden Sie die `GetFileAttributes` Funktion, um die Attributwerte anzeigen).

  - DATEI\_ATTRIBUT\_ABWEICHENDER\_PUNKT  
      

> [!NOTE]
> DFS-Replikation repliziert nicht Analysepunkt Punkt Attributwerte, es sei denn, die analysenkennung IO_REPARSE_TAG_SYMLINK ist. Dateien mit den IO_REPARSE_TAG_DEDUP, IO_REPARSE_TAG_SIS oder IO_REPARSE_TAG_HSM Analysepunkten-Tags werden wie normale Dateien repliziert. Allerdings werden die analysenkennung und Analyse von Datenpuffern nicht auf andere Server repliziert, da der Analysepunkt nur auf dem lokalen System funktioniert. 
<br>

  - DATEI\_ATTRIBUT\_COMPRESSED  
      
  - DATEI\_ATTRIBUT\_VERSCHLÜSSELT  
      

> [!NOTE]
> Dateien, die mithilfe der Encrypting File System (EFS) verschlüsselt sind, werden von DFS-Replikation nicht repliziert. DFS-Replikation werden Dateien repliziert, die mit nicht-Microsoft-Software, verschlüsselte, aber nur, wenn sie die Datei nicht den Wert des Attributs FILE_ATTRIBUTE_ENCRYPTED festgelegt ist. 
<br>

  - DATEI\_ATTRIBUT\_SPARSE\_DATEI  
      
  - DATEI\_ATTRIBUT\_VERZEICHNIS  
      

Die Datei wird von der DFS-Replikation nicht repliziert\_ATTRIBUT\_TEMPORÄREN Wert.

### <a name="can-i-control-which-member-is-replicated"></a>Kann ich steuern, welches Element repliziert wird?

Ja. Sie können eine Topologie auswählen, wenn Sie eine Replikationsgruppe erstellen. Oder Sie können auswählen, **keine Topologie** und Verbindungen manuell zu konfigurieren, nachdem die Replikationsgruppe erstellt wurde.

### <a name="can-i-seed-a-replication-group-member-with-data-prior-to-the-initial-replication"></a>Kann ich ein Replikationsgruppenmitglieds mit Daten, bevor die erste Replikation starten?

Ja. DFS-Replikation unterstützt Kopieren von Dateien in eines Replikationsgruppenmitglieds vor der ersten Replikation. Diese Vorabbereitstellung "von" kann die Menge der Daten, die während der ersten Replikation repliziert erheblich reduzieren.

Die erste Replikation muss es sich nicht um Inhalte zu replizieren, wenn die Dateien nur durch echte Attribute oder Zeitstempel unterscheiden. Eine echte Attribut ist ein Attribut, das mithilfe der Win32-Funktion festgelegt werden kann `SetFileAttributes`. Weitere Informationen finden Sie unter [SetFileAttributes Funktion](http://go.microsoft.com/fwlink/?linkid=182269) in der MSDN Library (http://go.microsoft.com/fwlink/?LinkId=182269). Wenn sich zwei Dateien durch andere Attribute wie die Komprimierung unterscheiden, werden dann den Inhalt der Datei repliziert.

Vorabbereitstellen eines Replikationsgruppenmitglieds, kopieren Sie die Dateien in den entsprechenden Ordner auf den Ziel-Servern, erstellen Sie die Replikationsgruppe, und wählen Sie dann ein primäres Mitglied. Wählen Sie das Mitglied mit den aktuellsten Dateien, die repliziert werden, da der Inhalt des primären Mitglieds als "autorisierend" betrachtet wird werden sollen Dies bedeutet, dass während der ersten Replikation des primären Mitglieds-Dateien immer andere Versionen der Dateien auf anderen Mitgliedern der Replikationsgruppe überschrieben werden.

Weitere Informationen zu vorab-seeding und das Klonen der DFSR-Datenbank, finden Sie unter [DFS-Replikation anfängliche Synchronisierung in Windows Server 2012 R2: Angriff der Klonkrieger](http://blogs.technet.com/b/filecab/archive/2013/08/21/dfs-replication-initial-sync-in-windows-server-2012-r2-attack-of-the-clones.aspx).

Weitere Informationen über die anfängliche Replikation finden Sie unter [erstellen Sie eine Replikationsgruppe](https://technet.microsoft.com/library/cc725893).

### <a name="does-dfs-replication-overcome-common-file-replication-service-issues"></a>Werden DFS-Replikation File Replication Service Probleme gelöst?

Ja. DFS-Replikation überwunden werden drei häufige Probleme des Dateireplikationsdiensts (FRS):

  - Journalumbrüche: DFS-Replikation Wiederherstellung Journal umschließt im laufenden Betrieb. Alle vorhandenen Dateien oder Ordner werden als JournalWrap gekennzeichnet und anhand des Dateisystems überprüft werden, bevor die Replikation wieder aktiviert wird. Während der Wiederherstellung ist die dieses Volume nicht verfügbar für die Replikation in beide Richtungen.  
      
  - Übermäßige Replikation: Um eine übermäßige Replikation zu verhindern, verwendet die DFS-Replikation ein System Gutschrift in Höhe von.  
      
  - Geänderten Ordnern: Um verwandelte Ordnernamen zu verhindern, speichert die DFS-Replikation in Konflikt stehenden Daten in einem ausgeblendeten DfsrPrivate\\ConflictandDeleted-Ordner (befindet sich unter dem lokalen Pfad des replizierten Ordners). Beispielsweise führt dazu, dass mehrere Ordner gleichzeitig erstellen, mit identischem Namen auf verschiedenen Servern mithilfe des Dateireplikationsdiensts (FRS) repliziert Dateireplikationsdienst (FRS), um die älteren Ordner umbenennen. DFS-Replikation werden stattdessen die älteren Ordner des lokalen Ordners für gelöschte Konfliktdateien verschoben.  
      

### <a name="does-dfs-replication-replicate-files-in-chronological-order"></a>Werden DFS-Replikation werden Dateien in chronologischer Reihenfolge repliziert?

Nein. Dateien können außerhalb der Reihenfolge repliziert werden.

### <a name="does-dfs-replication-replicate-files-that-are-being-used-by-another-application"></a>Repliziert die DFS-Replikation Dateien, die von einer anderen Anwendung verwendet werden?

Wenn eine Anwendung eine Datei öffnet und eine Dateisperre darauf erstellt (Verhindern von anderen Anwendungen verwendet werden, während er geöffnet ist), repliziert DFS-Replikation nicht die Datei, bis es geschlossen wird. Wenn die Anwendung die Datei mit dem Read-Share-Zugriff geöffnet wird, kann die Datei immer noch repliziert werden.

### <a name="does-dfs-replication-replicate-ntfs-file-permissions-alternate-data-streams-hard-links-and-reparse-points"></a>DFS-Replikation replizieren NTFS-Dateiberechtigungen, alternative Datenströme, feste Links, und Analysepunkte?

  - NTFS-Dateiberechtigungen und alternative Datenströme DFS-Replikation repliziert wird.  
      
  - Microsoft unterstützt keine Erstellung feste NTFS-Links in oder aus Dateien in einem replizierten Ordner – Dies kann führen Probleme bei der Replikation mit den betroffenen Dateien. Fester Link-Dateien von der DFS-Replikation ignoriert werden und werden nicht repliziert. Auch Verknüpfungspunkte werden nicht repliziert, und die DFS-Replikation protokolliert 4406-Ereignis für jeden gefundenen Verknüpfungspunkt.  
      
  - Die einzige Analysepunkte, die von der DFS-Replikation repliziert sind diejenigen, die die e/a verwenden\_ABWEICHENDER\_TAG\_SYMLINK Tag DFS-Replikation nicht garantiert jedoch, dass das Ziel eine symbolische Verknüpfung ebenfalls repliziert wird. Weitere Informationen finden Sie unter den [bitten Sie das Directory Services Team Blog](http://blogs.technet.com/b/askds/archive/2011/09/30/friday-mail-sack-super-slo-mo-edition.aspx).  
      
  - Dateien mit der e/a\_ABWEICHENDER\_TAG\_DEDUPLIZIERUNG, e/a-\_ABWEICHENDER\_TAG\_SIS oder e/a-\_ABWEICHENDER\_TAG\_HSM-Analysepunktes-Tags werden repliziert. wie normale Dateien überlagert. Die analysenkennung und Analyse von Datenpuffern sind nicht auf andere Server repliziert, da der Analysepunkt nur auf dem lokalen System funktioniert. Daher ist es möglich, DFS-Replikation replizieren können Sie Ordner auf Volumes mit Datendeduplizierung unter Windows Server 2012 oder Single Instance Storage (SIS), jedoch Daten für die Deduplizierung ist werden gesondert verwaltet von jedem Server, auf dem der Rollendienst aktiviert ist.  
      

### <a name="does-dfs-replication-replicate-timestamp-changes-if-no-other-changes-are-made-to-the-file"></a>Repliziert DFS-Replikation Zeitstempel Änderungen, wenn keine weiteren Änderungen an der Datei vorgenommen werden?

Nein, DFS-Replikation Dateien repliziert nicht für die die einzige Änderung eine Änderung an der Zeitstempel ist. Darüber hinaus wird der geänderte Zeitstempel nicht auf anderen Mitgliedern der Replikationsgruppe repliziert, es sei denn, andere Änderungen an der Datei vorgenommen werden.

### <a name="does-dfs-replication-replicate-updated-permissions-on-a-file-or-folder"></a>Erfolgt die DFS-Replikation replizieren aktualisierte Berechtigungen für eine Datei oder Ordner?

Ja. DFS-Replikation repliziert Änderungen an Berechtigungen für Dateien und Ordner. Nur der Teil der Datei mit der Zugriffssteuerungsliste (ACL) wird repliziert, auch wenn die DFS-Replikation weiterhin die gesamte Datei in den Stagingbereich lesen müssen.


> [!NOTE]
> Ändern von ACLs für eine große Anzahl von Dateien kann auf die replikationsleistung auswirken. Allerdings ist die Verwendung der RDC die Menge der übertragenen Daten proportional zu die Größe der ACLs, die nicht die Größe der gesamten Datei. Die Menge an Datenverkehr des Datenträgers ist immer noch proportional zur Größe der Dateien, da die Dateien in und aus dem Stagingordner gelesen werden müssen. 
<br>


### <a name="does-dfs-replication-support-merging-text-files-in-the-event-of-a-conflict"></a>Unterstützt DFS-Replikation das Zusammenführen von Textdateien im Falle von Widersprüchen?

Dateien werden von DFS-Replikation nicht zusammengeführt werden, wenn ein Konflikt vorliegt. Es wird jedoch versucht, die die ältere Version der Datei in den verborgenen DfsrPrivate beibehalten\\ConflictandDeleted-Ordner auf dem Computer, in dem der Konflikt wurde erkannt.

### <a name="does-dfs-replication-use-encryption-when-transmitting-data"></a>Verwendet DFS-Replikation Verschlüsselung beim Übertragen von Daten?

Ja. DFS-Replikation verwendet (Remoteprozeduraufruf) Verbindungen mit Verschlüsselung.

### <a name="is-it-possible-to-disable-the-use-of-encrypted-rpc"></a>Ist es möglich, die die Verwendung der verschlüsselten RPC deaktivieren?

Nein. Der DFS-Replikationsdienst verwendet von Remoteprozeduraufrufen (RPC) über TCP, um Daten zu replizieren. Der DFS-Replikationsdienst dient zum Sichern von Datenübertragungen über das Internet immer Konstanten auf Authentifizierungsebene verwenden `RPC_C_AUTHN_LEVEL_PKT_PRIVACY`. Dadurch wird sichergestellt, dass der RPC-Kommunikation über das Internet immer verschlüsselt wird. Aus diesem Grund ist es nicht möglich, die die Verwendung von verschlüsselten RPC von der DFS-Replikationsdienst deaktivieren.

Weitere Informationen finden Sie unter den folgenden Microsoft-Websites:

  - [Technische Referenz für den RPC-](http://go.microsoft.com/fwlink/?linkid=182278)  
      
  - [Zur Remotedifferenzialkomprimierung](http://go.microsoft.com/fwlink/?linkid=182279)  
      
  - [Konstanten auf Authentifizierungsebene](http://go.microsoft.com/fwlink/?linkid=182280)  
      

### <a name="how-are-simultaneous-replications-handled"></a>Behandlung von gleichzeitige Replikationen

Es gibt eine Update-Manager pro replizierten Ordner. Aktualisieren von Managern Arbeit unabhängig voneinander.

Standardmäßig maximal 16 (vier in Windows Server 2003 R2) gleichzeitige Downloads für alle Verbindungen und alle Replikationsgruppen freigegeben werden. Da Verbindungen und Replikationsupdates für die Gruppe nicht serialisiert werden, ist es keine bestimmte Reihenfolge, in der Updates empfangen werden. Wenn zwei Zeitpläne geöffnet sind, Updates in der Regel erhalten und beide Verbindungen zur selben Zeit installiert.

### <a name="how-do-i-force-replication-or-polling"></a>Wie erzwinge ich die Replikation oder Abrufen?

Sie können erzwingen Sie die Replikation sofort mithilfe von DFS-Verwaltung, siehe [Bearbeiten von Replikationszeitplänen](https://technet.microsoft.com/library/Cc732278). Sie können die Replikation auch erzwingen, indem Sie mit der `Sync-DfsReplicationGroup` -Cmdlet die DFSR-PowerShell-Moduls, das mit Windows Server 2012 R2 eingeführt wurde oder die **Dfsrdiag SyncNow** Befehl. Sie können Abruf erzwingen, indem Sie mit der `Update-DfsrConfigurationFromAD` -Cmdlet, oder die **Dfsrdiag PollAD** Befehl.

### <a name="is-it-possible-to-configure-a-quiet-time-between-replications-for-files-that-change-frequently"></a>Ist es möglich, eine Leerlaufzeit zwischen den Replikationen für Dateien zu konfigurieren, die sich häufig ändern?

Nein. Wenn der Zeitplan geöffnet ist, wird die DFS-Replikation Änderungen replizieren, wie er sie bemerkt. Es ist keine Möglichkeit, eine Leerlaufzeit für Dateien konfigurieren.

### <a name="is-it-possible-to-configure-one-way-replication-with-dfs-replication"></a>Ist es möglich, unidirektionalen Replikation mit DFS-Replikation konfigurieren zu können?

Ja. Wenn Sie Windows Server 2012 oder Windows Server 2008 R2 verwenden, können Sie einen schreibgeschützten replizierten Ordner erstellen, der Inhalte über eine unidirektionale Verbindung repliziert. Weitere Informationen finden Sie unter [stellen Sie eine schreibgeschützte für replizierte Ordner auf einem bestimmten Mitglied](http://go.microsoft.com/fwlink/?linkid=156740) (http://go.microsoft.com/fwlink/?LinkId=156740).

Wir unterstützen keine, erstellen eine Verbindung für die unidirektionale Replikation mit DFS-Replikation unter Windows Server 2008 oder Windows Server 2003 R2. Auf diese Weise kann dazu führen, dass zahlreiche Probleme einschließlich integritätsprüfung Topologie Fehler, staging, Probleme und Probleme mit der DFS-Replikationsdatenbank.

Wenn Sie Windows Server 2008 oder Windows Server 2003 R2 verwenden, können Sie eine Verbindung mit unidirektionale simulieren, indem Sie die folgenden Aktionen ausführen:

  - Schulen Sie Administratoren, die nur auf den Servern ändern, die Sie als primären Server festlegen möchten. Anschließend können Sie die Änderungen auf dem Zielserver zu replizieren.  
      
  - Konfigurieren Sie die Freigabeberechtigungen auf dem Zielserver, sodass Benutzer nicht über Schreibberechtigungen verfügen. Wenn keine Änderungen auf den Branch Servern zulässig sind, klicken Sie dann ist es keine Replikation zurück, simulieren eine Verbindung mit unidirektionale und WAN-Auslastung gering zu halten.  
      

### <a name="is-there-a-way-to-force-a-complete-replication-of-all-files-including-unchanged-files"></a>Gibt es eine Möglichkeit, eine vollständige Replikation aller Dateien, einschließlich der unveränderte Dateien erzwingen?

Nein. Wenn die DFS-Replikation die Dateien identisch berücksichtigt werden, wird es sie nicht repliziert. Wenn die geänderte Dateien nicht repliziert wurden, werden sie bei entsprechender Konfiguration automatisch vom DFS-Replikation repliziert werden. Um dem konfigurierten Zeitplan zu überschreiben, verwenden Sie die WMI-Methode **ForceReplicate()** . Dies ist jedoch nur ein Zeitplan zu überschreiben, und sie erzwingt nicht die Replikation unverändert oder identische Dateien.

### <a name="what-happens-if-the-primary-member-suffers-a-database-loss-during-initial-replication"></a>Was geschieht, wenn das primäre Mitglied leidet die Verlust Datenbank während der anfänglichen Replikation?

Während der ersten Replikation dauert des primären Mitglieds-Dateien immer Vorrang vor in der Lösung des Konflikts, die auftritt, wenn der empfangenden Mitglieder verschiedene Versionen von Dateien auf dem primären Mitglied haben. Bezeichnung des primären Mitglieds befindet sich in Active Directory Domain Services, und die Bezeichnung deaktiviert ist, nach das primäre Mitglied repliziert werden kann, aber bevor alle Mitglieder der Replikation replizieren gruppieren.

Wenn die erste Replikation ein Fehler auftritt oder der DFS-Replikationsdienst neu gestartet, während der Replikations wird, das primäre Mitglied sieht die Bezeichnung des primären Mitglieds in der lokalen Datenbank für die DFS-Replikation, und Sie werden die erste Replikation wiederholt. Wenn die DFS-Replikation Datenbank des primären Mitglieds verloren geht, nach dem Löschen der primären-Bezeichnung in Active Directory Domain Services, aber bevor alle Mitglieder der Replikationsgruppe die anfängliche Replikation abgeschlossen, können nicht alle Mitglieder der Replikationsgruppe Replizieren Sie den Ordner aus, weil kein Server als dem primären Mitglied festgelegt ist. In diesem Fall verwenden die **Dfsradmin Mitgliedschaft/set /isprimary:true** Befehl auf dem primären Mitglied-Server für die Bezeichnung des primären Mitglieds manuell wiederherstellen.

Weitere Informationen über die anfängliche Replikation finden Sie unter [erstellen Sie eine Replikationsgruppe](https://technet.microsoft.com/library/cc725893).


> [!WARNING]
> Bezeichnung des primären Mitglieds wird nur während der ersten Replikation verwendet. Bei Verwendung der <STRONG>Dfsradmin</STRONG> Befehl, um anzugeben, ein primäres Mitglied für einen replizierten Ordner nach der Replikation abgeschlossen ist, DFS-Replikation ist nicht den Server als ein primäres Mitglied in Active Directory Domain Services festlegen. Allerdings versucht die DFS-Replikationsdatenbank auf dem Server anschließend nicht rückgängig gemacht werden beschädigte oder verlorene Daten aufweist, der Server, führen Sie eine erste Replikation als dem primären Mitglied anstelle der Wiederherstellung von Daten aus einem anderen Member der Replikation Gruppe. Der Server wird im Wesentlichen ein autorisierter primärer Server Konflikte verursachen kann. Aus diesem Grund geben Sie für das primäre Element manuell nur wenn Sie sicher, dass sind unwiderruflich die anfängliche Replikation fehlgeschlagen ist. 
<br>


### <a name="what-happens-if-the-replication-schedule-closes-while-a-file-is-being-replicated"></a>Was geschieht, wenn der Replikationszeitplan wird geschlossen, während eine Datei repliziert wird?

Wenn die Remotedifferenzialkomprimierung (RDC, Remotedifferenzialkomprimierung) auf die Verbindung aktiviert ist, eingehende Replikation von einer Datei, die größer als 64 KB, die begann, unmittelbar vor dem schließenden Zeitplan repliziert (oder zum Ändern von **keine Bandbreite**) wird fortgesetzt, wenn die Planen Sie geöffnet wird (oder Änderungen an etwas anders als **keine Bandbreite**). Die Replikation wird fortgesetzt, an dem Zustand, der vorlag, wenn die Replikation wurde beendet.

Wenn RDC deaktiviert ist, wird die DFS-Replikation vollständig die Dateiübertragung neu gestartet. Dies kann verzögert werden, wenn die Datei auf dem empfangenden Mitglied verfügbar ist.

### <a name="what-happens-when-two-users-simultaneously-update-the-same-file-on-different-servers"></a>Was geschieht, wenn zwei Benutzer gleichzeitig dieselbe Datei auf verschiedenen Servern aktualisieren?

Wenn die DFS-Replikation einen Konflikt erkannt wird, verwendet er die Version der Datei, die zuletzt gespeichert wurde. Verschiebt die andere Datei in die DfsrPrivate\\ConflictandDeleted-Ordner (unter dem lokalen Pfad des replizierten Ordners auf dem Computer, der der Konflikt aufgelöst werden soll). Es bleibt bis Konfliktordners für gelöschte Ordner Bereinigung aus, das auftritt, wenn der Ordner für gelöschte Konfliktdateien die konfigurierte Größe überschreitet oder DFS-Replikation, einen Out-of Speicherplatzfehler auftritt. Des Konfliktordners für gelöschte Dateien wird nicht repliziert, und diese Methode der konfliktauflösung vermeidet das Problem der geänderten Verzeichnisse, das in den Dateireplikationsdienst möglich war.

Wenn ein Konflikt auftritt, protokolliert die DFS-Replikation ein Informationsereignis im Ereignisprotokoll der DFS-Replikation. Dieses Ereignis ist keine Benutzeraktion aus den folgenden Gründen erforderlich:

  - Es ist nicht für Benutzer (es ist nur für Server-Administratoren sichtbar) sichtbar.  
      
  - DFS-Replikation behandelt den Konfliktordner für gelöschte als Cache an. Wenn ein Schwellenwert erreicht wird, werden einige der Dateien bereinigt. Es gibt keine Garantie, die in Konflikt stehenden Dateien gespeichert werden.  
      
  - Der Konflikt konnte auf einem anderen Ursprung des Konflikts Server befinden.  
      

## <a name="staging"></a>Wird bereitgestellt

### <a name="does-dfs-replication-continue-staging-files-when-replication-is-disabled-by-a-schedule-or-bandwidth-throttling-quota-or-when-a-connection-is-manually-disabled"></a>Werden DFS-Replikation staging von Dateien, bei der Replikation von einem Zeitplan oder das Kontingent für die bandbreiteneinschränkung deaktiviert ist oder wenn eine Verbindung manuell deaktiviert ist, wird fortgesetzt?

Nein. DFS-Replikation wird nicht zum Bereitstellen von Dateien außerhalb der geplanten Replikationszeiten fortgesetzt, wenn das bandbreitenkontingent Drosselung überschritten wird oder wenn Verbindungen deaktiviert sind.

### <a name="does-dfs-replication-prevent-other-applications-from-accessing-a-file-during-staging"></a>Verhindert die DFS-Replikation andere Anwendungen Zugriff auf eine Datei während des Stagings?

Nein. DFS-Replikation öffnet Dateien in einer Weise, die keine Benutzer oder Anwendungen über das Öffnen von Dateien im Ordner "Replikation" blockiert. Diese Methode wird als "opportunistische Sperren." bezeichnet.

### <a name="is-it-possible-to-change-the-location-of-the-staging-folder-with-the-dfs-management-tool"></a>Ist es möglich, den Speicherort des Stagingordners mit dem Tool der DFS-Verwaltung ändern?

Ja. Auf der Ordner stagingspeicherort konfiguriert ist die **erweitert** Registerkarte die **Eigenschaften** im Dialogfeld für jedes Mitglied einer Replikationsgruppe.

### <a name="when-are-files-staged"></a>Wann werden Dateien bereitgestellt?

Dateien werden auf dem sendenden Member bereitgestellt, wenn empfangende Mitglied die Datei anfordert (es sei denn, die Datei 64 KB ist oder kleiner) wie in der folgenden Tabelle gezeigt. Wenn für die Verbindung (Remote Differential Compression, RDC) deaktiviert ist, wird die Datei bereitgestellt, es sei denn, es ist von 256 KB oder kleiner. Dateien werden auch auf dem empfangenden Mitglied bereitgestellt, bei der Übertragung, wenn sie weniger als 64 KB groß sind, obwohl Sie diese Einstellung zwischen 16 KB bis 1 MB konfigurieren können. Wenn der Zeitplan geschlossen ist, werden die Dateien nicht bereitgestellt.

### <a name="the-minimum-file-sizes-for-staging-files"></a>Die minimale Größe für das staging von Dateien

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th>RDC aktiviert</th>
<th>RDC deaktiviert</th>
</tr>
</thead>
<tbody>
<tr class="even">
<td><p>Sendendes Mitglied</p></td>
<td><p>64 KB</p></td>
<td><p>256 KB</p></td>
</tr>
<tr class="odd">
<td><p>Empfangendes Mitglied</p></td>
<td><p>64 KB standardmäßig</p></td>
<td><p>64 KB standardmäßig</p></td>
</tr>
</tbody>
</table>

### <a name="what-happens-if-a-file-is-changed-after-it-is-staged-but-before-it-is-completely-transmitted-to-the-remote-site"></a>Was geschieht, wenn eine Datei geändert wird, nachdem er bereitgestellt wird, aber bevor sie vollständig mit dem Remotestandort übertragen werden?

Einen beliebigen Teil der Datei bereits gesendet wird, wird die Übertragung von DFS-Replikation fortgesetzt. Wenn die Datei vor Beginn der DFS-Replikation übertragen die Datei geändert wird, wird die neuere Version der Datei gesendet.

## <a name="change-history"></a>„Änderungsverlauf“


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>date</th>
<th>Beschreibung</th>
<th>Grund</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>15. November 2018</p></td>
<td><p>Aktualisiert für WindowsServer 2019.</p></td>
<td><p>Neues Betriebssystem.</p></td>
</tr>
<tr class="even">
<td><p>09. Oktober 2013</p></td>
<td><p>Aktualisiert, was die unterstützten Grenzwerte der DFS-Replikation sind? Der Abschnitt mit den Ergebnissen von Tests auf Windows Server 2012 R2.</p></td>
<td><p>Updates für die neueste Version von Windows Server</p></td>
</tr>
<tr class="odd">
<td><p>30. Januar 2013</p></td>
<td><p>Hinzugefügt von der DFS-Replikation ist weiterhin das staging von Dateien, bei der Replikation von einem Zeitplan oder das Kontingent für die bandbreiteneinschränkung deaktiviert ist oder wenn eine Verbindung manuell deaktiviert wird? Eintrag.</p></td>
<td><p>Fragen von Kunden</p></td>
</tr>
<tr class="even">
<td><p>31. Oktober 2012</p></td>
<td><p>Bearbeitet, was die unterstützten Grenzwerte der DFS-Replikation sind? der Eintrag die getestete Anzahl der replizierten Dateien auf einem Volume erhöhen.</p></td>
<td><p>Kundenfeedback</p></td>
</tr>
<tr class="odd">
<td><p>15. August 2012</p></td>
<td><p>Bearbeitet, wird die DFS-Replikation replizieren NTFS-Datei, Berechtigungen, alternative Datenströme, feste Links, und Analysepunkte? um weiter zu verdeutlichen, wie die DFS-Replikation feste Links behandelt und abweichender Einstiegspunkte.</p></td>
<td><p>Feedback von den Microsoft Support Services</p></td>
</tr>
<tr class="even">
<td><p>13 Juni 2012</p></td>
<td><p>Bearbeitet die DFS-Replikation ist-Arbeit auf ReFS oder FAT-Volumes? Erläuterung der Verweise hinzuzufügende Eintrag</p></td>
<td><p>Kundenfeedback</p></td>
</tr>
<tr class="odd">
<td><p>25 April 2012</p></td>
<td><p>Bearbeitet, wird die DFS-Replikation replizieren NTFS-Datei, Berechtigungen, alternative Datenströme, feste Links, und Analysepunkte? der Eintrag, um zu verdeutlichen, wie die DFS-Replikation feste Links behandelt.</p></td>
<td><p>Verringern Sie mögliche Verwirrung vermieden</p></td>
</tr>
<tr class="even">
<td><p>Am 30. März 2011</p></td>
<td><p>Bearbeitet die können die DFS-Replikation replizieren Outlook PST oder Microsoft Office Access-Datenbankdateien? Eintrag, um die potenziellen Auswirkungen der Verwendung von DFS-Replikation mit PST-Datei und den Zugriff auf Dateien zu korrigieren.</p>
<p>Hinzugefügt, wie kann ich die replikationsleistung verbessern?</p></td>
<td><p>Fragen unserer Kunden vorherigen Eintrags, der fälschlicherweise angegeben, dass die Replikation von PST- oder den Zugriff auf Dateien die DFS-Replikationsdatenbank beschädigt werden könnte.</p></td>
</tr>
<tr class="odd">
<td><p>26 Januar 2011</p></td>
<td><p>Hinzugefügt, wie die Dateien aus dem ConflictAndDeleted wiederhergestellt werden können oder bereits vorhandene Ordner?</p></td>
<td><p>Kundenfeedback</p></td>
</tr>
<tr class="even">
<td><p>20 Oktober 2010</p></td>
<td><p>Hinzugefügt, wie kann ich ein upgrade oder ein DFS-Replikation-Element ersetzen?</p></td>
<td><p>Kundenfeedback</p></td>
</tr>
</tbody>
</table>

