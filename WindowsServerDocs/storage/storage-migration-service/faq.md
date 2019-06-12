---
title: Storage-Migration-Dienst häufig gestellte Fragen (FAQ)
description: Häufig gestellte Fragen zu Storage Migration-Dienst, z. B. welche Dateien von Übertragungen ausgeschlossen sind, bei der Migration von einem Server zu einem anderen.
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 06/04/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: 258f25a7e1ec5c796c15450625397e96db25d693
ms.sourcegitcommit: cd12ace92e7251daaa4e9fabf1d8418632879d38
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2019
ms.locfileid: "66501519"
---
# <a name="storage-migration-service-frequently-asked-questions-faq"></a>Storage-Migration-Dienst häufig gestellte Fragen (FAQ)

Dieses Thema enthält Antworten auf häufig gestellte Fragen (FAQs) zur Verwendung von [Speicherung Datenbankmigrationsdienst](overview.md) Servern zu migrieren.

## <a name="excluded-files"></a> Welche Dateien und Ordner von Übertragungen ausgeschlossen werden?

Storage-Migration-Dienst wird nicht übertragen, Dateien oder Ordner, in denen wir wissen, dass Windows-Betrieb beeinträchtigen könnten. Hier ist insbesondere, was wir nicht übertragen oder verschieben in den PreExistingData-Ordner auf dem Zielserver:

- Windows, Programme, die Programmdateien (x86), Daten aus dem Programm, Benutzer
- $Recycle.bin, Recycler, Recycled, System Volume Information, $UpgDrv$, $SysReset, $Windows. ~ BT, $Windows. ~ LS, "Windows.old", Start, Wiederherstellung, Dokumente und Einstellungen
- pagefile.sys, hiberfil.sys, swapfile.sys, winpepge.sys, config.sys, bootsect.bak, bootmgr, bootnxt
- Dateien oder Ordner auf dem Quellserver, der in Konflikt steht, mit der ausgeschlossenen Ordner auf dem Zielserver. <br>Angenommen, ein N:\Windows-Ordner auf dem Quellcomputer vorhanden ist und sie zu C:\ zugeordnet wird Volume auf dem Ziel, sie übertragen wird nicht zu erhalten – unabhängig davon, was es enthält, da es der Ordner C:\Windows System, auf dem Zielserver beeinträchtigen würde.

## <a name="domain-migration"></a> Werden Migrationen von Domänen verwendet?

Lässt keine Speicherung Datenbankmigrationsdienst zu migrieren zwischen Active Directory-Domänen. Migrationen zwischen Servern treten immer den Zielserver der gleichen Domäne. Sie können die Anmeldeinformationen für die Migration von unterschiedlicher Domänen im Active Directory-Gesamtstruktur verwenden. Migrieren zwischen Arbeitsgruppen, ist der Speicherdienst für die Migration unterstützt.  

## <a name="cluster-support"></a> Werden Cluster werden als Quellen oder Ziele unterstützt?

Storage-Migration-Dienst migrieren nicht zwischen Clustern in Windows Server-2019 derzeit. Wir planen Unterstützung für Cluster in einer zukünftigen Version von Storage Migration Service.

## <a name="local-principals"></a> Führen Sie die lokale Gruppen, und Migrieren von lokale Benutzern?

Storage-Migration-Dienst migrieren nicht derzeit lokale Benutzer oder die lokalen Gruppen in Windows Server-2019. Wir planen, dass lokale Benutzer und die Migration der lokalen Gruppe in einer zukünftigen Version von Storage Migration Service unterstützt.

## <a name="domain-controller"></a> Wird die Migration von Controller unterstützt?

Storage-Migration-Dienst migrieren nicht derzeit Domänencontroller in Windows Server-2019. Dieses Problem zu umgehen, solange Sie mehrere Domänencontroller in Active Directory-Domäne verfügen,-Herabstufung des Domänencontrollers vor der Migration der Anwendung, klicken Sie dann das Ziel heraufstufen, nach Abschluss der Übernahme. Wir planen die Migration Domänencontroller-Unterstützung in einer zukünftigen Version von Storage Migration Service hinzufügen.

