---
title: Neuerungen in Windows Server, Version 1709
description: Welche neuen Features sind für Compute, Identitäten, Verwaltung, Automatisierung, Netzwerk, Sicherheit und Speicher verfügbar?
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
ms.localizationpriority: medium
ms.date: 06/03/2019
ms.openlocfilehash: 07479bc5bd2fdf661db8a30e3a9f20c7cce0513e
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80825993"
---
# <a name="whats-new-in-windows-server-version-1709"></a>Neuerungen in Windows Server, Version 1709

>Gilt für: Windows Server (Halbjährlicher Kanal)

<img src=../media/landing-icons/new.png style='float:left; padding:.5em;' alt=Icon showing a newspaper>&nbsp;Weitere Informationen zu den neuesten Features in Windows finden Sie unter [Neuerungen in Windows Server](whats-new-in-windows-server.md). In diesem Abschnitt wird beschrieben, was in Windows Server, Version 1709, neu ist und was sich geändert hat. Die hier aufgeführten Neuerungen und Änderungen haben bei der Arbeit in dieser Version vermutlich die größte Auswirkung. Weitere Informationen finden Sie unter [Windows Server, Version 1709](https://blogs.technet.microsoft.com/windowsserver/2017/08/24/sneak-peek-1-windows-server-version-1709/).

> [!IMPORTANT]
> Der Support von Windows Server, Version 1709, ist seit dem 9. April 2019 beendet.


## <a name="new-cadence-of-releases"></a>Neuer Versionsrhythmus

Ab diesem Release haben Sie zwei Optionen für den Empfang von Funktionsupdates für Windows Server:
- **Long-Term Servicing Channel (LTSC)** : Dies bedeutet wie gewohnt 5 Jahre Mainstreamsupport und 5 Jahre erweiterter Support. Sie haben genau wie in den letzten 20 Jahren die Möglichkeit, alle 2 bis 3 Jahre auf das nächste LTSC-Release zu aktualisieren.
- **Halbjährlicher Kanal (Semi-Annual Channel, SAC)** : Dies ist eine Software Assurance-Leistung und wird in der Produktion vollständig unterstützt. Der Unterschied besteht darin, dass sie 18 Monate lang unterstützt wird, und es alle sechs Monate eine neue Version gibt.

Veröffentlichungskanäle werden in der folgenden Tabelle zusammengefasst.

|   | Halbjährlicher Kanal | Long Term Servicing Channel |
| ------------- | ------------- | ------------ |
| Versionsrhythmus  | Zweimal pro Jahr (Frühling und Herbst)  | Alle 2-3 Jahre |
| Supportzeitplan  | 18 Monate Mainstream-Production Support  | 5 Jahre Mainstreamsupport + 5 Jahre erweiterter Support |
| Verfügbarkeit  | Software Assurance oder Azure (in der Cloud gehostet)  | Alle Kanäle |
| Benennungskonvention  | Windows Server, Version JJMM  | Windows Server JJJJ |

Weitere Informationen finden Sie unter [Vergleich der Wartungskanäle](https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview).

## <a name="application-containers-and-micro-services"></a>Anwendungscontainer und Microservices

- Das Server Core-Containerimage wurde für Lift & Shift-Szenarien weiter optimiert, in denen Sie vorhandene Codebasen oder Anwendungen in Containern mit nur minimalen Änderungen migrieren können. Es ist zudem 60 % kleiner. 
- Das Nano Server-Containerimage ist fast 80 % kleiner.
    - In Windows Server (halbjährlicher Kanal) wird Nano Server als ein Containerbasis-Betriebssystemimage von 390 MB auf 80 MB verkleinert.
- Linux-Container mit Hyper-V-Isolation 

Weitere Informationen finden Sie unter [Änderungen bei Nano Server im nächsten Release von Windows Server](https://docs.microsoft.com/windows-server/get-started/nano-in-semi-annual-channel) und [Windows Server, Version 1709, für Entwickler](https://blogs.technet.microsoft.com/windowsserver/2017/09/13/sneak-peek-3-windows-server-version-1709-for-developers/).

## <a name="modern-management"></a>Moderne Verwaltung

Das [Projekt Honolulu](https://docs.microsoft.com/windows-server/manage/honolulu/honolulu) bietet eine vereinfachte, integrierte und sichere Umgebung, die IT-Administratoren bei der Verwaltung von Problembehandlungs-, Konfigurations- und Wartungsszenarien hilft.  Projekt Honolulu enthält die nächste Generation an Tools und bietet eine vereinfachte, integrierte, sichere und erweiterbare Benutzeroberfläche.
Projekt Honolulu enthält eine intuitive neue Verwaltungsoberfläche für die Verwaltung von PCs, Windows Server-Instanzen, Failoverclustern sowie hyperkonvergenter Infrastruktur auf Basis von direkten Speicherplätzen (Storage Spaces Direct), was die Betriebskosten reduziert.

## <a name="compute"></a>Computer:

**Nano-Container und Server Core-Container**: Zuallererst geht es in diesem Release darum, Anwendungsinnovationen voranzutreiben. Nano Server oder Nano als Host ist veraltet und wird durch Nano-Container (ein Nano, der als Containerimage ausgeführt wird) ersetzt. 

Weitere Informationen zu Containern finden Sie unter [Übersicht über Containernetzwerke](https://docs.microsoft.com/windows-server/networking/sdn/technologies/containers/container-networking-overview).

**Server Core als Container**- (und Infrastruktur)-Host bietet eine größere Flexibilität, Dichte und Leistung für vorhandene Anwendungen mit einem Modernisierungsprozess und neuen Apps, die bereits mit dem Cloudmodell entwickelt wurden.

**VM Start Ordering** wird ebenfalls mit dem Betriebssystem- und die Anwendungsinformationen optimiert, und bietet erweiterte Trigger wenn ein virtueller Computer als gestartet gilt, bevor der nächste gestartet wird.

**Speicherklassen-Speicherunterstützung für VMs** ermöglicht die Erstellung von NTFS-formatierten Direktzugriffsvolumes auf nichtflüchtigen DIMMs und die Bereitstellung auf Hyper-V-VMs. Dadurch können virtuelle Hyper-V-Computer die niedrige Latenzleistungsvorteile der Speicherklassenspeichergeräte nutzen.

**Virtualized Persistent Memory (vPMEM)** wird durch das Erstellen einer VHD-Datei (.vhdpmem) auf einem direkten Zugriffsvolume auf einem Host ermöglicht, wodurch ein vPMEM Controller auf einen VM und das erstelle Gerät (.vhdpmem) auf einen VM hinzugefügt wird. Das Verwenden von vhdpmem-Dateien auf Volumes mit direktem Zugriff auf einem Host zur Sicherung von vPMEM ermöglicht Zuordnungsflexibilität und nutzt ein vertrautes Verwaltungsmodell zum Hinzufügen von Datenträgern zum virtuellen Computer.

**Containerspeicher – permanente Datenvolumes auf freigegebenen Clustervolumes (CSV)** . In Windows Server, Version 1709 und Windows Server 2016 mit den neuesten Updates haben wir Unterstützung für Container hinzugefügt, damit Sie auf permanente Datenvolumes auf freigegebenen Clustervolumes zugreifen können, einschließlich freigegebener Clustervolumes für direkte Speicherplätze. Dadurch erhalten die Anwendungscontainer permanenten Zugriff auf das Volume, unabhängig davon, welchen Clusterknoten die Containerinstanz ausführt. Weitere Informationen finden Sie unter [Container Storage Support with Cluster Shared Volumes (CSV), Storage Spaces Direct (S2D), SMB Global Mapping](https://blogs.msdn.microsoft.com/clustering/2017/08/10/container-storage-support-with-cluster-shared-volumes-csv-storage-spaces-direct-s2d-smb-global-mapping/).

**Containerspeicher – permanente Datenvolumes mit SMB Global Mapping**. In Windows Server, Version 1709, wurde die Unterstützung für das Zuordnen einer SMB-Dateifreigabe auf einen Laufwerkbuchstaben in einem Container hinzugefügt. Dies wird als „SMB Global Mapping” bezeichnet. Dieses zugeordnete Laufwerk ist dann für alle Benutzer auf dem lokalen Server zugänglich, sodass das die Dateifreigabe der Container-E/A auf dem Datenvolume auf dem bereitgestellten Laufwerk die zugrunde liegende Dateifreigabe durchlaufen kann. Weitere Informationen finden Sie unter [Container Storage Support with Cluster Shared Volumes (CSV), Storage Spaces Direct (S2D), SMB Global Mapping](https://blogs.msdn.microsoft.com/clustering/2017/08/10/container-storage-support-with-cluster-shared-volumes-csv-storage-spaces-direct-s2d-smb-global-mapping/).

**Format der Konfigurationsdatei für virtuelle Computer (aktualisiert)** . Für virtuelle Computer mit der Konfigurationsversion 8.2 und höher wurde eine weitere Datei (.vmgs) hinzugefügt. VMGS steht für „VM Guest State” und ist eine neue interne Datei, die den Gerätezustand enthält, der zuvor Teil der VM-Laufzeitstatusdatei war.

## <a name="security-and-assurance"></a>Sicherheit und Assurance

**Netzwerkverschlüsselung** ermöglicht das schnelle Verschlüsseln von Netzwerksegmenten in einer softwaredefinierten Netzwerkinfrastruktur, um Sicherheits- und Compliance-Anforderungen zu erfüllen.

**Host-Überwachungsdienst (Host Guardian Service, HGS)** , wenn eine abgeschirmte VM aktiviert ist. Vor dieser Version war die Empfehlung, einen physischen 3-Knoten-Cluster bereitzustellen. Obwohl dadurch garantiert wurde, dass die Host-Überwachungsdienst-Umgebung nicht durch einen Administrator gefährdet ist, war dies oft sehr kostenintensiv.

**Linux als eine abgeschirmte VM** wird jetzt unterstützt.

Weitere Informationen finden Sie unter [Übersicht über geschütztes Fabric und abgeschirmte VMs](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms).

**SMBLoris-Sicherheitsrisiko** Ein als “SMBLoris” bezeichnetes Problem, das zu „Denial-of-Service” führen kann, wurde gelöst.

## <a name="storage"></a>Speicher

**Speicherreplikat**: Der Schutz für die von Storage Replica in Windows Server 2016 hinzugefügte Notfallwiederherstellung ist jetzt erweitert und umfasst:
- **Testen des Failovers**: Die Option zum Bereitstellen des Zielspeichers ist jetzt mit der Funktion zum Testen des Failovers möglich. Sie können eine Momentaufnahme des replizierten Speichers auf Zielknoten vorübergehend zu Test- und Sicherungszwecken bereitstellen.  Weitere Informationen finden Sie unter [Häufig gestellte Fragen zu Speicherreplikaten](https://aka.ms/srfaq). 
- **Unterstützung für das Projekt Honolulu**: Die Unterstützung für die grafische Verwaltung der Server-zu-Server-Replikation ist jetzt im Projekt Honolulu verfügbar. Dadurch wird die Anforderung, PowerShell zum Verwalten einer allgemeinen Arbeitslast zum Notfallschutz, entfernt.

**SMB**: 
- **SMB1 und das Entfernen der Gastauthentifizierung**: In Windows Server, Version 1709, wird der SMB1-Client und -Server nicht mehr standardmäßig installiert. Darüber hinaus ist die Möglichkeit deaktiviert, sich als Gast in SMB2 und höher standardmäßig zu authentifizieren. Weitere Informationen finden Sie unter [SMBv1 wird für Windows 10, Version 1709, und Windows Server, Version 1709, standardmäßig nicht installiert](https://support.microsoft.com/help/4034314/smbv1-is-not-installed-by-default-in-windows-10-rs3-and-windows-server). 

- **SMB2/SMB3-Sicherheit und Kompatibilität**: Es wurden zusätzliche Optionen für die Sicherheits- und Anwendungskompatibilität hinzugefügt, einschließlich der Möglichkeit, Oplocks SMB2+ für Legacy-Anwendungen zu deaktivieren, sowie die Signierung oder Verschlüsselung, die auf Basis jeder einzelnen Verbindung von einem Client erforderlich ist. Weitere Informationen finden Sie in der Hilfe zum SMBShare PowerShell-Modul.

**Datendeduplizierung**: 
- **Datendeduplizierung unterstützt jetzt ReFS**: Sie müssen nicht mehr zwischen den Vorteilen eines modernen Dateisystems mit ReFS und der Datendeduplizierung wählen: Sie können jetzt die Datendeduplizierung aktivieren, überall wo ReFS aktiviert werden kann. Erhöhen Sie die Speichereffizienz von schätzungsweise mehr als 95 % mit ReFS.
- **DataPort-API für den optimierten Eingang/Ausgang von deduplizierten Volumes**: Entwickler können jetzt die Kenntnisse der Datendeduplizierung zum effizienten Speichern von Daten, zum Verschieben von Daten zwischen Volumes, Servern und Clustern effizient nutzen.

## <a name="remote-desktop-services-rds"></a>Remotedesktopdienste (RDS)

**RDS ist in Azure AD integriert**, sodass Kunden die Richtlinien für den bedingten Zugriff, die Multi-Factor Authentication, die integrierte Authentifizierung mit anderen SaaS-Apps durch Azure AD und vieles mehr nutzen können. Weitere Informationen finden Sie unter [Integrieren von Azure AD Domain Services mit der RDS-Bereitstellung](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-azure-adds).

>[!TIP]
>Einen kurzen Einblick in andere interessante Neuigkeiten bei RDS finden Sie unter [Remote Desktop Services: Updates & bevorstehende Neuerungen](https://blogs.technet.microsoft.com/enterprisemobility/2017/09/20/first-look-at-updates-coming-to-remote-desktop-services/) (Remotedesktopdienste: Updates und bevorstehende Innovationen)

## <a name="networking"></a>Netzwerk

**Routing-Mesh von Docker** wird unterstützt. Der Eingangs-Routing-Mesh ist Teil des [Schwarmmodus](https://docs.docker.com/engine/swarm/), der integrierten Docker-Orchestrierungslösung für Container. Weitere Informationen finden Sie unter [Docker's routing mesh available with Windows Server version 1709](https://blogs.technet.microsoft.com/virtualization/2017/09/26/dockers-ingress-routing-mesh-available-with-windows-server-version-1709/) (Routing-Mesh von Docker, mit verfügbar mit Windows Server, Version 1709).

**Neue Features für Docker** sind verfügbar. Weitere Informationen finden Sie unter [Exciting new things for Docker with Windows Server 1709](https://blog.docker.com/2017/09/docker-windows-server-1709/) (Aufregende neue Funktionen für Docker mit Windows Server 1709).

**Windows-Netzwerke auf Augenhöhe mit Linux für Kubernetes**: Windows ist jetzt im Hinblick auf den Netzwerkbetrieb auf Augenhöhe mit Linux. Kunden können Kubernetes-Cluster mit vermischten Betriebssystemen in jeder Umgebung, einschließlich Azure, lokalen Umgebungen und Drittanbieter-Cloudstapeln, mit den gleichen Netzwerkgrundtypen und -topologien, die unter Linux unterstützt werden, ohne Problemumgehungen oder Switcherweiterungen bereitstellen.

**Core-Netzwerkstapel**: Es wurden mehrere Features des Core-Netzwerkstapels verbessert. Weitere Informationen zu diesen Features finden Sie unter [Core Network Stack Features in the Creators Update for Windows 10](https://blogs.technet.microsoft.com/networking/2017/07/13/core-network-stack-features-in-the-creators-update-for-windows-10/) (Features des Core-Netzwerkstapels im Creators Update für Windows 10).
- **TCP Fast Open (TFO)** : Es wurde Unterstützung für TFO hinzugefügt, um den TCP-3-Wege-Handshake-Prozess zu optimieren. TFO richtet bei der ersten Verbindung mit einem standardmäßigen 3-Wege-Handshake ein sicheres TFO-Cookie ein.  Nachfolgende Verbindungen mit dem gleichen Server verwenden das TFO-Cookie anstelle eines 3-Wege-Handshakes zum Herstellen einer Verbindung mit Null-Roundtripzeit.
- **CUBIC**: Die experimentelle native Windows-Implementierung von CUBIC, ein TCP-Überlastungssteuerungs-Algorithmus ist verfügbar. Die folgenden Befehle aktivieren oder deaktivieren CUBIC.

    ```
    netsh int tcp set supplemental template=internet congestionprovider=cubic
    netsh int tcp set supplemental template=internet congestionprovider=compound
    ```

- **Automatische Abstimmung erhalten**: Die automatische Logik von TCP berechnet den Parameter „Empfangsfenster“ einer TCP-Verbindung.  Verbindungen mit hoher Geschwindigkeit und/oder langen Verzögerungen benötigen diesen Algorithmus, um gute Leistungsmerkmale zu erzielen.  In dieser Version wurde der Algorithmus geändert, um mithilfe einer Schrittfunktion den maximal zulässigen Empfangsfensterwert für eine bestimmte Verbindung zusammenzuführen.
- **TCP-Statistik API**: Es wird eine neue API mit Namen SIO_TCP_INFO eingeführt.  Mit SIO_TCP_INFO können Entwickler umfassende Informationen zu einzelnen TCP-Verbindungen mit einer Socketoption abfragen.
- **IPv6**: Es gibt in dieser Version mehrere Verbesserungen in IPv6.
  - **RFC 6106** unterstützt: RFC 6106 erlaubt die DNS-Konfiguration über Routerankündigungen (RAs). Sie können die folgenden Befehle verwenden, um die RFC 6106-Unterstützung zu aktivieren oder zu deaktivieren:

    ```
    netsh int ipv6 set interface <ifindex> rabaseddnsconfig=<enabled | disabled>
    ```

  - **Flussbezeichnungen**: Ab dem Creators Update haben ausgehende TCP- und UDP-Pakete über IPv6 dieses Feld mit einem Hash der 5-Tupel (Quell-IP, Ziel-IP, Quellport, Zielport) festgelegt.  Hierdurch wird der Lastenausgleich oder die Flussklassifizierung der reinen IPv6-Rechenzentren effizienter ausgeführt. So aktivieren Sie die Flussbezeichnungen:

    ```
    netsh int ipv6 set flowlabel=[disabled|enabled] (enabled by default)
    netsh int ipv6 set global flowlabel=<enabled | disabled>
    ```

  - **ISATAP und 6to4**: Als Schritt in Richtung der zukünftigen Einstellung dieser Technologien sind sie im Creators Update standardmäßig deaktiviert.
- **Dead Gateway Detection (DGD)** : Der DGD-Algorithmus verschiebt automatisch die Verbindungen über auf ein anderes Gateway, wenn das aktuelle Gateway nicht erreichbar ist. In diesem Release wurde der Algorithmus verbessert, um die Netzwerkumgebung in regelmäßigen Abständen erneut zu überprüfen.
- [Test-NetConnection](https://technet.microsoft.com/itpro/powershell/windows/nettcpip/test-netconnection) ist ein integriertes Cmdlet in Windows PowerShell, das eine Vielzahl von Netzwerkdiagnosen ausführt.  In dieser Version wurde das Cmdlet verbessert, um detaillierte Informationen zur Auswahl der Route und der Quelladresse bereitzustellen.

**Software-Defined Networking**

- **Virtuelle Netzwerkverschlüsselung** ist ein neues Feature, das die Möglichkeit bietet, den virtuellen Netzwerkdatenverkehr zwischen virtuellen Computern zu verschlüsseln, die innerhalb der Subnetze miteinander kommunizieren und als „Verschlüsselung aktiviert“ gekennzeichnet sind. Dieses Feature nutzt Datagram Transport Layer Security (DTLS) im virtuellen Subnetz, um die Pakete zu verschlüsseln.  DTLS bietet Schutz vor Abhörversuchen, Manipulation und Fälschung durch jeden, der Zugriff auf das physische Netzwerk hat.
 
**Windows 10 VPN**

- **Infrastrukturtunnel vor der Anmeldung**. Standardmäßig erstellt Windows 10 VPN nicht automatisch Infrastrukturtunnel, wenn Benutzer nicht am Computer oder Gerät angemeldet sind. Sie können Windows 10 VPN so konfigurieren, dass vor der Anmeldung automatisch Infrastrukturtunnel mithilfe der Gerätetunnelfunktion (prelogon) im VPN-Profil erstellt werden.
- **Verwaltung von Remotecomputern und -geräten**.  Sie können Windows 10 VPN-Clients verwalten, indem Sie das Gerätetunnelfeature (prelogon) im VPN-Profil konfigurieren. Darüber hinaus müssen Sie die VPN-Verbindung so konfigurieren, dass die der VPN-Schnittstelle mit internen DNS-Diensten zugewiesenen IP-Adressen dynamisch registriert werden.
- **Gateways vor der Anmeldung angeben**. Sie können Gateways vor der Anmeldung mithilfe des Gerätetunnelfeatures (prelogon) im VPN-Profil angeben, kombiniert mit Datenverkehrsfiltern, um zu steuern, welche Verwaltungssysteme im Unternehmensnetzwerk über den Gerätetunnel zugänglich sind.

