---
ms.assetid: eafdddc3-40d7-4a75-8f4f-a45294aabfc8
title: Implementieren von sicheren Verwaltungshosts
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ed2ff7bfa0cc3b27506b1ca324e819860eef314c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890421"
---
# <a name="implementing-secure-administrative-hosts"></a>Implementieren von sicheren Verwaltungshosts

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sichere administrative Hosts sind Arbeitsstationen oder Server, die speziell für den Zweck der Erstellung der sicherer Plattformen, die von denen privilegierte Konten in Active Directory oder auf einem Domänencontroller von Verwaltungsaufgaben ausführen konfiguriert wurden, Domäne Angehörige Systeme und Anwendungen auf einer Domäne Angehörige Systeme ausgeführt werden. In diesem Fall bezieht sich "privilegierte Konten", nicht nur für Konten, die Mitglieder der Gruppen mit hohen Berechtigungen in Active Directory sind, sondern auch für sämtliche Konten, die delegierte Rechte wurden und die Berechtigungen, die administrative Aufgaben ausgeführt werden können.  
  
Diese Konten möglicherweise beim Helpdesk-Konten, die haben die Möglichkeit, Zurücksetzen von Kennwörtern für die meisten Benutzer in einer Domäne, die zum Verwalten von DNS-Einträge und Zonen verwendet werden oder Konten, die für die konfigurationsverwaltung verwendet werden. Sichere administrative Hosts auf administrative Funktionen reserviert sind, und sie führen keine Software, z. B. e-Mail-Anwendungen, Webbrowser oder Produktivitätssoftware z. B. Microsoft Office.  
  
Obwohl der "höchsten Berechtigungen" Konten und Gruppen entsprechend der am häufigsten repräsentative Motoröltemperatur geschützten sein sollte, ist dies beseitigt nicht die Notwendigkeit zum Schutz von Konten und Gruppen, die die Rechte als die eines Standardbenutzers Konten gewährt wurden.  
  
Eine sichere administrative Hosts kann eine dedizierte Arbeitsstation, die nur für administrative Aufgaben ein Mitgliedsserver verwendet wird, die die Remotedesktopgateway-Server-Rolle ausgeführt wird und die IT-Benutzern Verbindung zum Ausführen der Verwaltung des Zielhosts oder einem Server mit Hyper-V-Rolle und bietet einen eindeutigen virtueller Computer für jeden IT-Benutzer, die für seine administrativen Aufgaben verwendet. In vielen Umgebungen können die Kombination aller drei Ansätze implementiert werden.  
  
Implementieren sichere administrative Hosts erfordert, Planung und Konfiguration, die Größe, Verwaltungsmethoden, Risikobereitschaft und Budget Ihrer Organisation entspricht. Überlegungen und Optionen für das Implementieren sichere administrative Hosts dienen hier für die Verwendung bei der Entwicklung einer administrative Strategie für Ihre Organisation geeignet ist.  
  
## <a name="principles-for-creating-secure-administrative-hosts"></a>Prinzipien für das Erstellen sichere Administrative Hosts  
Um effektiv Systeme vor Angriffen zu schützen, sollten einige allgemeine Prinzipien Bedenken beibehalten werden:  
  
1.  Sie sollten niemals ein vertrauenswürdiges System (d. h. mit einem sicheren Server z. B. einen Domänencontroller) verwalten, von einem weniger vertrauenswürdigen Host (d. h. eine Arbeitsstation, die nicht so stark wie die Systeme sicher ist, die er verwaltet).  
  
2.  Sie sollten sich nicht auf einem einzelnen authentifizierungsfaktors verlassen, Ausführung privilegierte Aktivitäten; also sollte Kombinationen aus Benutzername und Kennwort nicht akzeptabel Authentifizierung betrachtet werden, da nur ein Faktor (etwas, das Sie wissen) dargestellt wird. Sie sollten erwägen, in denen Anmeldeinformationen generiert und zwischengespeichert oder gespeichert werden in der administrativen Szenarien.  
  
3.  Obwohl die meisten Angriffe in der aktuellen Bedrohungslandschaft Schadsoftware und böswillige Hacker nutzen zu können, ausgelassen Sie physischen Sicherheit beim Entwerfen und implementieren sichere administrative Hosts nicht werden.  
  