## <a name="share-attributes"></a> Welche Attribute vom Speicherdienst Migration migriert werden?

Storage-Migration-Dienst migriert alle Flags, Einstellungen und Sicherheit von SMB-Freigaben. Diese Liste von Flags, die Storage-Migration-Dienst migriert enthält:

    - Freigabe-Status
    - Typ der Verfügbarkeit
    - Freigabetyp
    - Ordner Enumerationsmodus *(auch bekannt als zugriffsbasierte Aufzählung oder ABE)*
    - Cachingmodus
    - Leasen Modus
    - SMB-Instanz
    - CA-Timeout
    - Limit für gleichzeitige Benutzer
    - Fortlaufend verfügbare
    - Beschreibung           
    - Verschlüsseln von Daten
    - Identity-Remoting
    - Infrastruktur
    - Name
    - Pfad
    - Im Bereich einer
    - Bereichsname
    - Sicherheitsbeschreibung
    - Schattenkopie
    - Spezielle
    - Temporäre

## <a name="move-db"></a> Kann ich die Speicherung Datenbankmigrationsdienst-Datenbank verschieben?

Der Storage-Migration-Dienst verwendet eine extensible Storage Engine (ESE)-Datenbank, die standardmäßig im Ordner "Ausgeblendete c:\programdata\microsoft\storagemigrationservice" installiert ist. Diese Datenbank wächst, wenn Aufträge hinzugefügt werden, und Übertragungen abgeschlossen sind und können erheblichen Speicherplatz nach der Migration nutzen Millionen von Dateien, wenn Sie Aufträge nicht löschen. Wenn die Datenbank zum Verschieben muss, führen Sie die folgenden Schritte aus:

1. Beenden Sie den Dienst "Storage-Migration-Dienst", auf dem Orchestrator-Computer.
2. Übernehmen des Besitzes von der `%programdata%/Microsoft/StorageMigrationService` Ordner
3. Fügen Sie Ihr Benutzerkonto über vollständige Kontrolle über, freigeben und alle seine Dateien und Unterordner.
4. Verschieben Sie den Ordner zu einem anderen Laufwerk, auf dem Orchestrator-Computer.
5. Legen Sie den folgenden Registrierungsschlüssel REG_SZ-Wert:

    HKEY_Local_Machine\Software\Microsoft\SMS DatabasePath = *Pfad zu dem neuen Ordner auf einem anderen Volume* . 
6. Sicherstellen Sie, dass das SYSTEM über Vollzugriff auf alle Dateien und Unterordner dieses Ordners verfügt
7. Entfernen Sie Ihre eigenen Konten Berechtigungen.
8. Starten des Diensts "Storage-Migration-Dienst".

## <a name="non-windows"></a> Kann ich aus anderen Quellen als Windows Server migrieren?

Die Speicherung Datenbankmigrationsdienst-Version, die im Lieferumfang von Windows Server-2019 unterstützt die Migration von Windows Server 2003 und späteren Betriebssystemen. Es kann nicht in der derzeit von Linux, Samba, NetApp, EMC oder andere Speichergeräte SAN- und NAS migrieren. Wir planen, um dies in einer zukünftigen Version von Storage-Migration-Dienst, beginnend mit Linux-Samba-Unterstützung zu ermöglichen.

## <a name="previous-versions"></a> Kann ich die vorherige Dateiversionen migrieren?

Die im Lieferumfang von Windows Server-2019 Storage Migration Service-Version unterstützt keine Migration von früheren Versionen (erstellt mit dem Volumeschattenkopie-Dienst) von Dateien. Es werden nur die aktuelle Version migriert. 

## <a name="ntfs-refs"></a> Kann ich von NTFS zu REFS migrieren?

