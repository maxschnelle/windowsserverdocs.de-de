---
title: 'DFS-Replikation: Häufig gestellte Fragen (FAQ)'
ms.date: 06/18/2014
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 1e11f6c596d7e5eb0bdf379adcf47d21e74e9f6b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815623"
---
# <a name="dfs-replication-frequently-asked-questions-faq"></a>DFS-Replikation: Häufig gestellte Fragen


Aktualisiert: 30. April 2019

Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Diese FAQ beantworten häufig gestellte Fragen zur DFS-Replikation (Distributed File System, verteiltes Dateisystem) für Windows Server (die auch als DFS-R oder DFSR bezeichnet wird).

Informationen zu DFS-Namespaces finden Sie unter [DFS-Namespaces: Häufig gestellte Fragen](https://technet.microsoft.com/library/ee404780).

Informationen zu den Neuerungen bei der DFS-Replikation findest du in den folgenden Themen:

  - [Übersicht über DFS-Namespaces und DFS-Replikation](https://technet.microsoft.com/library/jj127250) (in Windows Server 2012)  
      
  - Thema [Neues im verteilten Dateisystem](https://technet.microsoft.com/library/ee307957) unter [Änderungen an der Funktionalität zwischen Windows Server 2008 und Windows Server 2008 R2](https://technet.microsoft.com/library/dd391932)  
      
  - Thema [Verteiltes Dateisystem](https://technet.microsoft.com/library/cc753479) unter [Änderungen an der Funktionalität zwischen Windows Server 2003 SP1 und Windows Server 2008](https://technet.microsoft.com/library/cc753208)  
      

Eine Liste der zuletzt vorgenommenen Änderungen an diesem Thema finden Sie im Abschnitt [Änderungsverlauf](#change-history) dieses Themas.

      

## <a name="interoperability"></a>Interoperabilität

### <a name="can-dfs-replication-communicate-with-frs"></a>Können die DFS-Replikation und der Dateireplikationsdienst miteinander kommunizieren?

Nein Die DFS-Replikation kommuniziert nicht mit dem Dateireplikationsdienst (File Replication Service, FRS). Die DFS-Replikation und FRS können gleichzeitig auf demselben Server ausgeführt werden, dürfen jedoch nie für die Replikation derselben Ordner oder Unterordner konfiguriert werden, da dies zu Datenverlusten führen kann.

### <a name="can-dfs-replication-replace-frs-for-sysvol-replication"></a>Kann die DFS-Replikation FRS bei der SYSVOL-Replikation ersetzen?

Ja. Auf Servern mit Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 kann die DFS-Replikation FRS bei der SYSVOL-Replikation ersetzen. Server, auf denen Windows Server 2003 R2 ausgeführt wird, bieten keine Unterstützung für die Verwendung der DFS-Replikation zum Replizieren des SYSVOL-Ordners.

Weitere Informationen zum Replizieren von SYSVOL mithilfe der DFS-Replikation findest du in der [Anleitung für die Migration der SYSVOL-Replikation: FRS-zu-DFS-Replikation](https://technet.microsoft.com/library/dd640019).

### <a name="can-i-upgrade-from-frs-to-dfs-replication-without-losing-configuration-settings"></a>Kann ich ein Upgrade von FRS auf die DFS-Replikation durchführen, ohne dass die Konfigurationseinstellungen verloren gehen?

Ja. In den folgenden Dokumenten wird erläutert, wie die Replikation von FRS zur DFS-Replikation migriert wird:

  - Informationen zum Migrieren der Replikation von Ordnern außer dem SYSVOL-Ordner findest du im [DFS-Betriebshandbuch: Migration von der FRS- zur DFS-Replikation](https://go.microsoft.com/fwlink/?linkid=192776) und [FRS2DFSR – Hilfsprogramm für die FRS-zu-DFSR-Migration](https://go.microsoft.com/fwlink/?linkid=195437) (https://go.microsoft.com/fwlink/?LinkID=195437).  
      
  - Informationen zum Migrieren der Replikation des SYSVOL-Ordners zur DFS-Replikation findest du in der [Anleitung für die Migration der SYSVOL-Replikation: FRS-zu-DFS-Replikation](https://technet.microsoft.com/library/dd640019).  
      

### <a name="can-i-use-dfs-replication-in-a-mixed-windowsunix-environment"></a>Kann ich die DFS-Replikation in einer gemischten Windows-/UNIX-Umgebung verwenden?

Ja. Obwohl die DFS-Replikation nur das Replizieren von Inhalten zwischen Servern unterstützt, auf denen Windows Server ausgeführt wird, können UNIX-Clients auf Dateifreigaben auf den Windows-Servern zugreifen. Installiere dazu Dienste für Netzwerkdateisysteme (Network File System, NFS) auf dem DFS-Replikationsserver.

Du kannst auch die in vielen UNIX-Clients enthaltene SMB/CIFS-Clientfunktionalität verwenden, um direkt auf die Windows-Dateifreigaben zuzugreifen. Diese Funktion ist jedoch häufig eingeschränkt oder erfordert Änderungen an der Windows-Umgebung (z. B. müssen SMB-Signaturen mithilfe von Gruppenrichtlinien deaktiviert werden).

Die DFS-Replikation interagiert mit NFS auf einem Server, auf dem ein Windows Server-Betriebssystem ausgeführt wird, allerdings kannst du keinen NFS-Bereitstellungspunkt replizieren.

### <a name="can-i-use-the-volume-shadow-copy-service-with-dfs-replication"></a>Kann der Volumeschattenkopie-Dienst mit der DFS-Replikation verwendet werden?

Ja. Die DFS-Replikation wird auf Volumes des Volumeschattenkopie-Diensts (Volume Shadow Copy Service, VSS) unterstützt, und vorherige Momentaufnahmen können mit dem Client für frühere Versionen erfolgreich wiederhergestellt werden.

### <a name="can-i-use-windowsbackup-ntbackupexe-to-remotely-back-up-a-replicated-folder"></a>Kann ich die Windows-Sicherung (Ntbackup.exe) verwenden, um einen replizierten Ordner remote zu sichern?

Nein. Die Windows-Sicherung (Ntbackup.exe) kann auf einem Computer mit Windows Server 2003 oder früher nicht verwendet werden, um den Inhalt eines replizierten Ordners auf einem Computer mit Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 zu sichern.

Verwende zum Sichern von Dateien, die in einem replizierten Ordner gespeichert sind, die Windows Server-Sicherung oder Microsoft&reg; System Center Data Protection Manager. Informationen zu Sicherungs- und Wiederherstellungsfunktionen in Windows Server 2008 R2 und Windows Server 2008 findest du unter [Sicherung und Wiederherstellung](https://technet.microsoft.com/library/Cc754097). Weitere Informationen findest du unter [System Center Data Protection Manager](https://go.microsoft.com/fwlink/?linkid=182261) (https://go.microsoft.com/fwlink/?LinkId=182261).

### <a name="do-file-system-policies-impact-dfs-replication"></a>Wirken sich Dateisystemrichtlinien auf die DFS-Replikation aus?

Ja. Es sollten keine Dateisystemrichtlinien für replizierte Ordner konfiguriert werden. Die NTFS-Berechtigungen werden bei jedem Aktualisierungsintervall für Gruppenrichtlinien von der Dateisystemrichtlinie erneut angewendet. Dies kann zu Freigabeverletzungen führen, da eine geöffnete Datei erst repliziert wird, nachdem sie geschlossen wurde.

### <a name="does-dfs-replication-replicate-mailboxes-hosted-on-microsoft-exchange-server"></a>Werden bei der DFS-Replikation Postfächer repliziert, die von Microsoft Exchange Server gehostet werden?

Nein Die DFS-Replikation kann nicht verwendet werden, um Postfächer zu replizieren, die von Microsoft Exchange Server gehostet werden.

### <a name="does-dfs-replication-support-file-screens-created-by-file-server-resource-manager"></a>Unterstützt die DFS-Replikation Dateiprüfungen, die vom Ressourcen-Manager für Dateiserver erstellt wurden?

Ja. Allerdings müssen die Dateiprüfungseinstellungen des Ressourcen-Managers für Dateiserver (File Server Resource Manager, FSRM) auf beiden Seiten der Replikation übereinstimmen. Außerdem verfügt die DFS-Replikation über einen eigenen Filtermechanismus für Dateien und Ordner, den du verwenden kannst, um bestimmte Dateien und Dateitypen aus der Replikation auszuschließen.

Im Folgenden einige Best Practices für die Implementierung von Dateiprüfungen oder Kontingenten:

  - Der verborgene Ordner „DfsrPrivate“ darf keinen Kontingenten oder Dateiprüfungen unterliegen.  
      
  - Bevor die Prüfung aktiviert wird, dürfen in den replizierten Ordnern keine geprüften Dateien enthalten sein.  
      
  - Bevor das Kontingent aktiviert wird, darf das Kontingent von keinem Ordner überschritten werden.  
      
  - Harte Kontingentgrenzen sollten mit Vorsicht verwendet werden. Einzelne Mitglieder einer Replikationsgruppe können vor der Replikation eine Kontingentgrenze einhalten, diese nach der Replikation der Dateien jedoch überschreiten. Beispiel: Wenn ein Benutzer eine Datei mit einer Größe von 10 MB auf Server A kopiert (der dann die harte Kontingentgrenze erreicht hat) und ein anderer Benutzer eine Datei von 5 MB auf Server B kopiert, überschreiten beide Server bei der nächsten Replikation das Kontingent um 5 MB. Dies kann dazu führen, dass von der DFS-Replikation fortlaufend versucht wird, die Dateien zu replizieren, wodurch Lücken im Versionsvektor und mögliche Leistungsprobleme auftreten.  
      

### <a name="is-dfs-replication-cluster-aware"></a>Ist die DFS-Replikation clusterfähig?

Ja. Die DFS-Replikation in Windows Server 2012 R2, Windows Server 2012 und Windows Server 2008 R2 bietet die Möglichkeit, einen Failovercluster als Mitglied einer Replikationsgruppe hinzuzufügen. Weitere Informationen findest du unter [Hinzufügen eines Failoverclusters zu einer Replikationsgruppe](https://go.microsoft.com/fwlink/?linkid=155085) (https://go.microsoft.com/fwlink/?LinkId=155085). Der DFS-Replikationsdienst in Windows-Versionen vor Windows Server 2008 R2 ist nicht für die Koordination mit einem Failovercluster ausgelegt. Außerdem unterstützt der Dienst kein Failover auf einen anderen Knoten.


> [!NOTE]
> Die DFS-Replikation unterstützt keine Dateireplikation auf freigegebenen Clustervolumes. 
<br>


### <a name="is-dfs-replication-compatible-with-data-deduplication"></a>Ist die DFS-Replikation mit der Datendeduplizierung kompatibel?

Ja. Von der DFS-Replikation können Ordner auf Volumes repliziert werden, die die Datendeduplizierung in Windows Server nutzen.

### <a name="is-dfs-replication-compatible-with-ris-and-wds"></a>Ist die DFS-Replikation mit RIS und WDS kompatibel?

Ja. Bei der DFS-Replikation werden Volumes repliziert, auf denen die Einzelinstanz-Speicherung (Single Instance Storage, SIS) aktiviert ist. SIS wird von Remoteinstallationsdiensten (Remote Installation Services, RIS), Windows-Bereitstellungsdiensten (Windows Deployment Services, WDS) und Windows Storage Server verwendet.

### <a name="is-it-possible-to-use-dfs-replication-with-offline-files"></a>Ist es möglich, die DFS-Replikation mit Offlinedateien zu verwenden?

Du kannst die DFS-Replikation und Offlinedateien problemlos zusammen verwenden, vorausgesetzt, es schreibt jeweils nur ein Benutzer in die Dateien. Dies ist für Benutzer hilfreich, die zwischen zwei Zweigstellen pendeln und in der Lage sein möchten, in beiden Zweigstellen oder offline auf ihre Dateien zuzugreifen. Mit der Funktion für Offlinedateien werden die Dateien für die Offlineverwendung lokal zwischengespeichert, während die Daten mit der DFS-Replikation zwischen den einzelnen Zweigstellen repliziert werden.

Die DFS-Replikation sollte nicht in einer Umgebung mit mehreren Benutzern zusammen mit Offlinedateien verwendet werden, da die DFS-Replikation keinen verteilten Sperrmechanismus oder eine Funktion zum Auschecken von Dateien bietet. Wenn zwei Benutzer dieselbe Datei auf unterschiedlichen Servern gleichzeitig ändern, wird die ältere Datei von der DFS-Replikationsfunktion bei der nächsten Replikation in den Ordner „DfsrPrivate\\ConflictandDeleted“ (unter dem lokalen Pfad des replizierten Ordners) verschoben.

### <a name="what-antivirus-applications-are-compatible-with-dfs-replication"></a>Welche Antivirenanwendungen sind mit der DFS-Replikation kompatibel?

Antivirenanwendungen können zu einer übermäßigen Replikation führen, wenn durch die Überprüfungen Dateien in einem replizierten Ordner geändert werden. Weitere Informationen findest du unter [Testen der Interoperabilität von Antivirenanwendungen und DFS-Replikation](https://go.microsoft.com/fwlink/?linkid=73990) (https://go.microsoft.com/fwlink/?LinkId=73990).

### <a name="what-are-the-benefits-of-using-dfs-replication-instead-of-windows-sharepoint-services"></a>Welche Vorteile bietet die Verwendung der DFS-Replikation anstelle von Windows SharePoint Services?

Windows&reg; SharePoint&reg; Services bietet eine starke Kohärenz in Form einer Funktion zum Auschecken von Dateien, die die DFS-Replikation nicht aufweist. Wenn vermieden werden soll, dass mehrere Personen dieselbe Datei bearbeiten, empfehlen wir die Verwendung von Windows SharePoint Services. Windows SharePoint Services 2.0 mit Service Pack 2 ist als Teil von Windows Server 2003 R2 verfügbar. Windows SharePoint Services kann von der Microsoft-Website heruntergeladen werden. In neueren Versionen von Windows Server ist die Lösung nicht enthalten. Wenn jedoch Daten über mehrere Standorte repliziert werden und Benutzer nicht dieselben Dateien zur selben Zeit bearbeiten, bietet die DFS-Replikation eine größere Bandbreite und eine einfachere Verwaltung.

## <a name="limitations-and-requirements"></a>Einschränkungen und Anforderungen

### <a name="can-dfs-replication-replicate-between-branch-offices-without-a-vpn-connection"></a>Ist mit der DFS-Replikation eine Replikation zwischen Zweigstellen ohne eine VPN-Verbindung möglich?

Ja – vorausgesetzt, es gibt eine private WAN (Wide Area Network)-Verbindung (nicht das Internet), durch die die Zweigstellen verbunden sind. Du musst jedoch die richtigen Ports in den externen Firewalls öffnen. Die DFS-Replikation nutzt die RPC-Endpunktzuordnung (Port 135) und einen zufällig zugewiesenen kurzlebigen Port oberhalb von 1024. Du kannst das Befehlszeilentool **Dfsrdiag** verwenden, um einen statischen Port anstelle des kurzlebigen Ports anzugeben. Weitere Informationen zum Angeben der RPC-Endpunktzuordnung findest du in [Artikel 154596](https://go.microsoft.com/fwlink/?linkid=73991) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=73991).

### <a name="can-dfs-replication-replicate-files-encrypted-with-the-encrypting-file-system"></a>Können bei der DFS-Replikation Dateien repliziert werden, die mit dem verschlüsselnden Dateisystem verschlüsselt wurden?

Nein Von der DFS-Replikation werden keine Dateien oder Ordner repliziert, die mit dem verschlüsselnden Dateisystem (Encrypting File System, EFS) verschlüsselt wurden. Wenn ein Benutzer eine Datei verschlüsselt, die zuvor repliziert wurde, wird die Datei von der DFS-Replikation aus allen anderen Mitgliedern der Replikationsgruppe gelöscht. Dadurch wird sichergestellt, dass die einzige verfügbare Kopie der Datei die verschlüsselte Version auf dem Server ist.

### <a name="can-dfs-replication-replicate-outlook-pst-or-microsoft-office-access-database-files"></a>Können mit der DFS-Replikation PST-Dateien aus Outlook oder Microsoft Office Access-Datenbankdateien repliziert werden?

Mit der DFS-Replikation können Dateien im persönlichen Ordner von Microsoft Outlook (PST-Dateien) und Microsoft Access-Dateien nur dann sicher repliziert werden, wenn sie zu Archivierungszwecken gespeichert werden und nicht über das Netzwerk über einen Client wie Outlook oder Access darauf zugegriffen wird. (Zum Öffnen von PST- oder Access-Dateien müssen diese zunächst auf eine lokale Speichervorrichtung kopiert werden.) Dafür gibt es folgende Gründe:

  - Das Öffnen von PST-Dateien über Netzwerkverbindungen kann zu Datenbeschädigungen in den PST-Dateien führen. Weitere Informationen dazu, warum über ein Netzwerk kein sicherer Zugriff auf PST-Dateien möglich ist, findest du in [Artikel 297019](https://go.microsoft.com/fwlink/?linkid=125363) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=125363).  
      
  - PST- und Access-Dateien bleiben häufig über einen längeren Zeitraum geöffnet, während über einen Client wie Outlook oder Office Access darauf zugegriffen wird. Dadurch wird verhindert, dass die Dateien von der DFS-Replikation repliziert werden, weil sie erst geschlossen werden müssen.  
      

### <a name="can-i-use-dfs-replication-in-a-workgroup"></a>Kann ich die DFS-Replikation in einer Arbeitsgruppe verwenden?

Nein Die DFS-Replikation wird über Active Directory&reg; Domain Services konfiguriert und funktioniert nur in einer Domäne.

### <a name="can-more-than-one-folder-be-replicated-on-a-single-server"></a>Können auf einem einzelnen Server auch mehrere Ordner repliziert werden?

Ja. Mit der DFS-Replikation können zahlreiche Ordner zwischen Servern repliziert werden. Vergewissere dich, dass jeder replizierte Ordner über einen eindeutigen Stammpfad verfügt und dass sich diese nicht überschneiden. Beispielsweise können „D:\\Vertrieb“ und „D:\\Buchhaltung“ die Stammpfade für zwei replizierte Ordner sein, während „D:\\Vertrieb“ und „D:\\Vertrieb\\Berichte“ nicht die Stammpfade für zwei replizierte Ordner darstellen können.

### <a name="does-dfs-replication-require-dfs-namespaces"></a>Erfordert die DFS-Replikation DFS-Namespaces?

Nein Die DFS-Replikation und DFS-Namespaces können getrennt oder zusammen verwendet werden. Außerdem kann die DFS-Replikation verwendet werden, um eigenständige DFS-Namespaces zu replizieren, was mit FRS nicht möglich war.

### <a name="does-dfs-replication-require-time-synchronization-between-servers"></a>Erfordert die DFS-Replikation eine Zeitsynchronisierung zwischen Servern?

Nein Die DFS-Replikation erfordert nicht explizit eine Zeitsynchronisierung zwischen Servern. Allerdings erfordert die DFS-Replikation, dass die Serveruhren möglichst exakt aufeinander abgestimmt sind. Damit die Kerberos-Authentifizierung ordnungsgemäß funktioniert, dürfen die Serveruhren (standardmäßig) maximal fünf Minuten voneinander abweichen. Beispielsweise werden bei der DFS-Replikation Zeitstempel verwendet, um zu bestimmen, welche Datei im Falle eines Konflikts Vorrang hat. Exakte Zeiten sind auch für die Garbage Collection, für Zeitpläne und andere Features wichtig.

### <a name="does-dfs-replication-support-replicating-an-entire-volume"></a>Unterstützt die DFS-Replikation die Replikation eines gesamten Volumes?

Ja. Du musst du jedoch zuerst Windows Server 2003 Service Pack 2 oder den Hotfix installieren. Weitere Informationen findest du im [Artikel 920335](https://go.microsoft.com/fwlink/?linkid=76776) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=76776). Darüber hinaus kann die Replikation eines vollständigen Volumes folgende Probleme verursachen:

  - Wenn das Volume eine Windows-Auslagerungsdatei enthält, schlägt die Replikation fehl, und im Systemereignisprotokoll wird das DFSR-Ereignis 4312 protokolliert.  
      
  - Von der DFS-Replikation werden das System- und Hidden-Attribut für den replizierten Ordner auf den Zielservern festgelegt. Dies geschieht, weil Windows das System- und Hidden-Attribut standardmäßig auf den Volumestammordner anwendet. Wenn es sich bei dem lokalen Pfad des replizierten Ordners auf den Zielservern ebenfalls um einen Volumestamm handelt, werden keine weiteren Änderungen an den Ordnerattributen vorgenommen.  
      
  - Beim Replizieren eines Volumes, das den Windows-Systemordner enthält, wird der Ordner %WINDIR% von der DFS-Replikation erkannt und nicht repliziert. Allerdings werden von der DFS-Replikation Ordner repliziert, die von Nicht-Microsoft-Anwendungen verwendet werden, was zu Fehlern bei den Anwendungen auf den Zielservern führen kann, wenn die Anwendungen Interoperabilitätsprobleme mit der DFS-Replikation haben.  
      

### <a name="does-dfs-replication-support-rpc-over-http"></a>Unterstützt die DFS-Replikation RPC über HTTP?

Nein

### <a name="does-dfs-replication-work-across-wireless-networks"></a>Funktioniert die DFS-Replikation über Funknetzwerke?

Ja. Die DFS-Replikation ist unabhängig vom Verbindungstyp.

### <a name="does-dfs-replication-work-on-refs-or-fat-volumes"></a>Funktioniert die DFS-Replikation auf ReFS- oder FAT-Volumes?

Nein Die DFS-Replikation unterstützt nur Volumes, die mit dem NTFS-Dateisystem formatiert sind. ReFS (Resilient File System, Robustes Dateisystem) und das FAT-Dateisystem werden nicht unterstützt. Die DFS-Replikation erfordert NTFS, da sie das NTFS-Änderungsjournal und andere Funktionen des NTFS-Dateisystems verwendet.

### <a name="does-dfs-replication-work-with-sparse-files"></a>Unterstützt die DFS-Replikation Sparsedateien?

Ja. Sparsedateien können repliziert werden. Das **Sparse**-Attribut wird auf dem empfangenden Mitglied beibehalten.

### <a name="do-i-need-to-log-in-as-administrator-to-replicate-files"></a>Muss ich mich als Administrator anmelden, um Dateien zu replizieren?

Nein Die DFS-Replikation ist ein Dienst, der unter dem lokalen Systemkonto ausgeführt wird, sodass du dich nicht als Administrator anmelden musst, um Dateien zu replizieren. Du musst jedoch ein Domänenadministrator oder lokaler Administrator der betroffenen Dateiserver sein, um Änderungen an der DFS-Replikationskonfiguration vorzunehmen.

Weitere Informationen findest du im Thema zu „Sicherheitsanforderungen und Delegation bei der DFS-Replikation“ unter [Delegieren der Fähigkeit zum Verwalten der DFS-Replikation](https://go.microsoft.com/fwlink/?linkid=182294) (https://go.microsoft.com/fwlink/?LinkId=182294).

### <a name="how-can-i-upgrade-or-replace-a-dfs-replication-member"></a>Wie kann ich ein DFS-Replikationsmitglied aktualisieren oder ersetzen?

Informationen zum Aktualisieren oder Ersetzen eines DFS-Replikationsmitglieds findest du im folgenden Beitrag des Blogs „Ask the Directory Services Team“: [Austauschen der Hardware oder des Betriebssystems bei DFSR-Mitgliedern](https://blogs.technet.com/b/askds/archive/2010/09/10/series-wrap-up-and-downloads-replacing-dfsr-member-hardware-or-os.aspx).

### <a name="is-dfs-replication-suitable-for-replicating-roaming-profiles"></a>Ist die DFS-Replikation für die Replikation von Roamingprofilen geeignet?

Ja. Bestimmte Szenarien werden beim Replizieren von Roamingbenutzerprofilen unterstützt. Informationen zu den unterstützten Szenarien findest du in der [Anweisung des Microsoft-Supports zu replizierten Benutzerprofildaten](https://go.microsoft.com/fwlink/?linkid=201282) (https://go.microsoft.com/fwlink/?LinkId=201282).

### <a name="is-there-a-file-character-limit-or-limit-to-the-folder-depth"></a>Ist die Zeichenanzahl in Dateien oder die Länge der Ordnerpfade begrenzt?

Windows und die DFS-Replikation unterstützen Ordnerpfade mit bis zu 32.000 Zeichen. Die DFS-Replikation ist nicht auf Ordnerpfade von 260 Zeichen beschränkt.

### <a name="must-members-of-a-replication-group-reside-in-the-same-domain"></a>Müssen sich Mitglieder einer Replikationsgruppe in derselben Domäne befinden?

Nein Replikationsgruppen können auf Domänen innerhalb einer einzelnen Gesamtstruktur, aber nicht auf verschiedene Gesamtstrukturen verteilt sein.

### <a name="what-are-the-supported-limits-of-dfs-replication"></a>Wie lauten die unterstützten Grenzwerte für die DFS-Replikation?

Die folgende Liste enthält eine Reihe von Skalierbarkeitsrichtlinien, die von Microsoft getestet wurden und für Windows Server 2012 R2, Windows Server 2016 und Windows Server 2019 gelten.

  - Größe aller replizierten Dateien auf einem Server: 100 Terabytes  
      
  - Anzahl der replizierten Dateien auf einem Volume: 70 Millionen  
      
  - Maximale Dateigröße: 250 Gigabytes  
      


> [!IMPORTANT]
> Bei der Erstellung von Replikationsgruppen mit einer hohen Dateianzahl oder -größe empfehlen wir, einen Datenbankklon zu exportieren und Vorab-Seedingverfahren zu nutzen, um die Dauer der ersten Replikation zu minimieren. Weitere Informationen findest du unter [DFS Replication Initial Sync in Windows Server 2012 R2: Attack of the Clones](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/DFS-Replication-Initial-Sync-in-Windows-Server-2012-R2-Attack-of/ba-p/424877) (Erste Synchronisierung bei der DFS-Replikation in Windows Server 2012 R2: Angriff der Klone). 
<br>


Die folgende Liste enthält eine Reihe von Skalierbarkeitsrichtlinien, die von Microsoft unter Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008 getestet wurden:

  - Größe aller replizierten Dateien auf einem Server: 10 Terabytes  
      
  - Anzahl der replizierten Dateien auf einem Volume: 11 Millionen  
      
  - Maximale Dateigröße: 64 Gigabytes  
      


> [!NOTE]
> Die Anzahl von Replikationsgruppen, replizierten Ordnern, Verbindungen oder Mitgliedern von Replikationsgruppen ist nicht mehr begrenzt. 
<br>


Eine Liste der Skalierbarkeitsrichtlinien, die von Microsoft für Windows Server 2003 R2 getestet wurden, findest du im Thema zu [Skalierbarkeitsrichtlinien für die DFS-Replikation](https://go.microsoft.com/fwlink/?linkid=75043) (https://go.microsoft.com/fwlink/?LinkId=75043).

### <a name="when-should-i-not-use-dfs-replication"></a>Wann sollte die DFS-Replikation nicht verwendet werden?

Verwende die DFS-Replikation nicht in einer Umgebung, in der mehrere Benutzer dieselben Dateien auf unterschiedlichen Servern gleichzeitig aktualisieren oder ändern. Dies kann dazu führen, dass in Konflikt stehende Kopien der Dateien bei der DFS-Replikation in den ausgeblendeten Ordner „DfsrPrivate\\ConflictandDeleted“ verschoben werden.

Wenn mehrere Benutzer dieselben Dateien auf unterschiedlichen Servern gleichzeitig ändern müssen, verwende die Funktion zum Auschecken von Dateien von Windows SharePoint Services, um sicherzustellen, dass nur ein Benutzer an einer Datei arbeitet. Windows SharePoint Services 2.0 mit Service Pack 2 ist als Teil von Windows Server 2003 R2 verfügbar. Windows SharePoint Services kann von der Microsoft-Website heruntergeladen werden. In neueren Versionen von Windows Server ist die Lösung nicht enthalten.

### <a name="why-is-a-schema-update-required-for-dfs-replication"></a>Warum ist für die DFS-Replikation eine Schemaaktualisierung erforderlich?

Bei der DFS-Replikation werden neue Objekte im Domänennamenkontext von Active Directory Domain Services verwendet, um Konfigurationsinformationen zu speichern. Diese Objekte werden erstellt, wenn Sie das Schema der Active Directory-Domänendienste aktualisieren. Weitere Informationen findest du im Thema zum [Überprüfen der Anforderungen für die DFS-Replikation](https://go.microsoft.com/fwlink/?linkid=182264) (https://go.microsoft.com/fwlink/?LinkId=182264).

## <a name="monitoring-and-management-tools"></a>Überwachungs- und Verwaltungstools

### <a name="can-i-automate-the-health-report-to-receive-warnings"></a>Kann ich den Integritätsbericht automatisieren, um Warnungen zu erhalten?

Ja. Es gibt drei Möglichkeiten, Integritätsberichte zu automatisieren:

  - Verwende das in Windows Server 2012 R2 enthaltene DFSR Windows PowerShell-Modul oder „DfsrAdmin.exe“ zusammen mit „Geplante Aufgaben“, um regelmäßig Integritätsberichte zu generieren. Weitere Informationen findest du im Thema zum [Automatisieren von Integritätsberichten der DFS-Replikation](https://go.microsoft.com/fwlink/?linkid=74010) (https://go.microsoft.com/fwlink/?LinkId=74010).  
      
  - Verwende das DFS Replication Management Pack für System Center Operations Manager, um Warnungen zu erstellen, die auf bestimmten Bedingungen basieren.  
      
  - Verwende den WMI-Anbieter für die DFS-Replikation, um Skripts für Warnungen zu schreiben.  
      

### <a name="can-i-use-microsoft-system-center-operations-manager-to-monitor-dfs-replication"></a>Kann ich die DFS-Replikation mit Microsoft System Center Operations Manager überwachen?

Ja. Weitere Informationen findest du unter dem [DFS Replication Management Pack für System Center Operations Manager 2007](https://go.microsoft.com/fwlink/?linkid=182265) im Microsoft Download Center (https://go.microsoft.com/fwlink/?LinkId=182265).

### <a name="does-dfs-replication-support-remote-management"></a>Unterstützt die DFS-Replikation die Remoteverwaltung?

Ja. Die DFS-Replikation unterstützt die Remoteverwaltung über die DFS-Verwaltungskonsole und den Befehl **Replikationsgruppe hinzufügen**. Beispielsweise kannst du auf Server A eine Verbindung mit einer Replikationsgruppe herstellen, die in der Gesamtstruktur mit den Servern A und B als Mitgliedern definiert ist.

Die DFS-Verwaltung ist in Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 und Windows Server 2003 R2 enthalten. Um die DFS-Replikation in anderen Windows-Versionen zu verwalten, verwende Remotedesktop oder die [Remoteserver-Verwaltungstools für Windows 7](https://technet.microsoft.com/library/Ee449475).


> [!IMPORTANT]
> Zum Anzeigen oder Verwalten von Replikationsgruppen, die schreibgeschützte replizierte Ordner oder Mitglieder enthalten, die Failovercluster sind, musst du die Version der DFS-Verwaltung verwenden, die in Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, den <a href="https://go.microsoft.com/fwlink/p/?linkid=238560">Remoteserver-Verwaltungstools für Windows 8</a> oder den <a href="https://technet.microsoft.com/library/ee449475">Remoteserver-Verwaltungstools für Windows 7</a> enthalten ist. 
<br>


### <a name="do-ultrasound-and-sonar-work-with-dfs-replication"></a>Werden Ultrasound und Sonar von der DFS-Replikation unterstützt?

Nein Die DFS-Replikation verfügt über eigene Überwachungs- und Diagnosetools. Mit Ultrasound und Sonar kann nur FRS überwacht werden.

### <a name="how-can-files-be-recovered-from-the-conflictanddeleted-or-preexisting-folders"></a>Wie können Dateien aus den Ordnern „ConflictAndDeleted“ oder „PreExisting“ wiederhergestellt werden?

Um verlorene Dateien wiederherzustellen, müssen sie aus dem Dateisystemordner oder freigegebenen Ordner mithilfe des Dateiversionsverlaufs, des Befehls **Vorgängerversionen wiederherstellen** im Datei-Explorer oder durch die Wiederherstellung aus einer Sicherung wiederhergestellt werden. Um Dateien direkt aus dem Ordner „ConflictAndDeleted“ oder „PreExisting“ wiederherzustellen, verwende die Windows PowerShell-Cmdlets `Get-DfsrPreservedFiles` und `Restore-DfsrPreservedFiles` (aus dem DFSR-Modul in Windows Server 2012 R2) oder das Beispielskript [RestoreDFSR](https://code.msdn.microsoft.com/restoredfsr) aus der MSDN Code Gallery. Dieses Skript ist nur für die Notfallwiederherstellung vorgesehen und wird „wie besehen“ ohne Garantie zur Verfügung gestellt.

### <a name="is-there-a-way-to-know-the-state-of-replication"></a>Gibt es eine Möglichkeit, den Status der Replikation zu erkennen?

Ja. Es gibt eine Reihe von Möglichkeiten, die Replikation zu überwachen:

  - Die DFS-Replikation verfügt über ein Management Pack für System Center Operations Manager, das eine proaktive Überwachung ermöglicht.  
      
  - Die DFS-Verwaltung verfügt über einen integrierten Diagnosebericht, der Aufschluss über das Replikations-Rückstandsprotokoll, die Replikationseffizienz und die Anzahl der Dateien und Ordner in einer bestimmten Replikationsgruppe gibt.  
      
  - Das DFSR Windows PowerShell-Modul in Windows Server 2012 R2 umfasst Cmdlets zum Starten von Propagierungstests und zum Schreiben von Propagierungs- und Integritätsberichten. Weitere Informationen findest du im Thema zu [DFSR (Distributed File System Replication)-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/dn296601.aspx).  
      
  - „Dfsrdiag.exe“ ist ein Befehlszeilentool, mit dem die Anzahl der noch nicht verarbeiteten Dateien generiert oder ein Propagierungstest ausgelöst werden kann. In beiden Fällen wird der Status der Replikation angegeben. An der Propagierung ist erkennbar, ob Dateien auf alle Knoten repliziert werden. Im Rückstandsprotokoll ist angegeben, wie viele Dateien noch repliziert werden müssen, bis zwei Computer synchron sind. Die Anzahl im Rückstandsprotokoll entspricht der Anzahl von Aktualisierungen, die von einem Mitglied einer Replikationsgruppe noch nicht verarbeitet wurden. Auf Computern mit Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 können mithilfe von „Dfsrdiag.exe“ auch die Aktualisierungen angezeigt werden, die von der DFS-Replikation momentan repliziert werden.  
      
  - Mithilfe von WMI können Rückstandsprotokollinformationen – manuell oder über MOM – in Skripts erfasst werden.  
      

## <a name="performance"></a>Leistung

### <a name="does-dfs-replication-support-dial-up-connections"></a>Unterstützt die DFS-Replikation DFÜ-Verbindungen?

Obwohl die DFS-Replikation bei DFÜ-Geschwindigkeit funktioniert, kann es zu einem Rückstand kommen, wenn eine große Anzahl von Änderungen repliziert werden muss. Bei geringfügigen Änderungen an vorhandenen Dateien bietet die DFS-Replikation mit Remotedifferenzialkomprimierung (Remote Differential Compression, RDC) eine wesentlich höhere Leistung als das direkte Kopieren der Datei.

### <a name="does-dfs-replication-perform-bandwidth-sensing"></a>Verfügt die DFS-Replikation über eine Bandbreitenerkennung?

Nein Bei der DFS-Replikation wird keine Bandbreitenerkennung durchgeführt. Du kannst die DFS-Replikation so konfigurieren, dass pro Verbindung eine begrenzte Bandbreite verwendet wird (Bandbreiteneinschränkung). Allerdings wird die Bandbreitennutzung von der DFS-Replikation nicht weiter reduziert, wenn die Netzwerkschnittstelle ausgelastet ist. Außerdem kann die Verbindung durch die DFS-Replikation kurzzeitig ausgelastet werden. Bei der DFS-Replikation handelt es sich nicht exakt um eine Bandbreiteneinschränkung, da die Bandbreite bei der DFS-Replikation durch die Begrenzung von RPC-Aufrufen eingeschränkt wird. Daher können verschiedene Puffer auf tieferen Ebenen des Netzwerkstapels (einschließlich RPC) Probleme verursachen, wodurch Bursts im Netzwerkdatenverkehr entstehen.

### <a name="does-dfs-replication-throttle-bandwidth-per-schedule-per-server-or-per-connection"></a>Wird die Bandbreite bei der DFS-Replikation pro Zeitplan, pro Server oder pro Verbindung eingeschränkt?

Wenn du die Bandbreiteneinschränkung bei der Angabe des Zeitplans konfigurierst, wird diese Einstellung für alle Verbindungen dieser Replikationsgruppe genutzt, um die Bandbreite einzuschränken. Die Bandbreiteneinschränkung kann in der DFS-Verwaltung auch mit einer Einstellung auf Verbindungsebene festgelegt werden.

### <a name="does-dfs-replication-use-active-directory-domain-services-to-calculate-site-links-and-connection-costs"></a>Werden bei der DFS-Replikation Active Directory Domain Services verwendet, um die Kosten für Standortverknüpfungen und Verbindungen zu berechnen?

Nein Bei der DFS-Replikation wird die vom Administrator definierte Topologie verwendet, die unabhängig von den Standortkosten von Active Directory Domain Services ist.

### <a name="how-can-i-improve-replication-performance"></a>Wie kann ich die Replikationsleistung verbessern?

Informationen über die verschiedenen Methoden zum Optimieren der Replikationsleistung findest du im Thema zum [Optimieren der Replikationsleistung in DFSR](https://blogs.technet.com/b/askds/archive/2010/03/31/tuning-replication-performance-in-dfsr-especially-on-win2008-r2.aspx) im Blog [Ask the Directory Services Team](https://blogs.technet.com/b/askds/).

### <a name="how-does-dfs-replication-avoid-saturating-a-connection"></a>Wie lässt sich vermeiden, dass eine Verbindung durch die DFS-Replikation vollständig ausgelastet wird?

Bei der DFS-Replikation legst du die maximale Bandbreite fest, die für eine Verbindung verwendet werden soll, und der Dienst nutzt das Netzwerk bis zu diesem Level. Dies unterscheidet sich vom intelligenten Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS). Bei der DFS-Replikation wird die Verbindung nicht vollständig ausgelastet, wenn du die geeignete Einstellung festgelegt hast.

Trotzdem ist die Bandbreiteneinschränkung nicht zu 100 % genau, sodass die Verbindung von der DFS-Replikation kurzzeitig ausgelastet werden kann. Dies liegt daran, dass die Bandbreiteneinschränkung bei der DFS-Replikation durch die Einschränkung der RPC-Aufrufe erfolgt. Da dieser Prozess von verschiedenen Puffern auf tieferen Ebenen des Netzwerkstapels, einschließlich RPC, abhängig ist, wird der Replikationsdatenverkehr tendenziell in Bursts übertragen, wodurch die Netzwerkverbindungen zeitweise vollständig ausgelastet werden können.

Die DFS-Replikation in Windows Server 2008 umfasst mehrere Leistungsverbesserungen, die im Thema [Verteiltes Dateisystem](https://technet.microsoft.com/library/Cc753479) unter [Änderungen an der Funktionalität zwischen Windows Server 2003 SP1 und Windows Server 2008](https://technet.microsoft.com/library/cc753208) erläutert werden.

### <a name="how-does-dfs-replication-performance-compare-with-frs"></a>Welche Leistung bietet die DFS-Replikation im Vergleich mit FRS?

Die DFS-Replikation ist viel schneller als FRS, und zwar insbesondere dann, wenn kleine Änderungen an großen Dateien vorgenommen werden und RDC aktiviert ist. Mit RDC kann eine kleine Änderung an einer PowerPoint&reg;-Präsentation von 2 MB beispielsweise bewirken, dass nur 60 KB über das Netzwerk gesendet werden, was eine Einsparung von 97 Prozent an übertragenen Bytes bedeutet.

RDC wird bei Dateien unter 64 KB nicht verwendet und bietet bei Hochgeschwindigkeits-LANs, bei denen die Netzwerkbandbreite nicht begrenzt ist, u. U. keine Vorteile. RDC kann mithilfe der DFS-Verwaltung jeweils verbindungsbasiert deaktiviert werden.

### <a name="how-frequently-does-dfs-replication-replicate-data"></a>Wie häufig werden Daten von der DFS-Replikation repliziert?

Die Daten werden nach dem von dir festgelegten Zeitplan repliziert. Beispielsweise kannst du den Zeitplan auf 15-Minuten-Intervalle an sieben Tage die Woche festlegen. In diesen Intervallen ist die Replikation aktiviert. Die Replikation wird zeitnah gestartet, nachdem eine Dateiänderung erkannt wurde (in der Regel innerhalb von Sekunden).

Der Zeitplan für die Replikationsgruppe kann in koordinierter Weltzeit festgelegt werden, während für den Verbindungszeitplan die lokale Zeit des empfangenden Mitglieds gelten kann. Dies muss berücksichtigt werden, wenn sich die Replikationsgruppe über mehrere Zeitzonen erstreckt. Bei der lokalen Zeit handelt es sich um die Ortszeit des Mitglieds, das die eingehende Verbindung hostet. Der angezeigte Zeitplan der eingehenden Verbindung und der entsprechenden ausgehenden Verbindung spiegeln die Zeitzonenunterschiede wider, wenn der Zeitplan auf die lokale Zeit festgelegt ist.

### <a name="how-much-of-my-servers-system-resources-will-dfs-replication-consume"></a>Wie viele Serversystemressourcen werden von der DFS-Replikation genutzt?

Die von der DFS-Replikation genutzten Datenträger-, Arbeitsspeicher- und CPU-Ressourcen hängen von verschiedenen Faktoren ab, einschließlich der Anzahl und Größe der Dateien, der Anzahl der Replikationsgruppenmitglieder und replizierter Ordner und der Änderungsrate. Außerdem sind einige Ressourcen schwerer einzuschätzen. Beispielsweise kann die für die DFS-Replikationsdatenbank verwendete ESE (Extensible Storage Engine)-Technologie einen hohen Prozentsatz des verfügbaren Arbeitsspeichers beanspruchen, der bei Bedarf freigegeben wird. Andere Anwendungen als die DFS-Replikation können abhängig von der Serverkonfiguration auf demselben Server gehostet werden. Wenn jedoch mehrere Anwendungen oder Serverrollen auf einem einzelnen Server gehostet werden, ist es wichtig, diese Konfiguration zu testen, bevor sie in einer Produktionsumgebung implementiert wird.

### <a name="what-happens-if-a-wan-link-fails-during-replication"></a>Was geschieht, wenn eine WAN-Verbindung während der Replikation ausfällt?

Wenn die Verbindung ausfällt, versucht die DFS-Replikation, den Vorgang fortzusetzen, während der Zeitplan offen ist. Es gibt auch Verbindungsfehler, die im Ereignisprotokoll der DFS-Replikation aufgezeichnet werden. Die Protokollereignisse können mithilfe von MOM proaktiv (in Form von Warnungen) ausgegeben werden und mithilfe des Integritätsberichts der DFS-Replikation reaktiv genutzt werden (z. B. wenn der Bericht von einem Administrator ausgeführt wird).

## <a name="remote-differential-compression-details"></a>Remotedifferenzialkomprimierung – Details

### <a name="are-changes-compressed-before-being-replicated"></a>Werden die Änderungen vor dem Replizieren komprimiert?

Ja. Geänderte Teile von Dateien werden vor dem Senden komprimiert. Dies gilt für alle Dateitypen mit Ausnahme der folgenden (die bereits komprimiert sind): WMA, WMV, ZIP, JPG, MPG, MPEG, M1V, MP2, MP3, MPA, CAB, WAV, SND, AU, ASF, WM, AVI, Z, GZ, TGZ und FRX. Die Komprimierungseinstellungen für diese Dateitypen können nicht in Windows Server 2003 R2 konfiguriert werden.

### <a name="can-an-administrator-turn-off-rdc-or-change-the-threshold"></a>Kann ein Administrator RDC deaktivieren oder den Schwellenwert ändern?

Ja. Du kannst RDC über die Eigenschaftenseite der jeweiligen Verbindung deaktivieren. Durch die Deaktivierung von RDC können die CPU-Auslastung und die Replikationswartezeit bei schnellen lokalen Netzwerkverbindungen (LAN) reduziert werden, die keine Bandbreiteneinschränkungen aufweisen, oder bei Replikationsgruppen, die primär aus Dateien unter 64 KB bestehen. Wenn RDC für eine Verbindung deaktiviert wird, sollte die Effizienz der Replikation vor und nach der Änderung getestet werden, um zu sicherzustellen, dass die Replikationsleistung verbessert wurde.

Du kannst den Schwellenwert für die RDC-Größe ändern, indem du den Befehl **Dfsradmin Connection Set** oder den WMI-Anbieter der DFS-Replikation verwendest oder die XML-Konfigurationsdatei manuell bearbeitest.

### <a name="does-rdc-work-on-all-file-types"></a>Funktioniert RDC für alle Dateitypen?

Ja. Von RDC werden Unterschiede auf der Blockebene unabhängig vom Datentyp der Datei berechnet. RDC funktioniert bei bestimmten Dateitypen jedoch effizienter, z. B. bei Word-Dokumenten, PST-Dateien und VHD-Images.

### <a name="how-does-rdc-work-on-a-compressed-file"></a>Wie funktioniert RDC bei einer komprimierten Datei?

Die DFS-Replikation nutzt RDC, wodurch die geänderten Blöcke in der Datei berechnet und nur diese Blöcke über das Netzwerk gesendet werden. Die DFS-Replikation benötigt keine Informationen zum Inhalt der Datei, sondern lediglich dazu, welche Blöcke geändert wurden.

### <a name="is-cross-file-rdc-enabled-when-upgrading-to-windows-server-enterprise-edition-or-datacenter-edition"></a>Wird die dateiübergreifende RDC beim Upgrade auf Windows Server Enterprise Edition oder Datacenter Edition aktiviert?

Die Standard-Editionen von Windows Server unterstützen keine dateiübergreifenden RDC. Allerdings wird sie automatisch aktiviert, wenn du ein Upgrade auf eine Edition durchführst, die die dateiübergreifende RDC unterstützt, oder wenn von einem Mitglied der Replikationsverbindung eine unterstützte Edition ausgeführt wird. Eine Liste der Editionen, die die dateiübergreifende RDC unterstützen, findest du unter „Which editions of the Windows operating system support cross-file RDC“ (Welche Editionen des Windows-Betriebssystems unterstützen die dateiübergreifende RDC)?

### <a name="is-rdc-true-block-level-replication"></a>Ist RDC eine echte Replikation auf Blockebene?

Nein RDC ist ein universelles Protokoll zum Komprimieren der Dateiübertragung. Die DFS-Replikation nutzt RDC für Blöcke auf Dateiebene und nicht auf Datenträgerebene. RDC unterteilt eine Datei in Blöcke. Für jeden Block in einer Datei wird eine Signatur berechnet, bei der es sich um eine kleine Anzahl von Bytes handelt, die den größeren Block darstellen können. Der Signatursatz wird vom Server auf den Client übertragen. Der Client vergleicht die Serversignaturen mit seinen eigenen. Anschließend fordert der Client den Server auf, nur die Daten für Signaturen zu senden, die noch nicht auf dem Client enthalten sind.

### <a name="what-happens-if-i-rename-a-file"></a>Was geschieht, wenn ich eine Datei umbenenne?

Bei der DFS-Replikation wird die Datei während der nächsten Replikation auf allen anderen Mitgliedern der Replikationsgruppe umbenannt. Dateien werden mithilfe einer eindeutigen ID nachverfolgt. Daher hat das Umbenennen einer Datei und das Verschieben der Datei innerhalb des Replikats keine Auswirkungen auf die Fähigkeit der DFS-Replikation, eine Datei zu replizieren.

### <a name="what-is-cross-file-rdc"></a>Was ist die dateiübergreifende RDC?

Die dateiübergreifende Remotedifferenzialkomprimierung (RDC) ermöglicht der DFS-Replikation die Verwendung der RDC auch dann, wenn auf der Clientseite keine Datei mit demselben Namen vorhanden ist. Die dateiübergreifende RDC nutzt eine Heuristik, um Dateien zu ermitteln, die der zu replizierenden Datei ähneln, und verwendet Blöcke der ähnlicher Dateien, die mit der replizierten Datei identisch sind, um die über das WAN übertragene Datenmenge zu minimieren. Die dateiübergreifende RDC kann in diesem Prozess Blöcke von bis zu fünf ähnlichen Dateien verwenden.

Um die dateiübergreifende RDC zu verwenden, muss von einem Mitglied der Replikationsverbindung eine Edition von Windows ausgeführt werden, die die dateiübergreifende RDC unterstützt. Eine Liste der Editionen, die die dateiübergreifende RDC unterstützen, findest du unter „Which editions of the Windows operating system support cross-file RDC“ (Welche Editionen des Windows-Betriebssystems unterstützen die dateiübergreifende RDC)?

### <a name="what-is-rdc"></a>Was ist RDC?

Die Remotedifferenzialkomprimierung (Remote Differential Compression, RDC) ist ein Client/Server-Protokoll, das zum effizienten Aktualisieren von Dateien über ein Netzwerk mit eingeschränkter Bandbreite verwendet werden kann. RDC erkennt, ob Daten in Dateien eingefügt, anders angeordnet oder entfernt wurden, sodass von der DFS-Replikation nur die Änderungen repliziert werden können, nachdem Dateien aktualisiert wurden. RDC wird standardmäßig nur für Dateien ab 64 KB verwendet. RDC kann eine ältere Version einer Datei mit demselben Namen im replizierten Ordner oder im Ordner „DfsrPrivate\\ConflictandDeleted“ (unter dem lokalen Pfad des replizierten Ordners) verwenden.

### <a name="when-is-rdc-used-for-replication"></a>Wann wird RDC für die Replikation verwendet?

RDC wird verwendet, wenn die Dateigröße einen Mindestschwellenwert überschreitet. Der Schwellenwert für die Größe beträgt standardmäßig 64 KB. Nachdem eine Datei, die diesen Schwellenwert überschreitet, repliziert wurde, wird für aktualisierte Versionen der Datei immer RDC verwendet, es sei denn, ein großer Teil der Datei wurde geändert oder RDC ist deaktiviert.

### <a name="which-editions-of-the-windows-operating-system-support-cross-file-rdc"></a>Welche Editionen des Windows-Betriebssystems unterstützen die dateiübergreifende RDC?

Um die dateiübergreifende RDC zu verwenden, muss von einem Mitglied der Replikationsverbindung eine Edition des Windows-Betriebssystems ausgeführt werden, die die dateiübergreifende RDC unterstützt. Die folgende Tabelle veranschaulicht, welche Editionen des Windows-Betriebssystems die dateiübergreifende RDC unterstützen.

### <a name="cross-file-rdc-availability-in-editions-of-the-windows-operating-system"></a>Editionen des Windows-Betriebssystems, in denen die dateiübergreifende RDC verfügbar ist

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
<td><p>Windows Server 2012 R2</p></td>
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

\* Die dateiübergreifende RDC kann unter Windows Server 2012 R2 optional deaktiviert werden.

## <a name="replication-details"></a>Replikation – Details

### <a name="can-i-change-the-path-for-a-replicated-folder-after-it-is-created"></a>Kann ich den Pfad für einen replizierten Ordner nach der Erstellung ändern?

Nein Wenn du den Pfad eines replizierten Ordners ändern möchtest, musst du ihn in der DFS-Verwaltung löschen und als neuen replizierten Ordner wieder hinzufügen. Anschließend nutzt die DFS-Replikation die Remotedifferenzialkomprimierung (RDC), um eine Synchronisierung auszuführen und zu ermitteln, ob die Daten auf den sendenden und empfangenden Mitgliedern identisch sind. Es werden nicht alle Daten im Ordner erneut repliziert.

### <a name="can-i-configure-which-file-attributes-are-replicated"></a>Kann ich konfigurieren, welche Dateiattribute repliziert werden?

Nein. Du kannst nicht konfigurieren, welche Dateiattribute von der DFS-Replikation repliziert werden.

Eine Liste der Attributwerte und deren Beschreibungen findest du unter [Dateiattribute](https://go.microsoft.com/fwlink/?linkid=182268) auf MSDN (https://go.microsoft.com/fwlink/?LinkId=182268).

Die folgenden Attributwerte werden mithilfe der `SetFileAttributes dwFileAttributes`-Funktion festgelegt und durch die DFS-Replikation repliziert. Durch Änderungen an diesen Attributwerten wird die Replikation der Attribute ausgelöst. Der Inhalt der Datei wird erst repliziert, wenn sich der Inhalt ebenfalls ändert. Weitere Informationen findest du unter der [SetFileAttributes-Funktion](https://go.microsoft.com/fwlink/?linkid=182269) in der MSDN Library (https://go.microsoft.com/fwlink/?LinkId=182269).

  - FILE\_ATTRIBUTE\_HIDDEN  
      
  - FILE\_ATTRIBUTE\_READONLY  
      
  - FILE\_ATTRIBUTE\_SYSTEM  
      
  - FILE\_ATTRIBUTE\_NOT\_CONTENT\_INDEXED  
      
  - FILE\_ATTRIBUTE\_OFFLINE  
      

Die folgenden Attributwerte werden durch die DFS-Replikation repliziert, lösen aber keine Replikation aus.

  - FILE\_ATTRIBUTE\_ARCHIVE  
      
  - FILE\_ATTRIBUTE\_NORMAL  
      

Die folgenden Dateiattributwerte lösen ebenfalls eine Replikation aus, obwohl sie nicht mit der `SetFileAttributes`-Funktion festgelegt werden können. (Verwende die `GetFileAttributes`-Funktion, um die Attributwerte anzuzeigen.)

  - FILE\_ATTRIBUTE\_REPARSE\_POINT  
      

> [!NOTE]
> Von der DFS-Replikation werden keine Analysepunkt-Attributwerte repliziert, es sei denn, die Analysenkennung lautet IO_REPARSE_TAG_SYMLINK. Dateien mit den Analysenkennungen IO_REPARSE_TAG_DEDUP, IO_REPARSE_TAG_SIS oder IO_REPARSE_TAG_HSM werden als normale Dateien repliziert. Die Analysenkennung und die Analysedatenpuffer werden jedoch nicht auf andere Server repliziert, da der Analysepunkt nur auf dem lokalen System funktioniert. 
<br>

  - FILE\_ATTRIBUTE\_COMPRESSED  
      
  - FILE\_ATTRIBUTE\_ENCRYPTED  
      

> [!NOTE]
> Von der DFS-Replikation werden keine Dateien repliziert, die mit dem verschlüsselnden Dateisystem (Encrypting File System, EFS) verschlüsselt wurden. Von der DFS-Replikation werden Dateien repliziert, die mit einer Software verschlüsselt wurden, die nicht von Microsoft stammt. Dies trifft jedoch nur zu, wenn kein Attributwert FILE_ATTRIBUTE_ENCRYPTED für die Datei festgelegt wird. 
<br>

  - FILE\_ATTRIBUTE\_SPARSE\_FILE  
      
  - FILE\_ATTRIBUTE\_DIRECTORY  
      

Der Wert FILE\_ATTRIBUTE\_TEMPORARY wird von der DFS-Replikation nicht repliziert.

### <a name="can-i-control-which-member-is-replicated"></a>Kann ich steuern, welches Mitglied repliziert wird?

Ja. Beim Erstellen einer Replikationsgruppe kann eine Topologie ausgewählt werden. Alternativ kannst du **Keine Topologie** auswählen und Verbindungen nach der Erstellung der Replikationsgruppe manuell konfigurieren.

### <a name="can-i-seed-a-replication-group-member-with-data-prior-to-the-initial-replication"></a>Kann ich für ein Replikationsgruppenmitglied vor der ersten Replikation ein Datenseeding ausführen?

Ja. Die DFS-Replikation unterstützt vor der ersten Replikation das Kopieren von Dateien auf ein Replikationsgruppenmitglied. Diese „Vorabbereitstellung“ kann die während der ersten Replikation replizierte Datenmenge erheblich reduzieren.

Bei der ersten Replikation müssen keine Inhalte repliziert werden, wenn sich Dateien nur durch reale Attribute oder Zeitstempel unterscheiden. Ein reales Attribut ist ein Attribut, das durch die Win32-Funktion `SetFileAttributes` festgelegt werden kann. Weitere Informationen findest du unter der [SetFileAttributes-Funktion](https://go.microsoft.com/fwlink/?linkid=182269) in der MSDN Library (https://go.microsoft.com/fwlink/?LinkId=182269). Wenn sich zwei Dateien durch andere Attribute unterscheiden, z. B. die Komprimierung, wird der Inhalt der Datei repliziert.

Um ein Replikationsgruppenmitglied vorab bereitzustellen, müssen die Dateien in den entsprechenden Ordner auf den Zielservern kopiert, die Replikationsgruppe erstellt und dann ein primäres Mitglied ausgewählt werden. Wähle das Mitglied mit den aktuellsten Dateien aus, die repliziert werden sollen, da der Inhalt des primären Mitglieds als „autoritativ“ betrachtet wird. Das bedeutet, dass andere Versionen der Dateien auf anderen Mitgliedern der Replikationsgruppe während der ersten Replikation immer durch die Dateien des primären Mitglieds überschrieben werden.

Informationen dazu, wie du ein Vorab-Seeding für die DFSR-Datenbank ausführst und diese klonst, findest du unter [DFS Replication Initial Sync in Windows Server 2012 R2: Attack of the Clones](https://blogs.technet.com/b/filecab/archive/2013/08/21/dfs-replication-initial-sync-in-windows-server-2012-r2-attack-of-the-clones.aspx) (Erste Synchronisierung bei der DFS-Replikation in Windows Server 2012 R2: Angriff der Klone).

Weitere Informationen zur ersten Replikation findest du unter [Erstellen einer Replikationsgruppe](https://technet.microsoft.com/library/cc725893).

### <a name="does-dfs-replication-overcome-common-file-replication-service-issues"></a>Lassen sich mit der DFS-Replikation allgemeine Probleme des Dateireplikationsdiensts beheben?

Ja. Die DFS-Replikation hilft, drei häufige FRS-Probleme zu lösen:

  - Journalumbrüche: Die DFS-Replikation wird nach Journalumbrüchen zeitnah wiederhergestellt. Jede vorhandene Datei oder jeder vorhandene Ordner wird als „journalWrap“ gekennzeichnet und gegenüber dem Dateisystem überprüft, bevor die Replikation erneut aktiviert wird. Während der Wiederherstellung ist dieses Volume für die Replikation in keiner Richtung verfügbar.  
      
  - Übermäßige Replikation: Zur Vermeidung einer übermäßigen Replikation verwendet die DFS-Replikation ein Guthabensystem.  
      
  - Änderung von Ordnernamen: Um die Änderung von Ordnernamen zu verhindern, werden in Konflikt stehende Daten von der DFS-Replikation in einem ausgeblendeten Ordner namens „DfsrPrivate\\ConflictandDeleted“ (unter dem lokalen Pfad des replizierten Ordners) gespeichert. Beispiel: Wenn gleichzeitig mehrere Ordner mit identischen Namen auf unterschiedlichen Servern erstellt werden, die mit FRS repliziert werden, werden die älteren Ordner durch FRS umbenannt. Bei der DFS-Replikation werden die älteren Ordner stattdessen in den lokalen Ordner „ConflictandDeleted“ verschoben.  
      

### <a name="does-dfs-replication-replicate-files-in-chronological-order"></a>Werden Dateien von der DFS-Replikation in chronologischer Reihenfolge repliziert?

Nein Dateien können in einer zufälligen Reihenfolge repliziert werden.

### <a name="does-dfs-replication-replicate-files-that-are-being-used-by-another-application"></a>Werden von der DFS-Replikation Dateien repliziert, die von einer anderen Anwendung verwendet werden?

Wenn eine Datei von einer Anwendung geöffnet und gesperrt wird (um zu verhindern, dass sie von anderen Anwendungen verwendet wird, während sie geöffnet ist), wird die Datei erst von der DFS-Replikation repliziert, nachdem sie geschlossen wurde. Wenn die Datei von der Anwendung mit Lesezugriff für Freigaben geöffnet wird, kann die Datei trotzdem repliziert werden.

### <a name="does-dfs-replication-replicate-ntfs-file-permissions-alternate-data-streams-hard-links-and-reparse-points"></a>Werden von der DFS-Replikation NTFS-Dateiberechtigungen, alternative Datenströme, feste Links und Analysepunkte repliziert?

  - Die DFS-Replikation repliziert NTFS-Dateiberechtigungen und alternative Datenströme.  
      
  - Microsoft bietet keine Unterstützung für das Erstellen fester NTFS-Links zu oder von Dateien in einem replizierten Ordner. Dies kann zu Replikationsproblemen bei den betroffenen Dateien führen. Fest verknüpfte Dateien werden von der DFS-Replikation ignoriert und nicht repliziert. Verknüpfungspunkte werden auch nicht repliziert, und bei der DFS-Replikation wird für jeden gefundenen Verknüpfungspunkt das Ereignis 4406 protokolliert.  
      
  - Die einzigen von der DFS-Replikation replizierten Analysepunkte sind diejenigen, die die Kennung IO\_REPARSE\_TAG\_SYMLINK verwenden. Die DFS-Replikation gewährleistet jedoch nicht, dass das Ziel eines Symlinks ebenfalls repliziert wird. Weitere Informationen findest du im Blog [Ask the Directory Services Team](https://blogs.technet.com/b/askds/archive/2011/09/30/friday-mail-sack-super-slo-mo-edition.aspx).  
      
  - Dateien mit der Analysenkennung IO\_REPARSE\_TAG\_DEDUP, IO\_REPARSE\_TAG\_SIS oder IO\_REPARSE\_TAG\_HSM werden als normale Dateien repliziert. Die Analysenkennung und die Analysedatenpuffer werden nicht auf andere Server repliziert, da der Analysepunkt nur auf dem lokalen System funktioniert. Im eigentlichen Sinne können mit der DFS-Replikation Ordner auf Volumes repliziert werden, die die Datendeduplizierung in Windows Server 2012 oder die Einzelinstanz-Speicherung (Single Instance Storage, SIS) verwenden. Allerdings werden Informationen zur Datendeduplizierung von jedem Server, auf dem der Rollendienst aktiviert ist, separat verwaltet.  
      

### <a name="does-dfs-replication-replicate-timestamp-changes-if-no-other-changes-are-made-to-the-file"></a>Werden Zeitstempeländerungen von der DFS-Replikation repliziert, wenn keine anderen Änderungen an der Datei vorgenommen wurden?

Nein. Bei der DFS-Replikation werden keine Dateien repliziert, bei denen sich lediglich der Zeitstempel geändert hat. Außerdem wird der geänderte Zeitstempel nicht auf andere Mitglieder der Replikationsgruppe repliziert, es sei denn, es wurden andere Änderungen an der Datei vorgenommen.

### <a name="does-dfs-replication-replicate-updated-permissions-on-a-file-or-folder"></a>Werden von der DFS-Replikation aktualisierte Berechtigungen für eine Datei oder einen Ordner repliziert?

Ja. Bei der DFS-Replikation werden geänderte Berechtigungen für Dateien und Ordner repliziert. Es wird nur der Teil der Datei repliziert, der der Zugriffssteuerungsliste (Access Control List, ACL) zugeordnet ist, obwohl bei der DFS-Replikation weiterhin die gesamte Datei in den Stagingbereich eingelesen werden muss.


> [!NOTE]
> Die Änderung von ACLs für eine große Anzahl von Dateien kann sich auf die Replikationsleistung auswirken. Bei Verwendung von RDC verhält sich die übertragene Datenmenge jedoch proportional zur Größe der ACLs und nicht zur Größe der gesamten Datei. Der Datenverkehr auf dem Datenträger verhält sich nach wie vor proportional zur Größe der Dateien, da die Dateien in den und aus dem Stagingordner gelesen werden müssen. 
<br>


### <a name="does-dfs-replication-support-merging-text-files-in-the-event-of-a-conflict"></a>Unterstützt die DFS-Replikation bei einem Konflikt das Zusammenführen von Textdateien?

Bei einem Konflikt werden keine Dateien von der DFS-Replikation zusammengeführt. Allerdings wird versucht, die ältere Version der Datei im ausgeblendeten Ordner „DfsrPrivate-Ordner\\ConflictandDeleted“ auf dem Computer beizubehalten, auf dem der Konflikt erkannt wurde.

### <a name="does-dfs-replication-use-encryption-when-transmitting-data"></a>Verwendet die DFS-Replikation die Verschlüsselung beim Übertragen von Daten?

Ja. Die DFS-Replikation nutzt RPC-Verbindungen (Remote Procedure Call, Remoteprozeduraufruf) mit Verschlüsselung.

### <a name="is-it-possible-to-disable-the-use-of-encrypted-rpc"></a>Ist es möglich, die Verwendung von verschlüsseltem RPC zu deaktivieren?

Nein Der DFS-Replikationsdienst verwendet Remoteprozeduraufrufe über TCP, um Daten zu replizieren. Um Datenübertragungen über das Internet zu schützen, ist der DFS-Replikationsdienst so konzipiert, dass immer die Konstante `RPC_C_AUTHN_LEVEL_PKT_PRIVACY` auf Authentifizierungsebene verwendet wird. Dadurch wird sichergestellt, dass die RPC-Kommunikation über das Internet immer verschlüsselt ist. Daher ist es nicht möglich, die Verwendung von verschlüsseltem RPC durch den DFS-Replikationsdienst zu deaktivieren.

Weitere Informationen findest du auf den folgenden Microsoft-Websites:

  - [Technische Referenz zu RPC](https://go.microsoft.com/fwlink/?linkid=182278)  
      
  - [Informationen zur Remotedifferenzialkomprimierung](https://go.microsoft.com/fwlink/?linkid=182279)  
      
  - [Konstanten auf Authentifizierungsebene](https://go.microsoft.com/fwlink/?linkid=182280)  
      

### <a name="how-are-simultaneous-replications-handled"></a>Wie werden gleichzeitige Replikationen verarbeitet?

Es gibt einen Aktualisierungs-Manager pro repliziertem Ordner. Aktualisierungs-Manager arbeiten unabhängig voneinander.

Standardmäßig werden maximal 16 (vier in Windows Server 2003 R2) gleichzeitige Downloads von allen Verbindungen und Replikationsgruppen gemeinsam genutzt. Da Verbindungen und Aktualisierungen an Replikationsgruppen nicht serialisiert werden, gibt es keine bestimmte Reihenfolge, in der Aktualisierungen empfangen werden. Wenn zwei Zeitpläne geöffnet sind, werden Aktualisierungen in der Regel über beide Verbindungen gleichzeitig empfangen und installiert.

### <a name="how-do-i-force-replication-or-polling"></a>Wie kann ich die Replikation oder den Abruf erzwingen?

Mithilfe der DFS-Verwaltung lässt sich die Replikation sofort erzwingen, wie unter [Bearbeiten von Replikationszeitplänen](https://technet.microsoft.com/library/Cc732278) beschrieben. Du kannst die Replikation auch mit dem `Sync-DfsReplicationGroup`-Cmdlet erzwingen, das in dem mit Windows Server 2012 R2 eingeführten DFSR PowerShell-Modul enthalten ist, oder mit dem Befehl **Dfsrdiag SyncNow**. Das Abrufen kann mit dem `Update-DfsrConfigurationFromAD`-Cmdlet oder dem Befehl **Dfsrdiag PollAD** erzwungen werden.

### <a name="is-it-possible-to-configure-a-quiet-time-between-replications-for-files-that-change-frequently"></a>Ist es möglich, für häufig geänderte Dateien eine Ruhezeit zwischen Replikationen zu konfigurieren?

Nein Wenn der Zeitplan geöffnet ist, werden von der DFS-Replikation Änderungen repliziert, sobald diese erkannt werden. Es gibt keine Möglichkeit, eine Ruhezeit für Dateien zu konfigurieren.

### <a name="is-it-possible-to-configure-one-way-replication-with-dfs-replication"></a>Bietet die DFS-Replikation die Möglichkeit, eine unidirektionale Replikation zu konfigurieren?

Ja. Bei Verwendung von Windows Server 2012 oder Windows Server 2008 R2 kannst du einen schreibgeschützten replizierten Ordner erstellen, von dem Inhalte über eine unidirektionale Verbindung repliziert werden. Weitere Informationen findest du unter [Aktivieren des Schreibschutzes für einen replizierten Ordner auf einem bestimmten Mitglied](https://go.microsoft.com/fwlink/?linkid=156740) (https://go.microsoft.com/fwlink/?LinkId=156740).

Das Erstellen einer unidirektionalen Replikationsverbindung bei Verwendung der DFS-Replikation in Windows Server 2008 oder Windows Server 2003 R2 wird nicht unterstützt. Dies kann zu zahlreichen Problemen führen, beispielsweise zu Topologiefehlern bei der Integritätsprüfung, Stagingproblemen und Problemen mit der DFS-Replikationsdatenbank.

Bei Verwendung von Windows Server 2008 oder Windows Server 2003 R2 lässt sich mithilfe der folgenden Schritte eine unidirektionale Verbindung simulieren:

  - Weise Administratoren an, Änderungen nur auf den Servern vorzunehmen, die als primäre Server fungieren sollen. Lasse die Änderungen dann auf die Zielserver replizieren.  
      
  - Konfiguriere die Freigabeberechtigungen auf den Zielservern so, dass Endbenutzer keine Schreibberechtigungen besitzen. Wenn auf den Teilstrukturservern keine Änderungen zulässig sind, müssen sie nicht zurück repliziert werden, wodurch eine unidirektionale Verbindung simuliert wird und die WAN-Auslastung gering bleibt.  
      

### <a name="is-there-a-way-to-force-a-complete-replication-of-all-files-including-unchanged-files"></a>Gibt es eine Möglichkeit, eine vollständige Replikation aller Dateien, einschließlich unveränderter Dateien, zu erzwingen?

Nein Wenn Dateien von der DFS-Replikation als identisch betrachtet werden, werden sie nicht repliziert. Wenn geänderte Dateien nicht repliziert wurden, werden sie automatisch repliziert, wenn die DFS-Replikation dafür konfiguriert ist. Um den konfigurierten Zeitplan außer Kraft zu setzen, verwende die WMI-Methode **ForceReplicate ()** . Dadurch wird jedoch nur der Zeitplan außer Kraft gesetzt, ohne dass die Replikation nicht geänderter oder identischer Dateien erzwungen wird.

### <a name="what-happens-if-the-primary-member-suffers-a-database-loss-during-initial-replication"></a>Was geschieht, wenn während der ersten Replikation die Verbindung zwischen dem primären Mitglied und der Datenbank getrennt wird?

Während der ersten Replikation haben Dateien des primären Mitglieds bei der Konfliktauflösung immer Vorrang. Diese findet statt, wenn die empfangenden Mitglieder auf dem primären Mitglied über abweichende Dateiversionen verfügen. Die Definition des primären Mitglieds wird in Active Directory Domain Services gespeichert und gelöscht, nachdem das primäre Mitglied für die Replikation bereit ist, aber bevor alle Mitglieder der Replikationsgruppe repliziert werden.

Wenn bei der ersten Replikation ein Fehler auftritt oder der DFS-Replikationsdienst während der Replikation neu gestartet wird, erkennt das primäre Mitglied die Definition des primären Mitglieds in der lokalen DFS-Replikationsdatenbank und wiederholt die erste Replikation. Wenn die Verbindung des primären Mitglieds mit der DFS-Replikationsdatenbank getrennt wird, nachdem die Definition des primären Mitglieds in Active Directory Domain Services gelöscht wurde, aber bevor alle Mitglieder der Replikationsgruppe die erste Replikation abgeschlossen haben, tritt bei allen Mitgliedern der Replikationsgruppe ein Fehler bei der Ordnerreplikation auf, da kein Server als primäres Mitglied definiert ist. In diesem Fall muss der Befehl **Dfsradmin membership /set /isprimary:true** auf dem Server des primären Mitglieds verwendet werden, um die Definition des primären Mitglieds manuell wiederherzustellen.

Weitere Informationen zur ersten Replikation findest du unter [Erstellen einer Replikationsgruppe](https://technet.microsoft.com/library/cc725893).


> [!WARNING]
> Die Definition des primären Mitglieds wird nur während des ersten Replikationsprozesses verwendet. Wenn du den Befehl <STRONG>Dfsradmin</STRONG> verwendest, um nach Abschluss der Replikation ein primäres Mitglied für einen replizierten Ordner anzugeben, wird der Server von der DFS-Replikation in Active Directory Domain Services nicht als primäres Mitglied definiert. Wenn in der DFS-Replikationsdatenbank auf dem Server später jedoch eine unumkehrbare Beschädigung oder ein Datenverlust auftritt, versucht der Server, eine erste Replikation als primäres Mitglied auszuführen, anstatt seine Daten von einem anderen Mitglied der Replikationsgruppe wiederherzustellen. Dabei wird der Server im Wesentlichen zu einem nicht autorisierten primären Server, der Konflikte verursachen kann. Aus diesem Grund sollte das primäre Mitglied nur dann manuell angegeben werden, wenn du sicher bist, dass bei der ersten Replikation ein nicht behebbarer Fehler aufgetreten ist. 
<br>


### <a name="what-happens-if-the-replication-schedule-closes-while-a-file-is-being-replicated"></a>Was geschieht, wenn der Replikationszeitplan geschlossen wird, während eine Datei repliziert wird?

Wenn die Remotedifferenzialkomprimierung (RDC) für die Verbindung aktiviert ist, wird die eingehende Replikation einer Datei über 64 KB, deren Replikation unmittelbar vor dem Schließen des Zeitplans gestartet (oder deren Zustand in **Keine Bandbreite** geändert) wurde, fortgesetzt, wenn der Zeitplan geöffnet wird (oder wenn Änderungen an einem anderen Zustand als **Keine Bandbreite** auftreten). Die Replikation wird in dem Zustand fortgesetzt, in dem sie sich befand, als sie angehalten wurde.

Wenn RDC deaktiviert ist, wird die Dateiübertragung von der DFS-Replikation vollständig neu gestartet. Dies kann sich verzögern, wenn die Datei auf dem empfangenden Mitglied verfügbar ist.

### <a name="what-happens-when-two-users-simultaneously-update-the-same-file-on-different-servers"></a>Was geschieht, wenn zwei Benutzer dieselbe Datei auf unterschiedlichen Servern gleichzeitig aktualisieren?

Wenn die DFS-Replikation einen Konflikt erkennt, wird die zuletzt gespeicherte Version der Datei verwendet. Die andere Datei wird in den Ordner „DfsrPrivate\\ConflictandDeleted“ verschoben (der sich unter dem lokalen Pfad des replizierten Ordners auf dem Computer befindet, auf dem der Konflikt aufgelöst wurde). Sie verbleibt dort, bis der Ordner „ConflictandDeleted“ bereinigt wurde, was geschieht, wenn dieser Ordner die konfigurierte Größe überschreitet oder wenn von der DFS-Replikation ein Fehler aufgrund von unzureichendem Speicherplatz auf dem Datenträger erkannt wird. Der Ordner „ConflictandDeleted“ wird nicht repliziert. Durch diese Methode der Konfliktauflösung wird das Problem geänderter Verzeichnisse vermieden, das in FRS auftreten konnte.

Wenn ein Konflikt auftritt, wird von der DFS-Replikation zu Informationszwecken ein Ereignis im Ereignisprotokoll der DFS-Replikation protokolliert. Für dieses Ereignis ist aus den folgenden Gründen kein Benutzereingriff erforderlich:

  - Es ist für Benutzer nicht sichtbar (sondern nur für Serveradministratoren).  
      
  - Der Ordner „ConflictandDeleted“ wird von der DFS-Replikation als Cache behandelt. Wenn ein Kontingentschwellenwert erreicht wird, werden einige dieser Dateien bereinigt. Es gibt keine Garantie, dass in Konflikt stehende Dateien gespeichert werden.  
      
  - Der Konflikt kann auf einem anderen Server als dem Ursprungsserver des Konflikts aufgetreten sein.  
      

## <a name="staging"></a>Wird bereitgestellt

### <a name="does-dfs-replication-continue-staging-files-when-replication-is-disabled-by-a-schedule-or-bandwidth-throttling-quota-or-when-a-connection-is-manually-disabled"></a>Wird das Staging von Dateien von der DFS-Replikation fortgesetzt, wenn die Replikation durch einen Zeitplan oder ein Kontingent für die Bandbreiteneinschränkung deaktiviert wird oder wenn eine Verbindung manuell deaktiviert wird?

Nein Bei der DFS-Replikation wird das Staging von Dateien außerhalb der geplanten Replikationszeiten nicht fortgesetzt, wenn das Kontingent für die Bandbreiteneinschränkung überschritten oder Verbindungen deaktiviert wurden.

### <a name="does-dfs-replication-prevent-other-applications-from-accessing-a-file-during-staging"></a>Verhindert DFS-Replikation, dass andere Anwendungen während des Stagings auf eine Datei zugreifen?

Nein Bei der DFS-Replikation werden Dateien auf eine Weise geöffnet, die Benutzer oder Anwendungen nicht daran hindert, Dateien im Replikationsordner zu öffnen. Diese Methode wird als „opportunistische Sperre“ bezeichnet.

### <a name="is-it-possible-to-change-the-location-of-the-staging-folder-with-the-dfs-management-tool"></a>Ist es möglich, den Speicherort des Stagingordners mit dem DFS-Verwaltungstool zu ändern?

Ja. Der Speicherort des Stagingordners wird im Dialogfeld **Eigenschaften** auf der Registerkarte **Erweitert** für jedes Mitglied einer Replikationsgruppe konfiguriert.

### <a name="when-are-files-staged"></a>Wann werden Dateien gestaged?

Dateien werden auf dem sendenden Mitglied gestaged, wenn das empfangende Mitglied die Datei anfordert (es sei denn, die Dateigröße beträgt 64 KB oder weniger), wie in der folgenden Tabelle dargestellt. Wenn die Remotedifferenzialkomprimierung (RDC) für die Verbindung deaktiviert ist, wird die Datei gestaged, sofern ihre Größe nicht 256 KB oder weniger beträgt. Dateien werden ebenfalls auf dem empfangenden Mitglied gestaged, wenn sie übertragen werden und ihre Größe unter 64 KB liegt. Diese Einstellung kann jedoch zwischen 16 KB und 1 MB konfiguriert werden. Wenn der Zeitplan geschlossen ist, werden keine Dateien gestaged.

### <a name="the-minimum-file-sizes-for-staging-files"></a>Mindestgrößen für Stagingdateien

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
<td><p>64 KB</p></td>
<td><p>256 KB</p></td>
</tr>
<tr class="odd">
<td><p>Empfangendes Mitglied</p></td>
<td><p>Standardmäßig 64 KB</p></td>
<td><p>Standardmäßig 64 KB</p></td>
</tr>
</tbody>
</table>

### <a name="what-happens-if-a-file-is-changed-after-it-is-staged-but-before-it-is-completely-transmitted-to-the-remote-site"></a>Was geschieht, wenn eine Datei nach dem Staging, aber vor der vollständigen Übertragung an den Remotestandort geändert wird?

Wenn ein Teil der Datei bereits übertragen wird, wird die Übertragung von der DFS-Replikation fortgesetzt. Wenn die Datei geändert wird, bevor ihre Übertragung von der DFS-Replikation gestartet wird, wird die neuere Version der Datei gesendet.

## <a name="change-history"></a>Änderungsverlauf


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Datum</th>
<th>Beschreibung</th>
<th>Grund</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>15. November 2018</p></td>
<td><p>Für Windows Server 2019 aktualisiert.</p></td>
<td><p>Neues Betriebssystem.</p></td>
</tr>
<tr class="even">
<td><p>09. Oktober 2013</p></td>
<td><p>Der Abschnitt „Wie lauten die unterstützten Grenzwerte für die DFS-Replikation?“ wurde mit Testergebnissen aktualisiert, die unter Windows Server 2012 R2 ermittelt wurden.</p></td>
<td><p>Aktualisierungen für die aktuellen Versionen von Windows Server</p></td>
</tr>
<tr class="odd">
<td><p>30. Januar 2013</p></td>
<td><p>Der Eintrag „Wird das Staging von Dateien von der DFS-Replikation fortgesetzt, wenn die Replikation durch einen Zeitplan oder ein Kontingent für die Bandbreiteneinschränkung deaktiviert wird oder wenn eine Verbindung manuell deaktiviert wird?“ wurde hinzugefügt.</p></td>
<td><p>Fragen von Kunden</p></td>
</tr>
<tr class="even">
<td><p>31. Oktober 2012</p></td>
<td><p>Der Eintrag „Wie lauten die unterstützten Grenzwerte für die DFS-Replikation?“ wurde bearbeitet, um die getestete Anzahl replizierter Dateien auf einem Volume zu erhöhen.</p></td>
<td><p>Kundenfeedback</p></td>
</tr>
<tr class="odd">
<td><p>15. August 2012</p></td>
<td><p>Der Eintrag „Werden von der DFS-Replikation NTFS-Dateiberechtigungen, alternative Datenströme, feste Links und Analysepunkte repliziert?“ wurde bearbeitet, um zu verdeutlichen, wie feste Links und Analysepunkte von der DFS-Replikation behandelt werden.</p></td>
<td><p>Feedback vom Kundensupport</p></td>
</tr>
<tr class="even">
<td><p>13. Juni 2012</p></td>
<td><p>Der Eintrag „Funktioniert die DFS-Replikation auf ReFS- oder FAT-Volumes?“ wurde bearbeitet, um ReFS in die Erläuterungen aufzunehmen.</p></td>
<td><p>Kundenfeedback</p></td>
</tr>
<tr class="odd">
<td><p>25. April 2012</p></td>
<td><p>Der Eintrag „Werden von der DFS-Replikation NTFS-Dateiberechtigungen, alternative Datenströme, feste Links und Analysepunkte repliziert?“ wurde bearbeitet, um zu verdeutlichen, wie feste Links von der DFS-Replikation behandelt werden.</p></td>
<td><p>Mögliche Unklarheiten ausräumen</p></td>
</tr>
<tr class="even">
<td><p>30. März 2011</p></td>
<td><p>Der Eintrag „Können mit der DFS-Replikation PST-Dateien aus Outlook oder Microsoft Office Access-Datenbankdateien repliziert werden?“ wurde bearbeitet, um klarzustellen, welche Auswirkungen die Verwendung der DFS-Replikation mit PST- und Access-Dateien haben kann.</p>
<p>Der Eintrag „Wie kann ich die Replikationsleistung verbessern?“ wurde hinzugefügt.</p></td>
<td><p>Kundenfragen zum früheren Eintrag, in dem fälschlicherweise angegeben wurde, dass die DFS-Replikationsdatenbank durch die Replikation von PST- oder Access-Dateien beschädigt werden könnte.</p></td>
</tr>
<tr class="odd">
<td><p>26. Januar 2011</p></td>
<td><p>Der Eintrag „Wie können Dateien aus den Ordnern „ConflictAndDeleted“ oder „PreExisting“ wiederhergestellt werden?“ wurde hinzugefügt.</p></td>
<td><p>Kundenfeedback</p></td>
</tr>
<tr class="even">
<td><p>20. Oktober 2010</p></td>
<td><p>Der Eintrag „Wie kann ich ein DFS-Replikationsmitglied aktualisieren oder ersetzen?“ wurde hinzugefügt.</p></td>
<td><p>Kundenfeedback</p></td>
</tr>
</tbody>
</table>

