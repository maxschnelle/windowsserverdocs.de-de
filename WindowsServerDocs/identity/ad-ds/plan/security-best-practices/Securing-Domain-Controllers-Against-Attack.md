---
ms.assetid: ba28bd05-16e6-465f-982b-df49633cfde4
title: Schützen von Domänencontrollern vor Angriffen
ms.author: daveba
author: iainfoulds
manager: daveba
ms.date: 06/18/2017
ms.topic: article
ms.openlocfilehash: 31cb962d03fab418f3d98320662a15ef4f3f3764
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93069482"
---
# <a name="securing-domain-controllers-against-attack"></a>Schützen von Domänencontrollern vor Angriffen

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

*Gesetz Nummer 3: Wenn ein böswilliger Benutzer uneingeschränkten physischen Zugriff auf Ihren Computer hat, ist es nicht mehr der Computer.* - [Zehn unveränderliche Sicherheitsgesetze (Version 2,0)](https://www.microsoft.com/en-us/msrc?rtc=1)

Domänen Controller stellen den physischen Speicher für die AD DS-Datenbank bereit, zusätzlich zur Bereitstellung der Dienste und Daten, mit denen Unternehmen ihre Server, Arbeitsstationen, Benutzer und Anwendungen effektiv verwalten können. Wenn privilegierter Zugriff auf einen Domänen Controller von einem böswilligen Benutzer abgerufen wird, kann dieser Benutzer die AD DS Datenbank und durch Erweiterung alle Systeme und Konten, die von Active Directory verwaltet werden, ändern, beschädigen oder zerstören.

Da Domänen Controller aus der AD DS Datenbank lesen und in diese schreiben können, bedeutet eine Gefährdung eines Domänen Controllers, dass Ihre Active Directory-Gesamtstruktur niemals als vertrauenswürdig eingestuft werden kann, wenn Sie nicht mit einer als funktionierend bekannten Sicherung wieder hergestellt werden können und die Lücken schließen, die den Kompromiss im Prozess zugelassen haben.

Abhängig von der Vorbereitung, den Tools und der Fähigkeiten eines Angreifers können Änderungen oder sogar irreparabel Schäden an der AD DS Datenbank innerhalb von Minuten bis Stunden, nicht an Tagen oder Wochen abgeschlossen werden. Dabei spielt es keine Rolle, wie lange ein Angreifer privilegierten Zugriff auf Active Directory hat, aber wie viel der Angreifer für den Moment geplant hat, wenn privilegierter Zugriff abgerufen wird. Das kompromittieren eines Domänen Controllers kann den sinnvollsten Weg zur breiten Weitergabe des Zugriffs oder den direktesten Weg zur Zerstörung von Mitglieds Servern, Arbeitsstationen und Active Directory bereitstellen. Aus diesem Grund sollten Domänen Controller separat und restrichtig geschützt werden, als die allgemeine Windows-Infrastruktur.

## <a name="physical-security-for-domain-controllers"></a>Physische Sicherheit für Domänen Controller

Dieser Abschnitt enthält Informationen zur physischen Absicherung von Domänen Controllern, ob es sich bei den Domänen Controllern um physische oder virtuelle Computer, an Rechenzentrums Standorten, Zweigstellen und sogar an Remote Standorten mit grundlegenden Infrastruktur Kontrollen handelt.

### <a name="datacenter-domain-controllers"></a>Datacenter-Domänen Controller

#### <a name="physical-domain-controllers"></a>Physische Domänen Controller

In Rechenzentren sollten physische Domänen Controller in dedizierten sicheren Racks oder Käfigen installiert werden, die von der allgemeinen Server Population getrennt sind. Wenn möglich, sollten Domänen Controller mit Trusted Platform Module-Chips (TPM) konfiguriert werden, und alle Volumes auf den Domänen Controller Servern sollten über BitLocker-Laufwerkverschlüsselung geschützt werden. BitLocker erhöht in der Regel den Leistungs Aufwand in einstelligen Prozentsätzen, aber schützt das Verzeichnis vor Gefährdung, auch wenn die Datenträger vom Server entfernt werden. BitLocker kann auch dazu beitragen, Systeme gegen Angriffe wie Rootkits zu schützen, da die Änderung von Startdateien bewirkt, dass der Server im Wiederherstellungs Modus gestartet wird, sodass die ursprünglichen Binärdateien geladen werden können. Wenn ein Domänen Controller für die Verwendung von Software-RAID, seriell angehängtem SCSI, SAN/NAS-Speicher oder dynamischen Volumes konfiguriert ist, kann BitLocker nicht implementiert werden. Daher sollte lokal verbundener Speicher (mit oder ohne Hardware-RAID) auf Domänen Controllern verwendet werden, wenn dies möglich ist

#### <a name="virtual-domain-controllers"></a>Virtuelle Domänen Controller

Wenn Sie virtuelle Domänen Controller implementieren, sollten Sie sicherstellen, dass Domänen Controller auf separaten physischen Hosts ausgeführt werden, als auf anderen virtuellen Maschinen in der Umgebung. Auch wenn Sie eine Virtualisierungsplattform von Drittanbietern verwenden, sollten Sie virtuelle Domänen Controller unter Hyper-V Server in Windows Server 2012 oder Windows Server 2008 R2 bereitstellen. Dadurch wird eine minimale Angriffsfläche bereitgestellt, und Sie können mit den Domänen Controllern verwaltet werden, die Sie hostet, anstatt mit den restlichen Virtualisierungshosts verwaltet werden Wenn Sie System Center Virtual Machine Manager (SCVMM) für die Verwaltung Ihrer Virtualisierungsinfrastruktur implementieren, können Sie die Verwaltung der physischen Hosts, auf denen sich virtuelle Computer des Domänen Controllers befinden, und der Domänen Controller an autorisierte Administratoren delegieren. Erwägen Sie außerdem, die Speicherung von virtuellen Domänen Controllern zu trennen, um zu verhindern, dass Speicher Administratoren auf die Dateien der virtuellen Computer zugreifen.

### <a name="branch-locations"></a>Verzweigungs Standorte

#### <a name="physical-domain-controllers-in-branches"></a>Physische Domänen Controller in branches

An Standorten, an denen mehrere Server gespeichert sind, aber nicht physisch gesichert werden, wenn die Daten Center Server geschützt sind, sollten physische Domänen Controller mit TPM-Chips und BitLocker-Laufwerkverschlüsselung für alle Servervolumes konfiguriert werden. Wenn ein Domänen Controller in Zweigstellen nicht in einem gesperrten Raum gespeichert werden kann, sollten Sie die Bereitstellung von RODCs an diesen Standorten in Erwägung gezogen.

#### <a name="virtual-domain-controllers-in-branches"></a>Virtuelle Domänen Controller in branches

Wenn möglich, sollten Sie virtuelle Domänen Controller in Zweigniederlassungen auf separaten physischen Hosts ausführen als die anderen virtuellen Computer am Standort. In Zweigstellen, in denen virtuelle Domänen Controller nicht auf separaten physischen Hosts von der restlichen Virtual Server-Auffüllung ausgeführt werden können, sollten Sie TPM-Chips und BitLocker-Laufwerkverschlüsselung auf Hosts implementieren, auf denen virtuelle Domänen Controller mindestens ausgeführt werden, und alle Hosts, wenn dies möglich ist. Abhängig von der Größe der Zweigstelle und der Sicherheit der physischen Hosts sollten Sie die Bereitstellung von RODCs an Zweigstellen in Erwägung gezogen.

### <a name="remote-locations-with-limited-space-and-security"></a>Remote Standorte mit eingeschränktem Speicherplatz und Sicherheit

Wenn Ihre Infrastrukturstandorte umfasst, an denen nur ein einziger physischer Server installiert werden kann, sollte ein Server, der virtualisierungsworkloads ausführen kann, am Remote Speicherort installiert werden, und BitLocker-Laufwerkverschlüsselung sollte so konfiguriert werden, dass alle Volumes auf dem Server geschützt werden. Ein virtueller Computer auf dem Server muss einen RODC ausführen, wobei andere Server als separate virtuelle Maschinen auf dem Host ausgeführt werden. Informationen zum Planen der Bereitstellung von RODC finden Sie im [Handbuch zur Planung und Bereitstellung von schreibgeschützten Domänen Controllern](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc771744(v=ws.10)). Weitere Informationen zum Bereitstellen und Sichern von virtualisierten Domänen Controllern finden Sie unter [Ausführen von Domänen Controllern in Hyper-V](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd363553(v=ws.10)). Ausführlichere Anleitungen zum Härten von Hyper-v, Delegieren der Verwaltung virtueller Computer und schützen virtueller Computer finden Sie auf der Microsoft-Website im [Hyper-v-Sicherheits Leit Faden](https://www.microsoft.com/download/details.aspx?id=16650) Solution Accelerator.

## <a name="domain-controller-operating-systems"></a>Domänencontroller-Betriebssysteme

Sie sollten alle Domänen Controller auf der neuesten Version von Windows Server ausführen, die in Ihrer Organisation unterstützt wird, und die Außerbetriebnahme veralteter Betriebssysteme in der Auffüllung des Domänen Controllers priorisieren. Wenn Sie Ihre Domänen Controller auf dem neuesten standhalten und ältere Domänen Controller eliminieren, können Sie die neuen Funktionen und Sicherheitsfunktionen, die möglicherweise nicht in Domänen oder Gesamtstrukturen mit Domänen Controllern mit einem älteren Betriebssystem verfügbar sind, nutzen Domänen Controller sollten neu installiert und höher gestuft werden, anstatt von vorherigen Betriebssystemen oder Server Rollen aktualisiert zu werden. Führen Sie also keine direkten Upgrades von Domänen Controllern aus, oder führen Sie den AD DS Installations-Assistenten auf Servern aus, auf denen das Betriebssystem nicht neu installiert ist. Durch die Implementierung von neu installierten Domänen Controllern stellen Sie sicher, dass die Legacy Dateien und-Einstellungen nicht versehentlich auf Domänen Controllern belassen werden, und Sie vereinfachen die Durchsetzung der konsistenten, sicheren Domänen Controller Konfiguration

## <a name="secure-configuration-of-domain-controllers"></a>Sichere Konfiguration von Domänen Controllern

Eine Reihe von frei verfügbaren Tools, von denen einige standardmäßig in Windows installiert werden, können verwendet werden, um eine anfängliche Sicherheitskonfigurations-Baseline für Domänen Controller zu erstellen, die anschließend von GPOs erzwungen werden kann. Diese Tools werden hier beschrieben.

### <a name="security-configuration-wizard"></a>Sicherheitskonfigurations-Assistent

Alle Domänen Controller sollten beim ersten Build gesperrt werden. Dies kann mithilfe des Sicherheitskonfigurations-Assistenten erreicht werden, der System intern in Windows Server ausgeliefert wird, um Dienst-, Registrierungs-, System-und wfas-Einstellungen auf einem "Base Build"-Domänen Controller zu konfigurieren. Einstellungen können gespeichert und in ein Gruppenrichtlinien Objekt exportiert werden, das mit der Domänen Controller-Organisationseinheit in jeder Domäne in der Gesamtstruktur verknüpft werden kann, um eine konsistente Konfiguration von Domänen Controllern zu erzwingen. Wenn Ihre Domäne mehrere Versionen von Windows-Betriebssystemen enthält, können Sie Windows-Verwaltungsinstrumentation (WMI)-Filter so konfigurieren, dass GPOs nur auf die Domänen Controller angewendet werden, auf denen die entsprechende Version des Betriebssystems ausgeführt wird.

### <a name="microsoft-security-compliance-toolkit"></a>Microsoft Security Compliance Toolkit

Die [Microsoft Security Compliance Toolkit](https://microsoft.com/download/details.aspx?id=55319) -Domänen Controller Einstellungen können mit den Einstellungen für den Sicherheitskonfigurations-Assistenten kombiniert werden, um umfassende konfigurationsbaselines für Domänen Controller zu schaffen, die von GPOs bereitgestellt und erzwungen werden, Active Directory die auf der OE-Organisationseinheit

### <a name="rdp-restrictions"></a>RDP-Einschränkungen

Gruppenrichtlinie Objekte, die mit allen Domänen Controllern in einer Gesamtstruktur verknüpft sind, müssen so konfiguriert werden, dass RDP-Verbindungen nur von autorisierten Benutzern und Systemen (z. b. Sprung Server) zugelassen werden. Dies kann durch eine Kombination von Einstellungen für Benutzerrechte und wfas-Konfiguration erreicht werden und sollte in GPOs implementiert werden, damit die Richtlinie konsistent angewendet wird. Wenn Sie umgangen wird, gibt die nächste Gruppenrichtlinie Aktualisierung das System an die richtige Konfiguration zurück.

### <a name="patch-and-configuration-management-for-domain-controllers"></a>Patch-und Konfigurations Verwaltung für Domänen Controller

Obwohl es möglicherweise intuitiv erscheint, sollten Sie das Patchen von Domänen Controllern und anderen kritischen Infrastrukturkomponenten getrennt von ihrer allgemeinen Windows-Infrastruktur in Erwägung gezogen. Wenn Sie die Software für die Unternehmens Konfigurations Verwaltung für alle Computer in Ihrer Infrastruktur nutzen, kann eine Gefährdung der Systems Management Software verwendet werden, um alle von dieser Software verwalteten Infrastrukturkomponenten zu kompromittieren oder zu zerstören. Indem Sie die Patch-und Systemverwaltung von Domänen Controllern von der allgemeinen Population trennen, können Sie die auf Domänen Controllern installierte Software Menge reduzieren und deren Verwaltung genau steuern.

### <a name="blocking-internet-access-for-domain-controllers"></a>Blockieren des Internet Zugriffs für Domänen Controller

Eine der Überprüfungen, die im Rahmen einer Active Directory-Sicherheitsbewertung ausgeführt werden, ist die Verwendung und Konfiguration von Internet Explorer auf Domänen Controllern. Internet Explorer (oder ein beliebiger anderer Webbrowser) sollte nicht auf Domänen Controllern verwendet werden. die Analyse von Tausenden von Domänen Controllern hat jedoch zahlreiche Fälle ergeben, in denen privilegierte Benutzer Internet Explorer verwendet haben, um das Intranet oder das Internet der Organisation zu durchsuchen.

Wie bereits im Abschnitt "Fehlkonfiguration" der [Angriffsmöglichkeiten](../../../ad-ds/plan/security-best-practices/Avenues-to-Compromise.md)beschrieben, ist das Durchsuchen des Internets (oder eines infizierten Intranets) von einem der leistungsstärksten Computer in einer Windows-Infrastruktur mit einem Konto mit hohen Berechtigungen (bei dem es sich um die einzigen Konten handelt, die sich standardmäßig auf Domänen Controllern anmelden dürfen) ein außergewöhnliches Risiko für die Sicherheit eines Unternehmens. Ob über ein Laufwerk durch herunterladen oder durch Herunterladen von schadsoftwareinfizierten "Hilfsprogramme", können Angreifer Zugriff auf alles erhalten, was Sie benötigen, um die Active Directory Umgebung vollständig zu kompromittieren oder zu zerstören.

Obwohl Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 und die aktuellen Versionen von Internet Explorer eine Reihe von Schutz gegen böswillige Downloads bieten, werden in den meisten Fällen, in denen Domänen Controller und privilegierte Konten zum Durchsuchen des Internets verwendet wurden, die Domänen Controller unter Windows Server 2003 ausgeführt, oder die von neueren Betriebssystemen und Browsern angebotenen Schutzmaßnahmen wurden absichtlich deaktiviert.

Das Starten von Webbrowsern auf Domänen Controllern sollte nicht nur über die Richtlinie zugelassen werden, sondern auch durch technische Kontrollen, und Domänen Controllern sollten keinen Zugriff auf das Internet haben. Wenn Ihre Domänen Controller standortübergreifend repliziert werden müssen, sollten Sie sichere Verbindungen zwischen den Standorten implementieren. Obwohl ausführliche Konfigurations Anweisungen den Rahmen dieses Dokuments sprengen, können Sie eine Reihe von Steuerelementen implementieren, um zu verhindern, dass Domänen Controller missbraucht oder falsch konfiguriert und anschließend kompromittiert werden.

### <a name="perimeter-firewall-restrictions"></a>Einschränkungen der Umkreis Firewall

Perimeterfirewalls sollten so konfiguriert werden, dass ausgehende Verbindungen von Domänen Controllern zum Internet blockiert werden. Obwohl Domänen Controller über Standort Grenzen hinweg kommunizieren müssen, können Umkreis Firewalls so konfiguriert werden, dass die Kommunikation Zwischenstand Orten ermöglicht wird. Befolgen Sie hierzu die Richtlinien, die unter [Konfigurieren einer Firewall für Active Directory Domänen und](https://support.microsoft.com/kb/179442) Vertrauens Stellungen auf der Microsoft-Support-Website erläutert werden.

### <a name="dc-firewall-configurations"></a>DC-Firewallkonfigurationen

Wie bereits beschrieben, sollten Sie den Sicherheitskonfigurations-Assistenten verwenden, um Konfigurationseinstellungen für die Windows-Firewall mit erweiterter Sicherheit auf Domänen Controllern zu erfassen. Überprüfen Sie die Ausgabe des Sicherheitskonfigurations-Assistenten, um sicherzustellen, dass die Firewallkonfigurationseinstellungen die Anforderungen Ihrer Organisation erfüllen, und verwenden Sie dann GPOs, um die Konfigurationseinstellungen zu erzwingen.

### <a name="preventing-web-browsing-from-domain-controllers"></a>Verhindern des webbrowsens von Domänen Controllern

Sie können eine Kombination aus der AppLocker-Konfiguration, der Proxykonfiguration "Black Hole" und der wfas-Konfiguration verwenden, um zu verhindern, dass Domänen Controller auf das Internet zugreifen und die Verwendung von Webbrowsern auf Domänen Controllern verhindert wird.