### <a name="account-configuration"></a>Konfiguration des Kontos  
Auch wenn Ihre Organisation nicht gerade Smartcards verwendet, sollten Sie für die privilegierte Konten und sichere administrative Hosts implementieren. Dahingehend Smartcard-Anmeldung für alle Konten durch ändern die folgende Einstellung in einem Gruppenrichtlinienobjekt, das mit den administrativen Hosts mit Organisationseinheiten verknüpft ist, sollte administrativen Hosts konfiguriert werden:  
  
**Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Sicherheitsoptionen\Interaktive computeranmeldung: Smartcard erforderlich**  
  
Mit dieser Einstellung müssen alle interaktive Anmeldungen eine Smartcard, unabhängig von der Konfiguration auf einem einzelnen Konto in Active Directory verwenden.  
  
Sie sollten auch konfigurieren, dass sichere administrative Hosts zum Zulassen von Anmeldungen nur von autorisierten Konten, die in konfiguriert werden können:  
  
**Computer Computerkonfiguration\Richtlinien\Windows Einstellungen\Sicherheitseinstellungen\Lokale Sicherheitsoptionen Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten**  
  
Dies gewährt interaktive (und, sofern zutreffend, Remote Desktop Services) Anmelderechte nur auf autorisierte Benutzer des sicheren administrative Hosts.  
  
### <a name="physical-security"></a>Physische Sicherheit  
Für den administrativen Hosts als vertrauenswürdig angesehen werden müssen sie konfiguriert und so stark wie die Systeme, die sie verwalten geschützt werden. Die Empfehlungen in den meisten [Domäne-Controllern für Angriff Sichern](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md) gelten auch für die Hosts, die zur Verwaltung von Domänencontrollern und AD DS-Datenbank verwendet werden. Eine der Herausforderungen beim Implementieren von sicheren administrative Systemen in den meisten Umgebungen ist, dass physischer Sicherheit kann schwieriger zu implementieren, da diese Computer häufig in Bereichen, die nicht so sicher wie die Server befinden, die z. B. in Rechenzentren gehostet werden administrative Benutzer-Desktops.  
  
Physische Sicherheit umfasst die Steuerung des physischen Zugriffs auf administrativen Hosts. In einem kleinen Unternehmen kann dies bedeuten, dass Sie warten, dass eine dedizierte Administratorarbeitsstation, das gehalten wird in einem Büro oder einer Schreibtischschublade bei Nichtverwendung gesperrt wird. Oder es kann bedeuten, dass wenn Sie für die Verwaltung von Active Directory oder Ihren Domänencontrollern müssen, melden Sie sich der Domänencontroller direkt an.  
  
In mittelgroßen Organisationen in Erwägung, implementieren sichere "springen administrative Server", befinden sich an einem sicheren Ort in einem Büro und verwendet werden, wenn die Verwaltung von Active Directory oder die Domänencontroller erforderlich ist. Sie können auch Administratorarbeitsstationen implementieren, die an sicheren Orten bei Nichtverwendung, mit oder ohne jumpserver gesperrt sind.  
  
In großen Organisationen können Sie die Datacenter-untergebracht Jump-Server bereitstellen, die streng kontrollierten Zugriff auf Active Directory zu ermöglichen; -Domänencontrollern und Datei, drucken oder Anwendungsserver. Implementierung eine sprungbrettserverarchitektur ist wahrscheinlich eine Kombination von sicheren Arbeitsstationen und Server in großen Umgebungen enthalten.  
  
Unabhängig von der Größe Ihrer Organisation und den Entwurf Ihrer administrativen Hosts Sie sollten physische Computer vor nicht autorisiertem Zugriff oder Diebstahl schützen und sollte BitLocker Drive Encryption zum Verschlüsseln und schützen Sie die Laufwerke auf administrativen Hosts verwenden . Implementieren von BitLocker auf administrativen Hosts, können auch, wenn ein Host gestohlen wird oder der Datenträger entfernt werden, Sie sicherstellen, dass die Daten auf dem Laufwerk für nicht autorisierte Benutzer nicht zugänglich sind.  
  
