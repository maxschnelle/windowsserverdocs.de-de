---
ms.assetid: ba28bd05-16e6-465f-982b-df49633cfde4
title: "Sichern von Domänencontrollern vor Angriffen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: fc40d0ac536b128b799006214e360fa4d991ee44
ms.sourcegitcommit: 06a84f5caeab49b8480d6eed037aebbb59c77a9f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/14/2018
---
# <a name="securing-domain-controllers-against-attack"></a>Sichern von Domänencontrollern vor Angriffen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

*Recht Nummer drei: Wenn ein Angreifer physischen Zugriff auf Ihren Computer uneingeschränkten hat, es ist nicht Ihr Computer nicht mehr.* - [Zehn unveränderlichen Gesetze zur Sicherheit (Version 2.0)](https://technet.microsoft.com/security/hh278941.aspx)  
  
Domänencontroller Bereitstellen des physischen Speichers für die AD DS-Datenbank, zusätzlich zur Bereitstellung der Dienste und Daten, mit die Unternehmen effektiv ihre Server, Arbeitsstationen, Benutzer und Anwendungen verwalten können. Wenn privilegierten Zugriff auf einen Domänencontroller von einem böswilligen Benutzer abgerufen wird, die Benutzer kann ändern, beschädigt oder zerstören die AD DS-Datenbank und durch die Erweiterung aller Systeme und Konten, die von Active Directory verwaltet werden.  
  
Da Domänencontroller zum Lesen und in AD DS-Datenbank schreiben, Gefährdung eines Domänencontrollers bedeutet, dass Active Directory-Gesamtstruktur nicht vertrauenswürdig erneut berücksichtigt werden kann, wenn Sie mit einer bekannt fehlerfreien Sicherung wiederherstellen können und die Lücken zu schließen, die die Gefährdung des Prozesses zulässig.  
  
Je nach Vorbereitung, Tools und Fähigkeiten, Änderung oder sogar zudem zu irreparablen Schäden AD DS ein Angreifer kann die Datenbank in Minuten, Stunden, nicht Tagen oder Wochen ausgeführt werden. Was ist wichtig ist nicht wie lange ein Angreifer hat Zugriff auf Active Directory privilegierte, aber wie viel der Angreifer für den Moment geplant wurde beim Zugriff auf den privilegierten abgerufen wird. Einen Domänencontroller gefährden kann den kommt Pfad umfangreiche Weitergabe der Zugriff oder den direktesten Pfad zur Zerstörung von Mitgliedsservern, Arbeitsstationen und Active Directory bereitstellen. Aus diesem Grund sollten separat und strengere als die allgemeine Infrastruktur für Windows-Domänencontroller gesichert werden.  

  
## <a name="physical-security-for-domain-controllers"></a>Physische Sicherheit für Domänencontroller  
Dieser Abschnittenthält Informationen zum physisch sichern von Domänencontrollern, gibt an, ob die Domänencontroller physischen sind oder virtuelle Computer im Datencenter Speicherorte, Zweigstellen und sogar Remotestandorte mit nur grundlegende Infrastruktur-Steuerelemente.  
  
### <a name="datacenter-domain-controllers"></a>Datacenter-Domänencontroller  
  
#### <a name="physical-domain-controllers"></a>Physische Domänencontroller  
In Rechenzentren sollte physische Domänencontroller installiert werden, in dedizierten sicheren Racks oder Räume, die aus der allgemeine Population getrennt sind. Wenn möglich, Domänencontroller mit Trusted Platform Module (TPM)-Chips konfiguriert werden, und alle Volumes in der Domänencontroller-Server über BitLocker Drive Encryption geschützt werden sollte. BitLocker im Allgemeinen wird die Leistung in einer einstelligen Prozent, aber das Verzeichnis vor Angriffen geschützt, auch wenn der Datenträger vom Server entfernt werden. BitLocker hilft auch Systeme vor Angriffen, z.B. Rootkits zu schützen, da die Änderung der Startdateien bewirkt den Server im Wiederherstellungsmodus gestartet, damit die ursprünglichen Binärdateien geladen werden können. Wenn ein Domänencontroller zur Verwendung der Software-RAID, Serial attached SCSI, SAN/NAS-Speicher konfiguriert ist, oder dynamische Volumes, BitLocker können nicht implementiert werden, sollte also lokal installierter Speicher (mit oder ohne Hardware-RAID) Domänencontroller nach Möglichkeit verwendet werden.  
  
#### <a name="virtual-domain-controllers"></a>Virtuelle Domänencontroller  
Bei der Implementierung von virtuellen Domänencontrollern sollten Sie sicherstellen, dass der Domänencontroller auf separaten physischen Hosts als anderen virtuellen Computern in der Umgebung ausführen. Auch wenn Sie eine Drittanbieter-Virtualisierungsplattform verwenden, sollten Sie die Bereitstellung von virtuellen Domänencontrollern auf Hyper-V-Server in Windows Server2012 oder Windows Server2008 R2, die eine minimale Angriffsfläche bietet, und können mit den Domänencontrollern, anstatt mit dem Rest der die Virtualisierungshosts verwalteten Hostserver, verwaltet werden. Wenn Sie System Center Virtual Machine Manager (SCVMM) für die Verwaltung der Virtualisierungsinfrastruktur implementieren, können Sie Delegieren der Verwaltung der physischen Hosts, auf welche virtuellen Computern mit Domain Controller befinden und von den Domänencontrollern selbst autorisierte Administratoren. Außerdem sollten Sie die Trennung des Speichers von virtuellen Domänencontrollern, um zu verhindern, dass die Speicher-Administratoren den Zugriff auf Dateien des virtuellen Computers.  
  
### <a name="branch-locations"></a>Zweigstellen  
  
#### <a name="physical-domain-controllers"></a>Physische Domänencontroller  
An Standorten, in denen mehrere Server befinden sich aber nicht physisch in dem Umfang, der Datacenter Server gesichert werden gesichert, sollten physische Domänencontroller mit TPM-Chips und BitLocker Drive Encryption für alle Servervolumes konfiguriert werden. Wenn ein Domänencontroller in einem abgesperrten Raum in Zweigstellen gespeichert werden kann, sollten Sie das Bereitstellen von RODCs an diesen Standorten.  
  
#### <a name="virtual-domain-controllers"></a>Virtuelle Domänencontroller  
Wann immer möglich, sollten Sie virtuelle Domänencontroller in Filialen auf separaten physischen Hosts als die anderen virtuellen Computer am Standort ausführen. In Filialen, in denen virtuelle Domänencontroller auf separaten physischen Hosts vom Rest der Bevölkerung virtual Server ausgeführt werden können, sollten Sie TPM-Chips und BitLocker-Laufwerkverschlüsselung implementieren, auf Hosts, auf denen virtuelle Domänencontroller mindestens ausgeführt, und nach Möglichkeit alle Hosts. Je nach Größe der Filiale und die Sicherheit des physischen Hosts sollten Sie überlegen, Bereitstellen von RODCs in Zweigstellen.  
  
### <a name="remote-locations-with-limited-space-and-security"></a>Remote-Standorten mit begrenztem Platz und Sicherheit  
Enthält Ihre Infrastruktur Speicherorte in denen nur ein einzelner physischer Server installiert werden kann, ein Server zur Ausführung von Virtualisierungs-Workloads am Remotestandort installiert werden sollte, und BitLocker Drive Encryption sollte so konfiguriert werden, dass um alle Volumes auf dem Server zu schützen. Einen virtuellen Computer auf dem Server sollte einen RODC mit anderen Servern, die als separater virtueller Computer ausgeführt wird, auf dem Host ausgeführt werden. Informationen zum Planen für die Bereitstellung der RODC bereitgestellt wird, in der [Read-Only Domain Controller Planning and Deployment Guide](https://go.microsoft.com/fwlink/?LinkID=135993). Weitere Informationen zum Bereitstellen und Sichern von virtualisierten Domänencontrollern finden Sie unter [Ausführen von Domänencontrollern in Hyper-V](https://technet.microsoft.com/library/dd363553(v=ws.10).aspx) auf der TechNet-Website. Weitere Richtlinien für das Härten von Hyper-V Delegieren der Verwaltung virtueller Computer und schützen virtueller Computer, finden Sie unter der [Sicherheitshandbuch für Hyper-V](https://www.microsoft.com/download/details.aspx?id=16650) Solution Accelerator auf der Microsoft-Website.  
  
## <a name="domain-controller-operating-systems"></a>Domänencontroller-Betriebssysteme  
Sie sollten alle Domänencontroller auf die neueste Version von Windows Server ausführen, die in Ihrer Organisation unterstützt wird und der älteren Betriebssysteme in der Domäne Domänencontroller Population Außerbetriebsetzen priorisieren. Durch das beibehalten Ihrer Domänencontroller aktuelle und eliminiert ältere Domänencontroller, können Sie häufig nutzen der neuen Funktionen und Sicherheit, die nicht in Domänen oder Gesamtstrukturen mit Domänencontrollern, die älteren Betriebssysteme ausgeführt werden kann. Domänencontroller sollten werden neu installiert und heraufgestuft anstelle von vorherigen Betriebssystemen oder Serverrollen aktualisiert; Das heißt, nicht durchführen Sie direkte Upgrades von Domänencontrollern oder führen Sie die AD DS-Installations-Assistenten auf Servern, die auf denen das Betriebssystem nicht neu installiert wird. Durch die Implementierung neu installierte Domänencontroller, stellen Sie sicher, dass ältere Dateien und Einstellungen nicht versehentlich auf Domänencontrollern verbleiben, und Sie die Durchsetzung von konsistent und sichere Konfiguration des Domänencontrollers vereinfachen.  
  
## <a name="secure-configuration-of-domain-controllers"></a>Sichere Konfiguration von Domänencontrollern  
Eine Reihe von kostenlos verfügbare Tools, von die einige in Windows standardmäßig installiert sind, kann verwendet werden, um einer Konfigurationsbasislinie Erstkonfiguration der Sicherheit für Domänencontroller zu erstellen, die anschließend mithilfe von GPOs erzwungen werden kann. Diese Tools werden hier beschrieben.  
  
### <a name="security-configuration-wizard"></a>Sicherheitskonfigurations-Assistent  

Alle Domänencontroller sollten nach der ersten Erstellung gesperrt werden. Dies ist möglich mithilfe des Sicherheitskonfigurations-Assistenten, der direkt in Windows Server-Dienst, Registrierung, System- und WFAS Einstellungen auf einem Domänencontroller "Basis-Build" Konfigurieren ausgeliefert wird. Einstellungen können gespeichert und in ein Gruppenrichtlinienobjekt, das mit der Domänencontroller-Organisationseinheit in jeder Domäne in der Gesamtstruktur erzwungen einheitliche Konfiguration der Domänencontroller verknüpft werden kann exportiert werden. Wenn Ihre Domäne mehrere Versionen des Windows-Betriebssystemen enthalten ist, können Sie Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) Filter zum Anwenden von Gruppenrichtlinienobjekte nur auf den Domänencontrollern für die entsprechende Version des Betriebssystems konfigurieren.  
  
### <a name="microsoft-security-compliance-manager"></a>Microsoft Security Compliance Manager  
[Microsoft Security Compliance Manager](https://technet.microsoft.com/library/cc677002.aspx) Einstellungen des Domänencontrollers mit Sicherheitskonfigurations-Assistent-Einstellungen, und das umfassende von Konfigurationsbasislinien für Domänencontroller bereitgestellt und vom Gruppenrichtlinienobjekten, die an der Domänencontroller-Organisationseinheit in Active Directory bereitgestellt erzwungen kombiniert werden können.  
  
### <a name="applocker"></a>AppLocker  
AppLocker oder einer Drittanbieter-whitelistinganwendung sollten Sie zum Konfigurieren von Diensten und Anwendungen, die auf Domänencontrollern ausgeführt werden dürfen, und diese zugelassenen Programme und Dienste sollten werden bestehend aus nur für den Computer auf Host AD DS und möglicherweise DNS plus System Sicherheitssoftware wie Antivirensoftware erforderlich sind. Whitelisting zugelassenen Anwendungen auf Domänencontrollern wird eine zusätzliche Sicherheitsebene hinzugefügt, damit die Anwendung auch, wenn eine nicht autorisierte Anwendung auf einem Domänencontroller installiert ist, nicht ausgeführt werden kann.  
  
### <a name="rdp-restrictions"></a>RDP-Einschränkungen  
Group Policy Objects, die auf allen Domänencontrollern in einer Gesamtstruktur Organisationseinheiten verknüpfen sollte zum Zulassen von RDP-Verbindungen nur von autorisierten Benutzern und Systemen (z.B. sprungbrettservern) konfiguriert werden. Dies kann durch eine Kombination aus Benutzer Rechte Einstellungen und Konfiguration WFAS erreicht werden und sollten in Gruppenrichtlinienobjekten implementiert werden, damit die Richtlinie konsistent angewendet wird. Wenn es umgangen wird, gibt der nächste Aktualisierung der Gruppenrichtlinie das System auf die richtige Konfiguration zurück.  
  
### <a name="patch-and-configuration-management-for-domain-controllers"></a>Patch und Konfigurationsverwaltung für Domänencontroller  
Es mag nicht besonders intuitiv, sollten Sie das patching von Domänencontrollern und andere wichtige Infrastrukturkomponenten getrennt von der allgemeinen Windows-Infrastruktur. Wenn Sie die unternehmenskonfigurationsverwaltungssoftware für alle Computer in Ihrer Infrastruktur nutzen, kann die Gefährdung der Systems Management-Software Systemverwaltungssoftware alle von dieser Software verwalteten Infrastrukturkomponenten verwendet werden. Durch die Verwaltung der Patch und Systeme für Domänencontroller von der Allgemeinheit trennen, können Sie die Menge an auf Domänencontrollern, neben der Steuerung, deren Management eng installierte Software reduzieren.  
  
### <a name="blocking-internet-access-for-domain-controllers"></a>Sperren des Internetzugriffs für Domänencontroller  

Überprüft, die als Teil einer Active Directory Security Assessment erfolgt ist die Verwendung und Konfiguration von Internet Explorer auf Domänencontrollern. Internet Explorer (oder einen anderen Webbrowser) sollte nicht auf Domänencontrollern verwendet werden, aber Analyse der Tausende von Domänencontrollern verfügt über zahlreiche Fälle, in denen Benutzer die entsprechenden Berechtigungen Internet Explorer verwendet, um der Organisation im Intranet oder Internet durchsuchen, eingeblendet.  
  
Wie zuvor beschrieben im Abschnitt "Fehlkonfiguration" [Wege der Gefährdung](../../../ad-ds/plan/security-best-practices/Avenues-to-Compromise.md), Surfen im Internet (oder ein infiziertes Intranet) aus einer der leistungsstärksten Computer in einer Windows-Infrastruktur mit einem sehr privilegierten Konto (die standardmäßig lokal an Domänencontrollern anmelden dürfen nur Konten) stellt eine außergewöhnliche Risiko für die Sicherheit einer Organisation. Über ein Laufwerk als Download oder durch Herunterladen von Schadsoftware infiziert "Hilfsprogramme", können Angreifer auf Alles zugreifen, die sie vollständig Systemverwaltungssoftware Active Directory-Umgebung benötigen.  
  
Windows Server2012, Windows Server2008 R2, Windows Server2008 und aktuelle Versionen von Internet Explorer eine Reihe von Schutzmaßnahmen gegen bösartige Downloads bieten, zwar in den meisten Fällen, in der, die Domäne Domänencontroller und privilegierte Konten zum Durchsuchen des Internets verwendet worden, den Domänencontrollern Windows Server2003 ausgeführt wurden, oder schutzwirkung von neuere Betriebssysteme und Browser haben absichtlich deaktiviert.  
  
Starten von Webbrowsern auf Domänencontrollern, muss unterbunden werden, nicht nur durch eine Richtlinie, sondern auch durch technische Steuerelemente und Domänencontrollern sollte nicht gestattet werden, auf das Internet zugreifen. Wenn Ihre Domänencontroller über mehrere Standorte repliziert werden müssen, sollten Sie sichere Verbindungen zwischen den Standorten implementieren. Obwohl ausführliche konfigurationsanweisungen den Rahmen dieses Dokuments sind, können Sie eine Reihe von Steuerelementen zum Einschränken der Fähigkeit der Domänencontroller missbraucht oder falsch konfiguriert und anschließend gefährdet werden implementieren.  
  
### <a name="perimeter-firewall-restrictions"></a>Umkreis-Firewall-Einschränkungen  
Umkreisfirewalls sollte zum Blockieren des ausgehender Verbindungen von Domänencontrollern mit dem Internet konfiguriert werden. Aber möglicherweise Domänencontroller über Standortgrenzen miteinander kommunizieren müssen, Umkreisnetzwerk Firewalls so konfiguriert werden, um die standortübergreifende Kommunikation zu ermöglichen, anhand der Richtlinien in [Vorgehensweise beim Konfigurieren einer Firewall für Domänen und -Vertrauensstellungen](https://support.microsoft.com/kb/179442) auf der Microsoft Support-Website.  
  
### <a name="dc-firewall-configurations"></a>DC-Firewall-Konfigurationen  

Wie oben beschrieben, sollten Sie des Sicherheitskonfigurations-Assistenten verwenden, um Konfigurationen für die Windows-Firewall mit erweiterter Sicherheit auf Domänencontrollern zu erfassen. Lesen Sie die Ausgabe des Sicherheitskonfigurations-Assistenten, stellen Sie sicher, dass die Firewallkonfigurationseinstellungen der Anforderungen Ihrer Organisation erfüllen, und klicken Sie dann Gruppenrichtlinienobjekte verwenden, um Einstellungen für die Konfiguration zu erzwingen.  
  
### <a name="preventing-web-browsing-from-domain-controllers"></a>Verhindern von Domänencontrollern beim Browsen im Web  
Sie können eine Kombination von AppLocker-Konfiguration "Schwarzes Loch" Proxykonfiguration und WFAS Konfiguration Domänencontroller zu verhindern, dass Zugriff auf das Internet und zu verhindern, dass die Verwendung von Webbrowsern auf Domänencontrollern.  
  


