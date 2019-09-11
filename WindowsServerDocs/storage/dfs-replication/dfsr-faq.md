---
title: 'DFS-Replikation: Häufig gestellte Fragen'
ms.date: 06/18/2014
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 5bf85938f242ec29d75b32cdcb8b03c5f34bd1bb
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871971"
---
# <a name="dfs-replication-frequently-asked-questions-faq"></a>DFS-Replikation: Häufig gestellte Fragen


Aktualisiert: 30. April 2019

Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Diese FAQ beantwortet Fragen zur verteiltes Dateisystem (DFS)-Replikation (auch als DFS-R oder DFSR bezeichnet) für Windows Server.

Informationen zu DFS-Namespaces finden Sie unter [DFS-Namespaces: Häufig gestellte Fragen](https://technet.microsoft.com/library/ee404780).

Informationen zu den Neuerungen in DFS-Replikation finden Sie in den folgenden Themen:

  - [Übersicht über DFS-Namespaces und-DFS-Replikation](https://technet.microsoft.com/library/jj127250) (in Windows Server 2012)  
      
  - [Neues in verteiltes Dateisystem](https://technet.microsoft.com/library/ee307957) Thema in Änderungen der [Funktionalität von Windows Server 2008 zu Windows Server 2008 R2](https://technet.microsoft.com/library/dd391932)  
      
  - [Verteiltes Dateisystem](https://technet.microsoft.com/library/cc753479) Thema in [Funktionsänderungen von Windows Server 2003 mit SP1 zu Windows Server 2008](https://technet.microsoft.com/library/cc753208)  
      

Eine Liste der zuletzt vorgenommenen Änderungen an diesem Thema finden Sie im Abschnitt [Änderungsverlauf](#change-history) dieses Themas.

      

## <a name="interoperability"></a>Interoperabilität

### <a name="can-dfs-replication-communicate-with-frs"></a>Kann DFS-Replikation mit FRS kommunizieren?

Nein. DFS-Replikation kommuniziert nicht mit dem Datei Replikations Dienst (File Replication Service, FRS). DFS-Replikation und FRS können gleichzeitig auf demselben Server ausgeführt werden. Sie müssen jedoch nie so konfiguriert werden, dass dieselben Ordner oder Unterordner repliziert werden, da dies zu Datenverlusten führen kann.

### <a name="can-dfs-replication-replace-frs-for-sysvol-replication"></a>Kann DFS-Replikation für die SYSVOL-Replikation ersetzen

Ja, DFS-Replikation kann FRS für die SYSVOL-Replikation auf Servern mit Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ersetzen. Server, auf denen Windows Server 2003 R2 ausgeführt wird, unterstützen die Verwendung von DFS-Replikation zum Replizieren des Ordners SYSVOL

Weitere Informationen zum Replizieren von SYSVOL mithilfe DFS-Replikation finden Sie im Handbuch [zur Migration der SYSVOL-Replikation: FRS zum DFS-Replikation](https://technet.microsoft.com/library/dd640019).

### <a name="can-i-upgrade-from-frs-to-dfs-replication-without-losing-configuration-settings"></a>Kann ich ein Upgrade von FRS auf DFS-Replikation durchführen, ohne die Konfigurationseinstellungen zu verlieren?

Ja. Informationen zum Migrieren der Replikation von FRS zu DFS-Replikation finden Sie in den folgenden Dokumenten:

  - Informationen zum Migrieren der Replikation von Ordnern außer dem Ordner SYSVOL finden [Sie im DFS-Betriebshandbuch: Migrieren von FRS zu](http://go.microsoft.com/fwlink/?linkid=192776) DFS-Replikation und [FRS2DFSR – ein FRS-zu-DFSR-Migrations Dienstprogramm](http://go.microsoft.com/fwlink/?linkid=195437) (http://go.microsoft.com/fwlink/?LinkID=195437).  
      
  - Informationen zum Migrieren der Replikation des Ordners "SYSVOL" zu DFS-Replikation finden [Sie unter SYSVOL-Migrations Handbuch: FRS zum DFS-Replikation](https://technet.microsoft.com/library/dd640019).  
      

### <a name="can-i-use-dfs-replication-in-a-mixed-windowsunix-environment"></a>Kann ich DFS-Replikation in einer gemischten Windows-/UNIX-Umgebung verwenden?

Ja. Obwohl DFS-Replikation nur das Replizieren von Inhalten zwischen Servern unterstützt, auf denen Windows Server ausgeführt wird, können UNIX-Clients auf Dateifreigaben auf den Windows-Servern Installieren Sie hierzu Dienste für Network File Systems (NFS) auf dem DFS-Replikation-Server.

Sie können auch die in vielen UNIX-Clients enthaltene SMB/CIFS-Client Funktionalität verwenden, um direkt auf die Windows-Dateifreigaben zuzugreifen. diese Funktion ist zwar häufig eingeschränkt oder erfordert Änderungen an der Windows-Umgebung (z. b. das Deaktivieren der SMB-Signierung mit). Gruppenrichtlinie).

DFS-Replikation interagiert mit NFS auf einem Server, auf dem ein Windows Server-Betriebssystem ausgeführt wird, aber Sie können einen NFS-Bereitstellungs Punkt nicht replizieren.

### <a name="can-i-use-the-volume-shadow-copy-service-with-dfs-replication"></a>Kann ich die Volumeschattenkopie-Dienst mit DFS-Replikation verwenden?

Ja. DFS-Replikation wird auf Volumeschattenkopie-Dienst-Volumes (VSS) unterstützt, und vorherige Momentaufnahmen können erfolgreich mit dem Client für frühere Versionen wieder hergestellt werden.

### <a name="can-i-use-windowsbackup-ntbackupexe-to-remotely-back-up-a-replicated-folder"></a>Kann ich die Windows-Sicherung (Ntbackup. exe) verwenden, um einen replizierten Ordner Remote zu sichern?

Nein, die Verwendung der Windows-Sicherung (Ntbackup. exe) auf einem Computer mit Windows Server 2003 oder früher zum Sichern des Inhalts eines replizierten Ordners auf einem Computer mit Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 wird nicht unterstützt.

Verwenden Sie zum Sichern von Dateien, die in einem replizierten Ordner gespeichert sind, Windows Server-Sicherung oder Microsoft® System Center Data Protection Manager. Informationen zu Sicherungs-und Wiederherstellungs Funktionen in Windows Server 2008 R2 und Windows Server 2008 finden Sie unter [Sicherung und Wiederherstellung](https://technet.microsoft.com/library/Cc754097). Weitere Informationen finden Sie unter [System Center Data Protection Manager](http://go.microsoft.com/fwlink/?linkid=182261) (http://go.microsoft.com/fwlink/?LinkId=182261) ).

### <a name="do-file-system-policies-impact-dfs-replication"></a>Wirken sich Dateisystem Richtlinien DFS-Replikation aus?

Ja. Konfigurieren Sie keine Dateisystem Richtlinien für replizierte Ordner. Die Dateisystem Richtlinie wendet die NTFS-Berechtigungen bei jedem Gruppenrichtlinie Aktualisierungs Intervall erneut an. Dies kann zu Freigabe Verstößen führen, da eine geöffnete Datei nicht repliziert wird, bis die Datei geschlossen wird.

### <a name="does-dfs-replication-replicate-mailboxes-hosted-on-microsoft-exchange-server"></a>Repliziert DFS-Replikation Postfächer, die auf Microsoft Exchange Server gehostet werden?

Nein. DFS-Replikation können nicht zum Replizieren von Postfächern verwendet werden, die auf Microsoft Exchange Server gehostet werden.

### <a name="does-dfs-replication-support-file-screens-created-by-file-server-resource-manager"></a>Unterstützt DFS-Replikation Datei Bildschirme, die vom Datei Server Ressourcen-Manager erstellt werden?

Ja. Allerdings müssen die Datei Server-Ressourcen-Manager Datei Überprüfungs Einstellungen an beiden Enden der Replikation abgleichen. Außerdem verfügt DFS-Replikation über einen eigenen Filtermechanismus für Dateien und Ordner, die Sie verwenden können, um bestimmte Dateien und Dateitypen von der Replikation auszuschließen.

Im folgenden finden Sie bewährte Methoden für die Implementierung von Datei Bildschirmen oder Kontingenten:

  - Der verborgene DfsrPrivate-Ordner darf nicht Kontingenten oder Datei Bildschirmen unterliegen.  
      
  - Überwachte Dateien dürfen in keinem replizierten Ordner vorhanden sein, bevor die Überprüfung aktiviert ist.  
      
  - Keine Ordner können das Kontingent überschreiten, bevor das Kontingent aktiviert wird.  
      
  - Harte Kontingente müssen mit Bedacht verwendet werden. Einzelne Mitglieder einer Replikations Gruppe können vor der Replikation in einem Kontingent bleiben, aber überschreiten, wenn Dateien repliziert werden. Wenn ein Benutzer beispielsweise eine Datei mit einer Größe von 10 Megabyte (MB) auf Server a kopiert (was dann an der festen Grenze liegt) und ein anderer Benutzer eine 5-MB-Datei auf Server B kopiert, werden bei der nächsten Replikation beide Server das Kontingent um 5 Megabyte überschreiten. Dies kann dazu führen, dass DFS-Replikation fortlaufend versucht, die Dateien zu replizieren, wodurch Lücken im Versions Vektor und mögliche Leistungsprobleme verursacht werden.  
      

### <a name="is-dfs-replication-cluster-aware"></a>Ist DFS-Replikation Cluster fähig?

Ja, DFS-Replikation in Windows Server 2012 R2 bietet Windows Server 2012 und Windows Server 2008 R2 die Möglichkeit, einen Failovercluster als Mitglied einer Replikations Gruppe hinzuzufügen. Weitere Informationen finden Sie unter [Hinzufügen eines Failoverclusters zu einer Replikations Gruppe](http://go.microsoft.com/fwlink/?linkid=155085) (http://go.microsoft.com/fwlink/?LinkId=155085) ). Der DFS-Replikation-Dienst unter Windows-Versionen vor Windows Server 2008 R2 ist nicht für die Koordination mit einem Failovercluster konzipiert, und der Dienst führt kein Failover zu einem anderen Knoten durch.


> [!NOTE]
> Die Replikation von Dateien auf freigegebenen Clustervolumes wird von DFS-Replikation nicht unterstützt. 
<br>


### <a name="is-dfs-replication-compatible-with-data-deduplication"></a>Ist DFS-Replikation mit der Datendeduplizierung kompatibel?

Ja, DFS-Replikation kann Ordner auf Volumes replizieren, die die Datendeduplizierung in Windows Server verwenden.

### <a name="is-dfs-replication-compatible-with-ris-and-wds"></a>Ist DFS-Replikation mit RIS und WDS kompatibel?

Ja. DFS-Replikation repliziert Volumes, auf denen SIS (Single Instance Storage) aktiviert ist. SIS wird von Remoteinstallations Diensten (RIS), Windows-Bereitstellungs Diensten (Windows Deployment Services, WDS) und Windows Storage Server verwendet.

### <a name="is-it-possible-to-use-dfs-replication-with-offline-files"></a>Ist es möglich, DFS-Replikation mit Offlinedateien zu verwenden?

Sie können DFS-Replikation und Offlinedateien in Szenarios sicher verwenden, wenn nur ein Benutzer gleichzeitig in die Dateien schreibt. Dies ist nützlich für Benutzer, die zwischen zwei Zweigniederlassungen Reisen und in der Lage sein möchten, in einem Branch oder offline auf Ihre Dateien zuzugreifen. Offlinedateien speichert die Dateien für die Offline Verwendung lokal zwischen und DFS-Replikation die Daten zwischen den einzelnen Filialen repliziert.

Verwenden Sie DFS-Replikation nicht mit Offlinedateien in einer Umgebung mit mehreren Benutzern, da DFS-Replikation keinen verteilten Sperrmechanismus oder Datei Checkout Funktion bereitstellt. Wenn zwei Benutzer die gleiche Datei auf unterschiedlichen Servern gleichzeitig ändern, verschiebt DFS-Replikation die ältere Datei in den Ordner DfsrPrivate\\ConflictandDeleted (befindet sich unter dem lokalen Pfad des replizierten Ordners) während der nächsten Replikation.

### <a name="what-antivirus-applications-are-compatible-with-dfs-replication"></a>Welche Antivirenanwendungen sind mit DFS-Replikation kompatibel?

Antivirenanwendungen können zu einer übermäßigen Replikation führen, wenn Ihre Scan Aktivitäten die Dateien in einem replizierten Ordner ändern. Weitere Informationen finden Sie unter Testen der Interoperabilität von Antiviren- http://go.microsoft.com/fwlink/?LinkId=73990) [Anwendungen mit DFS-Replikation](http://go.microsoft.com/fwlink/?linkid=73990) (.

### <a name="what-are-the-benefits-of-using-dfs-replication-instead-of-windows-sharepoint-services"></a>Welche Vorteile bietet die Verwendung von DFS-Replikation anstelle von Windows SharePoint Services?

Windows® SharePoint® Services bietet strenge Konsistenz in Form von Datei-Auscheck Funktionen, die DFS-Replikation nicht. Wenn Sie Bedenken haben, dass mehrere Personen dieselbe Datei bearbeiten, empfehlen wir die Verwendung von Windows SharePoint Services. Windows SharePoint Services 2,0 mit Service Pack 2 ist als Teil von Windows Server 2003 R2 verfügbar. Windows SharePoint Services kann von der Microsoft-Website heruntergeladen werden. Sie ist nicht in neueren Versionen von Windows Server enthalten. Wenn Sie jedoch Daten über mehrere Standorte replizieren und die gleichen Dateien nicht gleichzeitig von den Benutzern bearbeitet werden, bietet DFS-Replikation eine größere Bandbreite und einfachere Verwaltung.

## <a name="limitations-and-requirements"></a>Einschränkungen und Anforderungen

### <a name="can-dfs-replication-replicate-between-branch-offices-without-a-vpn-connection"></a>Kann DFS-Replikation zwischen Zweigstellen ohne VPN-Verbindung repliziert werden?

Ja – vorausgesetzt, es gibt eine private WAN (Wide Area Network)-Verbindung (nicht das Internet), die die Zweigstellen verbindet. Sie müssen jedoch die richtigen Ports in externen Firewalls öffnen. DFS-Replikation verwendet den RPC-Endpunkt Mapper (Port 135) und einen zufällig zugewiesenen kurzlebigen Port oberhalb von 1024. Sie können das **Dfsrdiag** -Befehlszeilen Tool verwenden, um anstelle des kurzlebigen Ports einen statischen Port anzugeben. Weitere Informationen zum Angeben der RPC-Endpunkt Zuordnung finden Sie im [Artikel 154596](http://go.microsoft.com/fwlink/?linkid=73991) in der Microsoft Knowledge Base (http://go.microsoft.com/fwlink/?LinkId=73991).

### <a name="can-dfs-replication-replicate-files-encrypted-with-the-encrypting-file-system"></a>Können DFS-Replikation mit dem Verschlüsselndes Dateisystem verschlüsselte Dateien replizieren?

Nein. DFS-Replikation repliziert keine Dateien oder Ordner, die mit dem Verschlüsselndes Dateisystem (EFS) verschlüsselt sind. Wenn ein Benutzer eine Datei verschlüsselt, die zuvor repliziert wurde, wird DFS-Replikation die Datei von allen anderen Mitgliedern der Replikations Gruppe löscht. Dadurch wird sichergestellt, dass die einzige verfügbare Kopie der Datei die verschlüsselte Version auf dem Server ist.

### <a name="can-dfs-replication-replicate-outlook-pst-or-microsoft-office-access-database-files"></a>Kann DFS-Replikation Outlook. PST-oder Microsoft Office Access-Datenbankdateien replizieren?

DFS-Replikation können die persönlichen Microsoft Outlook-Ordner Dateien (PST) und Microsoft Access-Dateien nur dann sicher replizieren, wenn Sie zu Archivierungszwecken gespeichert werden und nicht über das Netzwerk über einen Client wie Outlook oder Access (zum Öffnen von PST oder Access) auf Sie zugreifen. Dateien, kopieren Sie zunächst die Dateien auf ein lokales Speichergerät.) Dies hat folgende Gründe:

  - Das Öffnen von PST-Dateien über Netzwerkverbindungen kann zu Daten Beschädigungen in den PST-Dateien führen. Weitere Informationen zur Ursache für den sicheren Zugriff auf PST-Dateien über ein Netzwerk finden Sie im [Artikel 297019](http://go.microsoft.com/fwlink/?linkid=125363) in der Microsoft Knowledge Base (http://go.microsoft.com/fwlink/?LinkId=125363).  
      
  - PST-und Access-Dateien bleiben in der Regel über einen längeren Zeitraum geöffnet, während der Zugriff durch einen Client wie Outlook oder Office Access erfolgt. Dadurch wird verhindert, dass DFS-Replikation diese Dateien replizieren, bis Sie geschlossen werden.  
      

### <a name="can-i-use-dfs-replication-in-a-workgroup"></a>Kann ich DFS-Replikation in einer Arbeitsgruppe verwenden?

Nein. DFS-Replikation auf Active Directory® Domänen Dienste für die Konfiguration basiert. Es funktioniert nur in einer Domäne.

### <a name="can-more-than-one-folder-be-replicated-on-a-single-server"></a>Können mehrere Ordner auf einem einzelnen Server repliziert werden?

Ja. DFS-Replikation können zahlreiche Ordner zwischen Servern replizieren. Stellen Sie sicher, dass jeder der replizierten Ordner über einen eindeutigen Stammpfad verfügt und dass Sie sich nicht überlappen. Beispielsweise können "d\\: Sales" und\\"d:" Accounting die Stamm Pfade für zwei replizierte Ordner sein\\, d: Sales\\und\\d: Verkaufsberichte können nicht die Stamm Pfade für zwei replizierte Ordner sein.

### <a name="does-dfs-replication-require-dfs-namespaces"></a>Erfordert DFS-Replikation DFS-Namespaces?

Nein. DFS-Replikation-und DFS-Namespaces können separat oder zusammen verwendet werden. Außerdem können DFS-Replikation verwendet werden, um eigenständige DFS-Namespaces zu replizieren, was mit FRS nicht möglich war.

### <a name="does-dfs-replication-require-time-synchronization-between-servers"></a>Erfordert DFS-Replikation Zeitsynchronisierung zwischen Servern?

Nein. DFS-Replikation erfordert nicht explizit eine Zeitsynchronisierung zwischen Servern. DFS-Replikation erfordert jedoch, dass die Server Uhren genau übereinstimmen. Die Server Uhren müssen innerhalb von fünf Minuten zueinander (standardmäßig) festgelegt werden, damit die Kerberos-Authentifizierung ordnungsgemäß funktioniert. Beispielsweise verwendet DFS-Replikation Zeitstempel, um zu bestimmen, welche Datei im Falle eines Konflikts Vorrang hat. Genaue Zeiten sind auch für Garbage Collection, Zeitpläne und andere Features wichtig.

### <a name="does-dfs-replication-support-replicating-an-entire-volume"></a>Unterstützt DFS-Replikation die Replikation eines gesamten Volumes?

Ja. Sie müssen jedoch zuerst Windows Server 2003 Service Pack 2 oder den Hotfix installieren. Weitere Informationen finden Sie im [Artikel 920335](http://go.microsoft.com/fwlink/?linkid=76776) in der Microsoft Knowledge Base (http://go.microsoft.com/fwlink/?LinkId=76776). Außerdem kann das Replizieren eines gesamten Volumes zu folgenden Problemen führen:

  - Wenn das Volume eine Windows-Auslagerungs Datei enthält, schlägt die Replikation fehl und protokolliert das DFSR-Ereignis 4312 im System Ereignisprotokoll.  
      
  - DFS-Replikation legt das System und die ausgeblendeten Attribute für den replizierten Ordner auf den Ziel Servern fest. Dies tritt auf, da Windows das System und die ausgeblendeten Attribute standardmäßig auf den volumestammordner anwendet. Wenn es sich bei dem lokalen Pfad des replizierten Ordners auf dem Zielserver ebenfalls um einen Volumestamm handelt, werden keine weiteren Änderungen an den Ordner Attributen vorgenommen.  
      
  - Beim Replizieren eines Volumes, das den Windows-Systemordner enthält, erkennt DFS-Replikation den Ordner "% windir%" und repliziert ihn nicht. DFS-Replikation repliziert jedoch Ordner, die von nicht-Microsoft-Anwendungen verwendet werden, was dazu führen kann, dass die Anwendungen auf den Ziel Servern fehlschlagen, wenn die Anwendungen Interoperabilitätsprobleme mit DFS-Replikation haben.  
      

### <a name="does-dfs-replication-support-rpc-over-http"></a>Unterstützt DFS-Replikation RPC-über-http?

Nein.

### <a name="does-dfs-replication-work-across-wireless-networks"></a>Funktioniert DFS-Replikation in drahtlosen Netzwerken?

Ja. DFS-Replikation ist unabhängig vom Verbindungstyp.

### <a name="does-dfs-replication-work-on-refs-or-fat-volumes"></a>Funktioniert DFS-Replikation an Refs-oder FAT-Volumes?

Nein. DFS-Replikation unterstützt nur Volumes, die mit dem NTFS-Dateisystem formatiert sind. Das robuste Dateisystem (Refs) und das FAT-Dateisystem werden nicht unterstützt. DFS-Replikation erfordert NTFS, weil das NTFS-Änderungs Journal und andere Funktionen des NTFS-Dateisystems verwendet werden.

### <a name="does-dfs-replication-work-with-sparse-files"></a>Funktioniert DFS-Replikation mit sparsesdateien?

Ja. Sie können sparsesdateien replizieren. Das **Sparse** -Attribut wird auf dem empfangenden Member beibehalten.

### <a name="do-i-need-to-log-in-as-administrator-to-replicate-files"></a>Muss ich mich als Administrator anmelden, um Dateien zu replizieren?

Nein. DFS-Replikation ist ein Dienst, der unter dem lokalen Systemkonto ausgeführt wird, sodass Sie sich nicht als Administrator anmelden müssen, um ihn zu replizieren. Sie müssen jedoch ein Domänen Administrator oder ein lokaler Administrator der betroffenen Dateiserver sein, um Änderungen an der DFS-Replikation Konfiguration vorzunehmen.

Weitere Informationen finden Sie unter "DFS-Replikation von Sicherheitsanforderungen und Delegierungen" im Delegat [The How to manage DFS-Replikation](http://go.microsoft.com/fwlink/?linkid=182294) (http://go.microsoft.com/fwlink/?LinkId=182294).

### <a name="how-can-i-upgrade-or-replace-a-dfs-replication-member"></a>Wie kann ich ein DFS-Replikation Mitglied aktualisieren oder ersetzen?

Wenn Sie ein DFS-Replikation Mitglied aktualisieren oder ersetzen möchten, finden Sie in diesem Blogbeitrag im Teamblog Fragen zum Verzeichnisdienste: [Ersetzen von DFSR-Mitglieds Hardware oder-Betriebssystem](http://blogs.technet.com/b/askds/archive/2010/09/10/series-wrap-up-and-downloads-replacing-dfsr-member-hardware-or-os.aspx).

### <a name="is-dfs-replication-suitable-for-replicating-roaming-profiles"></a>Ist DFS-Replikation für die Replikation von Roamingprofilen geeignet?

Ja. Bestimmte Szenarien werden beim Replizieren von Roamingbenutzerprofilen unterstützt. Informationen zu den unterstützten Szenarien finden Sie [in der Microsoft-Support Erklärung zu replizierten Benutzerprofil Daten](http://go.microsoft.com/fwlink/?linkid=201282) (http://go.microsoft.com/fwlink/?LinkId=201282).

### <a name="is-there-a-file-character-limit-or-limit-to-the-folder-depth"></a>Gibt es ein Datei Zeichenlimit oder eine Beschränkung für die Ordner Tiefe?

Windows und DFS-Replikation unterstützen Ordner Pfade mit bis zu 32000 Zeichen. DFS-Replikation ist nicht auf Ordner Pfade von 260 Zeichen beschränkt.

### <a name="must-members-of-a-replication-group-reside-in-the-same-domain"></a>Müssen sich Mitglieder einer Replikations Gruppe in derselben Domäne befinden?

Nein. Replikations Gruppen können Domänen übergreifend innerhalb einer einzelnen Gesamtstruktur, aber nicht in verschiedenen Gesamtstrukturen umfassen.

### <a name="what-are-the-supported-limits-of-dfs-replication"></a>Was sind die unterstützten Grenzwerte DFS-Replikation?

Die folgende Liste enthält eine Reihe von Richtlinien für die Skalierbarkeit, die von Microsoft auf Windows Server 2012 R2 getestet wurden:

  - Größe aller replizierten Dateien auf einem Server: 100 Terabyte.  
      
  - Anzahl der replizierten Dateien auf einem Volume: 70 Millionen.  
      
  - Maximale Dateigröße: 250 Gigabyte.  
      


> [!IMPORTANT]
> Beim Erstellen von Replikations Gruppen mit einer großen Anzahl oder Größe von Dateien sollten Sie einen Daten Bank Klon exportieren und präseedingtechniken verwenden, um die Dauer der ersten Replikation zu minimieren. Weitere Informationen finden <A href="http://blogs.technet.com/b/filecab/archive/2013/08/21/dfs-replication-initial-sync-in-windows-server-2012-r2-attack-of-the-clones.aspx">Sie unter DFS-Replikation Initial Sync in Windows Server 2012 R2: Angriff der Klone</A>. 
<br>


Die folgende Liste enthält eine Reihe von Richtlinien für die Skalierbarkeit, die von Microsoft auf Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008 getestet wurden:

  - Größe aller replizierten Dateien auf einem Server: 10 Terabyte.  
      
  - Anzahl der replizierten Dateien auf einem Volume: 11 Millionen.  
      
  - Maximale Dateigröße: 64 Gigabyte.  
      


> [!NOTE]
> Die Anzahl von Replikations Gruppen, replizierten Ordnern, Verbindungen oder Replikations Gruppenmitgliedern kann nicht länger begrenzt werden. 
<br>


Eine Liste der Skalierbarkeits Richtlinien, die von Microsoft für Windows Server 2003 R2 getestet wurden, finden Sie unter [DFS-Replikation Skalierbarkeits Richtlinien](http://go.microsoft.com/fwlink/?linkid=75043) (http://go.microsoft.com/fwlink/?LinkId=75043) ).

### <a name="when-should-i-not-use-dfs-replication"></a>Wann sollte ich DFS-Replikation nicht verwenden?

Verwenden Sie DFS-Replikation nicht in einer Umgebung, in der mehrere Benutzer dieselben Dateien gleichzeitig auf unterschiedlichen Servern aktualisieren oder ändern. Dies kann DFS-Replikation bewirken, dass in Konflikt stehende Kopien der Dateien in den ausgeblendeten\\Ordner "DfsrPrivate ConflictandDeleted" verschoben werden.

Wenn mehrere Benutzer die gleichen Dateien gleichzeitig auf unterschiedlichen Servern ändern müssen, verwenden Sie das Feature zum Auschecken von Dateien von Windows SharePoint Services, um sicherzustellen, dass nur ein Benutzer an einer Datei arbeitet. Windows SharePoint Services 2,0 mit Service Pack 2 ist als Teil von Windows Server 2003 R2 verfügbar. Windows SharePoint Services kann von der Microsoft-Website heruntergeladen werden. Sie ist nicht in neueren Versionen von Windows Server enthalten.

### <a name="why-is-a-schema-update-required-for-dfs-replication"></a>Warum ist für DFS-Replikation eine Schema Aktualisierung erforderlich?

In DFS-Replikation werden neue Objekte im Domänen namens Kontext von Active Directory Domain Services verwendet, um Konfigurationsinformationen zu speichern. Diese Objekte werden erstellt, wenn Sie das Schema der Active Directory-Domänendienste aktualisieren. Weitere Informationen finden Sie unter [Überprüfen der Anforderungen für DFS-Replikation](http://go.microsoft.com/fwlink/?linkid=182264) (http://go.microsoft.com/fwlink/?LinkId=182264) ).

## <a name="monitoring-and-management-tools"></a>Überwachungs-und Verwaltungs Tools

### <a name="can-i-automate-the-health-report-to-receive-warnings"></a>Kann ich den Integritäts Bericht für den Empfang von Warnungen automatisieren?

Ja. Es gibt drei Möglichkeiten, Integritäts Berichte zu automatisieren:

  - Verwenden Sie das in Windows Server 2012 R2 oder Dfsradmin. exe enthaltene DFSR-Windows PowerShell-Modul zusammen mit geplanten Aufgaben, um Regel Berichte regelmäßig zu generieren. Weitere Informationen finden Sie unter [Automatisieren von DFS-Replikation](http://go.microsoft.com/fwlink/?linkid=74010) Integritäts Berichten http://go.microsoft.com/fwlink/?LinkId=74010) (.  
      
  - Verwenden Sie das DFS-Replikation Management Pack für System Center Operations Manager, um Warnungen zu erstellen, die auf angegebenen Bedingungen basieren.  
      
  - Verwenden Sie den DFS-Replikation WMI-Anbieter zum Schreiben von Warnungen.  
      

### <a name="can-i-use-microsoft-system-center-operations-manager-to-monitor-dfs-replication"></a>Kann ich mit Microsoft System Center Operations Manager DFS-Replikation überwachen?

Ja. Weitere Informationen finden Sie im [DFS-Replikation Management Pack für System Center Operations Manager 2007](http://go.microsoft.com/fwlink/?linkid=182265) im Microsoft Download Center (http://go.microsoft.com/fwlink/?LinkId=182265).

### <a name="does-dfs-replication-support-remote-management"></a>Unterstützt DFS-Replikation die Remote Verwaltung?

Ja. DFS-Replikation unterstützt die Remote Verwaltung über die DFS-Verwaltungskonsole und den Befehl **Replikations Gruppe hinzufügen** . Beispielsweise können Sie auf Server a eine Verbindung mit einer Replikations Gruppe herstellen, die in der Gesamtstruktur mit den Servern A und B als Mitglieder definiert ist.

Die DFS-Verwaltung ist in Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 und Windows Server 2003 R2 enthalten. Um DFS-Replikation aus anderen Windows-Versionen zu verwalten, verwenden Sie Remotedesktop oder die [Remoteserver-Verwaltungstools für Windows 7](https://technet.microsoft.com/library/Ee449475).


> [!IMPORTANT]
> Zum Anzeigen oder Verwalten von Replikations Gruppen, die schreibgeschützte replizierte Ordner oder Mitglieder enthalten, bei denen es sich um Failovercluster handelt, müssen Sie die Version der DFS-Verwaltung verwenden, die in Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 und dem Remote Computer enthalten ist. <a href="http://go.microsoft.com/fwlink/p/?linkid=238560"> Server Verwaltungs Tools für Windows 8</a>oder die <a href="https://technet.microsoft.com/library/ee449475">Remoteserver-Verwaltungstools für Windows 7</a>. 
<br>


### <a name="do-ultrasound-and-sonar-work-with-dfs-replication"></a>Arbeiten Sie mit DFS-Replikation mit Ultraschall und Sonar?

Nein. DFS-Replikation verfügt über einen eigenen Satz von Überwachungs-und Diagnosetools. Ultraschall und Sonar sind nur in der Lage, FRS zu überwachen.

### <a name="how-can-files-be-recovered-from-the-conflictanddeleted-or-preexisting-folders"></a>Wie können Dateien aus den Ordnern "ConflictandDeleted" oder "bereits vorhanden" wieder hergestellt werden?

Stellen Sie zum Wiederherstellen verlorener Dateien die Dateien aus dem Dateisystem Ordner oder dem freigegebenen Ordner mithilfe des Datei Versions Verlaufs, des Befehls **vorherige Versionen wiederherstellen** im Datei-Explorer oder durch Wiederherstellen der Dateien aus einer Sicherung wieder her. Verwenden Sie die `Get-DfsrPreservedFiles` Windows PowerShell-Cmdlets und, die im DFSR-Modul `Restore-DfsrPreservedFiles` von Windows Server 2012 R2 enthalten sind, oder das [restoredfsr](http://code.msdn.microsoft.com/restoredfsr) -Beispielskript aus dem MSDN, um Dateien direkt aus dem Ordner "ConflictandDeleted" oder dem bereits vorhandenen Ordner wiederherzustellen. Code Gallery. Dieses Skript ist nur für die Notfall Wiederherstellung vorgesehen und wird ohne Garantie unverändert bereitgestellt.

### <a name="is-there-a-way-to-know-the-state-of-replication"></a>Gibt es eine Möglichkeit, den Status der Replikation zu erkennen?

Ja. Es gibt eine Reihe von Möglichkeiten, die Replikation zu überwachen:

  - DFS-Replikation verfügt über eine Management Pack für System Center Operations Manager, die eine proaktive Überwachung bereitstellt.  
      
  - Die DFS-Verwaltung verfügt über einen in-Box-Diagnosebericht für den Replikations Rückstand, die Replikations Effizienz und die Anzahl der Dateien und Ordner in einer bestimmten Replikations Gruppe.  
      
  - Das DFSR-Windows PowerShell-Modul in Windows Server 2012 R2 enthält Cmdlets zum Starten von propagierungs Tests und zum Schreiben von propagierungs-und Integritäts Berichten. Weitere Informationen finden Sie unter [verteiltes Dateisystem Replikations-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/dn296601.aspx).  
      
  - Dfsrdiag. exe ist ein Befehlszeilen Tool, das eine Rückstand Anzahl generieren oder einen propagierungs Test auslösen kann. Beide zeigen den Status der Replikation an. Die Weitergabe zeigt, ob Dateien auf alle Knoten repliziert werden. Der Rückstand zeigt Ihnen, wie viele Dateien noch repliziert werden müssen, bevor zwei Computer synchronisiert werden. Der Rückstands Zähler gibt die Anzahl der Updates an, die ein Replikations Gruppenmitglied nicht verarbeitet hat. Auf Computern, auf denen Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 ausgeführt wird, kann Dfsrdiag. exe auch die Updates anzeigen, die DFS-Replikation zurzeit replizieren.  
      
  - Skripts können mithilfe von WMI Rückstands Informationen – manuell oder über MOM sammeln.  
      

## <a name="performance"></a>Leistung

### <a name="does-dfs-replication-support-dial-up-connections"></a>Unterstützt DFS-Replikation DFÜ-Verbindungen?

Obwohl DFS-Replikation bei der DFÜ-Geschwindigkeit funktioniert, kann es zu einem Rückstand kommen, wenn eine große Anzahl von Änderungen repliziert werden muss. Wenn an vorhandenen Dateien kleine Änderungen vorgenommen werden, bietet DFS-Replikation mit Remote differenzieller Komprimierung (Remote Differential Compression, RDC) eine wesentlich höhere Leistung als das direkte Kopieren der Datei.

### <a name="does-dfs-replication-perform-bandwidth-sensing"></a>Führt DFS-Replikation Bandbreiten Erkennung durch?

Nein. DFS-Replikation führt keine Bandbreiten Erkennung aus. Sie können DFS-Replikation so konfigurieren, dass eine begrenzte Bandbreite pro Verbindung verwendet wird (Bandbreitendrosselung). Die Bandbreitenauslastung wird von DFS-Replikation jedoch nicht weiter reduziert, wenn die Netzwerkschnittstelle ausgelastet ist, und DFS-Replikation kann den Link für kurze Zeiträume vollständig vermindern. Die Bandbreitendrosselung mit DFS-Replikation ist nicht vollständig genau, da DFS-Replikation die Bandbreite durch Drosselung von RPC-Aufrufen drosselt. Daher können sich verschiedene Puffer in niedrigeren Ebenen des Netzwerk Stapels (einschließlich RPC) beeinträchtigen, wodurch der Netzwerkverkehr beeinträchtigt wird.

### <a name="does-dfs-replication-throttle-bandwidth-per-schedule-per-server-or-per-connection"></a>Wird die Bandbreite pro Zeitplan, pro Server oder pro Verbindung DFS-Replikation drosseln?

Wenn Sie die Bandbreiten Einschränkung bei der Angabe des Zeitplans konfigurieren, verwenden alle Verbindungen für diese Replikations Gruppe diese Einstellung für die Bandbreitendrosselung. Die Bandbreitendrosselung kann auch mithilfe der DFS-Verwaltung als Einstellung auf Verbindungs Ebene festgelegt werden.

### <a name="does-dfs-replication-use-active-directory-domain-services-to-calculate-site-links-and-connection-costs"></a>Werden DFS-Replikation Active Directory Domain Services zum Berechnen von Standort Verknüpfungen und Verbindungskosten verwenden?

Nein. DFS-Replikation verwendet die vom Administrator definierte Topologie, die unabhängig von Active Directory Domain Services Site Kosten ist.

### <a name="how-can-i-improve-replication-performance"></a>Wie kann ich die Replikations Leistung verbessern?

Weitere Informationen zu den verschiedenen Methoden zum Optimieren der Replikations Leistung finden Sie unter [Optimieren der Replikations Leistung in DFSR](http://blogs.technet.com/b/askds/archive/2010/03/31/tuning-replication-performance-in-dfsr-especially-on-win2008-r2.aspx) im [Teamblog "Ask The Directory Services](http://blogs.technet.com/b/askds/)".

### <a name="how-does-dfs-replication-avoid-saturating-a-connection"></a>Wie lässt sich DFS-Replikation die Verwendung einer Verbindung vermeiden?

In DFS-Replikation Sie die maximale Bandbreite festlegen, die Sie für eine Verbindung verwenden möchten, und der Dienst behält diese Ebene der Netzwerk Verwendung bei. Dies unterscheidet sich von der Bits (Bits), und DFS-Replikation die Verbindung nicht vollständig, wenn Sie Sie entsprechend festgelegt haben.

Trotzdem ist die Bandbreitendrosselung nicht 100% genau, und DFS-Replikation kann den Link für kurze Zeiträume vollständig verzieren. Dies liegt daran, dass DFS-Replikation Bandbreite durch Drosselung von RPC-Aufrufen drosselt. Da dieser Prozess auf unterschiedlichen Ebenen des Netzwerk Stapels basiert, einschließlich RPC, wird der Replikations Datenverkehr tendenziell in Spitzen bewegt, was manchmal zu einer Überlastung der Netzwerkverbindungen führt.

DFS-Replikation in Windows Server 2008 umfasst mehrere Leistungsverbesserungen, wie in [verteiltes Dateisystem](https://technet.microsoft.com/library/Cc753479)erläutert, ein Thema [zu Funktionsänderungen von Windows Server 2003 mit SP1 bis Windows Server 2008](https://technet.microsoft.com/library/cc753208).

### <a name="how-does-dfs-replication-performance-compare-with-frs"></a>Wie wird DFS-Replikation Leistung mit FRS verglichen?

DFS-Replikation ist viel schneller als FRS, insbesondere dann, wenn kleine Änderungen an großen Dateien vorgenommen werden und RDC aktiviert ist. Beispielsweise kann bei RDC eine kleine Änderung an einer PowerPoint-® Präsentation von 2 MB dazu führen, dass nur 60 Kilobyte (KB) über das Netzwerk gesendet werden – eine Einsparung von 97 Prozent bei übertragenen Bytes.

RDC wird nicht für Dateien verwendet, die kleiner als 64 KB sind und bei High-Speed-LANs, bei denen die Netzwerkbandbreite nicht in Konflikt steht, möglicherweise nicht vorteilhaft ist. RDC kann auf Verbindungs Basis mithilfe der DFS-Verwaltung deaktiviert werden.

### <a name="how-frequently-does-dfs-replication-replicate-data"></a>Wie häufig werden Daten DFS-Replikation repliziert?

Die Daten werden gemäß dem von Ihnen festgelegten Zeitplan repliziert. Beispielsweise können Sie den Zeitplan auf 15-Minuten-Intervalle, sieben Tage pro Woche festlegen. In diesen Intervallen ist die Replikation aktiviert. Die Replikation wird bald nach dem Erkennen einer Datei Änderung gestartet (in der Regel innerhalb von Sekunden).

Der Zeitplan für die Replikations Gruppe kann auf universelle Zeit Koordinate (UTC) festgelegt werden, während der Verbindungs Zeitplan auf die Ortszeit des empfangenden Members festgelegt ist. Berücksichtigen Sie dies, wenn die Replikations Gruppe mehrere Zeitzonen umfasst. Ortszeit bedeutet die Zeit des Mitglieds, das die eingehende Verbindung gehostet. Der angezeigte Zeitplan der eingehenden Verbindung und die zugehörige ausgehende Verbindung spiegeln Zeitzonenunterschiede wider, wenn der Zeitplan auf Ortszeit festgelegt ist.

### <a name="how-much-of-my-servers-system-resources-will-dfs-replication-consume"></a>Wie viele Systemressourcen des Servers werden DFS-Replikation verbrauchen?

Die von DFS-Replikation verwendeten Datenträger-, Arbeitsspeicher-und CPU-Ressourcen hängen von einer Reihe von Faktoren ab, einschließlich Anzahl und Größe der Dateien, Änderungs Rate, Anzahl der Replikations Gruppenmitglieder und Anzahl der replizierten Ordner. Außerdem sind einige Ressourcen schwerer zu schätzen. Beispielsweise kann die ESE-Technologie (Extensible Storage Engine), die für die DFS-Replikation-Datenbank verwendet wird, einen hohen Prozentsatz des verfügbaren Arbeitsspeichers beanspruchen, der bei Bedarf freigegeben wird. Andere Anwendungen als DFS-Replikation können abhängig von der Serverkonfiguration auf demselben Server gehostet werden. Wenn jedoch mehrere Anwendungen oder Server Rollen auf einem einzelnen Server gehostet werden, ist es wichtig, dass Sie diese Konfiguration testen, bevor Sie Sie in einer Produktionsumgebung implementieren.

### <a name="what-happens-if-a-wan-link-fails-during-replication"></a>Was geschieht, wenn ein WAN-Link während der Replikation ausfällt?

Wenn die Verbindung ausfällt, versucht DFS-Replikation, die Replikation fortzusetzen, während der Zeitplan geöffnet ist. Es gibt auch Verbindungsfehler, die im Ereignisprotokoll DFS-Replikation angegeben werden, das mithilfe von MOM (proaktiv durch Warnungen) und dem DFS-Replikation Integritäts Bericht (z. b. Wenn ein Administrator die Ausführung ausführt) geerntet werden kann.

## <a name="remote-differential-compression-details"></a>Details zur Remote differenziellen Komprimierung

### <a name="are-changes-compressed-before-being-replicated"></a>Werden die Änderungen vor dem Replizieren komprimiert?

Ja. Geänderte Teile von Dateien werden komprimiert, bevor Sie für alle Dateitypen gesendet werden, mit Ausnahme der folgenden (die bereits komprimiert sind):. WMA, WMV, ZIP, JPG,. mpg,. MPEG,. M1V,. MP2,. MP3,. MPa,. cab,. wav,. snd,. au,. ASF,. WM,. AVI,. z,. gz,. tgz und. frx. Die Komprimierungs Einstellungen für diese Dateitypen können in Windows Server 2003 R2 nicht konfiguriert werden.

### <a name="can-an-administrator-turn-off-rdc-or-change-the-threshold"></a>Kann ein Administrator den RDC ausschalten oder den Schwellenwert ändern?

Ja. Sie können RDC über die Eigenschaften Seite einer gegebenen Verbindung deaktivieren. Durch das Deaktivieren von RDC können CPU-Auslastung und Replikations Latenz bei schnellen LAN-Verbindungen (Local Area Network), die keine Bandbreiten Einschränkungen aufweisen, oder für Replikations Gruppen, die primär aus Dateien bestehen, die kleiner als 64 KB Wenn Sie die Remote Zugriffs Steuerung für eine Verbindung deaktivieren, testen Sie die Effizienz der Replikation vor und nach der Änderung, um zu überprüfen, ob die Replikations Leistung verbessert wurde.

Sie können den Schwellenwert für die RDC-Größe ändern, indem Sie den **Dfsradmin-Verbindungs Satz** Befehl, den DFS-Replikation WMI-Anbieter verwenden oder die XML-Konfigurationsdatei manuell bearbeiten.

### <a name="does-rdc-work-on-all-file-types"></a>Funktioniert RDC an allen Dateitypen?

Ja. RDC berechnet Unterschiede auf Blockebene unabhängig vom Datei Datentyp. RDC arbeitet jedoch effizienter mit bestimmten Dateitypen, z. b. Word-Dokumente, PST-Dateien und VHD-Images.

### <a name="how-does-rdc-work-on-a-compressed-file"></a>Wie funktioniert RDC an einer komprimierten Datei?

DFS-Replikation verwendet RDC, wodurch die Blöcke in der Datei berechnet werden, die sich geändert haben, und nur diese Blöcke über das Netzwerk sendet. DFS-Replikation muss nichts über den Inhalt der Datei wissen – nur welche Blöcke geändert wurden.

### <a name="is-cross-file-rdc-enabled-when-upgrading-to-windows-server-enterprise-edition-or-datacenter-edition"></a>Ist die Datei übergreifende RDC beim Upgrade auf Windows Server Enterprise Edition oder Datacenter Edition aktiviert?

Die Standard-Editionen von Windows Server unterstützen keine Datei übergreifenden RDC. Sie wird jedoch automatisch aktiviert, wenn Sie ein Upgrade auf eine Edition durchführen, die Datei übergreifende RDC unterstützt, oder wenn ein Mitglied der Replikations Verbindung eine unterstützte Edition ausgeführt wird. Eine Liste der Editionen, die Datei übergreifende RDC unterstützen, finden Sie unter welche Editionen des Windows-Betriebssystems unterstützen die Datei übergreifende RDC?

### <a name="is-rdc-true-block-level-replication"></a>Ist die RDC true-Replikation auf Blockebene?

Nein. RDC ist ein allgemeines Protokoll zum Komprimieren der Dateiübertragung. DFS-Replikation verwendet RDC in Blöcken auf Dateiebene, nicht auf der Datenträger Blockebene. RDC dividiert eine Datei in Blöcke. Für jeden Block in einer Datei wird eine Signatur berechnet, bei der es sich um eine kleine Anzahl von Bytes handelt, die den größeren Block darstellen können. Der Signatur Satz wird vom Server an den Client übertragen. Der Client vergleicht die Server Signaturen mit einem eigenen. Der Client fordert dann an, dass der Server nur die Daten für Signaturen sendet, die sich nicht bereits auf dem Client befinden.

### <a name="what-happens-if-i-rename-a-file"></a>Was geschieht, wenn ich eine Datei umbenenne?

DFS-Replikation die Datei bei der nächsten Replikation für alle anderen Mitglieder der Replikations Gruppe umbenannt. Dateien werden mithilfe einer eindeutigen ID nachverfolgt. das Umbenennen einer Datei und das Verschieben der Datei innerhalb des Replikats hat keine Auswirkung auf die Möglichkeit der DFS-Replikation, eine Datei zu replizieren.

### <a name="what-is-cross-file-rdc"></a>Was ist eine Datei übergreifende RDC?

Mit der Datei übergreifenden Remote Zugriffs Steuerung können DFS-Replikation RDC auch dann verwenden, wenn keine Datei mit demselben Namen am Client Ende vorhanden ist. Die Datei übergreifende Remote Zugriffs Steuerung verwendet eine Heuristik, um Dateien zu ermitteln, die mit der Datei vergleichbar sind, die repliziert werden muss, und verwendet Blöcke ähnlicher Dateien, die mit der replizierenden Datei identisch sind, um die Menge der über das WAN übertragenen Daten zu minimieren. Der Datei übergreifende RDC kann in diesem Prozess Blöcke mit bis zu fünf ähnlichen Dateien verwenden.

Um die Datei übergreifende RDC zu verwenden, muss ein Mitglied der Replikations Verbindung eine Edition von Windows ausführen, die eine Datei übergreifende RDC-Unterstützung unterstützt. Eine Liste der Editionen, die Datei übergreifende RDC unterstützen, finden Sie unter welche Editionen des Windows-Betriebssystems unterstützen die Datei übergreifende RDC?

### <a name="what-is-rdc"></a>Was ist RDC?

Remote Differenzial Komprimierung (Remote Differential Compression, RDC) ist ein Client/Server-Protokoll, das zum effizienten Aktualisieren von Dateien über ein Netzwerk mit eingeschränkter Bandbreite verwendet werden kann. RDC erkennt Einfügungen, Entfernungen und Neuanordnungen von Daten in Dateien, sodass DFS-Replikation nur die Änderungen replizieren kann, wenn Dateien aktualisiert werden. RDC wird nur für Dateien verwendet, die standardmäßig 64 KB oder größer sind. RDC kann eine ältere Version einer Datei mit demselben Namen im replizierten Ordner oder im Ordner DfsrPrivate\\ConflictandDeleted verwenden (befindet sich unter dem lokalen Pfad des replizierten Ordners).

### <a name="when-is-rdc-used-for-replication"></a>Wann wird RDC für die Replikation verwendet?

RDC wird verwendet, wenn die Datei einen minimalen Schwellenwert überschreitet. Der Schwellenwert für die Größe beträgt standardmäßig 64 KB. Nachdem eine Datei, die diesen Schwellenwert überschreitet, repliziert wurde, verwenden aktualisierte Versionen der Datei immer RDC, es sei denn, ein großer Teil der Datei wird geändert, oder RDC ist deaktiviert.

### <a name="which-editions-of-the-windows-operating-system-support-cross-file-rdc"></a>Welche Editionen des Windows-Betriebssystems unterstützen Datei übergreifende RDC?

Um die Datei übergreifende RDC zu verwenden, muss ein Mitglied der Replikations Verbindung eine Edition des Windows-Betriebssystems ausführen, die Datei übergreifende RDC unterstützt. In der folgenden Tabelle ist aufgeführt, welche Editionen des Windows-Betriebssystems Datei übergreifende RDC-Unterstützung unterstützen.

### <a name="cross-file-rdc-availability-in-editions-of-the-windows-operating-system"></a>Datei übergreifende RDC-Verfügbarkeit in Editionen des Windows-Betriebssystems

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
<td><p>Ja<em></p></td>
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

\*Optional können Sie die Datei übergreifende RDC unter Windows Server 2012 R2 deaktivieren.

## <a name="replication-details"></a>Replikations Details

### <a name="can-i-change-the-path-for-a-replicated-folder-after-it-is-created"></a>Kann ich den Pfad für einen replizierten Ordner nach der Erstellung ändern?

Nein. Wenn Sie den Pfad eines replizierten Ordners ändern müssen, müssen Sie ihn in der DFS-Verwaltung löschen und als neuen replizierten Ordner wieder hinzufügen. DFS-Replikation dann mithilfe der Remote differenziellen Komprimierung (Remote Differential Compression, RDC) eine Synchronisierung durchführen, die bestimmt, ob die Daten auf den sendenden und empfangenden Mitgliedern identisch sind Es werden nicht alle Daten im Ordner erneut repliziert.

### <a name="can-i-configure-which-file-attributes-are-replicated"></a>Kann ich konfigurieren, welche Dateiattribute repliziert werden?

Nein, Sie können nicht konfigurieren, welche Dateiattribute von DFS-Replikation repliziert werden.

Eine Liste der Attributwerte und deren Beschreibungen finden Sie unter [Dateiattribute](http://go.microsoft.com/fwlink/?linkid=182268) auf MSDN (http://go.microsoft.com/fwlink/?LinkId=182268).

Die folgenden Attributwerte werden mithilfe der `SetFileAttributes dwFileAttributes` -Funktion festgelegt, und Sie werden von DFS-Replikation repliziert. Durch Änderungen an diesen Attributwerten wird die Replikation der Attribute auslöst. Der Inhalt der Datei wird nur dann repliziert, wenn sich der Inhalt ändert. Weitere Informationen finden Sie unter [setfileattributfunktion](http://go.microsoft.com/fwlink/?linkid=182269) in der MSDN Library http://go.microsoft.com/fwlink/?LinkId=182269) (.

  - DATEI\_ATTRIBUT\_AUSGEBLENDET  
      
  - DATEI\_ATTRIBUT\_IST SCHREIBGESCHÜTZT.  
      
  - DATEI\_ATTRIBUT\_SYSTEM  
      
  - DATEI\_ATTRIBUT\_NICHTALS\_INHALTINDIZIERT\_  
      
  - DATEI\_ATTRIBUT\_OFFLINE  
      

Die folgenden Attributwerte werden von DFS-Replikation repliziert, aber Sie führen keine Replikation aus.

  - DATEI\_ATTRIBUT\_ARCHIV  
      
  - DATEI\_ATTRIBUT\_NORMAL  
      

Die folgenden Datei Attributwerte führen ebenfalls zu einer Replikation, obwohl Sie nicht mit der `SetFileAttributes` -Funktion festgelegt `GetFileAttributes` werden können (verwenden Sie die-Funktion, um die Attributwerte anzuzeigen).

  - ANALYSE\_\_PUNKT\_DES DATEI ATTRIBUTS  
      

> [!NOTE]
> DFS-Replikation repliziert keine Analyse Punkt Attributwerte, es sei denn, das Analyse-Tag ist IO_REPARSE_TAG_SYMLINK. Dateien mit den IO_REPARSE_TAG_DEDUP-, IO_REPARSE_TAG_SIS-oder IO_REPARSE_TAG_HSM-Analyse Tags werden als normale Dateien repliziert. Das Analyse-Tag und die Analysedaten Puffer werden jedoch nicht auf andere Server repliziert, da der Analyse Punkt nur auf dem lokalen System funktioniert. 
<br>

  - \_KOMPRIMIERTES\_DATEI ATTRIBUT  
      
  - DATEI\_ATTRIBUT\_VERSCHLÜSSELT  
      

> [!NOTE]
> DFS-Replikation repliziert keine Dateien, die mit dem Verschlüsselndes Dateisystem (EFS) verschlüsselt sind. DFS-Replikation repliziert Dateien, die mit nicht-Microsoft-Software verschlüsselt sind, jedoch nur, wenn der Wert des FILE_ATTRIBUTE_ENCRYPTED-Attributs nicht in der Datei festgelegt wird. 
<br>

  - DATEI\_ATTRIBUT\_MITGERINGERDICHTE\_  
      
  - DATEI\_ATTRIBUT\_VERZEICHNIS  
      

DFS-Replikation repliziert nicht den temporären\_Wert\_des Datei Attributs.

### <a name="can-i-control-which-member-is-replicated"></a>Kann ich Steuern, welcher Member repliziert wird?

Ja. Sie können eine Topologie auswählen, wenn Sie eine Replikations Gruppe erstellen. Oder Sie können **keine Topologie** auswählen und Verbindungen nach der Erstellung der Replikations Gruppe manuell konfigurieren.

### <a name="can-i-seed-a-replication-group-member-with-data-prior-to-the-initial-replication"></a>Kann ich ein Replikations Gruppenmitglied mit Daten vor der ersten Replikation als Ausgangswert ausführen?

Ja. DFS-Replikation unterstützt das Kopieren von Dateien in ein Replikations Gruppenmitglied vor der ersten Replikation. Diese "vorab Bereitstellung" kann die Menge der Daten, die während der ersten Replikation repliziert werden, erheblich reduzieren.

Bei der ersten Replikation müssen Inhalte nicht repliziert werden, wenn sich Dateien nur durch echte Attribute oder Zeitstempel unterscheiden. Ein reales Attribut ist ein Attribut, das von der Win32-Funktion `SetFileAttributes`festgelegt werden kann. Weitere Informationen finden Sie unter [setfileattributfunktion](http://go.microsoft.com/fwlink/?linkid=182269) in der MSDN Library http://go.microsoft.com/fwlink/?LinkId=182269) (. Wenn sich zwei Dateien durch andere Attribute unterscheiden, wie z. b. die Komprimierung, wird der Inhalt der Datei repliziert.

Wenn Sie ein Replikations Gruppenmitglied vorab bereitstellen möchten, kopieren Sie die Dateien in den entsprechenden Ordner auf den Ziel Servern, erstellen Sie die Replikations Gruppe, und wählen Sie dann ein primäres Mitglied aus. Wählen Sie das Element mit den aktuellsten Dateien aus, die Sie replizieren möchten, da der Inhalt des primären Members als "autorisierend" eingestuft wird. Dies bedeutet, dass die Dateien des primären Members während der ersten Replikation immer andere Versionen der Dateien auf anderen Mitgliedern der Replikations Gruppe überschreiben.

Informationen zum vorab-Seeding und zum Klonen der DFSR-Datenbank finden [Sie unter DFS-Replikation Initial Sync in Windows Server 2012 R2: Angriff der Klone](http://blogs.technet.com/b/filecab/archive/2013/08/21/dfs-replication-initial-sync-in-windows-server-2012-r2-attack-of-the-clones.aspx).

Weitere Informationen zur ersten Replikation finden Sie unter [Erstellen einer Replikations Gruppe](https://technet.microsoft.com/library/cc725893).

### <a name="does-dfs-replication-overcome-common-file-replication-service-issues"></a>Werden häufige Probleme mit dem Datei Replikations Dienst von DFS-Replikation gelöst?

Ja. DFS-Replikation überschreitet drei häufige FRS-Probleme:

  - Journal Umbrüche: DFS-Replikation wird im Handumdrehen aus Journal umschlossen. Jede vorhandene Datei oder dieser Ordner wird als journalwrap gekennzeichnet und mit dem Dateisystem überprüft, bevor die Replikation erneut aktiviert wird. Während der Wiederherstellung ist dieses Volume für die Replikation in keiner Richtung verfügbar.  
      
  - Übermäßige Replikation: Zur Vermeidung einer übermäßigen Replikation verwendet DFS-Replikation ein Guthaben.  
      
  - Morphte Ordner: Um die Verwendung von morphten Ordnernamen zu verhindern, speichert DFS-Replikation widersprüchliche Daten in einem\\verborgenen Ordner "DfsrPrivate ConflictandDeleted" (befindet sich unter dem lokalen Pfad des replizierten Ordners). Wenn Sie z. b. mehrere Ordner gleichzeitig mit identischen Namen auf unterschiedlichen Servern erstellen, die mit FRS repliziert werden, bewirkt FRS, dass der ältere Ordner umbenannt wird. DFS-Replikation verschiebt stattdessen die älteren Ordner in den lokalen Konflikt und den gelöschten Ordner.  
      

### <a name="does-dfs-replication-replicate-files-in-chronological-order"></a>Repliziert DFS-Replikation Dateien in chronologischer Reihenfolge?

Nein. Dateien können nicht in der richtigen Reihenfolge repliziert werden.

### <a name="does-dfs-replication-replicate-files-that-are-being-used-by-another-application"></a>Werden von DFS-Replikation Dateien repliziert, die von einer anderen Anwendung verwendet werden?

Wenn eine Anwendung eine Datei öffnet und eine Datei Sperre darauf erstellt (verhindert, dass Sie von anderen Anwendungen verwendet wird, während Sie geöffnet ist), repliziert DFS-Replikation die Datei erst, wenn Sie geschlossen wurde. Wenn die Anwendung die Datei mit Lesezugriff öffnet, kann die Datei trotzdem repliziert werden.

### <a name="does-dfs-replication-replicate-ntfs-file-permissions-alternate-data-streams-hard-links-and-reparse-points"></a>Werden von DFS-Replikation NTFS-Dateiberechtigungen, Alternative Datenströme, feste Links und Analyse Punkte repliziert?

  - DFS-Replikation repliziert NTFS-Dateiberechtigungen und alternative Datenströme.  
      
  - Microsoft unterstützt das Erstellen von festen NTFS-Links zu oder von Dateien in einem replizierten Ordner nicht – dies kann zu Replikations Problemen mit den betroffenen Dateien führen. Hardlinkdateien werden von DFS-Replikation ignoriert und nicht repliziert. Verknüpfungs Punkte werden auch nicht repliziert, und DFS-Replikation protokolliert das Ereignis 4406 für jeden gefundenen Verbindungspunkt.  
      
  - Die einzigen Analyse Punkte, die von DFS-Replikation repliziert werden, sind die\_, die\_das\_Tag für die e/a-Analyse Tag SYMLINK verwenden. DFS-Replikation gewährleistet jedoch nicht, dass das Ziel von SYMLINK ebenfalls repliziert wird. Weitere Informationen finden Sie im [Teamblog des Verzeichnis](http://blogs.technet.com/b/askds/archive/2011/09/30/friday-mail-sack-super-slo-mo-edition.aspx)Diensts.  
      
  - Dateien\_mit\_\_\_\_e/a\_-tagdeduplizierung,\_e/a-Analyse Tags oder e/a-Analyse Tags\_\_ als normale Dateien. Das Analyse Tag und die Analysedaten Puffer werden nicht auf andere Server repliziert, da der Analyse Punkt nur auf dem lokalen System funktioniert. Daher können DFS-Replikation Ordner auf Volumes replizieren, die die Datendeduplizierung in Windows Server 2012 oder SIS (Single Instance Storage) verwenden. datendeduplizierungsinformationen werden jedoch separat von jedem Server verwaltet, auf dem der Rollen Dienst aktiviert ist.  
      

### <a name="does-dfs-replication-replicate-timestamp-changes-if-no-other-changes-are-made-to-the-file"></a>Werden Zeitstempeländerungen von DFS-Replikation repliziert, wenn keine anderen Änderungen an der Datei vorgenommen werden?

Nein, DFS-Replikation repliziert keine Dateien, für die die einzige Änderung eine Änderung am Zeitstempel ist. Außerdem wird der geänderte Zeitstempel nicht an andere Mitglieder der Replikations Gruppe repliziert, es sei denn, es werden andere Änderungen an der Datei vorgenommen.

### <a name="does-dfs-replication-replicate-updated-permissions-on-a-file-or-folder"></a>Repliziert DFS-Replikation aktualisierte Berechtigungen für eine Datei oder einen Ordner?

Ja. DFS-Replikation repliziert Berechtigungs Änderungen für Dateien und Ordner. Nur der Teil der Datei, der der Access Control Liste (ACL) zugeordnet ist, wird repliziert, obwohl DFS-Replikation die gesamte Datei weiterhin im Stagingbereich lesen muss.


> [!NOTE]
> Das Ändern von ACLs für eine große Anzahl von Dateien kann sich auf die Replikations Leistung auswirken. Wenn Sie jedoch RDC verwenden, ist die Menge der übertragenen Daten proportional zur Größe der ACLs, nicht zur Größe der gesamten Datei. Der Datenverkehr des Datenträgers ist nach wie vor proportional zur Größe der Dateien, da die Dateien in den und aus dem Stagingordner gelesen werden müssen. 
<br>


### <a name="does-dfs-replication-support-merging-text-files-in-the-event-of-a-conflict"></a>Unterstützt DFS-Replikation das Zusammenführen von Textdateien im Fall eines Konflikts?

DFS-Replikation führt keine Dateien zusammen, wenn ein Konflikt vorliegt. Allerdings wird versucht, die ältere Version der Datei im ausgeblendeten DfsrPrivate\\ConflictandDeleted-Ordner auf dem Computer beizubehalten, auf dem der Konflikt erkannt wurde.

### <a name="does-dfs-replication-use-encryption-when-transmitting-data"></a>Verwendet DFS-Replikation beim Übertragen von Daten die Verschlüsselung?

Ja. DFS-Replikation verwendet RPC-Verbindungen (Remote Procedure Callcenter) mit Verschlüsselung.

### <a name="is-it-possible-to-disable-the-use-of-encrypted-rpc"></a>Ist es möglich, die Verwendung von verschlüsseltem RPC zu deaktivieren?

Nein. Der DFS-Replikation-Dienst verwendet Remote Prozedur Aufrufe (RPC) über TCP, um Daten zu replizieren. Um Datenübertragungen über das Internet zu schützen, wird der DFS-Replikation-Dienst so konzipiert, dass immer die Konstante `RPC_C_AUTHN_LEVEL_PKT_PRIVACY`auf Authentifizierungs Ebene verwendet wird. Dadurch wird sichergestellt, dass die RPC-Kommunikation über das Internet immer verschlüsselt ist. Daher ist es nicht möglich, die Verwendung von verschlüsseltem RPC durch den DFS-Replikation-Dienst zu deaktivieren.

Weitere Informationen finden Sie auf den folgenden Microsoft-Websites:

  - [Technische Referenz zu RPC](http://go.microsoft.com/fwlink/?linkid=182278)  
      
  - [Informationen zur Remote differenziellen Komprimierung](http://go.microsoft.com/fwlink/?linkid=182279)  
      
  - [Konstanten auf Authentifizierungs Ebene](http://go.microsoft.com/fwlink/?linkid=182280)  
      

### <a name="how-are-simultaneous-replications-handled"></a>Wie werden gleichzeitige Replizierungen behandelt?

Pro repliziertem Ordner ist ein Update-Manager vorhanden. Update-Manager arbeiten unabhängig voneinander.

Standardmäßig werden maximal 16 (vier in Windows Server 2003 R2) gleichzeitige Downloads von allen Verbindungen und Replikations Gruppen gemeinsam genutzt. Da Verbindungen und Replikations Gruppen Updates nicht serialisiert werden, gibt es keine bestimmte Reihenfolge, in der Updates empfangen werden. Wenn zwei Zeitpläne geöffnet werden, werden Updates in der Regel von beiden Verbindungen gleichzeitig empfangen und installiert.

### <a name="how-do-i-force-replication-or-polling"></a>Gewusst wie die Replikation oder den Abruf erzwingen?

Sie können die Replikation sofort mithilfe der DFS-Verwaltung erzwingen, wie unter [Bearbeiten von Replikations Zeitplänen](https://technet.microsoft.com/library/Cc732278)beschrieben. Sie können die Replikation auch erzwingen, `Sync-DfsReplicationGroup` indem Sie das Cmdlet verwenden, das im DFSR-PowerShell-Modul enthalten ist, das mit Windows Server 2012 R2 eingeführt wurde, oder den Befehl " **Dfsrdiag SyncNow** ". Sie können das Abrufen mit dem `Update-DfsrConfigurationFromAD` -Cmdlet oder dem **dfsrdiag pollad** -Befehl erzwingen.

### <a name="is-it-possible-to-configure-a-quiet-time-between-replications-for-files-that-change-frequently"></a>Ist es möglich, eine ruhige Zeit zwischen Replizierungen für Dateien zu konfigurieren, die sich häufig ändern?

Nein. Wenn der Zeitplan geöffnet ist, werden DFS-Replikation Änderungen repliziert, sobald Sie angezeigt werden. Es gibt keine Möglichkeit, für Dateien eine Stille Zeit zu konfigurieren.

### <a name="is-it-possible-to-configure-one-way-replication-with-dfs-replication"></a>Ist es möglich, die unidirektionale Replikation mit DFS-Replikation zu konfigurieren?

Ja. Wenn Sie Windows Server 2012 oder Windows Server 2008 R2 verwenden, können Sie einen schreibgeschützten replizierten Ordner erstellen, der Inhalte über eine unidirektionale Verbindung repliziert. Weitere Informationen finden Sie unter [Erstellen eines replizierten Ordners für einen bestimmten Member](http://go.microsoft.com/fwlink/?linkid=156740) (http://go.microsoft.com/fwlink/?LinkId=156740) ).

Das Erstellen einer unidirektionalen Replikations Verbindung mit DFS-Replikation in Windows Server 2008 oder Windows Server 2003 R2 wird nicht unterstützt. Dies kann zu zahlreichen Problemen führen, einschließlich der Integritäts Überprüfung-topologiefehler, stagingprobleme und Probleme mit der DFS-Replikation Datenbank.

Wenn Sie Windows Server 2008 oder Windows Server 2003 R2 verwenden, können Sie eine unidirektionale Verbindung simulieren, indem Sie die folgenden Aktionen ausführen:

  - Schulen Sie Administratoren, um Änderungen nur auf den Servern vorzunehmen, die Sie als primäre Server festlegen möchten. Lassen Sie die Änderungen dann auf den Ziel Servern replizieren.  
      
  - Konfigurieren Sie die Freigabe Berechtigungen auf den Ziel Servern, damit Endbenutzer keine Schreibberechtigungen besitzen. Wenn auf den Zweig Servern keine Änderungen zulässig sind, müssen Sie nicht zurück replizieren, eine unidirektionale Verbindung simulieren und die WAN-Auslastung gering halten.  
      

### <a name="is-there-a-way-to-force-a-complete-replication-of-all-files-including-unchanged-files"></a>Gibt es eine Möglichkeit, eine vollständige Replikation aller Dateien, einschließlich unveränderter Dateien, zu erzwingen?

Nein. Wenn DFS-Replikation die Dateien als identisch betrachtet, werden Sie nicht repliziert. Wenn geänderte Dateien nicht repliziert wurden, werden Sie von DFS-Replikation automatisch repliziert, wenn Sie dafür konfiguriert sind. Um den konfigurierten Zeitplan zu überschreiben, verwenden Sie die WMI-Methode **ForceReplicate ()** . Dies ist jedoch nur eine Zeit Plan Außerkraftsetzung, und es wird nicht erzwungen, dass nicht geänderte oder identische Dateien repliziert werden.

### <a name="what-happens-if-the-primary-member-suffers-a-database-loss-during-initial-replication"></a>Was geschieht, wenn der primäre Member während der ersten Replikation einen Daten Bank Verlust erleidet?

Während der ersten Replikation haben die Dateien des primären Members immer Vorrang bei der Konfliktlösung, die auftritt, wenn die empfangenden Member verschiedene Versionen von Dateien auf dem primären Element aufweisen. Die primäre Element Bezeichnung wird in Active Directory Domain Services gespeichert, und die Bezeichnung wird gelöscht, nachdem der primäre Member für die Replikation bereit ist, aber bevor alle Mitglieder der Replikations Gruppe repliziert werden.

Wenn bei der ersten Replikation ein Fehler auftritt oder der DFS-Replikation-Dienst während der Replikation neu gestartet wird, sieht das primäre Mitglied die Bezeichnung des primären Mitglieds in der lokalen DFS-Replikation Datenbank an und wiederholt die erste Replikation. Wenn die DFS-Replikation Datenbank des primären Mitglieds nach dem Löschen der primären Bezeichnung in Active Directory Domain Services verloren geht, aber bevor alle Mitglieder der Replikations Gruppe die erste Replikation durchführen, tritt bei allen Mitgliedern der Replikations Gruppe ein Fehler auf. Replizieren Sie den Ordner, da kein Server als primäres Mitglied festgelegt ist. Verwenden Sie in diesem Fall den Befehl **Dfsradmin Membership/Set/IsPrimary: true** auf dem primären Mitglieds Server, um die Bezeichnung für das primäre Element manuell wiederherzustellen.

Weitere Informationen zur ersten Replikation finden Sie unter [Erstellen einer Replikations Gruppe](https://technet.microsoft.com/library/cc725893).


> [!WARNING]
> Die Bezeichnung für das primäre Element wird nur während des ersten Replikations Prozesses verwendet. Wenn Sie den <STRONG>Dfsradmin</STRONG> -Befehl verwenden, um nach Abschluss der Replikation ein primäres Mitglied für einen replizierten Ordner anzugeben, legt DFS-Replikation den Server nicht als primäres Mitglied in Active Directory Domain Services fest. Wenn die DFS-Replikation Datenbank auf dem Server später jedoch zu einer unwiederherstellbaren Beschädigung oder einem Datenverlust führt, versucht der Server, eine anfängliche Replikation als primäres Mitglied auszuführen, anstatt seine Daten von einem anderen Mitglied der Replikation wiederherzustellen. Kreis. Im Wesentlichen wird der Server zu einem nicht autorisierten primären Server, der Konflikte verursachen kann. Geben Sie aus diesem Grund nur dann das primäre Mitglied manuell an, wenn Sie sicher sind, dass die anfängliche Replikation unwiederbringlich fehlgeschlagen ist. 
<br>


### <a name="what-happens-if-the-replication-schedule-closes-while-a-file-is-being-replicated"></a>Was geschieht, wenn der Replikations Zeitplan geschlossen wird, während eine Datei repliziert wird?

Wenn die Remote differenzielle Komprimierung (Remote Differential Compression, RDC) für die Verbindung aktiviert ist, wird die eingehende Replikation einer Datei mit einer Größe von mehr als 64 KB fortgesetzt, die unmittelbar vor dem Schließen des Zeitplans (oder der Umstellung auf **keine Bandbreite**) mit der Replikation Änderungen an einem anderen als der **Bandbreite**. Die Replikation wird fortgesetzt, wenn die Replikation angehalten wurde.

Wenn RDC ausgeschaltet ist, DFS-Replikation die Dateiübertragung vollständig neu gestartet. Dies kann sich verzögern, wenn die Datei auf dem empfangenden Mitglied verfügbar ist.

### <a name="what-happens-when-two-users-simultaneously-update-the-same-file-on-different-servers"></a>Was geschieht, wenn zwei Benutzer gleichzeitig dieselbe Datei auf unterschiedlichen Servern aktualisieren?

Wenn DFS-Replikation einen Konflikt erkennt, wird die Version der Datei verwendet, die zuletzt gespeichert wurde. Die andere Datei wird in den Ordner DfsrPrivate\\ConflictandDeleted verschoben (unter dem lokalen Pfad des replizierten Ordners auf dem Computer, der den Konflikt gelöst hat). Es bleibt so lange bestehen, bis die Bereinigung von Konflikten und gelöschten Ordnern erfolgt ist, wenn der Konflikt-und gelöschte Ordner die konfigurierte Größe überschreitet oder DFS-Replikation auf einen Fehler aufgrund von nicht genügend Speicherplatz Der Konflikt-und gelöschte Ordner wird nicht repliziert, und diese Methode der Konflikt Auflösung vermeidet das Problem der in FRS möglichen, nicht vertunnenen Verzeichnisse.

Wenn ein Konflikt auftritt, protokolliert DFS-Replikation ein Informations Ereignis im Ereignisprotokoll DFS-Replikation. Für dieses Ereignis ist aus den folgenden Gründen keine Benutzeraktion erforderlich:

  - Er ist für Benutzer nicht sichtbar (er ist nur für Server Administratoren sichtbar).  
      
  - DFS-Replikation behandelt den Konflikt und den gelöschten Ordner als Cache. Wenn ein Kontingent Schwellenwert erreicht wird, werden einige dieser Dateien bereinigt. Es gibt keine Garantie, dass widersprüchliche Dateien gespeichert werden.  
      
  - Der Konflikt kann sich auf einem anderen Server als dem Ursprung des Konflikts befinden.  
      

## <a name="staging"></a>Wird bereitgestellt

### <a name="does-dfs-replication-continue-staging-files-when-replication-is-disabled-by-a-schedule-or-bandwidth-throttling-quota-or-when-a-connection-is-manually-disabled"></a>Führt DFS-Replikation das Staging von Dateien fort, wenn die Replikation durch einen Zeitplan oder ein Bandbreitendrosselung deaktiviert wird oder wenn eine Verbindung manuell deaktiviert wird?

Nein. In DFS-Replikation werden Dateien nicht mehr außerhalb der geplanten Replikations Zeiten bereitgestellt, wenn das Kontingent für die Bandbreitendrosselung überschritten wurde oder wenn Verbindungen deaktiviert werden.

### <a name="does-dfs-replication-prevent-other-applications-from-accessing-a-file-during-staging"></a>Verhindert DFS-Replikation, dass andere Anwendungen während der Staging-Umgebung auf eine Datei zugreifen?

Nein. DFS-Replikation öffnet Dateien auf eine Weise, die verhindert, dass Benutzer oder Anwendungen Dateien im Replikations Ordner öffnen. Diese Methode wird als "opportunistische Sperre" bezeichnet.

### <a name="is-it-possible-to-change-the-location-of-the-staging-folder-with-the-dfs-management-tool"></a>Ist es möglich, den Speicherort des Stagingordners mit dem DFS-Verwaltungs Tool zu ändern?

Ja. Der Speicherort des Stagingordners wird auf der Registerkarte **erweitert** des Dialog Felds **Eigenschaften** für jedes Mitglied einer Replikations Gruppe konfiguriert.

### <a name="when-are-files-staged"></a>Wann werden Dateien bereitgestellt?

Dateien werden auf dem sendenden Member bereitgestellt, wenn das empfangende Element die Datei anfordert (es sei denn, die Datei ist 64 KB oder kleiner), wie in der folgenden Tabelle dargestellt. Wenn die Remote differenzielle Komprimierung (Remote Differential Compression, RDC) für die Verbindung deaktiviert ist, wird die Datei bereitgestellt, sofern Sie nicht 256 KB oder kleiner ist Dateien werden auch auf dem empfangenden Member bereitgestellt, wenn Sie übertragen werden, wenn Sie weniger als 64 KB groß sind. Sie können diese Einstellung jedoch zwischen 16 KB und 1 MB konfigurieren. Wenn der Zeitplan geschlossen ist, werden die Dateien nicht bereitgestellt.

### <a name="the-minimum-file-sizes-for-staging-files"></a>Die Mindestdateigrößen für Stagingdateien

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th>RDC-fähig</th>
<th>RDC deaktiviert</th>
</tr>
</thead>
<tbody>
<tr class="even">
<td><p>Senden von Mitgliedern</p></td>
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

### <a name="what-happens-if-a-file-is-changed-after-it-is-staged-but-before-it-is-completely-transmitted-to-the-remote-site"></a>Was geschieht, wenn eine Datei geändert wird, nachdem Sie bereitgestellt wurde, aber bevor Sie vollständig an den Remote Standort übertragen wird?

Wenn ein Teil der Datei bereits übertragen wird, wird die Übertragung DFS-Replikation fortgesetzt. Wenn die Datei geändert wird, bevor DFS-Replikation mit der Übertragung der Datei beginnt, wird die neuere Version der Datei gesendet.

## <a name="change-history"></a>Änderungsverlauf


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
<td><p>Aktualisiert für Windows Server 2019.</p></td>
<td><p>Neues Betriebssystem.</p></td>
</tr>
<tr class="even">
<td><p>09. Oktober 2013</p></td>
<td><p>Die unterstützten Grenzwerte für DFS-Replikation wurden aktualisiert. Abschnitt mit Ergebnissen aus Tests auf Windows Server 2012 R2.</p></td>
<td><p>Updates für die neueste Version von Windows Server</p></td>
</tr>
<tr class="odd">
<td><p>30. Januar, 2013</p></td>
<td><p>Wurde hinzugefügt, DFS-Replikation Stagingdateien fortzusetzen, wenn die Replikation durch einen Zeitplan oder ein Bandbreitendrosselung-Kontingent deaktiviert wird oder wenn eine Verbindung manuell deaktiviert wird? ein.</p></td>
<td><p>Kunden Fragen</p></td>
</tr>
<tr class="even">
<td><p>31. Oktober, 2012</p></td>
<td><p>Wurden die unterstützten Grenzwerte DFS-Replikation bearbeitet? Eintrag zum Erhöhen der getesteten Anzahl replizierter Dateien auf einem Volume.</p></td>
<td><p>Kundenfeedback</p></td>
</tr>
<tr class="odd">
<td><p>15. August 2012</p></td>
<td><p>Bearbeitet DFS-Replikation repliziert NTFS-Dateiberechtigungen, Alternative Datenströme, feste Links und Analyse Punkte? Eintrag, um zu verdeutlichen, wie DFS-Replikation feste Links und Analyse Punkte behandelt.</p></td>
<td><p>Feedback von Kunden Support Diensten</p></td>
</tr>
<tr class="even">
<td><p>13. Juni 2012</p></td>
<td><p>Bearbeitet DFS-Replikation funktioniert auf Refs-oder FAT-Volumes? Eintrag zum Hinzufügen einer Erörterung von refs.</p></td>
<td><p>Kundenfeedback</p></td>
</tr>
<tr class="odd">
<td><p>25. April 2012</p></td>
<td><p>Bearbeitet DFS-Replikation repliziert NTFS-Dateiberechtigungen, Alternative Datenströme, feste Links und Analyse Punkte? ein Eintrag, um zu verdeutlichen, wie DFS-Replikation feste Links behandelt.</p></td>
<td><p>Mögliche Verwirrung reduzieren</p></td>
</tr>
<tr class="even">
<td><p>30. März 2011</p></td>
<td><p>Bearbeitet kann DFS-Replikation Outlook. PST-oder Microsoft Office Access-Datenbankdateien replizieren? Eintrag, um die möglichen Auswirkungen der Verwendung von DFS-Replikation mit PST-und Access-Dateien zu korrigieren.</p>
<p>Wie kann ich die Replikations Leistung verbessern?</p></td>
<td><p>Kunden Fragen zum vorherigen Eintrag, die fälschlicherweise angegeben haben, dass durch das Replizieren von PST-oder Access-Dateien die DFS-Replikation Datenbank beschädigt werden konnte.</p></td>
</tr>
<tr class="odd">
<td><p>26. Januar 2011</p></td>
<td><p>Wie können Dateien aus den Ordnern "ConflictandDeleted" oder "bereits vorhanden" wieder hergestellt werden?</p></td>
<td><p>Kundenfeedback</p></td>
</tr>
<tr class="even">
<td><p>20. Oktober 2010</p></td>
<td><p>Wie kann ich ein DFS-Replikation Mitglied aktualisieren oder ersetzen?</p></td>
<td><p>Kundenfeedback</p></td>
</tr>
</tbody>
</table>

