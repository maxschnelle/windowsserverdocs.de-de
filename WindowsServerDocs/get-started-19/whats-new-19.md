---
title: Neuigkeiten in Windows Server 2019
description: Eine Übersicht über neue Features in Windows Server 2019, einschließlich Desktop Experience, Speichermigrationsdienst, Systemdaten, Azure-Netzwerkadapter, Verbesserungen für Storage Spaces Direct und andere Änderungen.
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: high
ms.date: 06/04/2019
ms.openlocfilehash: 7110fe78982fec616174a93514d86fb2e1cf9fa5
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66810766"
---
# <a name="whats-new-in-windows-server-2019"></a>Neuigkeiten in Windows Server 2019

> Gilt für: Windows Server 2019

Dieses Thema beschreibt einige der neuen Features in Windows Server 2019. Windows Server-2019 basiert auf der soliden Fundament von Windows Server 2016 und bietet zahlreiche Innovationen auf vier wichtigen Themen: Hybridcloud, Sicherheit, Plattform und Hyperkonvergenten Infrastruktur (HCL).

Neuerungen in Windows Server Halbjährlicher Kanal-Versionen finden Sie unter [Neuigkeiten in Windows Server](../get-started/whats-new-in-windows-server.md).

## <a name="general"></a>Allgemein

### <a name="windows-admin-center"></a>Windows Admin Center

Windows Admin Center ist eine lokal bereitgestellte, browserbasierte App zum Verwalten von Servern, Cluster, hyperkonvergenter Infrastruktur und Windows 10-PCs. Sie können es ohne zusätzliche Kosten neben Windows verwenden – es ist produktionsbereit.

Sie können Windows Admin Center auf Windows Server-2019 sowie Windows 10 und früheren Versionen von Windows und Windows Server installiert und zum Verwalten von Servern und Clustern unter Windows Server 2008 R2 verwenden und höher.

Weitere Informationen finden Sie unter [Windows Admin Center](../manage/windows-admin-center/understand/windows-admin-center.md).

### <a name="desktop-experience"></a>Desktop Experience

Da es sich bei Windows Server 2019 um eine Long-Term Servicing Channel (LTSC)-Version handelt, ist <b>Desktop Experience</b> enthalten. (Halbjährlicher Kanal \(SAC\) Releases enthalten die Desktopdarstellung nicht beabsichtigt; sie dienen ausschließlich Server Core und Nano Server-containerimage frei.) Wie bei Windows Server 2016 während des Setups des Betriebssystems können Sie zwischen Server Core-Installationen oder Server mit Desktopdarstellung Installationen.

### <a name="system-insights"></a>Systemdaten

System Insights ist eine neue Funktion von Windows Server 2019, mit der lokale Predictive Analytics-Funktionen direkt in Windows Server integriert werden können. Diese prädiktiven Funktionen, die jeweils von einem maschinellen Lernmodell unterstützt werden, analysieren lokal Windows Server-Systemdaten wie Leistungsindikatoren und Ereignisse und geben Einblick in die Funktionsweise Ihrer Server und helfen Ihnen dabei, die Betriebskosten im Zusammenhang mit der reaktiven Verwaltung von Problemen in Windows-Serverbereitstellungen zu reduzieren.

## <a name="hybrid-cloud"></a>Hybrid-Cloud

### <a name="server-core-app-compatibility-feature-on-demand"></a>Optionales Feature (FOD, Feature on Demand) „Server Core-App-Kompatibilität”