Die Speicherung Datenbankmigrationsdienst-Version, die im Lieferumfang von Windows Server-2019 unterstützt nicht die Migration von NTFS zu REFS-Dateisysteme. Sie können von NTFS zu NTFS und REFS mit ReFS migrieren. Dies ist beabsichtigt, aufgrund der viele Unterschiede zwischen Funktionalität, Metadaten und andere Aspekte, die Verweise nicht duplizieren von NTFS. ReFS ist als eine Anwendung Workload-Dateisystem, nicht mit einem allgemeinen Dateisystem gedacht. Weitere Informationen finden Sie unter [Resilient File System (ReFS)-Übersicht](../refs/refs-overview.md)

## <a name="consolidate-servers"></a> Kann ich mehrere Server bei einem Server konsolidieren?

Die Speicherung Datenbankmigrationsdienst-Version, die im Lieferumfang von Windows Server-2019 unterstützt nicht die Konsolidierung mehrerer Server bei einem Server. Ein Beispiel der Konsolidierung würde migrieren, wenn Sie drei separate Quellservern - die die gleichen Freigabenamen haben können und lokale Dateipfade - auf einen einzelnen neuen Server, der diese Pfade und Freigaben zu verhindern, dass alle überlappen oder Konflikte, virtualisiert beantwortet anschließend alle drei vorherigen Server-Namen und IP-Adresse. Wir können diese Funktion in einer zukünftigen Version von Storage Migration Service hinzufügen.  

## <a name="optimize"></a> Optimieren der Leistung von Inventur- und Übertragung

Die Storage-Migration-Dienst enthält einen Multithreaded lesen und kopieren-Engine aufgerufen, den Storage Migration Service-Dienst die wir entwickelt, um sowohl schnelle als auch auf perfekte Daten fehlen, Genauigkeit in viele Tools zum Kopieren von Dateien zu bringen. Während die Standardkonfiguration werden für viele Kunden optimal ist, gibt es jedoch Möglichkeiten zum Verbessern der Leistung während der Softwareinventur und die Übertragung von SMS.

- **Verwenden Sie für das Ziel-Betriebssystem Windows Server-2019.** Windows Server-2019 enthält den Proxydienst für Storage Migration-Dienst. Wenn Sie dieses Feature installieren und zu Windows Server-2019 Ziele migrieren, arbeiten alle Übertragungen als uneingeschränktem Zugriff zwischen Quelle und Ziel. Dieser Dienst wird auf die Orchestrator während der Übertragung ausgeführt, wenn die Zielcomputer WindowsServer 2012 R2 oder Windows Server 2016, d.h. die Übertragungen Doppel-Hop und sehr viel langsamer werden. Wenn Sie mehrere Aufträge, die mit Windows Server 2012 R2 oder Windows Server 2016-Ziele vorhanden sind, wird der Orchestrator als Engpass erweisen. 

- **Ändern Sie die Standard-Übertragungsthreads.** Der Proxydienst von Storage Migration-Dienst kopiert 8 Dateien gleichzeitig in einem bestimmten Auftrag. Sie können die Anzahl der gleichzeitigen Kopie Threads erhöhen, durch Anpassen der folgenden REG_DWORD-Wert der Name des Registrierungsschlüssels im Dezimalformat auf jedem Knoten, auf den SMS-Proxy ausführt:

    HKEY_Local_Machine\Software\Microsoft\SMSProxy   FileTransferThreadCount

   Der gültige Bereich ist 1 und 128 in Windows Server-2019. Nach der Änderung müssen Sie den Dienstproxy für Storage-Migration-Dienst auf allen Computern, die Teilnahme an einer Migrations starten. Gehen Sie vorsichtig vor, mit dieser Einstellung. höhere festlegen kann zusätzliche Kerne, speicherleistung und Netzwerkbandbreite erfordern. Zu hoch festlegen, kann dies zu Leistungseinbußen, die im Vergleich zu den Einstellungen der Standardrichtlinie führen. Die Fähigkeit, Threadeinstellungen, die basierend auf CPU, Arbeitsspeicher, Netzwerk und Speicher heuristisch zu ändern ist für eine höhere Version von SMS geplant.

