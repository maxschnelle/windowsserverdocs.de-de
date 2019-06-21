---
title: Neuerungen in Hyper-V unter Windows Server 2016
description: Bietet eine Übersicht über die neuen Funktionen in Hyper-V
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1a65a98e-54b6-4c41-9732-1e3d32fe3a5f
author: KBDAzure
ms.author: kathydav
ms.date: 09/21/2017
ms.openlocfilehash: 6ec5db82ecae2fb74731f3c52b9113325837a2fb
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280016"
---
# <a name="whats-new-in-hyper-v-on-windows-server"></a>Neuerungen in Hyper-V unter Windows Server

>Gilt für: WindowsServer 2019, Microsoft Hyper-V Server 2016, WindowsServer 2016
  
Dieser Artikel beschreibt die neue und geänderte Funktionen der Hyper-V unter Windows Server-2019, Windows Server 2016 und Microsoft Hyper-V Server 2016. Um neue Features auf virtuellen Computern mit Windows Server 2012 R2 erstellt wurden und verschoben oder auf einem Server mit Hyper-V unter Windows Server-2019 oder Windows Server 2016 importiert zu verwenden, müssen Sie die Konfigurationsversion des virtuellen Computers manuell aktualisieren. Anweisungen hierzu finden Sie unter [Upgrade der VM-Version](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md).  
  
Hier ist, was in diesem Artikel enthalten ist, und gibt an, ob die Funktionalität für neue oder aktualisierte ist.  

## <a name="windows-server-version-1903"></a>Windows Server, version 1903

### <a name="add-hyper-v-manager-to-server-core-installations-updated"></a>Hinzufügen von Hyper-V-Manager auf Server Core-Installationen (aktualisiert)

Wie Sie wissen vielleicht, wird empfohlen, mithilfe der Installationsoption Server Core, bei Verwendung von Windows Server, Halbjährlicher Kanal in der Produktion. Server Core standardmäßig lässt jedoch eine Reihe von Tools für hilfreiches Verwaltungstool aus. Sie können die viele der am häufigsten verwendeten Tools durch Installieren des App-Kompatibilität, es gibt aber immer noch einige fehlende Tools hinzufügen.

Daher wurde hinzugefügt basierend auf Feedback von Kunden, eine weitere Tools für das App-Kompatibilität-Feature in dieser Version: Hyper-V-Manager (virtmgmt.msc).

Weitere Informationen finden Sie unter [Kompatibilitätsfeature für Server Core-app](../../get-started-19/install-fod-19.md).

## <a name="windows-server-2019"></a>Windows Server 2019

### <a name="security-shielded-virtual-machines-improvements-new"></a>Sicherheit: Verbesserungen der abgeschirmten virtuellen Computern (neu)