### <a name="operating-system-versions-and-configuration"></a>Betriebssystemversionen und -Konfiguration  
Alle administrativen Hosts an, ob Server oder Arbeitsstationen, sollte das neueste Betriebssystem in Ihrer Organisation verwendet, die weiter oben in diesem Dokument beschriebenen Gründen ausgeführt. Mit aktuellen Betriebssystemen, die Vorteile Ihres Administrationsmitarbeiter über neue Sicherheitsfunktionen, vollständige anbietersupport und zusätzliche Funktionen, die im Betriebssystem eingeführt. Darüber hinaus, wenn Sie ein neues Betriebssystem durch die Bereitstellung ersten administrativen Hosts evaluieren, müssen Sie machen Sie sich mit den neuen Features, Einstellungen und Mechanismen bietet, die später bei der Planung genutzt werden können umfassendere Bereitstellung des Betriebssystems. Dann werden die Benutzer in Ihrer Organisation entwickelten auch die Benutzer, die mit dem neuen Betriebssystem vertraut sind und am besten zu ihrer Unterstützung positioniert sind.  
  
### <a name="microsoft-security-configuration-wizard"></a>Sicherheitskonfigurations-Assistent von Microsoft  
Wenn Sie Jump-Server als Teil Ihrer Strategie für die administrative Host implementieren, sollten Sie die integrierten Sicherheitskonfigurations-Assistenten verwenden, so konfigurieren Sie den Dienst, Registrierung, überwachungs- und Firewall-Einstellungen für die Angriffsfläche des Servers zu verringern. Wenn die Konfigurationseinstellungen für den Sicherheitskonfigurations-Assistent gesammelt und konfiguriert wurden, können die Einstellungen an einem GPO konvertiert werden, die verwendet wird, um eine konsistente Basisrichtlinie-Konfiguration auf alle Jump-Server zu erzwingen. Sie können weiter bearbeiten Sie das Gruppenrichtlinienobjekt zum Implementieren der Sicherheit Einstellungen spezifische Informationen zum Server und können alle Einstellungen mit zusätzlichen Einstellungen extrahiert aus der Microsoft Security Compliance Manager kombinieren.  
  
