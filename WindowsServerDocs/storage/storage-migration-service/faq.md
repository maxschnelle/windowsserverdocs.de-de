---
title: Storage-Migration-Dienst häufig gestellte Fragen (FAQ)
description: Häufig gestellte Fragen zu Storage Migration-Dienst, z. B. welche Dateien von Übertragungen ausgeschlossen sind, bei der Migration von einem Server zu einem anderen.
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 11/06/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: df03f722b7b36a163693f675a2eaade2fabeb82f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860911"
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

## <a name="transfer-threads"></a> Kann ich die Anzahl der Dateien erhöhen, die gleichzeitig kopieren?

Der Proxydienst von Storage Migration-Dienst kopiert 8 Dateien gleichzeitig in einem bestimmten Auftrag. Dieser Dienst auf dem Orchestrator während der Übertragung ausgeführt wird, wenn die Zielcomputer Windows Server 2012 R2 oder Windows Server 2016 sind jedoch auch auf alle Windows Server-2019 Zielknoten ausgeführt wird. Sie können die Anzahl der gleichzeitigen Kopie Threads erhöhen, durch Anpassen der folgenden REG_DWORD-Wert der Name des Registrierungsschlüssels im Dezimalformat auf jedem Knoten, auf den SMS-Proxy ausführt:

    HKEY_Local_Machine\Software\Microsoft\SMSProxy
    FileTransferThreadCount

 Der gültige Bereich ist 1 und 128 in Windows Server-2019. 

 Nach der Änderung müssen Sie den Storage-Migration-Dienstproxy-Dienst auf allen Computern Partipating bei der Migration neu starten. Wir planen, diese Zahl in einer zukünftigen Version von Storage-Migration-Dienst ausgelöst werden soll.

## <a name="non-windows"></a> Kann ich aus anderen Quellen als Windows Server migrieren?

Die Speicherung Datenbankmigrationsdienst-Version, die im Lieferumfang von Windows Server-2019 unterstützt die Migration von Windows Server 2003 und späteren Betriebssystemen. Es kann nicht in der derzeit von Linux, Samba, NetApp, EMC oder andere Speichergeräte SAN- und NAS migrieren. Wir planen, um dies in einer zukünftigen Version von Storage-Migration-Dienst, beginnend mit Linux-Samba-Unterstützung zu ermöglichen.

## <a name="previous-versions"></a> Kann ich die vorherige Dateiversionen migrieren?

Die im Lieferumfang von Windows Server-2019 Storage Migration Service-Version unterstützt keine Migration von früheren Versionen (erstellt mit dem Volumeschattenkopie-Dienst) von Dateien. Es werden nur die aktuelle Version migriert. 

## <a name="ntfs-refs"></a> Kann ich von NTFS zu REFS migrieren?

Die Speicherung Datenbankmigrationsdienst-Version, die im Lieferumfang von Windows Server-2019 unterstützt nicht die Migration von NTFS zu REFS-Dateisysteme. Sie können von NTFS zu NTFS und REFS mit ReFS migrieren. Dies ist beabsichtigt, aufgrund der viele Unterschiede zwischen Funktionalität, Metadaten und andere Aspekte, die Verweise nicht duplizieren von NTFS. ReFS ist als eine Anwendung Workload-Dateisystem, nicht mit einem allgemeinen Dateisystem gedacht. Weitere Informationen finden Sie unter [Resilient File System (ReFS)-Übersicht](../refs/refs-overview.md)

## <a name="consolidate-servers"></a> Kann ich mehrere Server bei einem Server konsolidieren?

Die Speicherung Datenbankmigrationsdienst-Version, die im Lieferumfang von Windows Server-2019 unterstützt nicht die Konsolidierung mehrerer Server bei einem Server. Ein Beispiel der Konsolidierung würde migrieren, wenn Sie drei separate Quellservern - die die gleichen Freigabenamen haben können und lokale Dateipfade - auf einen einzelnen neuen Server, der diese Pfade und Freigaben zu verhindern, dass alle überlappen oder Konflikte, virtualisiert beantwortet anschließend alle drei vorherigen Server-Namen und IP-Adresse. Wir können diese Funktion in einer zukünftigen Version von Storage Migration Service hinzufügen.  


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
