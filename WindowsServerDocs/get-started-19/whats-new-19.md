---
title: Neuerungen in Windows Server 2019
description: Eine Übersicht über neue Features in Windows Server 2019, einschließlich Desktopdarstellung, Speichermigrationsdienst, Systemdaten, Azure-Netzwerkadapter, Verbesserungen bei „Direkte Speicherplätze“ und weitere Änderungen.
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: high
ms.date: 06/04/2019
ms.openlocfilehash: fd094347679d147a04faefdf3741a06addda2026
ms.sourcegitcommit: 78b59522234825c43b00c271a04c35f3fd9d65e3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/22/2020
ms.locfileid: "86946578"
---
# <a name="whats-new-in-windows-server-2019"></a>Neuerungen in Windows Server 2019

> Gilt für: Windows Server 2019

In diesem Thema werden einige der neuen Features in Windows Server 2019 beschrieben. Windows Server 2019 basiert auf dem soliden Fundament von Windows Server 2016 und bietet zahlreiche Innovationen bei vier wichtigen Themen: „Hybrid Cloud“, „Sicherheit“, „Anwendungsplattform“ und „Hyperkonvergente Infrastruktur (HCI)“.

Wenn Sie erfahren möchten, welche Neuerungen es im halbjährlichen Kanal von Windows Server gibt, lesen Sie [Neuerungen in Windows Server](../get-started/whats-new-in-windows-server.md).

## <a name="general"></a>Allgemein

### <a name="windows-admin-center"></a>Windows Admin Center

Windows Admin Center ist eine lokal bereitgestellte, browserbasierte App zum Verwalten von Servern, Clustern, hyperkonvergenter Infrastruktur und Windows 10-PCs. Sie ist ohne über Windows hinausgehende Kosten erhältlich und für den Einsatz in Produktionsumgebungen bereit.

Sie können Windows Admin Center unter Windows Server 2019 sowie Windows 10 und früheren Versionen von Windows und Windows Server installieren und damit Server und Cluster verwalten, die unter Windows Server 2008 R2 und höher ausgeführt werden.

Weitere Informationen finden Sie unter [Windows Admin Center](../manage/windows-admin-center/overview.md).

### <a name="desktop-experience"></a>Desktopdarstellung

Da es sich bei Windows Server 2019 um eine Long-Term Servicing Channel (LTSC)-Version handelt, ist darin <b>Desktopdarstellung</b> enthalten. (Versionen des halbjährlichen Kanals (Semi-Annual Channel, \(SAC\))) enthalten standardmäßig nicht die Desktopdarstellung, sondern sind ausschließlich Versionen von Server Core- und Nano Server-Containerimages.) Wie bei Windows Server 2016 können Sie beim Einrichten des Betriebssystems zwischen Server Core-Installationen oder Server mit Desktopdarstellung-Installationen wählen.

### <a name="system-insights"></a>Systemdaten

Systemdaten ist ein neues Feature von Windows Server 2019, mit der lokale Predictive Analytics-Funktionen direkt in Windows Server integriert werden können. Diese Vorhersagefunktionen, die jeweils von einem Machine Learning-Modell unterstützt werden, analysieren lokal Windows Server-Systemdaten wie Leistungsindikatoren und Ereignisse, geben Einblick in die Funktionsweise Ihrer Server und helfen Ihnen dabei, die Betriebskosten im Zusammenhang mit der reaktiven Verwaltung von Problemen in Ihren Windows Server-Bereitstellungen zu reduzieren.

## <a name="hybrid-cloud"></a>Hybrid Cloud

### <a name="server-core-app-compatibility-feature-on-demand"></a>Optionales Feature (FOD, Feature on Demand) „Server Core-App-Kompatibilität”

Das [optionale Feature (FOD) "Server Core-App-Kompatibilität"](./install-fod-19.md) verbessert die App-Kompatibilität für die Windows Server Core-Installationsoption erheblich durch Hinzufügen einer Teilmenge von Binärdateien und Komponenten von Windows Server mit Desktop Experience, ohne dass die Windows Server Desktop Experience-Grafikumgebung selbst hinzugefügt wird.  Dies erfolgt, um die Funktionalität und Kompatibilität von Server Core zu erhöhen und es gleichzeitig möglichst schlank zu halten.  

Dieses optionale FOD ist in einer separaten ISO verfügbar und kann nur Windows Server Core-Installationen und -Images mithilfe von DISM hinzugefügt werden. 