- **Hinzufügen von Kernen und Arbeitsspeicher.**  Es wird dringend empfohlen, dass die Quelle, Ziel und Orchestrator-Computer über mindestens zwei Prozessorkerne oder zwei vCPUs und weitere erheblich Inventur und Übertragen der Leistung beitragen können, insbesondere, wenn Sie in Kombination mit FileTransferThreadCount (oben). Beim Übertragen von Dateien, die größer als die üblichen Office-Formate sind (GB oder größer) übertragungsleistung profitieren von mehr Arbeitsspeicher als das Minimum von Standard 2GB.

- **Erstellen Sie mehrere Auftrag.** Beim Erstellen eines Auftrags mit mehreren Server-Datenquellen wird im seriellen Modus für die Inventur, Übertragung, jeden Server kontaktiert und Umstellung durchführen. Dies bedeutet, dass die Phase vor einem anderen Server Beginn jeder Server abgeschlossen werden muss. Um mehrere Server gleichzeitig ausführen zu können, erstellen Sie einfach mehrere Aufträge mit jedem Auftrag, die nur einen Server enthält. SMS unterstützt bis zu 100 gleichzeitig ausgeführte Aufträge, was bedeutet, dass einem einzelnen "Orchestrator" viele Windows Server-2019 Zielcomputern parallelisieren kann. Wir empfehlen nicht mehrere parallele Aufträge ausgeführt, wenn es sich bei die Zielcomputer sind Windows Server 2016 oder Windows Server 2012 R2 als ohne der SMS-Dienst auf dem Zielserver ausgeführt wird, der Orchestrator alle ausführen muss, sich selbst überträgt und werden konnte ein Engpass. Die Möglichkeit, dass der Server in einen einzelnen Auftrag parallel ausgeführt, ist ein Feature, das wir in einer späteren Version von SMS hinzufügen möchten.

- **Verwenden Sie SMB-3, mit dem RDMA-Netzwerke.** Wenn aus einem Windows Server 2012 oder höher Quellcomputer SMB 3.x unterstützt SMB Direct Modus und RDMA-Netzwerk zu übertragen. RDMA verschiebt die meisten CPU-Kosten der Übertragung von der Hauptplatine CPUs integrieren NIC-Prozessoren, verringert die Netzwerklatenz und CPU-Auslastung. Darüber hinaus RDMA-Netzwerke wie ROCE und iWARP in der Regel über wesentlich höhere Bandbreite als typische TCP/Ethernet, einschließlich 25, 50 und Geschwindigkeit von 100Gb pro Schnittstelle. In der Regel mithilfe von SMB Direct, verschiebt das Tempolimit Übertragung über das Netzwerk auf den Speicher selbst.   

- **Verwenden Sie SMB-3-Multichannel.** Wenn von einem Windows Server 2012 oder höher Quellcomputer zu übertragen, Dateikopien SMB 3.x unterstützt multichannel, die erheblich verbessern können, Leistung beim Kopieren. Dieses Feature funktioniert automatisch, solange die Quelle und Ziel verfügen:

   - Mehrere Netzwerkadapter
   - Eine oder mehrere Netzwerkadapter, die empfangen empfangsseitige Skalierung (RSS) unterstützen.
   - Einer der mehr Netzwerkadaptern, die mithilfe des NIC-Teamvorgang konfiguriert sind
   - Ein oder mehrere Netzwerkadapter, die RDMA unterstützen

- **Aktualisieren Sie Treiber.** Installieren Sie nach Bedarf auf Quell-, Ziel- und Orchestrator neuesten Anbieter-Speicher und Gehäuse Firmware und Treiber, neueste Anbieter HBA-Treiber, neueste Anbieter BIOS/UEFI-Firmware, Netzwerktreiber und neuesten hauptplatinenchipsatz-Treiber Server. Starten Sie die Knoten gegebenenfalls neu. Konfigurieren Sie die Hardware für freigegebenen Speicher und Netzwerk gemäß der Dokumentation des jeweiligen Herstellers.