- **Branch Office-Verbesserungen**

    Sie können nun abgeschirmte virtuelle Maschinen auf Maschinen mit intermittierender Konnektivität zum Host Guardian-Dienst ausführen, indem Sie die neuen [Fallback-HGS](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office#fallback-configuration)- und [Offline-Modus](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office#offline-mode)-Funktionen nutzen. Fallback HGS ermöglicht es Ihnen, einen zweiten Satz von URLs für Hyper-V zu konfigurieren, um zu prüfen, ob Ihr primärer HGS-Server erreicht werden kann.

    Im Offline-Modus können Sie Ihre abgeschirmten VMs auch dann starten, wenn HGS nicht erreichbar ist, sofern die VM einmal erfolgreich gestartet wurde und sich die Sicherheitskonfiguration des Hosts nicht geändert hat.

- **Verbesserungen bei der Problembehandlung**

    Darüber hinaus haben wir die Fehlerbehebung für Ihre [abgeschirmten virtuellen Maschinen](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-shielded-vms) vereinfacht, indem wir den erweiterten VMConnect-Sitzungsmodus und PowerShell Direct unterstützen. Diese Tools sind besonders nützlich, wenn Sie die Netzwerkverbindung zu Ihrer VM verloren haben und ihre Konfiguration aktualisieren müssen, um den Zugriff wiederherzustellen.

    Diese Funktionen müssen nicht konfiguriert werden, und sie werden automatisch zur Verfügung gestellt, wenn eine abgeschirmte VM auf einem Hyper-V-Host mit Windows Server Version 1803 oder höher ausgeführt wird.

- **Linux-Unterstützung**

    Wenn Sie Umgebungen mit gemischten Betriebssystemen ausführen, unterstützt Windows Server 2019 jetzt die Ausführung von Ubuntu, Red Hat Enterprise Linux und SUSE Linux Enterprise Server in abgeschirmten virtuellen Maschinen.

## <a name="windows-server-2016"></a>Windows Server 2016

### <a name="compatible-with-connected-standby-new"></a>Kompatibel mit den verbundenen Standbymodus \(neu\)

Wenn die Hyper-V-Rolle auf einem Computer installiert ist, der immer Energiemodus verbunden (AOAC)-Power-Objektmodell verwendet, das **verbundenen Standbymodus** Energiezustand ist jetzt verfügbar.  
  
### <a name="discrete-device-assignment-new"></a>Diskrete gerätezuordnung \(neu\)

Dieses Feature können Sie eine virtuellen Computer direkte und exklusiven Zugriff auf einige PCIe-Hardwaregeräte zu geben. Verwenden ein Gerät auf diese Weise wird die Hyper-V-virtualisierungsstapels, was zu schnelleren Zugriff führt umgangen werden. Ausführliche Informationen zu unterstützter Hardware, finden Sie unter "diskrete gerätezuordnung" in [Systemanforderungen für Hyper-V unter Windows Server 2016](System-requirements-for-Hyper-V-on-Windows.md). Informationen, einschließlich Informationen zum Verwenden dieser Funktion und Überlegungen, die im Beitrag finden Sie unter "[diskrete Gerätezuordnung, Beschreibung und Hintergrund](https://blogs.technet.microsoft.com/virtualization/2015/11/19/discrete-device-assignment-description-and-background/)" im Virtualization-Blog.

### <a name="encryption-support-for-the-operating-system-disk-in-generation-1-virtual-machines-new"></a>Unterstützung der Verschlüsselung für den Betriebssystem-Datenträger in virtuelle Maschinen der Generation 1 \(neu)

Sie können jetzt mithilfe von BitLocker-laufwerkverschlüsselung in virtuelle Maschinen der Generation 1 Betriebssystem-Datenträgers schützen. Ein neues Feature, Schlüsselspeicher, erstellt einen kleinen, dedizierten Laufwerk zum Speichern von BitLocker-Schlüssel für das Systemlaufwerk. Dies erfolgt, anstatt eine virtual Trusted Platform Module (TPM), steht nur in der virtuelle Computer der Generation 2. Zum Entschlüsseln des Datenträgers, und starten den virtuellen Computer, muss Hyper-V-Hosts entweder Teil einer autorisierten geschütztes Fabric oder den privaten Schlüssel aus einem der Überwachungen des virtuellen Computers haben. Speichern von Schlüsseln erfordert eine Version 8-VM. Informationen zur Version von Virtual Machine, finden Sie unter [Upgrade VM-Konfigurationsversion in Hyper-V unter Windows 10 oder Windows Server 2016](./deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md).  
  
### <a name="host-resource-protection-new"></a>Hosten von Ressourcenschutz \(neu\)

Diese Funktion verhindert, dass eine VM mit mehr als die Freigabe von Systemressourcen durch Suchen nach übermäßig viele Ebenen der Aktivität. Damit können verhindern, dass eine übermäßige Aktivität des virtuellen Computers beeinträchtigen die Leistung des Hosts oder anderen virtuellen Computern. Bei der Überwachung ein virtuellen Computers mit übermäßiger Aktivität erkannt wird, erhält der virtuelle Computer weniger Ressourcen. Diese Überwachung und Erzwingung ist standardmäßig deaktiviert. Verwenden von Windows PowerShell zum Aktivieren oder deaktivieren. Um es zu aktivieren, führen Sie diesen Befehl aus:  
  
```
Set-VMProcessor TestVM -EnableHostResourceProtection $true
```

Weitere Informationen zu diesem Cmdlet finden Sie unter [Set-VMProcessor](https://docs.microsoft.com/powershell/module/hyper-v/set-vmprocessor).

### <a name="hot-add-and-remove-for-network-adapters-and-memory-new"></a>Speicherebenen "Hot" hinzufügen und Entfernen von Netzwerkadaptern und Arbeitsspeicher \(neu\)

Sie können jetzt hinzufügen oder Entfernen eines Netzwerkadapters, während die virtuelle Maschine, ohne dass Ausfallzeiten ausgeführt wird. Dies funktioniert für virtuelle Maschinen der Generation 2, auf denen entweder Windows oder Linux-Betriebssysteme ausgeführt werden soll.  
  
Sie können auch anpassen, dass die Menge an Arbeitsspeicher zugewiesen an einen virtuellen Computer, während er ausgeführt wird, auch wenn Sie nicht Dynamic Memory aktiviert haben. Dies funktioniert für sowohl der Generation 1 und virtuellen Maschinen der Generation 2 unter Windows Server 2016 oder Windows 10.  

### <a name="hyper-v-manager-improvements-updated"></a>Verbesserungen der Hyper-V-Manager \(aktualisiert\) 
  
-   **Unterstützung alternativer Anmeldeinformationen** – Sie können jetzt einen anderen Satz von Anmeldeinformationen im Hyper-V-Manager verwenden, beim Herstellen einer Verbindung mit einem anderen Windows Server 2016 oder Windows 10-Remotehost. Sie können diese Anmeldeinformationen, um eine erneute Anmeldung vereinfachen auch speichern.  
  
-   **Verwalten von früheren Versionen** -mit Hyper-V-Manager in Windows Server-2019, Windows Server 2016 und Windows 10 können Sie Computer mit Hyper-V auf Windows Server 2012, Windows 8, Windows Server 2012 R2 und Windows 8.1 verwalten.  
  
-   **Verwaltungsprotokoll aktualisiert** -Hyper-V-Manager jetzt kommuniziert wird, mit Hyper-V-Remotehosts mithilfe des WS-MAN-Protokolls, das die CredSSP-, Kerberos- oder NTLM-Authentifizierung zulässt. Wenn Sie CredSSP für die Verbindung mit einem Hyper-V-Remotehost verwenden, können Sie eine Livemigration ausführen, ohne Aktivierung der eingeschränkten Delegierung in Active Directory. Die WS-MAN basierende Infrastruktur vereinfacht auch einen Host für die Remoteverwaltung zu aktivieren. WS-MAN stellt über Port 80 eine Verbindung her, der standardmäßig geöffnet ist.  
  
### <a name="integration-services-delivered-through-windows-update-updated"></a>Integrationsdienste über Windows Update bereitgestellt \(aktualisiert\) 

Updates für Integrationsservices für Windows-Gastbetriebssysteme werden über Windows Update verteilt. Für Dienstanbieter und private Cloud-Hoster fügt ihn die Kontrolle der Anwendung von Updates in die Hände der Mandanten, die die virtuellen Computer besitzen. Mandanten können ihre Windows-VMs mit allen Updates, einschließlich der Integration Services, Aktualisieren über eine einzelne Methode. Weitere Informationen zu Integrationsdiensten für Linux-Gastbetriebssystemen finden Sie unter [Linux- und FreeBSD-Maschinen auf Hyper-V](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md).  
  
> [!IMPORTANT]  
> Die Bilddatei vmguest.iso ist nicht mehr benötigt, damit sie nicht mit Hyper-V unter Windows Server 2016 enthalten ist.  
  
### <a name="linux-secure-boot-new"></a>Linux sicherer Start \(neu\) 

Linux-Betriebssysteme auf virtuellen Maschinen der Generation 2 können jetzt mit aktivierter Option für den sicheren Start starten. Ubuntu 14.04 und höher, SUSE Linux Enterprise Server 12 und höher, Red Hat Enterprise Linux 7.0 und höher und CentOS 7.0 und höher sind für den sicheren Start auf Hosts aktiviert, auf denen Windows Server 2016 ausgeführt. Bevor Sie den virtuellen Computer zum ersten Mal starten, müssen Sie den virtuellen Computer, verwenden Sie die Microsoft-UEFI-Zertifizierungsstelle konfigurieren. Sie können Hyper-V-Manager, Virtual Machine Manager oder eine Windows Powershell-Sitzung mit erhöhten Rechten dazu. Führen Sie für Windows PowerShell diesen Befehl ein:  
  
```  
Set-VMFirmware TestVM -SecureBootTemplate MicrosoftUEFICertificateAuthority  
```  
  
Weitere Informationen zu virtuellen Linux-Computern auf Hyper-V, finden Sie unter [Linux- und FreeBSD-Maschinen auf Hyper-V](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md). Weitere Informationen zum Cmdlet finden Sie unter [Set-VMFirmware](https://docs.microsoft.com/powershell/module/hyper-v/set-vmfirmware).

### <a name="more-memory-and-processors-for-generation-2-virtual-machines-and-hyper-v-hosts-updated"></a>Mehr Arbeitsspeicher und Prozessoren für virtuelle Maschinen der Generation 2 und Hyper-V-Hosts \(aktualisiert\)

Ab Version 8 können virtuelle Maschinen der Generation 2 deutlich mehr Arbeitsspeicher und virtuelle Prozessoren verwenden. Hosts können ebenfalls mit wesentlich mehr Arbeitsspeicher und virtuelle Prozessoren konfiguriert werden, als zuvor unterstützt wurden. Diese Änderungen neue Szenarien wie das Ausführen von e-Commerce-großer in-Memory-Datenbanken für die onlinetransaktionsverarbeitung (OLTP) "und" Data warehousing (DW) zu unterstützen. Windows Server-Blog veröffentlicht vor kurzem die Leistungsergebnisse eines virtuellen Computers mit Exchange 5.5 Terabyte Arbeitsspeicher und 128 virtuelle Prozessoren, 4-TB-in-Memory-Datenbank ausgeführt wird. Leistung war größer als 95 % der Leistung eines physischen Servers. Weitere Informationen finden Sie unter [Leistung für umfangreiche virtueller Computer in Windows Server 2016 Hyper-V für die in-Memory-transaktionsverarbeitung](https://blogs.technet.microsoft.com/windowsserver/2016/09/28/windows-server-2016-hyper-v-large-scale-vm-performance-for-in-memory-transaction-processing/). Weitere Informationen zu VM-Versionen finden Sie unter [Upgrade VM-Konfigurationsversion in Hyper-V unter Windows 10 oder Windows Server 2016](./deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md). Die vollständige Liste der unterstützten maximalen Konfigurationen, finden Sie unter [Planen der Hyper-V-Skalierbarkeit unter Windows Server 2016](./plan/plan-hyper-v-scalability-in-windows-server.md). 

### <a name="nested-virtualization-new"></a>Geschachtelte Virtualisierung \(neu\)

Dieses Feature können Sie verwenden einen virtuellen Computer als Hyper-V-Host, und Erstellen von virtuellen Computern in dieser virtualisierten Host. Dies kann besonders für Entwicklungs- und testumgebungen nützlich sein. Zur Verwendung der geschachtelten Virtualisierung ist Folgendes erforderlich:  
  
-   Zumindest ausgeführt 2019 für Windows Server, Windows Server 2016 oder Windows 10 auf dem physischen Hyper-V-Host und dem virtualisierten Host.  
  
-   Ein Prozessor mit Intel VT-X (geschachtelter Virtualisierung ist nur für Intel-Prozessoren verfügbar zu diesem Zeitpunkt).  
  
Details und Anweisungen finden Sie unter [Ausführen von Hyper-V auf einem virtuellen Computer mit der geschachtelten Virtualisierung](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization).  
  
### <a name="networking-features-new"></a>Netzwerkfeatures \(neu\)

Neue Features zählen:  
  
-   **Remote direct Memory Access (RDMA) und switch embedded teaming (SET)** . Sie können RDMA einrichten, auf den Netzwerkadapter gebunden, die mit einem virtuellen Hyper-V-Switch, unabhängig davon, ob der Satz auch verwendet wird. Einen virtuellen Switch mit einigen der gleichen Funktionen wie die NIC-Teamvorgang bieten. Weitere Informationen finden Sie unter [(Remote Direct Memory Access, RDMA) und Switch Embedded Teaming (SET)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming).  
  
-   **Virtuellen Computer mit mehreren Warteschlangen (VMMQ)** . VMQ-Durchsatz verbessert durch Zuweisen von mehreren Hardware Warteschlangen pro virtuellem Computer.  Die Standardwarteschlange ist eine Reihe von Warteschlangen für eine virtuelle Maschine, und Datenverkehr wird zwischen den Warteschlangen verteilt.  
  
-   **Quality of Service (QoS) für softwaredefinierte Netzwerke**. Verwaltet die Standardklasse des Datenverkehrs über den virtuellen Switch in die Bandbreite der Standard-Klasse.  
  
Weitere Informationen zu neuen Netzwerkfunktionen, finden Sie unter [Neuigkeiten bei Netzwerken](../../networking/What-s-New-in-Networking.md).  
  
### <a name="production-checkpoints-new"></a>Produktionsprüfpunkte \(neu\)

Produktionsprüfpunkte sind "Point-in-Time" Images eines virtuellen Computers. Diese bieten Ihnen eine Möglichkeit, einen Prüfpunkt anzuwenden, der Support-Richtlinien entspricht bei ein virtuellen Computer eine produktionsworkload ausgeführt wird. Produktionsprüfpunkte basieren auf sicherungstechnologie im Gastbetriebssystem, anstatt einen gespeicherten Zustand versetzt. Für Windows-Computer wird der Volume Snapshot Service (VSS) verwendet. Für virtuelle Linux-Computer werden die Dateisystem-Puffer geleert, um einen Prüfpunkt zu erstellen, der mit dem Dateisystem konsistent ist. Wählen Sie standardprüfpunkte verwenden, wenn Ihnen stattdessen Prüfpunkte basierend auf den gespeicherten Zuständen stattdessen ein. Weitere Informationen finden Sie unter [wählen zwischen Standard- und produktionsprüfpunkten im Hyper-V](manage/Choose-between-standard-or-production-checkpoints-in-Hyper-V.md).  
  
> [!IMPORTANT]  
> Neuer virtuelle Computer verwenden produktionsprüfpunkte als Standard.  
  
### <a name="rolling-hyper-v-cluster-upgrade-new"></a>Paralleles Upgrade von Hyper-V-Cluster \(neu\)

Sie können jetzt auf einen Knoten unter 2019 für Windows Server oder Windows Server 2016 mit einem Hyper-V-Cluster mit Knoten, die mit Windows Server 2012 R2 hinzufügen. Dadurch können Sie den Cluster ohne Ausfallzeiten zu aktualisieren. Der Cluster auf eine Windows Server 2012 R2-Funktionsebene ausgeführt wird, bis Sie aktualisieren Sie alle Knoten im Cluster, und aktualisieren Sie die Funktionsebene des Clusters mit Windows PowerShell-Cmdlet [Update-ClusterFunctionalLevel](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel).  
  
> [!IMPORTANT]  
> Nachdem Sie die Funktionsebene des Clusters aktualisieren, können keine Sie für Windows Server 2012 R2 zurückgegeben werden.  
  
Beachten Sie für einen Hyper-V-Cluster mit der Funktionsebene von Windows Server 2012 R2 mit Knoten, die mit Windows Server 2012 R2, Windows Server-2019 und Windows Server 2016 Folgendes ein:  
  
-   Verwalten Sie den Cluster, Hyper-V und virtuelle Computer von einem Knoten unter Windows Server 2016 oder Windows 10.  
  
-   Sie können virtuelle Maschinen zwischen allen Knoten im Hyper-V-Cluster migrieren.  
  
-   Um die neuen Hyper-V-Features verwenden zu können, müssen alle Knoten Windows Server 2016 ausführen oder und Funktionsebene des Clusters muss aktualisiert werden.  
  
-   Die Konfigurationsversion des virtuellen Computers für vorhandene virtuelle Computer wird nicht aktualisiert. Sie können die Version der Konfiguration aktualisieren, nur nach dem upgrade der Funktionsebene des Clusters.  
  
-   Virtuelle Computer, die Sie erstellen, sind mit Windows Server 2012 R2 Virtual Machine Configuration Ebene 5 kompatibel.  
  
Aktualisieren Sie nach der Funktionsebene des Clusters aus:  
  
-   Sie können die neuen Hyper-V-Features aktivieren.  
  
-   Um neue Features für virtuelle Computer verfügbar zu machen, verwenden Sie das Cmdlet "Update-VmConfigurationVersion" die Ebene der virtuellen Maschine-Konfiguration manuell zu aktualisieren. Anweisungen hierzu finden Sie unter [Upgrade der VM-Version](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md).    
-   Sie können nicht mit dem Hyper-V-Cluster, die Windows Server 2012 R2 ausgeführt wird, einen Knoten hinzufügen.  
  
> [!NOTE]  
> Hyper-V unter Windows 10 unterstützt nicht die Failover-Clusterunterstützung.  
  
Details und Anweisungen finden Sie unter den [Cluster Operating System Rolling Upgrade](https://technet.microsoft.com/library/dn850430.aspx).  

### <a name="shared-virtual-hard-disks-updated"></a>Freigegebene virtuelle Festplatten \(aktualisiert\)
Sie können jetzt freigegebene virtuelle Festplatten (vhdx-Dateien) zum Gast-clustering ohne Ausfallzeiten ändern. Freigegebener virtueller Festplatten können vergrößert oder verkleinert werden, während der virtuelle Computer online ist. Gastcluster können jetzt auch freigegebenen virtuellen Festplatten schützen mithilfe von Hyper-V-Replikat für die notfallwiederherstellung.

Aktivieren der Replikation in der Auflistung. Aktivieren der Replikation für eine Sammlung ist **nur über die WMI-Schnittstelle verfügbar gemacht**. Siehe die Dokumentation für [Msvm_CollectionReplicationService Klasse](https://msdn.microsoft.com/library/mt167787%28v=vs.85%29.aspx) Weitere Details. **Sie können keine Replikation einer Sammlung über PowerShell-Cmdlets oder der Benutzeroberfläche verwalten.** Die virtuellen Computer sollte auf Hosts, die Teil eines Hyper-V-Clusters auf Funktionen zugreifen, die für eine Sammlung spezifisch sind. Dies umfasst freigegebene VHD - freigegebene virtuelle Festplatten auf eigenständigen Hosts werden von Hyper-V-Replikat nicht unterstützt.

Befolgen Sie die Richtlinien für freigegebene virtuelle Festplatten in [Virtual Hard Disk Sharing Overview](https://technet.microsoft.com/library/dn281956.aspx), und achten Sie darauf, dass die freigegebenen virtuellen Festplatten Teil eines gastclusters sind. 

Eine Auflistung mit einer freigegebenen virtuellen Festplatte, aber keine zugeordneten gastcluster kann nicht Bezugspunkte für die Sammlung (unabhängig davon, ob die freigegebene virtuelle Festplatte in die Erstellung von Verweis oder nicht enthalten ist) erstellt werden. 

### <a name="virtual-machine-backupnew"></a>VM-Sicherung\(neu\)

Wenn Sie eine Sicherung ausführen einem einzelnen virtuellen Computer (unabhängig davon, ob Host oder nicht geclustert ist), sollten Sie eine VM-Gruppe nicht verwenden.  Auch sollten Sie eine momentaufnahmesammlung verwenden. VM-Gruppen und Erfassung von Momentaufnahmen, sollen verwendet werden, ausschließlich für die gastcluster, die freigegebenen Vhdx verwenden, sichern. Sie sollten stattdessen durchführen, eine Momentaufnahme mit der [Hyper-V wmiv2-Anbieter](https://msdn.microsoft.com/library/windows/desktop/hh850319(v=vs.85).aspx). Ebenso verwenden Sie nicht die [Failover Cluster-WMI-Anbieter](https://msdn.microsoft.com/library/windows/desktop/mt167750(v=vs.85).aspx).

### <a name="shielded-virtual-machines-new"></a>Von geschützten virtuellen Maschinen \(neu\)

Abgeschirmte virtuelle Computer verwenden verschiedene Funktionen, die es schwieriger zu machen für Hyper-V-Administratoren und Schadsoftware auf dem Host, zu prüfen, Daten aus dem Zustand, der eine geschützte virtuelle Maschine zu stehlen oder manipulieren. Und zustandsmeldungen werden verschlüsselt, Hyper-V-Administratoren nicht angezeigt, die Ausgabe der video- und die Datenträger und die virtuellen Computer beschränkt, nur auf bekannten, fehlerfreien Hosts, der bestimmt, von einem Host-Überwachungsdienst-Server ausgeführt werden. Weitere Informationen finden Sie unter [geschützten Fabric und abgeschirmte VMs](../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md).
  
> [!NOTE]  
> Abgeschirmte virtuelle Computer sind kompatibel mit dem Hyper-V-Replikat. Um eine geschützte VM zu replizieren, muss der Host, die, dem Sie zum replizieren möchten, führen Sie die geschützte virtuelle Maschine autorisiert werden.  

### <a name="start-order-priority-for-clustered-virtual-machines-new"></a>Starten Sie die Priorität der Bestellung für virtuelle Clustercomputer \(neu\)

Dieses Feature bietet Ihnen mehr Kontrolle über die geclusterte virtuelle Computer gestartet oder zuerst neu gestartet. Dies erleichtert es, virtuelle Computer zu starten, die Dienste vor virtuellen Maschinen bereitstellen, die von diesen Diensten verwendet. Definieren von Gruppen, platzieren Sie virtuelle Computer in Gruppen und Angeben von Abhängigkeiten. Verwenden Sie Windows PowerShell-Cmdlets, um die Sätze, zu verwalten, z. B. [New-ClusterGroupSet](https://docs.microsoft.com/powershell/module/failoverclusters/new-clustergroupset), [Get-ClusterGroupSet](https://docs.microsoft.com/powershell/module/failoverclusters/get-clustergroupset), und [hinzufügen-ClusterGroupSetDependency](https://docs.microsoft.com/powershell/module/failoverclusters/add-clustergroupsetdependency).
.  
### <a name="storage-quality-of-service-qos-updated"></a>Quality of Service (QoS) für Speicher \(aktualisiert\)

Sie können nun Speicher-QoS-Richtlinien auf einem Dateiserver mit horizontaler Skalierung erstellen und diese einem oder mehreren virtuellen Datenträgern auf virtuellen Hyper-V-Computern zuweisen. Bei Änderungen der Speicherlast wird die Speicherleistung automatisch neu angepasst, um die Richtlinien einzuhalten. Weitere Informationen finden Sie unter [Storage Quality of Service](../../storage/storage-qos/storage-qos-overview.md).  
  
### <a name="virtual-machine-configuration-file-format-updated"></a>VM-Konfigurationsdateiformat \(aktualisiert\)

Konfigurationsdateien virtueller Computer verwenden Sie ein neues Format, das ist das Lesen und Schreiben von Konfigurationsdaten, die effizienter. Das Format wird auch beschädigte Daten weniger wahrscheinlich, dass im Falle ein Speicherausfalls. Daten-Konfigurationsdateien virtueller Computer verwenden, Erweiterung vmcx, und Runtime Status Datendateien verwenden Erweiterung vmrs.  
  
> [!IMPORTANT]  
> Die Erweiterung vmcx gibt eine binäre Datei an. Bearbeiten der vmcx- oder vmrs-Dateien wird nicht unterstützt.  
  
### <a name="virtual-machine-configuration-version-updated"></a>VM-Konfigurationsversion \(aktualisiert\)

Die Version darstellt, die Kompatibilität der gespeicherte Zustand und Snapshot-Dateien mit der Version von Hyper-V-Konfiguration des virtuellen Computers. Virtuelle Computer mit Version 5 sind kompatibel mit Windows Server 2012 R2 und können auf Windows Server 2012 R2 und Windows Server 2016 ausführen. Virtuelle Computer mit Versionen, die in Windows Server 2016 und Windows Server-2019 eingeführt wird nicht in Hyper-V auf Windows Server 2012 R2 ausgeführt.   
  
Wenn Sie verschieben oder Importieren eines virtuellen Computers auf einem Server mit Hyper-V unter Windows Server 2016 oder Windows Server-2019 von Windows Server 2012 R2, ist nicht der VM Konfiguration automatisch aktualisiert. Dies bedeutet, dass Sie die virtuelle Maschine zurück auf einen Server verschieben können, die Windows Server 2012 R2 ausgeführt wird. Aber dies bedeutet auch, dass Sie neue Features für virtuelle Computer verwenden können, bis Sie die Version der Konfiguration des virtuellen Computers manuell aktualisieren.  
  
Anweisungen zum Überprüfen und Aktualisieren der Version, finden Sie unter [Upgrade der VM-Version](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md). Dieser Artikel beschreibt auch die Version, in der einige Funktionen eingeführt wurden.   
  
> [!IMPORTANT]  
> -   Nachdem Sie die Version aktualisieren, können nicht Sie die virtuelle Maschine auf einem Server verschieben, die Windows Server 2012 R2 ausgeführt wird.  
> -   Sie können nicht die Konfiguration auf eine frühere Version herabstufen.  
> -   Die [Update-VMVersion](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion) Cmdlet wird auf einem Hyper-V-Cluster blockiert, wenn die clusterfunktionsebene auf Windows Server 2012 R2 ist.  

### <a name="virtualization-based-security-for-generation-2-virtual-machines-new"></a>Virtualization-based Sicherheit für virtuelle Maschinen der Generation 2 \(neu)

Virtualisierungsbasierte Sicherheit unterstützt Funktionen wie die Device Guard und Credential Guard, besseren Schutz des Betriebssystems vor Exploits vor Schadsoftware bieten. Virtualisierungsbasierte-Sicherheit ist in virtuelle Maschinen der Generation 2 Gast ab Version 8 verfügbar. Informationen zur Version von Virtual Machine, finden Sie unter [Upgrade VM-Konfigurationsversion in Hyper-V unter Windows 10 oder Windows Server 2016](./deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md).

### <a name="windows-containers-new"></a>Windows-Containern \(neu\)

Windows-Containern können viele isolierte Anwendungen zur Ausführung auf einem Computersystem. Sie können schnell zum Erstellen und hochgradig skalierbaren und hoch portabel. Es sind zwei Arten von containerlaufzeiten verfügbar, jeweils mit unterschiedlichen anwendungsisolierungsgraden bereit. Windows Server-Container verwenden, Namespace- und prozessisolierung. Hyper-V-Container verwenden eine Lightweight-VM für die einzelnen Container.  
  
Wichtige Merkmale:  
  
-   Unterstützung für Websites und Anwendungen, die mithilfe von HTTPS  
  
-   Nano Server kann Windows Server und Hyper-V-Container hosten.  
  
-   Möglichkeit zum Verwalten von Daten über den freigegebenen Ordnern  
  
-   Einschränken von containerressourcen  
  
Weitere Details, einschließlich anhand von schnellstartanleitungen, finden Sie unter den [Dokumentation zu Windows-Containern](https://docs.microsoft.com/virtualization/windowscontainers/index).  
  
### <a name="windows-powershell-direct-new"></a>Windows PowerShell Direct \(neu\)

Dies bietet Ihnen eine Möglichkeit zum Ausführen von Windows PowerShell-Befehle auf einem virtuellen Computer vom Host. Windows PowerShell Direct zwischen Host und dem virtuellen Computer ausgeführt wird. Dies bedeutet, es erfordert keine Netzwerk- oder Anforderungen an Firewalls, und es funktioniert, unabhängig von Ihrer Konfiguration der Remoteverwaltung sichergestellt.  
  
Windows PowerShell Direct ist eine Alternative zu vorhandenen Tools, die Hyper-V-Administratoren für die Verbindung zu einer virtuellen Maschine auf einem Hyper-V-Host verwenden:  
  
-   Remoteverwaltungstools wie PowerShell oder Remotedesktop  
  
-   Verbindung mit Hyper-V virtuellen Computern (VMConnect)  
  
Diese Tools funktionieren gut, aber Sie haben vor-und Nachteile: VMConnect ist zuverlässig, aber es kann schwierig sein zu automatisieren. Remote-PowerShell ist leistungsstark, aber es kann schwierig sein, einrichten und verwalten. Diese vor-und Nachteile sind möglicherweise noch wichtiger, wächst die Hyper-V-Bereitstellung. Windows PowerShell Direct zu diesem Zweck eine leistungsfähige Skripterstellung und Automatisierung zu bieten, die so einfach wie unter Verwendung von VMConnect.
  
Anforderungen und Anleitungen finden Sie unter [verwalten Windows-VMs mit PowerShell Direct](manage/Manage-Windows-virtual-machines-with-PowerShell-Direct.md).  