## <a name="security"></a>Sicherheit

### <a name="windows-defender-advanced-threat-protection-atp"></a>Windows Defender Advanced Threat Protection (ATP)

Die umfassenden Plattformsensoren und Reaktionsaktionen von ATP decken Angriffe auf Speicher- und Kernel-Ebene auf und reagieren darauf, indem sie bösartige Dateien unterdrücken und schädliche Prozesse beenden.

-   Weitere Informationen zu Windows Defender ATP finden Sie in der [Übersicht über die Windows Defender ATP-Funktionen](/windows/security/threat-protection/windows-defender-atp/overview).

-   Weitere Informationen zum Onboarding von Servern finden Sie unter [Integrieren von Servern im Windows Defender ATP-Dienst](/windows/security/threat-protection/windows-defender-atp/configure-server-endpoints-windows-defender-advanced-threat-protection).

**Windows Defender ATP Exploit Guard** ist eine neue Reihe von Host-Intrusion-Prevention-Funktionen. Die vier Komponenten von Windows Defender Exploit Guard wurden entwickelt, um das Gerät gegen eine Vielzahl von Angriffsvektoren zu schützen und Verhaltensweisen zu blockieren, die häufig bei Angriffen durch Schadsoftware eingesetzt werden. Gleichzeitig können Sie Sicherheitsrisiken und Produktivitätsanforderungen ausbalancieren.

-   [Attack Surface Reduction (ASR)](/windows/security/threat-protection/windows-defender-exploit-guard/attack-surface-reduction-exploit-guard?ocid=cx-blog-mmpc) umfasst eine Reihe von Steuerelementen, mit denen Unternehmen verhindern können, dass Schadsoftware auf die Computer gelangt, indem sie verdächtige schädliche Dateien (z.B. Office-Dateien), Skripts, seitliche Bewegungen, Ransomware-Verhalten und E-Mail-basierte Bedrohungen blockieren.

-   [Netzwerkschutz](/windows/security/threat-protection/microsoft-defender-atp/network-protection) schützt den Endpunkt vor webbasierten Bedrohungen, indem er jeden ausgehenden Prozess auf dem Gerät an nicht vertrauenswürdige Hosts/IP-Adressen über Windows Defender SmartScreen blockiert.