- **Leistungsstarke Verarbeitung zu aktivieren.** Stellen Sie sicher, dass die BIOS/UEFI-Einstellungen für Server eine hohe Leistung ermöglichen (z. B. Deaktivieren des C-Status, Festlegen der QPI-Geschwindigkeit, Aktivieren von NUMA und Festlegen der höchsten Speicherfrequenz). Stellen Sie sicher, dass die energieverwaltung in Windows Server auf eine hohe Leistung festgelegt ist. Führen Sie gegebenenfalls einen Neustart aus. Vergessen Sie nicht, diese zu entsprechenden Status zurückzugeben, nach Abschluss der Migration. 

- **Optimieren der Hardware** überprüfen Sie die [Performance Tuning Richtlinien für Windows Server 2016](https://docs.microsoft.com/en-us/windows-server/administration/performance-tuning/) für die Optimierung der Orchestrator und Zielcomputern, die unter WindowsServer 2019 und Windows Server 2016. Die [Optimieren der Leistung mit Subsystem](https://docs.microsoft.com/en-us/windows-server/networking/technologies/network-subsystem/net-sub-performance-tuning-nics) Abschnitt besonders nützlich, Informationen enthält.

- **Verwenden Sie schneller Speicher.** Während es schwierig, aktualisieren Sie die Quelle Computer speichergeschwindigkeit sein kann, sollten Sie sicherstellen, dass der Zielspeicher ist mindestens genauso schnell schreiben e/a-Leistung wie die Quelle lesen e/a-Leistung ist, um sicherzustellen, dass keine unnötigen Engpass in Übertragungen vorhanden ist. Wenn das Ziel eines virtuellen Computers ist, stellen Sie sicher, dass mindestens für die Zwecke der Migration, er in der am schnellsten Speicherebene Hypervisor-Hosts, z. B. den Tarif "flash" oder mit Storage Spaces Direct HCI-Clustern, die mit gespiegelten All-Flash- oder hybride Leerzeichen ausgeführt wird. Nach Abschluss der SMS-Migration kann die VM live können zu einem langsameren Ebene oder Host migriert.

- **Aktualisieren Sie Antivirensoftware.** Versichern Sie sich die Quelle und das Ziel die jeweils neueste Patchversion von antivirus-Software, um sicherzustellen, dass minimalen Verwaltungsaufwand ausgeführt werden. Testen, können Sie *vorübergehend* Ausschließen von Ordnern, die Sie inventarisieren oder migrieren, die auf den Quell- und Ziel von überprüfen. Wenn die übertragungsleistung verbessert wird, wenden Sie sich an Hersteller der Antivirensoftware, für Anweisungen oder für eine aktualisierte Version der Software oder eine Erläuterung der erwarteten Leistung.

## <a name="give-feedback"></a> Welche Optionen habe ich Feedback oder melden Sie Fehler, oder Unterstützung zu erhalten?

Geben Sie Feedback zur den Storage-Migration-Dienst:

- Verwenden Sie das Feedback Hub-Tool, das in Windows 10, "Feature vorschlagen" klicken und Angeben der Kategorie "Windows Server" und die Unterkategorie der "Storage-Migration" enthalten
- Verwenden der [UserVoice für Windows Server](https://windowsserver.uservoice.com) Standort
- E-Mail smsfeed@microsoft.com

Datei-Fehler:

- Verwenden Sie das Feedback Hub-Tool, das in Windows 10, Sie auf "Problem melden" und Angeben der Kategorie "Windows Server" "und" Unterkategorie "Storage-Migration" enthalten
- Öffnen Sie eine Supportanfrage über [Microsoft-Support](https://support.microsoft.com)

Um Unterstützung zu erhalten:

 - Stellen Sie eine Frage der [Windows Server-Tech-Community](https://techcommunity.microsoft.com/t5/Windows-Server/ct-p/Windows-Server)
 - Veröffentlichen Sie auf die [Technet-Forum für Windows Server 2019](https://social.technet.microsoft.com/Forums/en-US/home?forum=ws2019&filter=alltypes&sort=lastpostdesc) 
 - Öffnen Sie eine Supportanfrage über [Microsoft-Support](https://support.microsoft.com)


## <a name="see-also"></a>Siehe auch

- [Übersicht über Storage-Migration Service](overview.md)
