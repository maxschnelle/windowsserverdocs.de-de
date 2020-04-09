---
title: Neues in Hyper-V unter Windows Server 2016
description: Bietet eine Zusammenfassung der neuen Features in Hyper-V
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 1a65a98e-54b6-4c41-9732-1e3d32fe3a5f
author: kbdazure
ms.author: kathydav
ms.date: 09/21/2017
ms.openlocfilehash: 5fc82d8eea78ad5605dceb6a21e8d543f9d9c88e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857963"
---
# <a name="whats-new-in-hyper-v-on-windows-server"></a>Neues in Hyper-V unter Windows Server

>Gilt für: Windows Server 2019, Microsoft Hyper-V Server 2016, Windows Server 2016
  
In diesem Artikel werden die neuen und geänderten Funktionen von Hyper-V auf Windows Server 2019, Windows Server 2016 und Microsoft Hyper-V Server 2016 erläutert. Wenn Sie neue Features auf virtuellen Computern verwenden möchten, die mit Windows Server 2012 R2 erstellt wurden und auf einen Server mit Hyper-V unter Windows Server 2019 oder Windows Server 2016 verschoben oder importiert wurden, müssen Sie die Konfigurations Version des virtuellen Computers manuell aktualisieren. Anweisungen finden Sie unter [Aktualisieren der Version der virtuellen Maschine](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md).  
  
Dies ist in diesem Artikel enthalten, und es wird erläutert, ob die Funktionalität neu ist oder aktualisiert wurde.  

## <a name="windows-server-version-1903"></a>Windows Server, Version 1903

### <a name="add-hyper-v-manager-to-server-core-installations-updated"></a>Hinzufügen von Hyper-V-Manager zu Server Core-Installationen (aktualisiert)

Wie Ihnen vielleicht bekannt ist, empfehlen wir die Verwendung der Server Core-Installationsoption beim Einsatz von Windows Server im halbjährlichen Kanal in Produktionsumgebungen. Standardmäßig sind in Server Core jedoch eine Reihe nützlicher Verwaltungstools fortgelassen. Viele der häufig verwendeten Tools lassen sich durch Installieren des App-Kompatibilitätsfeatures hinzufügen, aber einige Tools fehlten immer noch.

Basierend auf dem Kundenfeedback haben wir dem App-Kompatibilitäts Feature in dieser Version noch ein paar weitere Tools hinzugefügt: Hyper-V-Manager (virtmgmt. msc).

Weitere Informationen finden Sie unter [Server Core-App-Kompatibilitätsfeature](../../get-started-19/install-fod-19.md).

## <a name="windows-server-2019"></a>Windows Server 2019

### <a name="security-shielded-virtual-machines-improvements-new"></a>Sicherheit: Verbesserungen der abgeschirmten Virtual Machines (neu)

