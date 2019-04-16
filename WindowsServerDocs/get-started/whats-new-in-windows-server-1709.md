---
title: Neues in IPAM unter Windows Server, Version 1709.
description: Welche neuen Features sind für Compute, Identitäten, Verwaltung, Automatisierung, Netzwerk, Sicherheit und Speicher verfügbar?
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
ms.localizationpriority: medium
ms.openlocfilehash: 1d63721dde484756e67b68bcff078257c130ae36
ms.sourcegitcommit: 2ffd664a771421231a583d0b90827e922ed47ae3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/15/2018
ms.locfileid: "4646127"
---
# Neues in IPAM unter Windows Server, Version 1709.

>Gilt für: Windows Server (Semi-Annual Channel)

<img src="../media/landing-icons/new.png" style='float:left; padding:.5em;' alt="Icon showing a newspaper">&nbsp;In diesem Abschnitt wird beschrieben, was in Windows Server, Version 1709, neu ist und was sich geändert hat. Die hier aufgeführten Neuerungen und Änderungen haben bei der Arbeit in dieser Version vermutlich die größte Auswirkung. Weitere Informationen finden Sie unter [Windows Server, Version 1709](https://blogs.technet.microsoft.com/windowsserver/2017/08/24/sneak-peek-1-windows-server-version-1709/).
   

## Neuer Versionsrhythmus

Ab dieser Version haben Sie zwei Optionen für den Empfang von Funktionsupdates für Windows Server:
- **Long-Term Servicing Channel (LTSC))**: Dies bedeutet wie gewohnt 5Jahre Mainstreamsupport und 5Jahre erweiterter Support. Sie haben die Möglichkeit, alle 2 bis 3Jahre auf die nächste LTSC-Version zu aktualisieren, die genau wie auch die letzten 20Jahre unterstützt wird.
- **Semi-Annual Channel (SAC)**: Dies ist eine Software Assurance-Leistung und wird in der Produktion vollständig unterstützt. Der Unterschied besteht darin, dass sie 18Monate lang unterstützt wird, und es alle sechs Monate eine neue Version gibt.

Veröffentlichungskanäle werden in der folgenden Tabelle zusammengefasst:

|   | Semi-Annual Channel | Long Term Servicing Channel |
| ------------- | ------------- | ------------ |
| Versionsrhythmus  | Zweimal pro Jahr (Frühling und Herbst)  | Alle 2-3 Jahre |
| Supportzeitplan  | 18Monate grundlegender produktionsbegleitender Mainstreamsupport  | 5Jahre Mainstreamsupport + 5Jahre erweiterter Support |
| Verfügbarkeit  | Software Assurance oder Azure (in der Cloud gehostet)  | Alle Kanäle |
| Benennungskonvention  | Windows Server, Version JJMM  | YYYY für Windows Server |

Weitere Informationen finden Sie unter [Übersicht: Windows Server, Semi-Annual Channel](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview).

## Anwendungscontainer und Microservices

- Das Server Core-Containerimage wurde weiter für "Lift and Shift"-Szenarien optimiert, in denen Sie vorhandenen Code oder Anwendungen in Containern mit nur minimalen Änderungen migrieren können. Es ist ebenfalls 60% kleiner. 
- Das Nano Server-Containerimage ist fast 80% kleiner.
    - Im Windows Server, Semi-Annual Channel wird der Nano Server als ein Container-Basis-Betriebssystemimage von 390MB auf 80MB verkleinert.
- Linux-Container mit Hyper-V-Isolation 

