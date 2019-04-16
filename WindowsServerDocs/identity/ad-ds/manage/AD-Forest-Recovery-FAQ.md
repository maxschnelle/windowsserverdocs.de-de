---
title: "Wiederherstellung der Active Directory-Gesamtstruktur - häufig gestellte Fragen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: ac9e5a3d-8b1e-41b7-8e02-f64b7acf1359
ms.technology: identity-adfs
ms.openlocfilehash: 839e01c88b7ced22501154d8752c6c71cc52b696
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---faq"></a>Wiederherstellung der Active Directory-Gesamtstruktur - häufig gestellte Fragen

>Gilt für: Windows Server 2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2, Windows Server 2003

Dieses Dokument enthält häufig gestellte Fragen (FAQs) zur Wiederherstellung der Gesamtstruktur:  
 
## <a name="general-recovery"></a>Allgemeine Wiederherstellung
  
 
**F: Was kann ich tun, um schnellere Wiederherstellung?** 
 
Geschwindigkeit der Wiederherstellung ist, zwar nicht das Hauptziel dieser Anleitung erreichen Sie kürzere Wiederherstellungszeiten durch:  
  
-   Erstellen einen Wiederherstellungsplan detaillierte Gesamtstruktur, in regelmäßigen Abständen aktualisiert, und üben es in einer simulierten Umgebung angemessene Größe mindestens einmal im Jahr  
  
-   Mithilfe von Klonen virtualisierter Domänencontroller (DC)  
  
     Virtualisierte Domänencontroller Klonen beschleunigt den Prozess zum Abrufen zusätzlicher Domänencontroller ausgeführt wird, nachdem ein Domänencontroller aus einer Sicherung in jeder Domäne wiederhergestellt wird. Der zusätzliche virtualisierte Domänencontroller können anstatt zu warten, bis potenziell langwierige AD DS-Installationen zu abgeschlossen werden und für den Abschluss der nicht kritische Replikation nach der Installation geklont werden.  
  
     Gesamtstrukturen, in denen virtuelle Domänencontroller potenziell in eine relativ kleine Anzahl von schnellen Datencentern gehostet werden, profitieren am meisten von Klonen während der Wiederherstellung. Profitieren sollten jedoch die jeder Umgebung, in denen mehrere virtualisierte Domänencontroller für dieselbe Domäne auf demselben hypervisorhost zusammengestellt werden.  
  
-   Bereitstellen von schreibgeschützten Domänencontrollern (RODCs)  
  
     RODCs können während der Wiederherstellung Geschäftskontinuität bereitstellen, da sie nicht vom Netzwerk getrennt werden, wie beschreibbaren Domänencontroller verfügen. RODCs führen Sie die ausgehende Replikation nicht. Daher werden sie nicht demselben Risiko stellen, das beschreibbaren Domänencontroller für die Replikation von schädliche Daten zurück in die wiederhergestellten Umgebung darstellen.  
  
 Andere Faktoren, die die Dauer des Wiederherstellungsprozesses Gesamtstruktur auswirken, umfassen Folgendes:  
  
-   Wenn Sie Domänencontroller aus Sicherungen wiederherstellen, dauert es, bis:  
  
    -   Suchen Sie nach dem physischen Sicherungsmedium, z.B. Bänder.  
  
    -   Installieren Sie das Betriebssystem neu.  
  
    -   Stellen Sie Daten von einem Sicherungsmedium wieder her.  
  
     Sie können den Zeitaufwand für das Betriebssystem neu installieren und Wiederherstellen von Daten aus einer Sicherung durch Ausführen der vollständigen Wiederherstellung anstelle der Wiederherstellung des Systemstatus reduzieren. Da der vollständigen Wiederherstellung Binärdatei-basiert ist, ist es sehr viel schneller als die Wiederherstellung des Systemstatus abgeschlossen.  
  
     Jedoch, wenn der Server Daten, die von Systemstatusdaten ausgeschlossen wird, die nicht wiederhergestellt werden sollen enthält, vollständige Wiederherstellung des Servers eine gute Alternative zur Wiederherstellung des Systemstatus möglicherweise nicht. Berücksichtigen Sie die Vorteile eine vollständigen Wiederherstellung anstatt eine Wiederherstellung des Systemstatus speziell für Ihren Servern ausgeführt, und bereiten Sie entsprechend durch Ausführen des richtigen Typs Sicherung, die Sie später wiederherstellen möchten.  
  
-   Wenn Sie Domänencontroller neu erstellen, dauert es Zeit, Daten für eine netzwerkbasierte Aktionen zu replizieren.  
  
 Sie können verringern, dass den Zeitaufwand für die Wiederherstellung der Domänencontroller anhand der folgenden Schritte:  
  