-   [Kontrollierter Ordnerzugriff](https://cloudblogs.microsoft.com/microsoftsecure/2017/10/23/stopping-ransomware-where-it-counts-protecting-your-data-with-controlled-folder-access/?ocid=cx-blog-mmpc?source=mmpc) schützt sensible Daten vor Ransomware, indem er verhindert, dass nicht vertrauenswürdige Prozesse auf Ihre geschützten Ordner zugreifen.

-   [Exploit-Schutz](/windows/security/threat-protection/windows-defender-exploit-guard/exploit-protection-exploit-guard) ist eine Reihe von Maßnahmen zur Minderung von Schwachstellen (ersetzt EMET), die einfach konfiguriert werden können, um Ihr System und Ihre Anwendungen zu schützen.

[Windows Defender-Anwendungssteuerung](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) (auch bekannt als „Codeintegritätsrichtlinie – CI-Richtlinie“) wurde in Windows Server 2016 veröffentlicht.
Das Feedback von Kunden hat gezeigt, dass dies ein großartiges Konzept ist, das aber nur unter Schwierigkeiten bereitgestellt werden kann.
Um dies zu beheben, haben wir standardmäßige CI-Richtlinien erstellt, die alle Windows-internen Dateien und Microsoft-Anwendungen wie SQL Server zulassen, aber bekannte ausführbare Dateien blockieren, die CI umgehen können. 

### <a name="security-with-software-defined-networking-sdn"></a>Sicherheit mit Software-Defined Networking (SDN)

[Sicherheit mit SDN](../networking/sdn/security/sdn-security-top.md) bietet zahlreiche Features, um das Kundenvertrauen bei der Ausführung von Workloads – entweder lokal oder als Dienstanbieter in der Cloud – zu erhöhen. 

Diese Sicherheitsverbesserungen sind in die umfassende SDN-Plattform integriert, die in Windows Server 2016 eingeführt wurde.

Eine vollständige Liste der Neuerungen in SDN finden Sie unter [Neuerungen in SDN für Windows Server 2019](../networking/sdn/sdn-whats-new.md).

### <a name="shielded-virtual-machines-improvements"></a>Verbesserungen für abgeschirmte virtuelle Computer

- **Verbesserungen für Filialen**

    Sie können nun abgeschirmte virtuelle Computer auf Computern mit intermittierender Konnektivität zum Host-Überwachungsdienst (Host Guardian Service, HGS) ausführen, indem Sie die neuen [Fallback-HGS](../security/guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office.md#fallback-configuration)- und [Offline-Modus](../security/guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office.md#offline-mode)-Features nutzen. Fallback HGS ermöglicht es Ihnen, einen zweiten Satz von URLs für Hyper-V zu konfigurieren, um zu prüfen, ob Ihr primärer HGS-Server erreicht werden kann.

    Im Offline-Modus können Sie Ihre abgeschirmten VMs auch dann starten, wenn HGS nicht erreichbar ist, sofern die VM einmal erfolgreich gestartet wurde und sich die Sicherheitskonfiguration des Hosts nicht geändert hat.

- **Verbesserungen bei der Problembehandlung**

    Darüber hinaus haben wir die Problembehandlung bei Ihren [abgeschirmten virtuellen Computern](../security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-shielded-vms.md) vereinfacht, indem wir den erweiterten VMConnect-Sitzungsmodus und PowerShell Direct unterstützen. Diese Tools sind besonders nützlich, wenn Sie die Netzwerkverbindung zu Ihrer VM verloren haben und ihre Konfiguration aktualisieren müssen, um den Zugriff wiederherzustellen. 

    Diese Features müssen nicht konfiguriert werden, und sie werden automatisch zur Verfügung gestellt, wenn eine abgeschirmte VM auf einem Hyper-V-Host mit Windows Server, Version 1803 oder höher, ausgeführt wird.

- **Linux-Unterstützung**

    Wenn Sie Umgebungen mit gemischten Betriebssystemen ausführen, unterstützt Windows Server 2019 jetzt die Ausführung von Ubuntu, Red Hat Enterprise Linux und SUSE Linux Enterprise Server in abgeschirmten virtuellen Computern.

### <a name="http2-for-a-faster-and-safer-web"></a>HTTP/2 für ein schnelleres und sichereres Web

- Verbessertes Zusammenführen von Verbindungen für ununterbrochene und korrekt verschlüsselte Möglichkeiten des Browsens.

- Die serverseitige Cipher-Suite-Verhandlung von HTTP/2 wurde aktualisiert, um Verbindungsfehler automatisch zu mindern und die Bereitstellung zu vereinfachen.

- Unser Standardanbieter für TCP-Überlastung wurde auf Cubic umgestellt, um Ihnen mehr Durchsatz zu bieten!

## <a name="storage"></a>Speicher

Hier sind einige der Änderungen, die wir in Windows Server 2019 am Speicher vorgenommen haben. Weitergehende Informationen finden Sie unter [Neuigkeiten zum Speicher](../storage/whats-new-in-storage.md).

### <a name="storage-migration-service"></a>Speichermigrationsdienst

Der Speichermigrationsdienst ist eine neue Technologie, mit der Server einfacher auf eine neuere Version von Windows Server migriert werden können. Er bietet ein grafisches Tool, das Daten auf Servern inventarisiert, Daten und Konfiguration auf neuere Server überträgt und dann optional die Identitäten der alten Server auf die neuen Server überträgt, sodass Apps und Benutzer nichts ändern müssen. Weitere Informationen finden Sie unter [Speichermigrationsdienst)](../storage/storage-migration-service/overview.md).

### <a name="storage-spaces-direct"></a>Speicherplätze DAS

Hier ist eine Liste der Neuerungen in „Direkte Speicherplätze“. Weitergehende Informationen finden Sie unter [Neuerungen in „Direkte Speicherplätze“](../storage/whats-new-in-storage.md#storage-spaces-direct). Lesen Sie auch [Azure Stack HCI](/azure-stack/operator/azure-stack-hci-overview). Dort finden Sie Informationen zum Abrufen von überprüften Systemen für „Direkte Speicherplätze“.

- **Datendeduplizierung und -komprimierung für ReFS-Volumes**
- **Systemeigene Unterstützung für den dauerhaften Speicher**
- **Verschachtelte Ausfallsicherheit für hyperkonvergente Infrastruktur mit zwei Knoten am Rand**
- **Zwei-Servercluster mit einem USB-Speicherstick als Zeuge**
- **Support für Windows Admin Center**
- **Leistungsverlauf**
- **Skalieren bis zu 4 PB pro Cluster**
- **Durch Spiegelung beschleunigte Parität mit doppelter Geschwindigkeit**
- **Erkennung von Laufwerkslatenz-Ausreißern**
- **Manuelle Begrenzung der Volumenzuweisung zur Erhöhung der Fehlertoleranz**

### <a name="storage-replica"></a>Speicherreplikat

Hier sind die Neuigkeiten für Speicherreplikate. Weitergehende Informationen finden Sie unter [Neuigkeiten für Speicherreplikate](../storage/whats-new-in-storage.md#storage-replica).

- Speicherreplikate sind jetzt in Windows Server 2019 Standard Edition verfügbar.
- Test-Failover ist ein neues Feature zum Bereitstellen von Zielspeicher für die Validierung von Replikations- oder Backupdaten. Weitere Informationen finden Sie unter [Häufig gestellte Fragen zu Speicherreplikaten](../storage/storage-replica/storage-replica-frequently-asked-questions.md).
- Verbesserungen der Protokollierungsleistung für Speicherreplikate
- Support für Windows Admin Center

## <a name="failover-clustering"></a>Failoverclusterunterstützung

Hier ist eine Liste der Neuigkeiten für das Failoverclustering. Weitergehende Informationen finden Sie unter [Neuigkeiten für Failoverclustering](../failover-clustering/whats-new-in-failover-clustering.md).

- **Clustergruppen**
- **Azure erkennende Cluster**
- **Domänenübergreifende Clustermigration**
- **USB-Zeugen**
- **Verbesserungen der Clusterinfrastruktur**
- **Clusterfähiges Aktualisieren unterstützt „Direkte Speicherplätze“**
- **Verbesserungen für Dateifreigabezeugen**
- **Clusterhärtung**
- **Failovercluster verwendet keine NTLM-Authentifizierung mehr**

## <a name="application-platform"></a>Anwendungsplattform

### <a name="linux-containers-on-windows"></a>Linux-Container unter Windows

Es ist nun möglich, Windows- und Linux-basierte Container auf demselben Container-Host mit demselben Docker-Daemon auszuführen. Dies ermöglicht Ihnen das Betreiben einer heterogenen Container-Host-Umgebung und bietet Anwendungsentwicklern zugleich Flexibilität.

### <a name="built-in-support-for-kubernetes"></a>Integrierte Unterstützung für Kubernetes

Windows Server 2019 setzt die Verbesserungen in Bezug auf Computing, Netzwerk und Speicher fort, die in den Versionen des halbjährlichen Kanals zur Unterstützung von Kubernetes unter Windows erforderlich sind. Weitere Details sind in den kommenden Kubernetes-Versionen verfügbar.

- [Containernetzwerke](../networking/sdn/technologies/containers/container-networking-overview.md) in Windows Server 2019 verbessert die Benutzerfreundlichkeit von Kubernetes unter Windows erheblich, indem die Widerstandsfähigkeit der Plattformnetzwerke verbessert und Container-Netzwerk-Plugins unterstützt werden.

- Bereitgestellte Workloads auf Kubernetes können die Netzwerksicherheit zum Schutz von Linux- und Windows-Diensten mit integrierten Tools nutzen.

### <a name="container-improvements"></a>Containerverbesserungen
    
- **Verbesserte integrierte Identität**

    Wir haben die integrierte Windows-Authentifizierung in Containern einfacher und zuverlässiger gemacht und dabei einige Einschränkungen aus früheren Versionen von Windows Server behoben.

- **Verbesserte Anwendungskompatibilität**

    Die Umstellung von Windows-basierten Anwendungen auf Container wird jetzt einfacher: Die App-Kompatibilität für das vorhandene *windowsservercore*-Image wurde erhöht. Für Anwendungen mit zusätzlichen API-Abhängigkeiten gibt es jetzt ein drittes Basis-Image: *windows*.

- **Reduzierte Größe und höhere Leistung**

    Die Download-Größen des Basiscontainers, die Größe auf der Festplatte und die Startzeiten wurden verbessert. Dies beschleunigt die Container-Workflows.

- **Verwaltungsoberfläche mit Windows Admin Center\( (Vorschau)\)**

    Wir haben es einfacher denn je gemacht zu sehen, welche Container auf Ihrem Computer ausgeführt werden, und einzelne Container mit einer neuen Erweiterung für Windows Admin Center zu verwalten. Suchen Sie im [öffentlichen Windows Admin Center-Feed](../manage/windows-admin-center/configure/using-extensions.md) nach der Erweiterung „Container”.

### <a name="encrypted-networks"></a>Verschlüsselte Netzwerke

[Verschlüsselte Netzwerke](../networking/sdn/sdn-whats-new.md) – Die virtuelle Netzwerkverschlüsselung ermöglicht die Verschlüsselung des virtuellen Netzwerkdatenverkehrs zwischen virtuellen Computern, die miteinander in Teilnetzen kommunizieren, die als **Verschlüsselung aktiviert** markiert sind. Sie nutzt auch Datagram Transport Layer Security (DTLS) im virtuellen Subnetz, um Pakete zu verschlüsseln. DTLS schützt vor Abhörversuchen, Manipulation und Fälschung durch jeden, der Zugriff auf das physische Netzwerk hat.

### <a name="network-performance-improvements-for-virtual-workloads"></a>Verbesserungen der Netzwerkleistung für virtuelle Workloads

[Verbesserungen der Netzwerkleistung für virtuelle Workloads](../networking/technologies/hpn/hpn-insider-preview.md) maximieren den Netzwerkdurchsatz für virtuelle Computer, ohne dass Sie Ihren Host ständig optimieren oder übermäßig bereitstellen müssen. Dies reduziert die Betriebs- und Wartungskosten und erhöht gleichzeitig die verfügbare Dichte Ihrer Hosts. Diese neuen Features sind:

* Empfangen von Segmentkoaleszenzen im vSwitch

* Dynamic Virtual Machine Multi-Queue (d.VMMQ)

### <a name="low-extra-delay-background-transport"></a>Low Extra Delay Background Transport (LEDBAT)

Der Low Extra Delay Background Transport (LEDBAT) ist ein latenzoptimierter Anbieter für die Netzwerküberlastungssteuerung, der Benutzern und Anwendungen automatisch Bandbreite zur Verfügung stellt und dabei die gesamte verfügbare Bandbreite verbraucht, wenn das Netzwerk nicht verwendet wird.   
Diese Technologie ist für die Bereitstellung großer, kritischer Updates in einer IT-Umgebung vorgesehen, ohne die Services für Kunden und die damit verbundene Bandbreite zu beeinträchtigen.

### <a name="windows-time-service"></a>Windows-Zeitdienst

Der [Windows-Zeitdienst](../networking/windows-time-service/insider-preview.md) enthält echte UTC-kompatible Schaltsekundenunterstützung, ein neues Zeitprotokoll namens „Precision Time Protocol“ und End-to-End-Rückverfolgbarkeit.


### <a name="high-performance-sdn-gateways"></a>Hochleistungs-SDN-Gateways

[Hochleistungs-SDN-Gateways](../networking/sdn/gateway-performance.md) in Windows Server 2019 verbessert die Leistung für IPsec- und GRE-Verbindungen erheblich und bietet einen extrem hohen Durchsatz bei deutlich geringerer CPU-Auslastung.
<br/>

### <a name="new-deployment-ui-and-windows-admin-center-extension-for-sdn"></a>Neue Bereitstellungsbenutzeroberfläche und Windows Admin Center-Erweiterung für SDN

Mit Windows Server 2019 ist es nun einfach, eine neue Bereitstellungsbenutzeroberfläche und eine Windows Admin Center-Erweiterung bereitzustellen und zu verwalten, die es jedem ermöglicht, die Leistungsfähigkeit von SDN zu nutzen. 

### <a name="persistent-memory-support-for-hyper-v-vms"></a>Unterstützung von persistentem Speicher für Hyper-V-VMs

Um den hohen Durchsatz und die niedrige Latenz von persistentem Speicher (auch „Speicherklassenspeicher“ genannt) in virtuellen Computern zu nutzen, kann er nun direkt in VMs projiziert werden. Dies kann dazu beitragen, die Latenzzeit für Datenbanktransaktionen drastisch zu reduzieren oder die Wiederherstellungszeiten für In-Memory-Datenbanken mit niedriger Latenz bei einem Ausfall zu reduzieren.