Weitere Informationen finden Sie unter [Änderungen an Nano Server in der nächsten Version von Windows Server](https://docs.microsoft.com/windows-server/get-started/nano-in-semi-annual-channel) und [Version 1709 für Entwickler von Windows Server](https://blogs.technet.microsoft.com/windowsserver/2017/09/13/sneak-peek-3-windows-server-version-1709-for-developers/).

## Moderne Verwaltung

Sehen Sie sich das [Projekt Honolulu](https://docs.microsoft.com/windows-server/manage/honolulu/honolulu) für eine vereinfachte, integrierte und sichere Erfahrung an, die IT-Administratoren bei der Verwaltung der Problembehandlung, Konfiguration und Wartungsszenarien hilft.  Projekt Honolulu enthält die nächste Generation an Tools und bietet eine vereinfachte, integrierte, sichere und erweiterbare Benutzeroberfläche.
Projekt Honolulu enthält eine intuitive neue Verwaltungsfunktion für die Verwaltung von PCs, Windows Server, Failovercluster und zusammengeführter Infrastruktur auf Basis von "direkten Speicherplätze", was die Betriebskosten reduziert.

## Compute

**Nano-Container und Server Core-Container**: Es handelt sich bei dieser Version zuerst um die Innovation der Anwendung. Nano Server oder Nano als Host, ist veraltet und wird durch Nano-Container ersetzt, der als Nano als Containerimage ausgeführt wird. 

Weitere Informationen zu Containern finden Sie unter [Übersicht über Container-Networking](https://docs.microsoft.com/windows-server/networking/sdn/technologies/containers/container-networking-overview).

**Server Core als Container** (und Infrastruktur)-Host, bietet eine größere Flexibilität, Dichte und Leistung für vorhandene Anwendungen mit einem modernisierten Prozess und neuen Apps, die bereits mit dem Cloud-Modell entwickelt wurden.

**VM Start Ordering** wird ebenfalls mit dem Betriebssystem- und die Anwendungsinformationen optimiert, und bietet erweiterte Trigger wenn ein virtueller Computer als gestartet gilt, bevor der nächste gestartet wird.

**Speicherklassen-Speicherunterstützung für VMs** ermöglicht die Erstellung von NTFS-formatierten Direktzugriffsvolumes auf nichtflüchtigen DIMMs und die Bereitstellung auf Hyper-V-VMs. Dadurch können virtuelle Hyper-V-Computer die niedrige Latenzleistungsvorteile der Speicherklassenspeichergeräte nutzen.

**Virtualized Persistent Memory (vPMEM)** wird durch das Erstellen einer VHD-Datei (.vhdpmem) auf einem direkten Zugriffsvolume auf einem Host ermöglicht, wodurch ein vPMEM Controller auf einen VM und das erstelle Gerät (.vhdpmem) auf einen VM hinzugefügt wird. Das Verwenden von vhdpmem-Dateien auf Volumes mit direktem Zugriff auf einem Host zur Sicherung von vPMEM ermöglicht die Zuordnung von Flexibilität und nutzt ein vertrautes Verwaltungsmodell zum Hinzufügen von Datenträgern zum virtuellen Computer.

**Container-Speicher – permanente Datenvolumes auf freigegebenen Clustervolumes (CSV)**. In Windows Server, Version 1709, und auf Windows Server2016 mit den neuesten Updates, haben wir Unterstützung für Container hinzugefügt, damit Sie auf permanente Datenvolumes auf freigegebenen Clustervolumes zugreifen können, einschließlich freigegebenen Clustervolumes für "direkte Speicherplätze". Dadurch erhalten die Anwendungscontainer permanenten Zugriff auf das Volume, unabhängig davon, welchen Cluster-Knoten die Container-Instanz ausführt. Weitere Informationen finden Sie unter [Container Storage Support with Cluster Shared Volumes (CSV), direkte Speicherplätze (S2D), SMB Global Mapping](https://blogs.msdn.microsoft.com/clustering/2017/08/10/container-storage-support-with-cluster-shared-volumes-csv-storage-spaces-direct-s2d-smb-global-mapping/).

**Container Storage – permanente Datenvolumes mit SMB Global Mapping**. In Windows Server, Version 1709, wurde die Unterstützung für das Zuordnen einer SMB-Dateifreigabe auf einen Laufwerkbuchstaben in einem Container hinzugefügt – Dies wird als „SMB Global Mapping” bezeichnet. Dieses zugeordnete Laufwerk ist dann für alle Benutzer auf dem lokalen Server zugänglich, sodass das die Dateifreigabe der Container-E/A auf dem Datenvolume auf dem bereitgestellten Laufwerk die zugrunde liegende Dateifreigabe durchlaufen kann. Weitere Informationen finden Sie unter [Container Storage Support with Cluster Shared Volumes (CSV), direkte Speicherplätze (S2D), SMB Global Mapping](https://blogs.msdn.microsoft.com/clustering/2017/08/10/container-storage-support-with-cluster-shared-volumes-csv-storage-spaces-direct-s2d-smb-global-mapping/).

**Format der Konfigurationsdatei für virtuelle Computer (aktualisiert)** Für virtuelle Computer mit der Konfigurationsversion 8.2 und höher wurde eine weitere Datei (.vmgs) hinzugefügt. VMGS steht für „VM Guest State” und ist eine neue interne Datei, die den Gerätezustand enthält, der zuvor Teil der VM-Laufzeitstatusdatei war.

## Sicherheit und Zuverlässigkeit

**Netzwerkverschlüsselung** ermöglicht das schnelle Verschlüsseln von Netzwerksegmenten auf einer Software-definierten Networking-Infrastruktur, um Sicherheits- und Compliance-Anforderungen zu erfüllen.

**Host-Überwachungsdienst (Host Guardian Service, HGS)**, wenn eine abgeschirmte VM aktiviert ist. Vor dieser Version war die Empfehlung, einen physischen 3-Knoten-Cluster bereitzustellen. Obwohl dadurch garantiert wurde, dass die Host-Überwachungsdienst-Umgebung nicht durch einen Administrator gefährdet ist, war dies oft sehr kostenintensiv.

**Linux als eine abgeschirmte VM** wird jetzt unterstützt.

Weitere Informationen finden Sie unter [Übersicht über geschütztes Fabric und abgeschirmte VMs](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms).

**SMBLoris vulnerability** Ein als “SMBLoris” gekennzeichnetes Problem, das zu „Denial-of-Service” führen kann, wurde gelöst.

## Speicher

**Speicherreplikat**: Der Schutz für die von Storage Replica in Windows Server2016 hinzugefügte Notfallwiederherstellung ist jetzt erweitert und umfasst:
- **Testen des Failovers**: die Option zum Bereitstellen des Ziel-Speichers ist jetzt mit der Funktion zum Testen des Failovers möglich. Sie können einen Snapshot des replizierten Speichers auf Zielknoten vorübergehend zu Test- und Sicherungszwecken bereitstellen.  Weitere Informationen finden Sie unter [Häufig gestellte Fragen zu Speicherreplikaten](https://aka.ms/srfaq). 
- **Unterstützung für das Projekt Honolulu**: Die Unterstützung für die grafische Verwaltung der Server-zu-Server-Replikation ist jetzt im Projekt Honolulu verfügbar. Dadurch wird die Anforderung, PowerShell zum Verwalten einer allgemeinen Arbeitslast zum Notfallschutz, entfernt.

**SMB**: 
- **SMB1 und das das Entfernen der Gastauthentifizierung**: In Windows Server, Version 1709, wird der SMB1-Client und -Server nicht mehr standardmäßig installiert. Darüber hinaus ist die Möglichkeit deaktiviert, sich als Gast in SMB2 und höher standardmäßig zu authentifizieren. Weitere Informationen finden Sie unter [SMBv1 wird nicht standardmäßig in Windows10, Version 1709 und Windows Server, Version 1709, installiert](https://support.microsoft.com/help/4034314/smbv1-is-not-installed-by-default-in-windows-10-rs3-and-windows-server). 

- **SMB2/SMB3-Sicherheit und Kompatibilität**: Es wurden zusätzliche Optionen für die Sicherheits- und Anwendungskompatibilität hinzugefügt, einschließlich der Möglichkeit, Oplocks SMB2+ für Legacy-Anwendungen zu deaktivieren, sowie die Signierung oder Verschlüsselung, die auf Basis jeder einzelnen Verbindung von einem Client erforderlich ist. Weitere Informationen finden Sie in der SMBShare PowerShell-Modul-Hilfe.

**Datendeduplizierung**: 
- **Datendeduplizierung unterstützt jetzt ReFS**: Sie müssen nicht mehr zwischen den Vorteilen eines modernen Dateisystems mit ReFS und der Datendeduplizierung wählen: Sie können jetzt die Datendeduplizierung aktivieren, überall wo ReFS aktiviert werden kann. Erhöhen Sie die Speichereffizienz von schätzungsweise mehr als 95% mit ReFS.
- **DataPort-API für den optimierten Eingang/Ausgang von deduplizierten Volumes**: Entwickler können jetzt die Kenntnisse der Datendeduplizierung zum effizienten Speichern von Daten, zum Verschieben von Daten zwischen Volumes, Servern und Clustern effizient nutzen.

## Remotedesktopdienste (RDS)

**RDS ist in Azure AD integriert**, sodass Kunden die Richtlinien für den bedingten Zugriff, die Multi-Factor Authentication, die integrierte Authentifizierung mit anderen SaaS-Apps durch Azure AD und vieles mehr nutzen können. Weitere Informationen finden Sie unter [Azure AD Domain Services mit der RDS-Bereitstellung integrieren](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-azure-adds).

>[!TIP]
>Einen kurzen Einblick in andere interessante Neuigkeiten bei RDS finden Sie unter [Remotedesktop-Services: Updates und bevorstehende Innovationen](https://blogs.technet.microsoft.com/enterprisemobility/2017/09/20/first-look-at-updates-coming-to-remote-desktop-services/)

## Netzwerk

**Routing-Mesh für Docker** wird unterstützt. Der Eingangs-Routing-Mesh ist Teil des [Schwarmmodus](https://docs.docker.com/engine/swarm/), der integrierten Orchestrierungslösung von Docker für Container. Weitere Informationen finden Sie unter [Routing-Mesh für Docker, die mit Windows Server, Version 1709 verfügbar sind](https://blogs.technet.microsoft.com/virtualization/2017/09/26/dockers-ingress-routing-mesh-available-with-windows-server-version-1709/).

**Neue Features für Docker** sind verfügbar. Weitere Informationen finden Sie unter [aufregende neue Funktionen for Docker mit Windows Server 1709](https://blog.docker.com/2017/09/docker-windows-server-1709/).

**Windows-Netzwerke haben Parität mit Linux für Kubernetes**: Windows ähnelt Linux jetzt in Bezug auf die Netzwerke. Kunden können gemischt-OS, Kubernetes-Cluster in einer Umgebung bereitstellen, die Azure, lokale, und auf Drittanbieter-Cloud-Stapel mit den gleichen Netzwerk-Grundtypen und Topologien unter Linux unterstützt, ohne Problemumgehungen oder Switcherweiterungen.

**Core-Netzwerkstapel**: Es wurden mehrere Features des Core-Netzwerkstapels verbessert. Weitere Informationen zu diesen Features finden Sie unter [Core-Netzwerkstapelfunktionen im Creators Update für Windows10](https://blogs.technet.microsoft.com/networking/2017/07/13/core-network-stack-features-in-the-creators-update-for-windows-10/).
- **TCP Fast Open (TFO)**: Es wurde Unterstützung für TFO hinzugefügt, um den TCP-3-Wege-Handshake-Prozess zu optimieren. TFO richtet ein sicheren TFO Cookie in der ersten Verbindung mit einem standardmäßigen 3-Wege-Handshake ein.  Nachfolgende Verbindungen auf dem gleichen Server verwenden das TFO-Cookie anstelle eines 3-Wege-Handshakes zum Herstellen einer Verbindung mit 0 (null) Roundtripzeit.
- **CUBIC**: Die experimentelle systemeigenen Windows-Implementierung von CUBIC, ein TCP-Überlastungssteuerungs-Algorithmus ist verfügbar. Die folgenden Befehle aktivieren oder deaktivieren CUBIC.

    ```
    netsh int tcp set supplemental template=internet congestionprovider=cubic
    netsh int tcp set supplemental template=internet congestionprovider=compound
    ```

- **Automatische Abstimmung erhalten**: Die automatische Logik von TCP berechnet den Parameter "Empfangsfenster" einer TCP-Verbindung.  Verbindungen mit hoher Geschwindigkeit und/oder Verzögerungen der Verbindungen benötigen diesen Algorithmus, um gute Leistungsmerkmale zu erzielen.  In dieser Version wurde der Algorithmus geändert, um eine Schritt-Funktion zu verwenden, um den maximal zulässigen Empfangsfensterwert für eine bestimmte Verbindung zu erhalten.
- **TCP-Statistik API**: Es wird eine neue API mit Namen SIO_TCP_INFO eingeführt.  Mit SIO_TCP_INFO können Entwickler umfassende Informationen zu einzelnen TCP-Verbindungen mit einer Socketoption abfragen.
- **IPv6**: Es gibt in dieser Version mehrere Verbesserungen in IPv6.
    - **RFC 6106** unterstützt: RFC 6106 für die DNS-Konfiguration über Routerankündigungen (RAs). Sie können die folgenden Befehle verwenden, um den RFC 6106 -Support zu aktivieren oder zu deaktivieren:

    ```
    netsh int ipv6 set interface <ifindex> rabaseddnsconfig=<enabled | disabled>
    ```

    - **Flussbezeichnungen**: Ab dem Creators Update haben ausgehende TCP- und UDP-Pakete über IPv6 dieses Feld mit einem Hash der 5-Tupel (Quell-IP, Ziel-IP, Quellport, Zielport) festgelegt.  Hierdurch wird der Lastenausgleich oder die Flussklassifizierung der „nur IPv6-Rechenzentren” effizienter ausgeführt. So aktivieren Sie die Flussbezeichnungen:

    ```
    netsh int ipv6 set flowlabel=[disabled|enabled] (enabled by default)
    netsh int ipv6 set global flowlabel=<enabled | disabled>
    ```

    - **ISATAP und 6to4**: Im Creators Update sind diese Technologien in der Standardeinstellung als Schritt in Richtung der zukünftigen Veraltung deaktiviert.
- **Dead Gateway Detection (DGD)**: der DGD-Algorithmus verschiebt automatisch die Verbindungen über auf ein anderes Gateway, wenn das aktuelle Gateway nicht erreichbar ist. In dieser Version ist der Algorithmus verbessert, um die Netzwerkumgebung in regelmäßigen Abständen erneut zu überprüfen.
- [Test-NetConnection](https://technet.microsoft.com/itpro/powershell/windows/nettcpip/test-netconnection) ist ein integriertes Cmdlet in Windows PowerShell, das eine Vielzahl von Netzwerkdiagnosen ausführt.  In dieser Version haben wir das Cmdlet verbessert, um detaillierte Informationen sowohl zur Routenauswahl als auch zur Quelladresse zu verbessern.

**Software-Defined Networking**

- **Virtuelle Netzwerkverschlüsselung** ist ein neues Feature, das die Möglichkeit bietet, den virtuellen Netzwerkdatenverkehr zwischen virtuellen Computern zu verschlüsseln, die innerhalb der Subnetze miteinander kommunizieren können und als "Verschlüsselung aktiviert" gekennzeichnet sind. Dieses Feature nutzt Datagram Transport Layer Security (DTLS) auf dem virtuellen Subnetz, um die Pakete zu verschlüsseln.  DTLS bietet Schutz vor Lauschangriffen, Manipulationen und Fälschung von jedem Benutzer mit Zugriff auf das physische Netzwerk.
 
**Windows10 VPN**

- **Pre-Logon Infrastrukturtunnel**. Standardmäßig erstellt Windows10-VPN-nicht automatisch Infrastruktur Tunnel, wenn Benutzer nicht am Computer oder Gerät angemeldet sind. Sie können Windows10 VPN so konfigurieren, dass vor der Anmeldung Pre-Logon Infrastrukturtunnel automatisch mithilfe der Gerätetunnelfunktion (Prelogon) im VPN-Profil erstellt werden.
- **Verwaltung der Remotecomputer und -Geräte**.  Sie können Windows10-VPN-Clients verwalten, indem Sie die Gerätetunnelfunktion (Prelogon) im VPN-Profil konfigurieren. Darüber hinaus müssen Sie die VPN-Verbindung konfigurieren, um die IP-Adressen dynamisch zu registrieren, die der VPN-Schnittstelle mit internen DNS-Diensten zugewiesen sind.
- **Pre-Logon-Gateways angeben**. Sie können mithilfe der Gerätetunnelfunktion (Prelogon) im VPN-Profil Pre-Logon-Gateways angeben, kombiniert mit Datenverkehrsfiltern, um zu steuern, welche Managementsysteme auf dem internen Netzwerk über den Gerätetunnel zugänglich sind.