### <a name="microsoft-security-compliance-manager"></a>Microsoft Security Compliance Manager  
Die [Microsoft Security Compliance Manager](https://technet.microsoft.com/library/cc677002.aspx) ist ein Tool, kostenlos zur Verfügung, die Sicherheitskonfigurationen integriert ist, die von Microsoft, basierend auf der Konfiguration des Betriebssystems Version und die Rolle, empfohlen werden und erfasst sie in einem ein einzelnes Tool und die Benutzeroberfläche, die zum Erstellen und konfigurieren die grundlegenden Sicherheitseinstellungen für Domänencontroller verwendet werden kann. Microsoft Security Compliance Manager-Vorlagen können kombiniert werden, mit Sicherheitskonfigurations-Assistent-Einstellungen, um umfassende Konfigurationsbasislinien für Jump-Server zu erstellen, die bereitgestellt und erzwungen werden, mithilfe von GPOs, die unter der die Organisationseinheiten in der Jump-Server sind bereitgestellt. befindet sich in Active Directory.  
  
> [!NOTE]  
> Während ich dies schreibe, Microsoft Security Compliance Manager gehören keine Einstellungen, die spezifisch für Jump-Server oder andere sichere administrative Hosts, aber Security Compliance Manager (SCM) können weiterhin verwendet werden, um anfängliche Baselines für Ihre administrativen zu erstellen -Hosts. Sichern Sie die Hosts sollten Sie jedoch zusätzliche Sicherheitseinstellungen für extrem sichere Arbeitsstationen und Server anwenden.  
  
### <a name="applocker"></a>AppLocker  
Administrative Hosts und virtuellen Machinesshould werden mit Skripts, Tools und Anwendung Whitelists über AppLocker oder einer Drittanbieter-Einschränkung Anwendungssoftware konfiguriert. Administrative Anwendungen oder Hilfsprogramme, die nicht erfüllen, um Einstellungen zu sichern sollten aktualisiert oder ersetzt, die mit Tools, die sichere Entwicklung und administrative Verfahren entspricht. Wenn neuer oder zusätzlicher Tools auf einem Host administrative benötigt wird, Anwendungen und Dienstprogramme sollten gründlich getestet werden, und wenn die Tools für die Bereitstellung auf administrativen Hosts geeignet ist, kann es auf den Systemen Whitelists hinzugefügt werden.  
  
### <a name="rdp-restrictions"></a>RDP-Einschränkungen  
Obwohl die spezifische Konfiguration abhängig von der Architektur Ihrer Systeme, administrative variieren sollten Einschränkungen werden für die Konten und -Computer verwendet werden können, um Remote Desktop Protocol (RDP)-Verbindungen auf verwalteten Systemen herzustellen, springen Sie Server, um den Zugriff auf Domänencontroller und andere verwaltete Systeme von autorisierten Benutzern und Systemen zu steuern, wie die Verwendung von Remotedesktopgateway (RD-Gateway).  
  
Interaktive Anmeldungen durch autorisierte Benutzer können sollte und sollten entfernt oder so lange blockiert, andere Logon-Typen, die für den Zugriff auf Server nicht benötigt werden.  
  
### <a name="patch-and-configuration-management"></a>Patch- und Konfigurationsverwaltung  
Kleinere Organisationen benötigen möglicherweise-Produkte wie Windows Update oder [Windows Server Update Services](https://technet.microsoft.com/windowsserver/bb332157) (WSUS) zur Bereitstellung von Updates für Windows-Systeme verwalten, während größere Unternehmen Enterprise Patch implementieren können, und Software zur konfigurationsverwaltung wie System Center Configuration Manager. Unabhängig von den Mechanismen ab, die Sie zum Bereitstellen von Updates auf Ihre allgemeine und arbeitsstationsstruktur verwenden, sollten Sie separate Bereitstellungen für Hochsicherheitssystemen wie z. B. Domänencontrollern, Zertifizierungsstellen und administrativen Hosts. Durch Trennung dieser Systeme die allgemeine-Infrastruktur, wenn Ihre Software oder Service Management-Konten gefährdet sind, kann keine Gefährdung problemlos auf die sicherste Systeme in Ihrer Infrastruktur erweitert werden.  
  
Obwohl Sie keine manuellen Prozesse für sichere Systeme implementieren müssen, sollten Sie eine separate Infrastruktur für die Aktualisierung sicherer Systeme konfigurieren. Selbst in großen Organisationen kann diese Infrastruktur in der Regel über dedizierte WSUS-Server und Gruppenrichtlinienobjekte für sichere Systeme implementiert werden.  
  
### <a name="blocking-internet-access"></a>Zugriff auf das Internet blockiert  
Administrativen Hosts Zugriff auf das Internet nicht zugelassen werden sollen, noch müssen diese im Intranet einer Organisation navigieren können. Webbrowser und ähnliche Anwendungen sollten auf administrativen Hosts nicht zugelassen. Sie können Zugriff auf das Internet für sichere Hosts über eine Kombination von Perimeter Firewall-Einstellungen, WFAS-Konfiguration und "Black Hole" Proxykonfiguration sichere Hosts blockieren. Sie können auch Anwendungswhitelisting verwenden, um zu verhindern, dass Webbrowser auf administrativen Hosts verwendet wird.  
  
### <a name="virtualization"></a>Virtualisierung  
Wenn möglich, sollten erwägen Sie, virtuellen Computern als administrativen Hosts zu verwenden. Mithilfe der Virtualisierung, können Sie pro-Benutzer erstellen administrative Systemen, die zentral gespeichert und verwaltet werden und die kann problemlos heruntergefahren werden bei Nichtverwendung, sicherzustellen, dass die Anmeldeinformationen nicht aktiv auf die administrativen Systeme bleiben. Sie können auch anfordern, dass virtuelle administrativen Hosts, eine anfangsmomentaufnahme nach jeder Verwendung zurückgesetzt werden, um sicherzustellen, dass die virtuellen Computer makellose bleiben. Weitere Informationen zu Optionen für die Virtualisierung von administrativen Hosts wird im folgenden Abschnitt bereitgestellt.  
  
## <a name="sample-approaches-to-implementing-secure-administrative-hosts"></a>Beispiel-Methoden zum Implementieren der sichere Administrative Hosts  
Unabhängig davon, wie Sie entwerfen und Bereitstellen Ihrer administrativen Hostinfrastruktur sollten Sie Bedenken in den "Prinzipien für Erstellen von sicheren Administrative Hosts" weiter oben in diesem Thema bereitgestellten Richtlinien halten. Jeder der hier beschriebenen Ansätze bietet allgemeine Informationen, wie Sie "Verwaltung" und "Productivity"-Systemen, die von der IT-Abteilung verwendet trennen können. Produktivität-Systeme sind Computer, die IT-Administratoren verwenden zum Überprüfen von e-Mail-Adresse im Internet zu surfen, und um allgemeine Produktivitätssoftware z. B. Microsoft Office zu verwenden. Administrative Systeme sind Computer, die festgeschrieben und speziell für die für die tägliche Verwaltung einer IT-Umgebung verwenden.  
  
Die einfachste Möglichkeit, implementieren Sie sichere administrative Hosts ist Ihre IT-Mitarbeiter mit sicheren Arbeitsstationen Bereitstellen von dem sie administrative Aufgaben ausführen können. In einer reinen Workstation-Implementierung wird jeder administrativen Arbeitsstation zum Starten von Verwaltungstools und RDP-Verbindungen zum Server und andere Infrastruktur verwalten. Arbeitsstation-only-Implementierungen können in kleineren Organisationen effektiv sein, obwohl umfangreicher und komplexere Infrastrukturen von einer verteilten Entwurfs profitieren können, für die administrativen Hosts in der dedizierten administrativer Servern und Arbeitsstationen verwendet werden, wird als beschrieben in "Implementieren sicherer administrativen Arbeitsstationen und springen Server" weiter unten in diesem Thema.  
  
### <a name="implementing-separate-physical-workstations"></a>Implementieren Separate physikalische Workstations  
Eine Möglichkeit, dass Sie den administrativen Hosts implementieren können, besteht darin, jeden IT-Benutzer zwei Arbeitsstationen auszugeben. Eine Arbeitsstation ist mit einem "regular" Benutzerkonto verwendet, zum Durchführen von Aktivitäten wie e-Mails und produktivitätsanwendungen, verwenden, während die zweite Arbeitsstation ausschließlich auf administrativen Funktionen vorgesehen ist.  
  
Für die Produktivität Workstation kann das IT-Personal reguläre Benutzerkonten anstelle der Verwendung von privilegierter Konten zur Anmeldung beim ungeschützten Computer zugewiesen werden. Die Verwaltungsarbeitsstation mit eine repräsentative Motoröltemperatur kontrollierten Konfiguration konfiguriert werden, und die IT-Mitarbeiter sollten ein anderes Konto verwenden, um auf die administrativen Arbeitsstation anmelden.  
  
Wenn Sie die Smartcards implementiert haben, Arbeitsstationen für Administratoren sollte smartcardanmeldungen dahingehend konfiguriert werden, und IT-Mitarbeiter sollten separate Konten für administrative Zwecke, die auch so konfiguriert, dass die Verwendung von Smartcards für die interaktive Anmeldung zugewiesen werden. Der administrative Host sollte mit verstärkter Sicherheit wie zuvor beschrieben, und darf nur bestimmte IT-Benutzer zur lokalen Anmeldung auf der Verwaltungsarbeitsstation.  
  
#### <a name="pros"></a>Vorteile  
Implementieren Sie separate physische Systeme, können Sie sicherstellen, dass jeder Computer, für die Rolle entsprechend konfiguriert ist und IT-Benutzern versehentlich administrative Systeme Risiken aussetzen nicht möglich.  
  
#### <a name="cons"></a>Nachteile  
  
-   Implementieren von separaten physischen Computern erhöht die Hardwarekosten anfallen.  
  
-   Anmelden bei einem physischen Computer mit den Anmeldeinformationen, die zur Verwaltung von remote-Systems verwendet werden, werden die Anmeldeinformationen im Arbeitsspeicher zwischenspeichert.  
  
-   Wenn Arbeitsstationen für Administratoren nicht sicher gespeichert werden, möglicherweise sie anfällig für über Mechanismen wie z. B. Key Logger physischer Hardware oder andere Angriffe auf physischer Basis zu gefährden.  
  
### <a name="implementing-a-secure-physical-workstation-with-a-virtualized-productivity-workstation"></a>Implementieren einer sicheren physischen Arbeitsstation mit einer virtualisierten Produktivität Arbeitsstation  
Bei diesem Ansatz IT-Benutzer erhalten eine sichere Verwaltungsarbeitsstation aus dem sie alltägliche administrative Funktionen ausführen, können mithilfe von Remoteserver-Verwaltungstools (RSAT) oder RDP-Verbindungen mit Servern innerhalb ihres Bereichs Verantwortung. Wenn IT-Benutzern produktivitätstasks durchführen müssen, können sie auf eine remote-Produktivität Arbeitsstation ausgeführt als virtueller Computer über RDP verbinden. Separate Anmeldeinformationen für jede Arbeitsstation verwendet werden soll, und Steuerelemente wie z. B. Smartcards sollte implementiert werden.  
  
#### <a name="pros"></a>Vorteile  
  
-   Arbeitsstationen für Administratoren und produktionsarbeitsstationen werden getrennt.  
  
-   Mit sicheren Arbeitsstationen für die Verbindung auf produktionsarbeitsstationen IT-Mitarbeiter können eigene Anmeldedaten eingeben und Smartcards, und privilegierte Anmeldeinformationen sind nicht auf dem Computer mit geringerer Sicherheit-Änderungstabellen abgelegt.  
  
#### <a name="cons"></a>Nachteile  
  
-   Implementieren der Lösung erfordert das Entwerfen und Implementierungsarbeiten und stabile Virtualisierungsoptionen.  
  
-   Wenn die physikalische Workstations nicht sicher gespeichert werden, können sie anfällig für Angriffe auf physischer Basis sein, die Hardware oder des Betriebssystems gefährdet und Kommunikation abfangen anfällig machen.  
  
### <a name="implementing-a-single-secure-workstation-with-connections-to-separate-productivity-and-administrative-virtual-machines"></a>Implementieren eine einzelne sichere Arbeitsstation mit Verbindungen mit dem "Produktivität" und "Verwaltung" virtuelle Computer zu trennen.  
Bei diesem Ansatz können Sie IT-Benutzern ausgeben eine einzigen physische Workstation, gesperrt, wie zuvor beschrieben, und für die IT-Benutzer haben keinen privilegierten Zugriff. Sie können Remote Desktop Services-Verbindungen mit virtuellen Computern auf dedizierten Servern bereitstellen, der Bereitstellung von IT-Mitarbeiter mit einem virtuellen Computer, die e-Mail-Adresse und anderer produktivitätsanwendungen ausgeführt wird und einen zweiten virtuellen Computer, der als des Benutzers konfiguriert ist dedizierten administrativen Hosts.  
  
Sie sollten erfordern Smartcard- oder andere mehrstufigen Anmeldung für die virtuellen Computer mithilfe separater Konten als das Konto, das verwendet wird, um auf den physischen Computer anmelden. Nachdem ein IT-Benutzer, die sich auf einen physischen Computer anmeldet, können sie ihre Produktivität Smartcard verwenden, für die Verbindung zu ihren Computer remote Produktivität und ein separates Konto Smartcard zur Verbindung mit ihren Computer für die Remoteverwaltung.  
  
#### <a name="pros"></a>Vorteile  
  
-   IT-Benutzer können eine einzelne physische Arbeitsstation verwenden.  
  
-   Durch eine separate Konten für den virtuellen Hosts, und über Remote Desktop Services-Verbindungen mit den virtuellen Computern werden IT-Benutzer-Anmeldeinformationen nicht im Arbeitsspeicher auf dem lokalen Computer zwischengespeichert.  
  
-   Der physische Host kann so stark wie administrativen Hosts, verringert die Wahrscheinlichkeit, dass eine Kompromittierung des lokalen Computers gesichert werden.  
  
-   In Fällen, in denen des Benutzers, der ein IT-Produktivität-VM oder ihre virtueller Verwaltungscomputer möglicherweise gefährdet ist, kann der virtuelle Computer ganz einfach in einen Zustand "als funktionierend bekannte" zurückgesetzt werden.  
  
-   Wenn der physische Computer gefährdet ist, wird keine privilegierten Anmeldeinformationen werden im Arbeitsspeicher zwischengespeichert werden, und die Verwendung von Smartcards kann verhindern, dass die Gefährdung der Anmeldeinformationen durch tastatureingabeprotokollierung.  
  
#### <a name="cons"></a>Nachteile  
  
-   Implementieren der Lösung erfordert das Entwerfen und Implementierungsarbeiten und stabile Virtualisierungsoptionen.  
  
-   Wenn die physikalische Workstations nicht sicher gespeichert werden, können sie anfällig für Angriffe auf physischer Basis sein, die Hardware oder des Betriebssystems gefährdet und Kommunikation abfangen anfällig machen.  
  
### <a name="implementing-secure-administrative-workstations-and-jump-servers"></a>Implementieren von sicheren Administratorarbeitsstationen und Jump-Server  
Als Alternative zum Sichern von Arbeitsstationen für Administratoren oder in Kombination mit ihnen Sie können sichere jumpserver implementieren, und Administratoren können eine Verbindung herstellen, um die jumpserver, RDP und Smartcards verwenden, um administrative Aufgaben auszuführen.  
  
Jump-Server müssen konfiguriert werden, führen Sie die Remotedesktop-Gateway-Rolle, um ermöglichen es Ihnen, implementieren Sie die Einschränkungen für Verbindungen mit dem sprungbrettserver und zu Zielservern, die von ihm verwaltet werden. Wenn möglich, sollten Sie auch die Hyper-V-Rolle installieren und erstellen [persönliche virtuelle Desktops](https://technet.microsoft.com/library/dd759174.aspx) oder anderen virtuellen Computern pro Benutzer, für Administratoren, die für ihre Aufgaben auf der Jump-Server verwendet.  
  
Ermöglicht Administratoren die virtuellen Computern pro Benutzer auf dem sprungbrettserver, Sie die physischen Sicherheit für die Arbeitsstationen für Administratoren bereitstellen, und Administratoren ihre virtuellen Maschinen bei Nichtverwendung Herunterfahren oder zurücksetzen können. Wenn Sie nicht auf dem gleichen Host für die Verwaltung der Hyper-V-Rolle und der RD-Gateway-Rolle installieren möchten, können Sie sie auf separaten Computern installieren.  
  
Wo immer dies möglich ist, sollte die Remoteserver-Verwaltungstools zum Verwalten von Servern verwendet werden. Die Funktion Remote Server Administration Tools (RSAT) auf virtuellen Maschinen von den Benutzern (oder dem sprungbrettserver, wenn Sie benutzerdefinierte virtuelle Computer für die Verwaltung nicht implementiert werden), installiert werden sollte und Administrationsmitarbeiter sollte eine Verbindung herstellen über RDP-Verbindung mit ihren virtuelle Computer, um administrative Aufgaben auszuführen.  
  
In Fällen, wenn ein Administrator eine Verbindung über RDP auf einen Zielserver für die direkte Verwaltung herstellen muss sollte RD-Gateway konfiguriert sein die Verbindung hergestellt werden, nur dann, wenn der entsprechende Benutzer und Computer, zum Herstellen der Verbindung an das Ziel verwendet werden zulassen Server. Ausführung der Remoteserver-Verwaltungstools (oder ähnlich) Tools verboten werden auf Systemen, die nicht der Management-Systeme festgelegt sind wie allgemeine Arbeitsstationen und Mitgliedsservern, die nicht zu Servern wechseln.  
  
#### <a name="pros"></a>Vorteile  
  
-   Erstellen Jump-Server, können Sie die zum Zuordnen von bestimmten Servern zu "Zones" (Sammlungen von Systemen mit ähnlichen Anforderungen für Konfiguration, Verbindungen und Sicherheit) in Ihrem Netzwerk und anfordern, dass es sich bei die Verwaltung jeder Zone durch Administrationsmitarbeiter erreicht ist Herstellen einer Verbindung von sicheren administrative Hosts auf einem Server festgelegten "Zone".  
  
-   Durch die Zuordnung Jump-Server, Zonen, Sie können präzise Steuerelemente für die Verbindungseigenschaften und konfigurationsanforderungen implementieren und Verbindungen von nicht autorisierten Systeme können ganz einfach ermitteln.  
  
-   Implementieren von pro-Administratoren virtuelle Computer auf jumpserver, zu erzwingen, indem Sie Herunterfahren und der virtuellen Computer auf einen bekannten fehlerfreien Zustand zurücksetzen, wenn administrative Aufgaben abgeschlossen sind. Durch erzwingen Herunterfahren (oder neu starten), der die virtuellen Computer aus, wenn administrative Aufgaben abgeschlossen sind, die virtuellen Computer kann nicht sein Ziel von Angreifern, noch Angriffen mit gestohlenen Anmeldeinformationen möglich sind, da der Arbeitsspeicher zwischengespeicherte Anmeldeinformationen nicht nach einem Neustart beibehalten werden.  
  
#### <a name="cons"></a>Nachteile  
  
-   Dedizierte Server müssen sich für jumpserver, ob physisch oder virtuell.  
  
-   Implementieren die angegebenen Server wechseln und Arbeitsstationen für Administratoren erfordert eine sorgfältige Planung und Konfiguration, die alle Sicherheitszonen, konfiguriert in der Umgebung zugeordnet ist.  
  