-   Verkürzen Sie die Zeit für das Abrufen von Sicherungsmedien durch:  
  
    -   Verwenden die Active Directory-Datenbank bereitstellen Tool (Dsamain.exe) Wiederherstellungsvorgänge mit der besten Sicherung zu identifizieren. Weitere Informationen zur Verwendung von Active Directory-Datenbank bereitstellen Tool finden Sie unter der [Active Directory-Datenbank bereitstellen Tool Step-by-Step Handbuch](https://go.microsoft.com/fwlink/?LinkId=132577) (https://go.microsoft.com/fwlink/?LinkId=132577).  
  
    -   Beschriftung der Sicherungsmedien klar und speichern das Medium organisierten an einem benutzerfreundlichen, noch sicherer, Speicherort, der schnelles abrufen kann.  
  
    -   Bei Verwendung der Volumeschattenkopie-Dienst mit einem Storage Area Network (SAN) Sicherungen von verschiedenen Punkten in Zeit beibehalten. Weitere Informationen finden Sie unter [Windows Server2003 Active Directory schnelle Wiederherstellung mit dem Volumeschattenkopie-Dienst und Virtual Disk Service](https://go.microsoft.com/fwlink/?LinkId=70781) (https://go.microsoft.com/fwlink/?LinkId=70781).  
  
-   Erzwingen Sie Entfernen von AD DS von den Domänencontrollern anstelle einer Neuinstallation des Betriebssystems. Wenn die Ursache des Fehlers Gesamtstruktur werden nur innerhalb des Bereichs von AD DS ermittelt wurde, müssen Sie nicht auf den Domänencontrollern das Betriebssystem neu installieren.  
  
     Weitere Informationen zu erzwingen des Entfernens von AD DS von einem Domänencontroller, der Windows Server 2008 oder höher ausgeführt wird, finden Sie unter [Erzwingen des Entfernens von einem Windows Server2008-Domänencontroller](https://go.microsoft.com/fwlink/?LinkId=132627) (https://go.microsoft.com/fwlink/?LinkId=132627). Weitere Informationen zu erzwingen des Entfernens von AD DS von einem Domänencontroller, der Windows Server2003 ausgeführt wird, finden Sie unter [Artikel 332199](https://go.microsoft.com/fwlink/?LinkId=70780) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=70780).  
  
-   Schnellere Bandmedien verwenden oder Wiederherstellungsvorgänge Sicherungen auf Datenträger die Zeit verringern, die erforderlich ist.  
  
 Darüber hinaus können AD DS-Installationen mithilfe von Install from Media (IFM) Feature Domänencontroller in jeder Domäne neu erstellt und beschleunigen. IFM reduziert die Replikationswartezeit, die erforderlich ist, wenn Sie Domänencontroller in jeder Domäne neu erstellen.  
  
 Unternehmen, die eine aggressivere Vereinbarung zum Servicelevel (SLA) haben sollten, ändern die Wiederherstellungsschritte Gesamtstruktur zur schnelleren Wiederherstellung.  
  

**F: Automatisieren kann ich die Gesamtstruktur-Recovery-Vorgang?**  
 Aufgrund der Bedeutung der Natur des Wiederherstellungsprozesses Gesamtstruktur können besteht zurzeit keine End-to-End-Automatisierung des. Der Wiederherstellungsvorgang für die Gesamtstruktur ist mehr eine Herausforderung logistische und Organisation der Wiederherstellung der Geschäftskontinuität als eines technischen Problems der Automatisierung. Daher sollte die Person, die die Umgebung verwaltet erstellen Sie einen Gesamtstruktur-Wiederherstellungsplan, der in dieser Umgebung gelten und Bereiche, die erfolgreich automatisiert werden können dann automatisieren.  
  
 Sie können die meisten Schrittezur Wiederherstellung der Gesamtstruktur mithilfe von Befehlszeilentools ausführen. Aus diesem Grund sind die meisten Schritteskriptfähig. Beispielsweise ist Ntdsutil.exe eines der am häufigsten verwendeten Tools in der Gesamtstruktur Recovery-Vorgang.  
  
 Auch Skripts Wiederherstellung zu beschleunigen können, müssen Sie diese Skripts gründlich testen, bevor Sie sie in einer echten Umgebung anwenden. Darüber hinaus müssen Sie diese entsprechend den Änderungen in Active Directory-Umgebung, z.B. das Hinzufügen einer neuen Domäne oder ein Domänencontroller oder eine neue Version des Active Directory aktualisieren.

## <a name="next-steps"></a>Nächste Schritte
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
-   [Wiederherstellung des AD-Gesamtstruktur - Konzipierung einen Wiederherstellungsplan benutzerdefinierte Gesamtstruktur](AD-Forest-Recovery-Devising-a-Plan.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - identifizieren](AD-Forest-Recovery-Identify-the-Problem.md)
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Bestimmen der Vorgehensweise beim Wiederherstellen](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [Wiederherstellung der Active Directory-Gesamtstruktur - führen Sie erste wiederherstellen](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)  
-   [AD-Gesamtstruktur-Wiederherstellung – häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
-   [Wiederherstellung des AD-Gesamtstruktur - Wiederherstellung von einer einzelnen Domäne innerhalb einer Gesamtstruktur Multidomain](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [Wiederherstellung der Active Directory-Gesamtstruktur - Wiederherstellung der Gesamtstruktur mit Windows Server2003-Domänencontroller](AD-Forest-Recovery-Windows-Server-2003.md)  