Das [optionale Feature (FOD) "Server Core-Anwendungskompatibilität"](https://docs.microsoft.com/windows-server/get-started-19/install-fod-19) verbessert die App-Kompatibilität für die Windows Server Core-Installationsoption erheblich durch Hinzufügen einer Teilmenge von Binärdateien und Komponenten von Windows Server mit Desktop Experience, ohne dass die Windows Server Desktop Experience-Grafikumgebung selbst hinzugefügt wird.  Dies erfolgt, um die Funktionalität und Kompatibilität von Server Core zu erhöhen und gleichzeitig möglichst schlank zu halten.  

Dieses optionale FOD ist in einer separaten ISO verfügbar und kann nur Windows Server Core-Installationen und -Bildern mit DISM hinzugefügt werden. 

## <a name="security"></a>Sicherheit

### <a name="windows-defender-advanced-threat-protection-atp"></a>Windows Defender Advanced Threat Protection (ATP)

Die umfassenden Plattformsensoren und Reaktionsaktionen von ATP decken Angriffe auf Speicher- und Kernel-Ebene auf und reagieren darauf, indem sie bösartige Dateien unterdrücken und schädliche Prozesse beenden.

-   Weitere Informationen zu Windows Defender ATP finden Sie in der [Übersicht über die Windows Defender ATP-Funktionen](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/overview).

-   Weitere Informationen zum Onboarding-Servern finden Sie unter [Integrieren von Servern im Windows Defender ATP-Dienst](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-server-endpoints-windows-defender-advanced-threat-protection).

**Windows Defender ATP Exploit Guard** ist eine neue Serie von Host-Intrusion-Prevention-Funktionen. Die vier Komponenten von Windows Defender Exploit Guard wurden entwickelt, um das Gerät gegen eine Vielzahl von Angriffsvektoren zu schützen und Verhaltensweisen zu blockieren, die häufig bei Malware-Angriffen eingesetzt werden. Gleichzeitig können Sie Sicherheitsrisiken und Produktivitätsanforderungen ausbalancieren.

-   [Attack Surface Reduction (ASR)](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/attack-surface-reduction-exploit-guard?ocid=cx-blog-mmpc) umfasst eine Reihe von Steuerelementen, mit denen Unternehmen verhindern können, dass Malware auf die Computer gelangt, indem sie verdächtige schädliche Dateien (z. B. Office-Dateien), Skripts, seitliche Bewegungen, Ransomware-Verhalten und E-Mail-basierte Bedrohungen blockieren.

-   [Netzwerkschutz](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/network-protection-exploit-guard?ocid=cx-blog-mmpc) schützt den Endpunkt vor webbasierten Bedrohungen, indem er jeden ausgehenden Prozess auf dem Gerät über Windows Defender SmartScreen an nicht vertrauenswürdige Hosts/IP-Adressen blockiert.

-   [Kontrollierter Ordnerzugriff](https://cloudblogs.microsoft.com/microsoftsecure/2017/10/23/stopping-ransomware-where-it-counts-protecting-your-data-with-controlled-folder-access/?ocid=cx-blog-mmpc?source=mmpc) schützt sensible Daten vor Ransomware, indem es verhindert, dass nicht vertrauenswürdige Prozesse auf Ihre geschützten Ordner zugreifen.

-   [Exploit-Schutz](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/exploit-protection-exploit-guard) ist eine Reihe von Maßnahmen zur Minderung von Schwachstellen (ersetzt EMET), die einfach konfiguriert werden können, um Ihr System und Ihre Anwendungen zu schützen.

[Windows Defender-Anwendungssteuerung](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) (auch bekannt als Code Codeintegrität (CI)-Richtlinie) wurde in Windows Server 2016 veröffentlicht.
Das Feedback von Kunden hat gezeigt, dass dies ein großartiges Konzept ist, das aber nur schwer bereitgestellt werden kann.
Um dies zu beheben, haben wir standardmäßige CI-Richtlinien erstellt, die alle Windows-internen Dateien und Microsoft-Anwendungen wie SQL Server zulassen, aber bekannte ausführbare Dateien blockieren, die CI umgehen können. 

### <a name="security-with-software-defined-networking-sdn"></a>Sicherheit mit Software-Defined Networking (SDN)

[Sicherheit mit SDN](https://docs.microsoft.com/windows-server/networking/sdn/security/sdn-security-top) bietet zahlreiche Features, um Kundenvertrauen bei der Ausführung von Workloads, entweder lokal, oder als Dienstanbieter in der Cloud zu erhöhen. 

Diese Sicherheitsverbesserungen sind in die umfassende, in Windows Server 2016 eingeführte SDN-Plattform integriert.

Eine vollständige Liste der Neuigkeiten in SDN finden Sie unter [Neuigkeiten in SDN für Windows Server 2019](https://docs.microsoft.com/windows-server/networking/sdn/sdn-whats-new).

### <a name="shielded-virtual-machines-improvements"></a>Verbesserungen für abgeschirmte virtuelle Computer

- **Branch Office-Verbesserungen**

    Sie können nun abgeschirmte virtuelle Maschinen auf Maschinen mit intermittierender Konnektivität zum Host Guardian-Dienst ausführen, indem Sie die neuen [Fallback-HGS](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office#fallback-configuration)- und [Offline-Modus](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office#offline-mode)-Funktionen nutzen. Fallback HGS ermöglicht es Ihnen, einen zweiten Satz von URLs für Hyper-V zu konfigurieren, um zu prüfen, ob Ihr primärer HGS-Server erreicht werden kann.

    Im Offline-Modus können Sie Ihre abgeschirmten VMs auch dann starten, wenn HGS nicht erreichbar ist, sofern die VM einmal erfolgreich gestartet wurde und sich die Sicherheitskonfiguration des Hosts nicht geändert hat.

- **Verbesserungen bei der Problembehandlung**

    Darüber hinaus haben wir die Fehlerbehebung für Ihre [abgeschirmten virtuellen Maschinen](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-shielded-vms) vereinfacht, indem wir den erweiterten VMConnect-Sitzungsmodus und PowerShell Direct unterstützen. Diese Tools sind besonders nützlich, wenn Sie die Netzwerkverbindung zu Ihrer VM verloren haben und ihre Konfiguration aktualisieren müssen, um den Zugriff wiederherzustellen. 

    Diese Funktionen müssen nicht konfiguriert werden, und sie werden automatisch zur Verfügung gestellt, wenn eine abgeschirmte VM auf einem Hyper-V-Host mit Windows Server Version 1803 oder höher ausgeführt wird.

- **Linux-Unterstützung**

    Wenn Sie Umgebungen mit gemischten Betriebssystemen ausführen, unterstützt Windows Server 2019 jetzt die Ausführung von Ubuntu, Red Hat Enterprise Linux und SUSE Linux Enterprise Server in abgeschirmten virtuellen Maschinen.

### <a name="http2-for-a-faster-and-safer-web"></a>HTTP/2 für ein schnelleres und sichereres Web

- Verbessertes Zusammenführen von Verbindungen für ein ununterbrochenes und korrekt verschlüsseltes Browser-Erlebnis

- Die serverseitige Cipher-Suite-Verhandlung von HTTP/2 wurde aktualisiert, um Verbindungsfehler automatisch zu mindern und die Bereitstellung zu vereinfachen.

- Unser Standard-TCP-Congestion-Provider wurde auf Cubic umgestellt, um Ihnen mehr Durchsatz zu bieten!

## <a name="storage"></a>Speicher

Hier einige der Änderungen, die wir in Windows Server 2019 am Speicher vorgenommen haben. Weitergehende Informationen finden Sie unter [Neuigkeiten zum Speicher](../storage/whats-new-in-storage.md).

### <a name="storage-migration-service"></a>Speichermigrationsdienst

Der Speichermigrationsdienst ist eine neue Technologie, mit der Server leichter auf eine neuere Version von Windows Server migriert werden können. Es bietet ein grafisches Tool, das Daten auf Servern inventarisiert, Daten und Konfiguration auf neuere Server überträgt und dann optional die Identitäten der alten Server auf die neuen Server überträgt, sodass Apps und Benutzer nichts ändern müssen. Weitere Informationen finden Sie unter [Speichermigrationsdienst)](../storage/storage-migration-service/overview.md).

### <a name="storage-spaces-direct"></a>Direkte Speicherplätze

Hier eine Liste der Neuigkeiten in Storage Spaces Direct Weitergehende Informationen finden Sie unter [Neuigkeiten in Storage Spaces Direct](../storage/whats-new-in-storage.md#storage-spaces-direct). Siehe auch [Azure Stack HCI](https://docs.microsoft.com/azure-stack/operator/azure-stack-hci-overview) für Informationen zum Abrufen von "direkte Speicherplätze" Systeme überprüft.

- **Deduplizierung und Komprimierung für ReFS-volumes**
- **Systemeigene Unterstützung für den persistenten Speicher**
- **Geschachtelte Flexibilität in Bezug auf zwei Knoten hyperkonvergenten Infrastruktur am Rand**
- **Zwei-Server-Clustern mithilfe eines USB-Speicherstick als Zeuge**
- **Unterstützung für Windows Admin Center**
- **Leistungsverlauf**
- **Skalieren Sie bis zu 4 PB pro Cluster**
- **Mirror-beschleunigte Parität ist 2 X schneller**
- **Steuern der Wartezeit ausreißererkennung**
- **Trennen Sie manuell die Zuordnung von Volumes, um die Fehlertoleranz zu erhöhen.**

### <a name="storage-replica"></a>Speicherreplikat

Neuigkeiten für Speicherreplikate Weitergehende Informationen finden Sie unter [Neuigkeiten für Speicherreplikate](../storage/whats-new-in-storage.md#storage-replica).

- Speicherreplikate sind jetzt in Windows Server 2019 Standard Edition verfügbar.
- Test-Failover ist ein neues Feature zum Bereitstellen von Zielspeicher für die Validierung von Replikations- oder Backupdaten. Weitere Informationen finden Sie unter [Häufig gestellte Fragen zu Speicherreplikaten](../storage/storage-replica/storage-replica-frequently-asked-questions.md).
- Verbesserungen der Protokollierungsleistung für Speicherreplikate
- Support für Windows Admin Center

## <a name="failover-clustering"></a>Failoverclustering

Hier eine Liste der Neuigkeiten für das Failoverclustering. Weitergehende Informationen finden Sie unter [Neuigkeiten für Failovercluster](../failover-clustering/whats-new-in-failover-clustering.md).

- **Clustergruppen**
- **Azure-fähigen Clustern**
- **Domänenübergreifende-clustermigration**
- **USB-Zeugen**
- **Verbesserungen der Cluster-Infrastruktur**
- **Clusterfähiges aktualisieren unterstützt "direkte Speicherplätze".**
- **File Share Witness-Verbesserungen**
- **Cluster-Härtung**
- **Failovercluster verwendet nicht mehr die NTLM-Authentifizierung.**

## <a name="application-platform"></a>Anwendungsplattform

### <a name="linux-containers-on-windows"></a>Linux-Container unter Windows

Es ist nun möglich, Windows- und Linux-basierte Container auf demselben Container-Host mit demselben Docker-Daemon auszuführen. Dies ermöglicht Ihnen eine heterogene Container-Host-Umgebung und bietet Anwendungsentwicklern zugleich Flexibilität.

### <a name="built-in-support-for-kubernetes"></a>Integrierte Unterstützung für Kubernetes

Windows Server 2019 setzt die Verbesserungen in Bezug auf Computing, Netzwerk und Speicher fort, die in den Versionen des halbjährlichen Kanals zur Unterstützung von Kubernetes unter Windows erforderlich sind. Weitere Details sind in den kommenden Kubernetes-Versionen verfügbar.

- [Container Networking](https://docs.microsoft.com/windows-server/networking/sdn/technologies/containers/container-networking-overview) in Windows Server 2019 verbessert die Benutzerfreundlichkeit von Kubernetes unter Windows erheblich, indem die Widerstandsfähigkeit der Plattformnetzwerke verbessert und Container-Netzwerk-Plugins unterstützt werden.

- Bereitgestellte Workloads auf Kubernetes können die Netzwerksicherheit zum Schutz von Linux- und Windows-Diensten mit integrierten Tools nutzen.

### <a name="container-improvements"></a>Container-Verbesserungen
    
- **Verbesserte integrierte Identität**

    Wir haben die integrierte Windows-Authentifizierung in Containern einfacher und zuverlässiger gemacht und dabei einige Einschränkungen früherer Versionen von Windows Server behoben.

- **Eine bessere Anwendungskompatibilität**

    Es ist einfacher, das containerisieren von Windows-basierten Anwendungen einfach: Die app-Kompatibilität für die vorhandene *Windowsservercore* Image wurde erhöht. Für Anwendungen mit zusätzlichen API-Abhängigkeiten gibt es jetzt ein drittes Basis-Image: *windows*.

- **Verringerte Größe und höhere Leistung**

    Die Download-Größen des Basiscontainers, die Größe auf der Festplatte und die Startzeiten wurden verbessert. Dies beschleunigt die Container-Workflows.

- **Verwaltungsfunktionen, die mithilfe von Windows Admin Center \((Vorschau)\)**

    Wir haben es einfacher denn je gemacht zu sehen, welche Container auf Ihrem Computer ausgeführt werden, und einzelne Container mit einer neuen Erweiterung für Windows Admin Center zu verwalten. Suchen Sie im öffentlichen [Windows Admin Center-Feed](https://docs.microsoft.com/windows-server/manage/windows-admin-center/configure/using-extensions) nach der Erweiterung „Container”.

### <a name="encrypted-networks"></a>Verschlüsselte Netzwerke

[Verschlüsselte Netzwerke](https://docs.microsoft.com/windows-server/networking/sdn/sdn-whats-new) – Die virtuelle Netzwerkverschlüsselung ermöglicht die Verschlüsselung des virtuellen Netzwerkverkehrs zwischen virtuellen Maschinen, die miteinander in Teilnetzen kommunizieren, die als **Verschlüsselung aktiviert** markiert sind. Es nutzt auch Datagram Transport Layer Security (DTLS) im virtuellen Subnetz, um Pakete zu verschlüsseln. DTLS schützt vor Abhörversuchen, Manipulation und Fälschung durch jeden, der Zugriff auf das physische Netzwerk hat.

### <a name="network-performance-improvements-for-virtual-workloads"></a>Verbesserungen der Netzwerkleistung für virtuelle Workloads

[Verbesserungen der Netzwerkleistung für virtuelle Workloads](https://docs.microsoft.com/windows-server/networking/technologies/hpn/hpn-insider-preview) maximieren den Netzwerkdurchsatz für virtuelle Maschinen, ohne dass Sie Ihren Host ständig optimieren oder übermäßig bereitstellen müssen. Dies reduziert die Betriebs- und Wartungskosten und erhöht gleichzeitig die verfügbare Dichte Ihrer Hosts. Diese neuen Features sind:

* Empfangen von Segmentkoaleszenzen im vSwitch

* Dynamische virtuelle Maschine Multi-Queue (d.VMMQ)

### <a name="low-extra-delay-background-transport"></a>Niedrige zusätzliche Verzögerung Hintergrund-Transport

Der Low Extra Delay Background Transport (LEDBAT) ist ein latenzoptimierter Anbieter für die Netzwerküberlastungssteuerung, der Benutzern und Anwendungen automatisch Bandbreite zur Verfügung stellt und dabei die gesamte verfügbare Bandbreite verbraucht, wenn das Netzwerk nicht verwendet wird.   
Diese Technologie ist für die Bereitstellung großer, kritischer Updates in einer IT-Umgebung vorgesehen, ohne die Services für Kunden und die damit verbundene Bandbreite zu beeinträchtigen.

### <a name="windows-time-service"></a>Windows-Zeitdienst

Der [Windows-Zeitdienst](https://docs.microsoft.com/windows-server/networking/windows-time-service/insider-preview) enthält echte UTC-kompatible Schaltsekundenunterstützung, ein neues Zeitprotokoll namens Precision Time Protocol und End-to-End-Rückverfolgbarkeit.


### <a name="high-performance-sdn-gateways"></a>Hochleistungs-SDN-Gateways

[Hochleistungs-SDN-Gateways](https://docs.microsoft.com/windows-server/networking/sdn/gateway-performance) in Windows Server 2019 verbessert die Leistung für IPsec- und GRE-Verbindungen erheblich und bietet einen extrem hohen Durchsatz bei deutlich geringerer CPU-Auslastung.
<br/>

### <a name="new-deployment-ui-and-windows-admin-center-extension-for-sdn"></a>Neue Bereitstellungsbenutzeroberfläche und Windows Admin Center-Erweiterung für SDN

Mit Windows Server 2019 ist es nun einfach, eine neue Bereitstellungsbenutzeroberfläche und eine Windows Admin Center-Erweiterung bereitzustellen und zu verwalten, die es jedem ermöglicht, die Leistungsfähigkeit von SDN zu nutzen. 

### <a name="persistent-memory-support-for-hyper-v-vms"></a>Unterstützung von persistentem Speicher für Hyper-V-VMs

Um den hohen Durchsatz und die niedrige Latenz von persistentem Speicher (auch Speicherklassenspeicher genannt) in virtuellen Maschinen zu nutzen, kann er nun direkt in VMs projiziert werden. Dies kann dazu beitragen, die Latenzzeit für Datenbanktransaktionen drastisch zu reduzieren oder die Wiederherstellungszeiten für In-Memory-Datenbanken mit niedriger Latenz bei einem Ausfall zu reduzieren.