- **Verbesserungen für Filialen**

    Sie können nun abgeschirmte virtuelle Computer auf Computern mit intermittierender Konnektivität zum Host-Überwachungsdienst (Host Guardian Service, HGS) ausführen, indem Sie die neuen [Fallback-HGS](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office#fallback-configuration)- und [Offline-Modus](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office#offline-mode)-Features nutzen. Fallback HGS ermöglicht es Ihnen, einen zweiten Satz von URLs für Hyper-V zu konfigurieren, um zu prüfen, ob Ihr primärer HGS-Server erreicht werden kann.

    Im Offline-Modus können Sie Ihre abgeschirmten VMs auch dann starten, wenn HGS nicht erreichbar ist, sofern die VM einmal erfolgreich gestartet wurde und sich die Sicherheitskonfiguration des Hosts nicht geändert hat.

- **Verbesserungen bei der Problembehandlung**

    Darüber hinaus haben wir die Problembehandlung bei Ihren [abgeschirmten virtuellen Computern](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-shielded-vms) vereinfacht, indem wir den erweiterten VMConnect-Sitzungsmodus und PowerShell Direct unterstützen. Diese Tools sind besonders nützlich, wenn Sie die Netzwerkverbindung zu Ihrer VM verloren haben und ihre Konfiguration aktualisieren müssen, um den Zugriff wiederherzustellen.

    Diese Features müssen nicht konfiguriert werden, und sie werden automatisch zur Verfügung gestellt, wenn eine abgeschirmte VM auf einem Hyper-V-Host mit Windows Server, Version 1803 oder höher, ausgeführt wird.

- **Linux-Unterstützung**

    Wenn Sie Umgebungen mit gemischten Betriebssystemen ausführen, unterstützt Windows Server 2019 jetzt die Ausführung von Ubuntu, Red Hat Enterprise Linux und SUSE Linux Enterprise Server in abgeschirmten virtuellen Computern.

## <a name="windows-server-2016"></a>Windows Server 2016

### <a name="compatible-with-connected-standby-new"></a>Kompatibel mit verbundenen Standby-\(neue\)

Wenn die Hyper-V-Rolle auf einem Computer installiert ist, der das Energiemodell Always on/Always Connected (AOAC) verwendet, ist der Energiezustand " **verbundener** Standbymodus" nun verfügbar.  
  
### <a name="discrete-device-assignment-new"></a>Diskrete Geräte Zuweisung \(neue\)

Mit diesem Feature können Sie einem virtuellen Computer einen direkten und exklusiven Zugriff auf einige PCIe-Hardware Geräte ermöglichen. Wenn Sie ein Gerät auf diese Weise verwenden, wird der Hyper-V-Virtualisierungsstapel umgangen, was zu einem schnelleren Zugriff führt. Weitere Informationen zur unterstützten Hardware finden Sie unter "diskrete Geräte Zuweisung" unter [System Anforderungen für Hyper-V auf Windows Server 2016](System-requirements-for-Hyper-V-on-Windows.md). Weitere Informationen, einschließlich der Verwendung dieses Features und Überlegungen, finden Sie im Beitrag "[diskrete Geräte Zuweisung – Beschreibung und Hintergrund](https://blogs.technet.microsoft.com/virtualization/2015/11/19/discrete-device-assignment-description-and-background/)" im virtualisierungsblog.

### <a name="encryption-support-for-the-operating-system-disk-in-generation-1-virtual-machines-new"></a>Verschlüsselungs Unterstützung für den Betriebssystem Datenträger in virtuellen Maschinen der Generation 1 \(neu)

Sie können den Betriebssystem Datenträger jetzt mithilfe der BitLocker-Laufwerk Verschlüsselung auf virtuellen Computern der Generation 1 schützen. Ein neues Feature, Schlüsselspeicher, erstellt ein kleines, dediziertes Laufwerk zum Speichern des BitLocker-Schlüssels des System Laufwerks. Dies erfolgt anstelle der Verwendung eines virtuellen Trusted Platform Module (TPM), das nur auf virtuellen Computern der Generation 2 verfügbar ist. Um den Datenträger zu entschlüsseln und den virtuellen Computer zu starten, muss der Hyper-V-Host entweder Teil eines autorisierten geschützten Fabrics sein oder den privaten Schlüssel von einem der Wächter der virtuellen Maschine aufweisen. Der Schlüsselspeicher erfordert einen virtuellen Computer der Version 8. Informationen zur Version der virtuellen Maschine finden Sie unter [Aktualisieren der Version virtueller Computer in Hyper-V unter Windows 10 oder Windows Server 2016](./deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md).  
  
### <a name="host-resource-protection-new"></a>Host Ressourcenschutz \(neue\)

Mit dieser Funktion wird verhindert, dass ein virtueller Computer mehr als den Anteil der Systemressourcen verwendet, indem er nach übermäßigen Aktivitätsstufen sucht. Dadurch kann verhindert werden, dass die übermäßige Aktivität eines virtuellen Computers die Leistung des Hosts oder anderer virtueller Maschinen beeinträchtigt. Wenn die Überwachung einen virtuellen Computer mit übermäßiger Aktivität erkennt, erhält die virtuelle Maschine weniger Ressourcen. Diese Überwachung und Durchsetzung ist standardmäßig deaktiviert. Aktivieren oder deaktivieren Sie diese mithilfe von Windows PowerShell. Um dies zu aktivieren, führen Sie den folgenden Befehl aus:  
  
```
Set-VMProcessor TestVM -EnableHostResourceProtection $true
```

Weitere Informationen zu diesem Cmdlet finden Sie unter [Set-vmprocessor](https://docs.microsoft.com/powershell/module/hyper-v/set-vmprocessor).

### <a name="hot-add-and-remove-for-network-adapters-and-memory-new"></a>Hot Add und Remove für Netzwerkadapter und Arbeitsspeicher \(neue\)

Sie können nun einen Netzwerkadapter hinzufügen oder entfernen, während der virtuelle Computer ausgeführt wird, ohne Ausfallzeiten zu verursachen. Dies funktioniert für virtuelle Computer der Generation 2, auf denen Windows-oder Linux-Betriebssysteme ausgeführt werden.  
  
Sie können auch die Menge an Arbeitsspeicher anpassen, die einem virtuellen Computer während der Ausführung zugewiesen wird, auch wenn Sie dynamischer Arbeitsspeicher nicht aktiviert haben. Dies funktioniert für virtuelle Computer der Generation 1 und Generation 2, auf denen Windows Server 2016 oder Windows 10 ausgeführt wird.  

### <a name="hyper-v-manager-improvements-updated"></a>Verbesserungen der Hyper-V-Manager \(aktualisiert\) 
  
-   **Unterstützung alternativer Anmelde** Informationen: Sie können nun einen anderen Satz von Anmelde Informationen im Hyper-V-Manager verwenden, wenn Sie eine Verbindung mit einem anderen Windows Server 2016-oder Windows 10-Remote Host herstellen. Sie können diese Anmelde Informationen auch speichern, um die Anmeldung zu vereinfachen.  
  
-   **Verwalten früherer Versionen** : mit dem Hyper-v-Manager in Windows Server 2019, Windows Server 2016 und Windows 10 können Sie Computer verwalten, auf denen Hyper-v unter Windows Server 2012, Windows 8, Windows Server 2012 R2 und Windows 8.1 ausgeführt wird.  
  
-   **Aktualisiertes Verwaltungs Protokoll** : der Hyper-v-Manager kommuniziert jetzt mit Remote-Hyper-v-Hosts mithilfe des WS-man-Protokolls, das die CredSSP-, Kerberos-oder NTLM-Authentifizierung zulässt. Wenn Sie zum Herstellen einer Verbindung mit einem Hyper-V-Remote Host mithilfe von "andssp" eine Verbindung herstellen, können Sie eine Live Migration durchführen, ohne die eingeschränkte Delegierung Active Directory in Mit der WS-man-basierten Infrastruktur wird auch das Aktivieren eines Hosts für die Remote Verwaltung vereinfacht. WS-MAN stellt über Port 80 eine Verbindung her, der standardmäßig geöffnet ist.  
  
### <a name="integration-services-delivered-through-windows-update-updated"></a>Von Windows Update \(aktualisierte Integrationsdienste\) 

Aktualisierungen von Integration Services für Windows-Gäste werden über Windows Update verteilt. Für Dienstanbieter und Private Cloud Hoster wird dadurch das Anwenden von Updates auf die Hände der Mandanten, die die virtuellen Computer besitzen, gesteuert. Mandanten können nun Ihre virtuellen Windows-Computer mit allen Updates, einschließlich der Integrationsdienste, mithilfe einer einzigen Methode aktualisieren. Ausführliche Informationen zu Integration Services für Linux-Gäste finden Sie [unter Linux und FreeBSD Virtual Machines auf Hyper-V](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md).  
  
> [!IMPORTANT]  
> Die Image Datei "vmguest. ISO" wird nicht mehr benötigt und ist daher nicht in Hyper-V unter Windows Server 2016 enthalten.  
  
### <a name="linux-secure-boot-new"></a>Virtueller Linux-Start \(neue\) 

Linux-Betriebssysteme auf virtuellen Computern der Generation 2 können jetzt mit aktivierter Option "sicherer Start" gestartet werden. Ubuntu 14,04 und höher, SuSE Linux Enterprise Server 12 und höher, Red Hat Enterprise Linux 7,0 und höher, und CentOS 7,0 und höher sind für den sicheren Start auf Hosts aktiviert, auf denen Windows Server 2016 ausgeführt wird. Bevor Sie den virtuellen Computer zum ersten Mal starten, müssen Sie den virtuellen Computer für die Verwendung der Microsoft UEFI-Zertifizierungsstelle konfigurieren. Hierzu können Sie den Hyper-V-Manager, Virtual Machine Manager oder eine Windows PowerShell-Sitzung mit erhöhten Rechten verwenden. Führen Sie für Windows PowerShell den folgenden Befehl aus:  
  
```  
Set-VMFirmware TestVM -SecureBootTemplate MicrosoftUEFICertificateAuthority  
```  
  
Weitere Informationen zu virtuellen Linux-Computern in Hyper-v finden Sie [unter Linux und FreeBSD Virtual Machines auf Hyper-v](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md). Weitere Informationen zum Cmdlet finden Sie unter [Set-vmfirmware](https://docs.microsoft.com/powershell/module/hyper-v/set-vmfirmware).

### <a name="more-memory-and-processors-for-generation-2-virtual-machines-and-hyper-v-hosts-updated"></a>Mehr Arbeitsspeicher und Prozessoren für virtuelle Maschinen der Generation 2 und Hyper-V-Hosts \(aktualisiert\)

Ab Version 8 können virtuelle Maschinen der Generation 2 erheblich mehr Arbeitsspeicher und virtuelle Prozessoren verwenden. Hosts können auch mit wesentlich mehr Arbeitsspeicher und virtuellen Prozessoren konfiguriert werden, als zuvor unterstützt wurden. Diese Änderungen unterstützen neue Szenarien, wie z. b. das Ausführen von großen in-Memory-Datenbanken für die Online Transaktionsverarbeitung (OLTP) und Data Warehousing (DW). Der Windows Server-Blog veröffentlichte vor kurzem die Leistungsergebnisse eines virtuellen Computers mit 5,5 Terabyte Arbeitsspeicher und 128 virtuellen Prozessoren mit einer in-Memory Database von 4 TB. Die Leistung war größer als 95% der Leistung eines physischen Servers. Weitere Informationen finden Sie unter [Windows Server 2016 Hyper-V-VM-Leistung in großem Maßstab für die Verarbeitung im Arbeitsspeicher](https://blogs.technet.microsoft.com/windowsserver/2016/09/28/windows-server-2016-hyper-v-large-scale-vm-performance-for-in-memory-transaction-processing/). Weitere Informationen zu Versionen von virtuellen Computern finden Sie unter [Aktualisieren der Version virtueller Computer in Hyper-V unter Windows 10 oder Windows Server 2016](./deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md). Die vollständige Liste der unterstützten maximalen Konfigurationen finden Sie unter [Planen der Hyper-V-Skalierbarkeit in Windows Server 2016](./plan/plan-hyper-v-scalability-in-windows-server.md). 

### <a name="nested-virtualization-new"></a>\(neue\)

Mit dieser Funktion können Sie einen virtuellen Computer als Hyper-V-Host verwenden und virtuelle Maschinen innerhalb dieses virtualisierten Hosts erstellen. Dies kann besonders für Entwicklungs-und Testumgebungen nützlich sein. Um die Netzwerkvirtualisierung verwenden zu können, benötigen Sie Folgendes:  
  
-   Zum Ausführen von mindestens Windows Server 2019, Windows Server 2016 oder Windows 10 auf dem physischen Hyper-V-Host und dem virtualisierten Host.  
  
-   Ein Prozessor mit Intel VT-x (Nested Virtualization steht zurzeit nur für Intel-Prozessoren zur Verfügung).  
  
Weitere Informationen und Anweisungen finden Sie unter [Ausführen von Hyper-V auf einem virtuellen Computer mit der Netzwerkvirtualisierung](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization).  
  
### <a name="networking-features-new"></a>Netzwerk Features \(neue\)

Zu den neuen Netzwerk Features gehören:  
  
-   **Remote Zugriff auf den direkten Speicher (RDMA) und Switch Embedded Team Vorgang (Set)** . Sie können RDMA für Netzwerkadapter einrichten, die an einen virtuellen Hyper-V-Switch gebunden sind, unabhängig davon, ob auch Set verwendet wird. Set bietet einen virtuellen Switch mit einigen der gleichen Funktionen wie der NIC-Team Vorgang. Weitere Informationen finden Sie unter [Remote Direct Memory Access (RDMA) und Switch Embedded Teaming (Set)](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming).  
  
-   **Virtual Machine-multiwarteschlangen (vmmq)** . Verbessert den VMQ-Durchsatz durch Zuordnen mehrerer Hardware Warteschlangen pro virtuellem Computer.  Die Standard Warteschlange wird zu einem Satz von Warteschlangen für einen virtuellen Computer, und der Datenverkehr wird zwischen den Warteschlangen verteilt.  
  
-   **Quality of Service (QoS) für softwaredefinierte Netzwerke**. Verwaltet die Standardklasse des Datenverkehrs über den virtuellen Switch innerhalb der standardmäßigen Klassen Bandbreite.  
  
Weitere Informationen zu neuen Netzwerk Features finden Sie unter [What es New in Networking](../../networking/What-s-New-in-Networking.md).  
  
### <a name="production-checkpoints-new"></a>Produktions Prüfpunkte \(neue\)

Produktions Prüfpunkte sind "Point-in-Time"-Images einer virtuellen Maschine. Auf diese Weise können Sie einen Prüfpunkt anwenden, der den Unterstützungs Richtlinien entspricht, wenn ein virtueller Computer eine produktionsworkloads ausführt. Produktions Prüfpunkte basieren auf Sicherungs Technologie innerhalb des Gast Betriebssystems anstelle eines gespeicherten Zustands. Bei virtuellen Windows-Computern wird der volumemomentaufnahme-Dienst (VSS) verwendet. Bei virtuellen Linux-Computern werden die Dateisystem Puffer geleert, um einen Prüfpunkt zu erstellen, der mit dem Dateisystem konsistent ist. Wenn Sie stattdessen Prüfpunkte auf der Grundlage gespeicherter Zustände verwenden möchten, wählen Sie stattdessen Standard Prüfpunkte aus. Weitere Informationen finden [Sie unter Auswählen zwischen Standard-oder Produktions Prüfpunkten in Hyper-V](manage/Choose-between-standard-or-production-checkpoints-in-Hyper-V.md).  
  
> [!IMPORTANT]  
> Bei neuen virtuellen Computern werden Produktions Prüfpunkte als Standard verwendet.  
  
### <a name="rolling-hyper-v-cluster-upgrade-new"></a>Paralleles Upgrade für Hyper-V-Cluster \(neue\)

Sie können nun einen Knoten unter Windows Server 2019 oder Windows Server 2016 zu einem Hyper-V-Cluster hinzufügen, auf dem Windows Server 2012 R2 ausgeführt wird. Dies ermöglicht es Ihnen, den Cluster ohne Ausfallzeiten zu aktualisieren. Der Cluster wird auf einer Windows Server 2012 R2-Funktionsebene ausgeführt, bis Sie ein Upgrade für alle Knoten im Cluster durchführen und die Cluster Funktionsebene mit dem Windows PowerShell-Cmdlet [Update-clusterfunctionallevel](https://docs.microsoft.com/powershell/module/failoverclusters/Update-ClusterFunctionalLevel)aktualisieren.  
  
> [!IMPORTANT]  
> Nachdem Sie die Cluster Funktionsebene aktualisiert haben, können Sie Sie nicht mehr an Windows Server 2012 R2 zurückgeben.  
  
Für einen Hyper-V-Cluster mit einer Funktionsebene von Windows Server 2012 R2 mit Knoten, auf denen Windows Server 2012 R2, Windows Server 2019 und Windows Server 2016 ausgeführt wird, beachten Sie Folgendes:  
  
-   Verwalten Sie den Cluster, Hyper-V und virtuelle Computer von einem Knoten, auf dem Windows Server 2016 oder Windows 10 ausgeführt wird.  
  
-   Sie können virtuelle Maschinen zwischen allen Knoten im Hyper-V-Cluster verschieben.  
  
-   Wenn Sie neue Hyper-V-Features verwenden möchten, müssen auf allen Knoten Windows Server 2016 oder ausgeführt werden, und die Cluster Funktionsebene muss aktualisiert werden.  
  
-   Die Konfigurations Version des virtuellen Computers für vorhandene virtuelle Maschinen wird nicht aktualisiert. Sie können die Konfigurations Version erst aktualisieren, nachdem Sie die Cluster Funktionsebene aktualisiert haben.  
  
-   Virtuelle Computer, die Sie erstellen, sind kompatibel mit Windows Server 2012 R2, VM-Konfigurations Ebene 5.  
  
Nachdem Sie die Cluster Funktionsebene aktualisiert haben:  
  
-   Sie können neue Hyper-V-Features aktivieren.  
  
-   Um neue Features für virtuelle Computer verfügbar zu machen, verwenden Sie das Update-vmconfigurationversion-Cmdlet, um die Konfigurations Ebene des virtuellen Computers manuell zu aktualisieren. Anweisungen finden Sie unter [Aktualisieren der Version der virtuellen Maschine](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md).    
-   Sie können dem Hyper-V-Cluster, auf dem Windows Server 2012 R2 ausgeführt wird, keinen Knoten hinzufügen.  
  
> [!NOTE]  
> Hyper-V unter Windows 10 unterstützt kein Failoverclustering.  
  
Weitere Informationen und Anweisungen finden Sie unter Paralleles [Upgrade des Cluster Betriebssystems](https://technet.microsoft.com/library/dn850430.aspx).  

### <a name="shared-virtual-hard-disks-updated"></a>Freigegebene virtuelle Festplatten \(aktualisiert\)
Sie können jetzt die Größe der freigegebenen virtuellen Festplatten (vhdx-Dateien), die für Gastclustering verwendet werden, ohne Ausfallzeiten ändern. Freigegebene virtuelle Festplatten können vergrößert oder verkleinert werden, während der virtuelle Computer online ist. Gast Cluster können jetzt auch freigegebene virtuelle Festplatten mithilfe des Hyper-V-Replikats für die Notfall Wiederherstellung schützen.

Aktivieren Sie die Replikation für die Sammlung. Das Aktivieren der Replikation für eine Sammlung wird **nur über die WMI-Schnittstelle**verfügbar gemacht. Weitere Informationen finden Sie in der Dokumentation zur [Msvm_CollectionReplicationService-Klasse](https://msdn.microsoft.com/library/mt167787%28v=vs.85%29.aspx) . **Die Replikation einer Sammlung kann nicht über das PowerShell-Cmdlet oder die Benutzeroberfläche verwaltet werden.** Die VMs sollten sich auf Hosts befinden, die Teil eines Hyper-V-Clusters sind, um auf Features zuzugreifen, die für eine Sammlung spezifisch sind. Dies gilt auch für freigegebene virtuelle Festplatten: freigegebene virtuelle Festplatten auf eigenständigen Hosts werden vom Hyper-V-Replikat nicht unterstützt.

Befolgen Sie die Richtlinien für freigegebene VHDs unter [Übersicht über die Freigabe virtueller Festplatten](https://technet.microsoft.com/library/dn281956.aspx), und stellen Sie sicher, dass die freigegebenen VHDs Teil eines Gast Clusters sind. 

Eine Sammlung mit einer freigegebenen VHD, aber keinem zugeordneten Gast Cluster, kann keine Referenzpunkte für die Sammlung erstellen (unabhängig davon, ob die freigegebene virtuelle Festplatte in der Referenzpunkt Erstellung enthalten ist oder nicht). 

### <a name="virtual-machine-backupnew"></a>Sicherung virtueller Computer\(neue\)

Wenn Sie einen einzelnen virtuellen Computer sichern (unabhängig davon, ob der Host geclustert ist), sollten Sie keine VM-Gruppe verwenden.  Sie sollten auch keine Momentaufnahme Sammlung verwenden. VM-Gruppen und die Momentaufnahme Sammlung dienen ausschließlich zum Sichern von Gast Clustern, die freigegebene vhdx verwenden. Stattdessen sollten Sie eine Momentaufnahme mithilfe des [Hyper-V-WMI v2-Anbieters](https://msdn.microsoft.com/library/windows/desktop/hh850319(v=vs.85).aspx)erstellen. Verwenden Sie auch den [WMI-Anbieter für den Failovercluster](https://msdn.microsoft.com/library/windows/desktop/mt167750(v=vs.85).aspx)nicht.

### <a name="shielded-virtual-machines-new"></a>Geschützte virtuelle Computer \(neue\)

Abgeschirmte virtuelle Computer verwenden mehrere Features, um Hyper-V-Administratoren und Schadsoftware auf dem Host das überprüfen, manipulieren oder stehlen von Daten aus dem Zustand eines abgeschirmten virtuellen Computers zu erschweren. Daten und Status sind verschlüsselt, Hyper-V-Administratoren können die Videoausgabe und die Datenträger nicht anzeigen, und die virtuellen Computer können so eingeschränkt werden, dass Sie nur auf bekannten, fehlerfreien Hosts ausgeführt werden, die von einem Host-Überwachungs Server bestimmt werden. Weitere Informationen finden Sie unter geschütztes [Fabric und abgeschirmte VMS](../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md).
  
> [!NOTE]  
> Abgeschirmte virtuelle Computer sind mit dem Hyper-V-Replikat kompatibel. Zum Replizieren einer abgeschirmten virtuellen Maschine muss der Host, auf den Sie replizieren möchten, autorisiert sein, die geschützte virtuelle Maschine auszuführen.  

### <a name="start-order-priority-for-clustered-virtual-machines-new"></a>Priorität der Reihenfolge der virtuellen Cluster Computer \(neue\)

Diese Funktion ermöglicht Ihnen mehr Kontrolle darüber, welche virtuellen Cluster Computer zuerst gestartet oder neu gestartet werden. Dies erleichtert das Starten von virtuellen Computern, die Dienste vor virtuellen Computern bereitstellen, die diese Dienste verwenden. Definieren von Sätzen, platzieren virtueller Maschinen in Gruppen und Angeben von Abhängigkeiten. Verwenden Sie Windows PowerShell-Cmdlets, um die Sätze zu verwalten, z. b. [New-clustergroupset](https://docs.microsoft.com/powershell/module/failoverclusters/new-clustergroupset), [Get-clustergroupset](https://docs.microsoft.com/powershell/module/failoverclusters/get-clustergroupset)und [Add-clustergroupsetabhängigkeit](https://docs.microsoft.com/powershell/module/failoverclusters/add-clustergroupsetdependency).
.  
### <a name="storage-quality-of-service-qos-updated"></a>Quality of Service (QoS) für Speicher \(aktualisiert\)

Sie können nun Speicher-QoS-Richtlinien auf einem Dateiserver mit horizontaler Skalierung erstellen und diese einem oder mehreren virtuellen Datenträgern auf virtuellen Hyper-V-Computern zuweisen. Bei Änderungen der Speicherlast wird die Speicherleistung automatisch neu angepasst, um die Richtlinien einzuhalten. Weitere Informationen finden Sie unter [Storage Quality of Service](../../storage/storage-qos/storage-qos-overview.md).  
  
### <a name="virtual-machine-configuration-file-format-updated"></a>Das Konfigurationsdatei Format des virtuellen Computers \(aktualisiert\)

Konfigurationsdateien für virtuelle Computer verwenden ein neues Format, das das Lesen und Schreiben von Konfigurationsdaten effizienter macht. Das Format führt auch zu einer Beschädigung der Daten, wenn ein Speicherfehler auftritt. Die Datendateien der Konfiguration der virtuellen Maschine verwenden eine vmcx-Dateinamenerweiterung und Datendateien für den Lauf Zeit Zustand verwenden die Dateinamenerweiterung. VMRS.  
  
> [!IMPORTANT]  
> Die vmcx-Dateierweiterung gibt eine Binärdatei an. Das Bearbeiten von vmcx-oder VMRS-Dateien wird nicht unterstützt.  
  
### <a name="virtual-machine-configuration-version-updated"></a>Die Konfigurations Version des virtuellen Computers \(aktualisiert\)

Die Version stellt die Kompatibilität der Konfiguration der virtuellen Maschine, des gespeicherten Zustands und der Momentaufnahme Dateien mit der Hyper-V-Version dar. Virtuelle Computer mit Version 5 sind kompatibel mit Windows Server 2012 R2 und können unter Windows Server 2012 R2 und Windows Server 2016 ausgeführt werden. Virtuelle Computer, deren Versionen in Windows Server 2016 und Windows Server 2019 eingeführt wurden, werden nicht in Hyper-V unter Windows Server 2012 R2 ausgeführt.   
  
Wenn Sie eine virtuelle Maschine auf einen Server mit Hyper-V unter Windows Server 2016 oder Windows Server 2019 von Windows Server 2012 R2 verschieben oder importieren, wird die Konfiguration der virtuellen Maschine nicht automatisch aktualisiert. Dies bedeutet, dass Sie den virtuellen Computer auf einen Server zurück verschieben können, auf dem Windows Server 2012 R2 ausgeführt wird. Dies bedeutet jedoch auch, dass Sie die neuen Features für virtuelle Computer erst verwenden können, wenn Sie die Version der Konfiguration der virtuellen Maschine manuell aktualisieren.  
  
Anweisungen zum Überprüfen und Aktualisieren der Version finden Sie unter [Aktualisieren der Version der virtuellen Maschine](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md). In diesem Artikel wird außerdem die Version aufgeführt, in der einige Features eingeführt wurden.   
  
> [!IMPORTANT]  
> -   Nachdem Sie die Version aktualisiert haben, können Sie die virtuelle Maschine nicht auf einen Server mit Windows Server 2012 R2 verschieben.  
> -   Sie können die Konfiguration nicht auf eine frühere Version herabstufen.  
> -   Das [Update-VMVersion-](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion) Cmdlet wird auf einem Hyper-V-Cluster blockiert, wenn die Cluster Funktionsebene Windows Server 2012 R2 ist.  

### <a name="virtualization-based-security-for-generation-2-virtual-machines-new"></a>Virtualisierungsbasierte Sicherheit für virtuelle Maschinen der Generation 2 \(neu)

Virtualisierungsbasierte Sicherheit stellt Features wie Device Guard und Credential Guard bereit und bietet einen verstärkten Schutz des Betriebssystems gegen Exploits von Schadsoftware. Virtualisierungsbasiert: Sicherheit ist auf virtuellen Gast Computern der Generation 2 ab Version 8 verfügbar. Informationen zur Version der virtuellen Maschine finden Sie unter [Aktualisieren der Version virtueller Computer in Hyper-V unter Windows 10 oder Windows Server 2016](./deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md).

### <a name="windows-containers-new"></a>Windows-Container \(neue\)

Mit Windows-Containern können viele isolierte Anwendungen auf einem Computersystem ausgeführt werden. Sie können schnell erstellt werden und sind hochgradig skalierbar und portabel. Es sind zwei Typen von Container Laufzeit verfügbar, von denen jede einen anderen Grad an Anwendungs Isolation hat. Windows Server-Container verwenden Namespace-und Prozess Isolation. Für Hyper-V-Container wird für jeden Container ein einfacher virtueller Computer verwendet.  
  
Wichtige Merkmale:  
  
-   Unterstützung für Websites und Anwendungen mit HTTPS  
  
-   Nano Server kann sowohl Windows Server-als auch Hyper-V-Container hosten.  
  
-   Möglichkeit zum Verwalten von Daten über freigegebene Container Ordner  
  
-   Möglichkeit zum Einschränken von Container Ressourcen  
  
Weitere Informationen, einschließlich Schnellstart Handbücher, finden Sie in der [Dokumentation zu Windows-Containern](https://docs.microsoft.com/virtualization/windowscontainers/index).  
  
### <a name="windows-powershell-direct-new"></a>Windows PowerShell Direct \(neue\)

Dadurch haben Sie die Möglichkeit, Windows PowerShell-Befehle auf einem virtuellen Computer auf dem Host auszuführen. Windows PowerShell Direct wird zwischen dem Host und dem virtuellen Computer ausgeführt. Dies bedeutet, dass keine Netzwerk-oder Firewallanforderungen erforderlich sind und unabhängig von Ihrer Remote Verwaltungs Konfiguration funktionieren.  
  
Windows PowerShell Direct ist eine Alternative zu den vorhandenen Tools, die von Hyper-v-Administratoren verwendet werden, um eine Verbindung mit einer virtuellen Maschine auf einem Hyper-v-Host herzustellen:  
  
-   Remoteverwaltungstools wie PowerShell oder Remotedesktop  
  
-   Verbindung mit dem virtuellen Hyper-V-Computer (VMConnect)  
  
Diese Tools funktionieren gut, haben jedoch Kompromisse: VMConnect ist zuverlässig, kann aber nur schwer automatisiert werden. Remote-PowerShell ist leistungsstark, kann aber nur schwer einzurichten und zu warten. Diese Kompromisse werden möglicherweise wichtiger, wenn Ihre Hyper-V-Bereitstellung zunimmt. Windows PowerShell Direct wendet dies durch die Bereitstellung einer leistungsstarken Skript-und Automatisierungsfunktion an, die so einfach ist wie die Verwendung von VMConnect.
  
Anforderungen und Anweisungen finden Sie unter [Verwalten virtueller Windows-Computer mit PowerShell Direct](manage/Manage-Windows-virtual-machines-with-PowerShell-Direct.md).  
