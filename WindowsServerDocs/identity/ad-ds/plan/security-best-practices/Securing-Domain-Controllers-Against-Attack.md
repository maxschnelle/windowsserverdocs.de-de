---
ms.assetid: ba28bd05-16e6-465f-982b-df49633cfde4
title: Schützen von Domänencontrollern vor Angriffen
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 06/18/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 6be2899e85b68578518d9de1805c287367608163
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863091"
---
# <a name="securing-domain-controllers-against-attack"></a>Schützen von Domänencontrollern vor Angriffen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

*Gesetz Nummer 3: Falls ein Bösewicht uneingeschränkten physischen Zugriff auf Ihren Computer hat, ist es nicht mehr Ihrem Computer.* - [10 unveränderlichen Gesetze zur Sicherheit (Version 2.0)](https://technet.microsoft.com/security/hh278941.aspx)  
  
Domänencontroller Geben Sie den physischen Speicher für AD DS-Datenbank, abgesehen von der die Dienste und Daten, mit die Unternehmen ihre Server, Arbeitsstationen, Benutzer und Anwendungen effektiv verwalten können. Wenn von einem böswilligen Benutzer privilegierten Zugriff auf einen Domänencontroller abgerufen wird, diesen Benutzer kann ändern, beschädigen oder Zerstören von AD DS-Datenbank und durch Erweiterung, aller Systeme und Konten, die von Active Directory verwaltet werden.  
  
Da Domänencontroller können auslesen und in AD DS-Datenbank schreiben, Gefährdung eines Domänencontrollers bedeutet, dass die Active Directory-Gesamtstruktur nie trustworthy erneut berücksichtigt werden kann, wenn Sie mit einer bekannt fehlerfreien Sicherung wiederherstellen können und Schließen Sie die Lücken, die die Beeinträchtigung im Prozess zulässig.  
  
Je nach eines Angreifers Vorbereitung, Tools und Fähigkeiten, Änderung oder sogar irreparablen Schäden an der AD DS kann die Datenbank in Minuten, Stunden, nicht Tage oder Wochen abgeschlossen werden. Was spielt eine Rolle nicht wie lange ein Angreifer verfügt über privilegierte Zugriff auf Active Directory, aber wie viel der Angreifer für den Moment geplant hat beim Zugriff auf den privilegierten abgerufen wird. Gefährden von einem Domänencontroller bieten der zweckmäßigste Pfad zur umfangreiche Weitergabe des Zugriffs und der direkte Weg, Zerstörung von Servern, Arbeitsstationen und Active Directory. Aus diesem Grund sollten Domänencontroller einzeln und präziser als die allgemeinen Windows-Infrastruktur gesichert werden.  

## <a name="physical-security-for-domain-controllers"></a>Physische Sicherheit für Domänencontroller

Dieser Abschnitt enthält Informationen über die physikalische Sicherung von Domänencontrollern, gibt an, ob die Domänencontroller physischen sind oder virtuellen Computer in Rechenzentren, Zweigstellen und sogar Remotestandorte mit nur grundlegende Infrastruktur-Steuerelemente.  
  
### <a name="datacenter-domain-controllers"></a>Datacenter-Domänencontroller  
  
#### <a name="physical-domain-controllers"></a>Physischen Domänencontrollern

In Rechenzentren sollte physischen Domänencontrollern installiert werden, in dedizierten sicheren Serverschränken, die aus der Population für allgemeine Server getrennt sind. Wenn möglich, Domänencontroller mit Trusted Platform Module (TPM)-Chips konfiguriert werden, und alle Volumes in die Domäne-Controller-Server sollten über die BitLocker-Laufwerkverschlüsselung geschützt werden. BitLocker in der Regel wird die Leistung in einstellige Prozentsätzen, aber das Verzeichnis vor Angriffen geschützt, auch wenn der Datenträger vom Server entfernt werden. BitLocker hilft auch Systeme vor Angriffen wie z. B. Rootkits geschützt werden, da die Änderung der Startdateien führt den Server im Wiederherstellungsmodus gestartet wird, sodass die ursprünglichen Binärdateien geladen werden können. Wenn ein Domänencontroller so konfiguriert ist, um Software-RAID, Serial attached SCSI, SAN/NAS-Speicher zu verwenden, oder dynamische Volumes und BitLocker können nicht implementiert werden, sollte also lokal verbundenen Speicher (mit oder ohne Hardware-RAID) in Domänencontrollern verwendet werden immer möglich ist.  
  
#### <a name="virtual-domain-controllers"></a>Die virtuellen Domänencontroller unter 

Wenn Sie virtuelle Domänencontroller implementieren, sollten Sie sicherstellen, dass Domänencontroller auf separaten physischen Hosts als andere virtuelle Computer in der Umgebung ausgeführt. Auch wenn Sie eine Drittanbieter-Virtualisierungsplattform verwenden, erwägen Sie die Bereitstellung von virtuellen Domänencontrollern in Hyper-V-Server in Windows Server 2012 oder Windows Server 2008 R2, die eine minimale Angriffsfläche bietet, und mit den Domänencontrollern, die als Host dienende verwaltet werden können anstatt mit den restlichen die Virtualisierungshosts verwaltet wird. Wenn Sie System Center Virtual Machine Manager (SCVMM) für die Verwaltung der Virtualisierungsinfrastruktur implementieren, können Sie die Verwaltung delegieren für den physischen Hosts, auf die virtuellen Maschinen des Netzwerkcontrollers befinden und den Domänencontrollern selbst autorisierte Administratoren. Sie sollten auch berücksichtigen, trennen den Speicher von virtuellen Domänencontrollern, um zu verhindern, dass die Speicher-Administratoren den Zugriff auf Dateien der virtuellen Maschine.  
  
### <a name="branch-locations"></a>Zweigstellen  
  
#### <a name="physical-domain-controllers-in-branches"></a>Physische Domänencontroller in Zweigstellen

An Standorten, in denen mehrere Server befinden, jedoch werden nicht physisch gesichert, die den Grad an, dem Datacenter-Servern geschützt sind, sollten physischen Domänencontrollern für alle Servervolumes mit TPM-Chips und zur BitLocker-Laufwerkverschlüsselung konfiguriert werden. Wenn ein Domänencontroller in einem verschlossenen Raum in Zweigstellen gespeichert werden kann, sollten Sie erwägen, Bereitstellen von RODCs an diesen Standorten.  
  
#### <a name="virtual-domain-controllers-in-branches"></a>Virtuelle Domänencontroller in Zweigstellen

Wann immer möglich, sollten Sie virtuelle Domänencontroller in Filialen auf separaten physischen Hosts als die anderen virtuellen Computer auf der Website ausführen. In Filialen, die in der virtuelle Domänencontroller können nicht auf separaten physischen Hosts vom Rest der Auffüllung virtueller Server ausgeführt werden, sollten Sie TPM-Chips und zur BitLocker-Laufwerkverschlüsselung auf Hosts, die auf dem virtuellen Domänencontroller, zumindest ausgeführt, implementieren und Alle Hosts, falls möglich. Abhängig von der Größe der Zweigstelle und die Sicherheit der physischen Hosts sollten Sie erwägen, Bereitstellen von RODCs in Zweigstellen.  
  
### <a name="remote-locations-with-limited-space-and-security"></a>Remote-Standorten mit begrenzten Speicherplatz und Sicherheit

Wenn Ihre Infrastruktur Standorte enthält, in denen nur ein einzigen physischer Server installiert werden kann, ein Server, die auf die von virtualisierungsworkloads ausgeführt werden kann, sollte am Remotestandort installiert werden und sollte BitLocker Drive Encryption konfiguriert werden, um alle zu schützen Volumes auf dem Server. Einen virtuellen Computer auf dem Server sollte einen RODC mit anderen Servern als separate virtuelle Computer ausgeführt wird, auf dem Host ausgeführt werden. Informationen zur Planung für die Bereitstellung der RODC bereitgestellt wird, in der [Read-Only Domain Controller Planungs- und Bereitstellungshandbuch](https://go.microsoft.com/fwlink/?LinkID=135993). Weitere Informationen zum Bereitstellen und Sichern von virtuellen Domänencontrollern finden Sie unter [Ausführen von Domänencontrollern in Hyper-V](https://technet.microsoft.com/library/dd363553(v=ws.10).aspx) auf der TechNet-Website. Ausführlichere Anleitungen zum Absichern von Hyper-V Delegieren der Verwaltung virtueller Computer und den Schutz von virtuellen Computern finden Sie unter den [Hyper-V-Sicherheitshandbuch](https://www.microsoft.com/download/details.aspx?id=16650) Solution Accelerator auf der Microsoft-Website.  
  
## <a name="domain-controller-operating-systems"></a>Domänencontroller-Betriebssysteme

Sie sollten alle Domänencontroller auf die neueste Version von Windows Server ausführen, die in Ihrer Organisation unterstützt wird und priorisieren die Außerbetriebnahme der älteren Betriebssysteme in der Domäne Domänencontroller Population. Halten Ihre Domänencontroller aktuellen und dem Entfernen älterer Domänencontroller, können Sie häufig nutzen neue Funktionalität und die Sicherheit, die in Domänen oder Gesamtstrukturen mit Domänencontrollern, die mit älteren Betriebssystem sind möglicherweise nicht verfügbar. Domänencontroller müssen neu installiert und höher gestuft, anstatt ein Upgrade von vorherigen Betriebssystemen oder Serverrollen; d. h. nicht durchführen Sie direkte Upgrades von Domänencontrollern oder führen Sie den AD DS-Installations-Assistenten auf Servern, die auf denen das Betriebssystem nicht neu installiert wird. Implementieren Sie die neu installierte Domänencontroller, stellen Sie sicher, dass ältere Dateien und Einstellungen nicht versehentlich auf Domänencontrollern belassen werden, und Sie die Erzwingung von konsistenten und sicheren Domänencontrollerkonfiguration vereinfachen.  
  
## <a name="secure-configuration-of-domain-controllers"></a>Sichere Konfiguration von Domänencontrollern

Eine Reihe von kostenlos verfügbare Tools, von die einige in Windows standardmäßig installiert sind, kann verwendet werden, um eine Erstkonfiguration der Sicherheit einer Konfigurationsbasislinie für Domänencontroller zu erstellen, die anschließend mithilfe von GPOs erzwungen werden kann. Diese Tools werden hier beschrieben.  
  
### <a name="security-configuration-wizard"></a>Sicherheitskonfigurations-Assistent  

Alle Domänencontroller sollten beim ersten Build gesperrt werden. Dies kann erreicht werden, mithilfe des Sicherheitskonfigurations-Assistenten, die nativ unter Windows Server so konfigurieren Sie Service "," Registrierung "," System "und" WFAS-Einstellungen auf einem Domänencontroller "Basis-Build" enthalten ist. Einstellungen können gespeichert und in ein Gruppenrichtlinienobjekt, das mit der Domänencontroller-Organisationseinheit in jeder Domäne in der Gesamtstruktur zum Erzwingen der konsistenten Konfiguration von Domänencontrollern verknüpft werden kann exportiert werden. Wenn Ihre Domäne mehrere Versionen der Windows-Betriebssysteme enthalten ist, können Sie die Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI)-Filter zum Anwenden von Gruppenrichtlinienobjekte nur auf den Domänencontrollern, die mit der entsprechenden Version des Betriebssystems konfigurieren.  
  
### <a name="microsoft-security-compliance-toolkit"></a>Microsoft Security Compliance Toolkit

[Microsoft Security Compliance Toolkit](https://www.microsoft.com/download/details.aspx?id=55319) Einstellungen des Domänencontrollers mit Sicherheitskonfigurations-Assistent-Einstellungen, um umfassende von Konfigurationsbasislinien für die Domänencontroller zu erstellen, die bereitgestellt und von GPOs erzwungen kombiniert werden können Klicken Sie auf der Domänencontroller-Organisationseinheit in Active Directory bereitgestellt.  
  
### <a name="rdp-restrictions"></a>RDP-Einschränkungen

Group Policy Objects, die auf allen Domänencontrollern Organisationseinheiten in einer Gesamtstruktur zu verknüpfen sollte für das Zulassen von RDP-Verbindungen nur von autorisierten Benutzern und Systemen (beispielsweise jumpserver) konfiguriert werden. Dies kann durch eine Kombination von benutzereinstellungen für die Rechte und WFAS-Konfiguration erreicht werden und sollte in Gruppenrichtlinienobjekten implementiert werden, sodass die Richtlinie, konsistent angewendet wird. Wenn sie umgangen wird, gibt der nächsten Aktualisierung der Gruppenrichtlinie das System auf die richtige Konfiguration zurück.  
  
### <a name="patch-and-configuration-management-for-domain-controllers"></a>Patch- und Konfigurationsverwaltung für Domänencontroller

Obwohl es nicht intuitiv erscheinen mag, sollten Sie das patching von Domänencontrollern und andere wichtige Infrastrukturkomponenten getrennt von der allgemeinen Windows-Infrastruktur. Wenn Sie Enterprise Software zur konfigurationsverwaltung für alle Computer in Ihrer Infrastruktur nutzen, kann die Gefährdung der Systemverwaltungssoftware beeinträchtigen oder Zerstören von dieser Software verwaltete Infrastrukturkomponenten verwendet werden. Durch die Trennung von Patch- und Systems Management für Domänencontroller über die allgemeine Population, können Sie die Menge der Software, die auf Domänencontrollern, zusätzlich zum eng steuern ihrer Verwaltung installiert reduzieren.
  
### <a name="blocking-internet-access-for-domain-controllers"></a>Sperren des Internetzugriffs für Domänencontroller  

Eine der Überprüfungen, die als Teil einer Active Directory-Sicherheitsbewertung ausgeführt wird wird die Verwendung und Konfiguration von Internet Explorer auf einem Domänencontroller. Internet Explorer (oder einen beliebigen anderen Webbrowser) sollte nicht auf einem Domänencontroller verwendet werden, aber die Analyse von Tausenden von Domänencontrollern ergab zahlreiche Fälle, in dem privilegierte Benutzer mit Internet Explorer um Intranet des Unternehmens zu durchsuchen, oder das Internet.  
  
Wie oben beschrieben im Abschnitt "Fehlkonfiguration" [Wege der Gefährdung](../../../ad-ds/plan/security-best-practices/Avenues-to-Compromise.md), Browsen im Internet (oder einem infizierten Intranet) aus einer der leistungsfähigsten Computer in einer Windows-Infrastruktur, die mit einem weit reichenden Berechtigungen Konto (die die einzigen Konten, die zur lokalen Anmeldung auf Domänencontrollern standardmäßig zulässig sind) stellt eine außergewöhnliche Risiko für die Sicherheit einer Organisation. Egal ob Sie über ein Laufwerk durch Herunterladen oder durch Herunterladen von Schadsoftware infizierte "Dienstprogramme", erhalten Angreifer Zugriff auf alle benötigten vollständig beeinträchtigen oder Zerstören von Active Directory-Umgebung.  
  
Obwohl Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 und die aktuellen Versionen von Internet Explorer auf eine Anzahl von Schutz vor schädlichen Downloads in den meisten, denen Fällen, in denen Controller und privilegierten Konten bieten, hätte im Internet zu surfen, die Domänencontrollern Windows Server 2003 ausgeführt wurden oder Schutzmaßnahmen, die von neueren Betriebssystemen und Browsern bereitgestellt hatte wurde absichtlich deaktiviert.  
  
Starten von Webbrowsern auf Domänencontrollern, muss unterbunden werden, nicht nur von der Richtlinie, sondern auch durch technische Steuerelemente und Domänencontroller kein Zugriff auf das Internet zugelassen werden sollen. Wenn Ihre Domänencontroller zwischen Standorten replizieren müssen, sollten Sie sichere Verbindungen zwischen den Standorten implementieren. Obwohl ausführliche konfigurationsanweisungen würde den Rahmen dieses Dokuments sind, können Sie implementieren eine Reihe von Steuerelementen zum Beschränken der Möglichkeit von Domänencontrollern missbräuchlich verwendet werden oder falsch konfiguriert und anschließend kompromittiert werden.  
  
### <a name="perimeter-firewall-restrictions"></a>Umkreis-Firewalleinschränkungen

Umkreisfirewalls sollte konfiguriert werden, dass ausgehende Verbindungen von Domänencontrollern mit dem Internet blockiert. Aber möglicherweise Domänencontroller über Standortgrenzen miteinander kommunizieren müssen, können Umkreisfirewalls konfiguriert werden, um die standortübergreifende Kommunikation zu ermöglichen, gemäß die Richtlinien in [Gewusst wie: Konfigurieren einer Firewall für Domänen und-Vertrauensstellungen](https://support.microsoft.com/kb/179442) auf der Microsoft-Support-Website.  
  
### <a name="dc-firewall-configurations"></a>DC-Firewallkonfigurationen  

Wie zuvor beschrieben, sollten Sie den Sicherheitskonfigurations-Assistenten verwenden, um Konfigurationseinstellungen für die Windows-Firewall mit erweiterter Sicherheit auf Domänencontrollern zu erfassen. Sie sollten überprüfen, dass die Ausgabe des Sicherheitskonfigurations-Assistenten, stellen Sie sicher, dass die firewallkonfigurationseinstellungen die Anforderungen Ihres Unternehmens erfüllen, und klicken Sie dann Gruppenrichtlinienobjekte verwenden, um Einstellungen zu erzwingen.  
  
### <a name="preventing-web-browsing-from-domain-controllers"></a>Verhindern von Domänencontrollern Browsen im Web

Sie können eine Kombination von AppLocker-Konfiguration, "Black Hole" Proxykonfiguration und WFAS-Konfiguration verwenden, um zu verhindern, dass Domänencontroller auf das Internet zugreifen und die Verwendung der Web-Browser auf einem Domänencontroller zu verhindern.
