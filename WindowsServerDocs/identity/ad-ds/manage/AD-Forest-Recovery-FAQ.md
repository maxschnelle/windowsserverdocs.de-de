---
title: Wiederherstellung der AD-Gesamtstruktur - häufig gestellte Fragen
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: ac9e5a3d-8b1e-41b7-8e02-f64b7acf1359
ms.technology: identity-adds
ms.openlocfilehash: 36c9560b490cc28f006770c869bdcdf2b152dd74
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878451"
---
# <a name="ad-forest-recovery---faq"></a>Wiederherstellung der AD-Gesamtstruktur - häufig gestellte Fragen

>Gilt für: WindowsServer 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2, WindowsServer 2003

Dieses Dokument enthält häufig gestellte Fragen (FAQs) zur Wiederherstellung der Gesamtstruktur:  

## <a name="general-recovery"></a>Allgemeine-Wiederherstellung

**F: Was kann ich tun, um eine schnellere Wiederherstellung?**

Obwohl die Geschwindigkeit der Wiederherstellung nicht der primäre Zweck dieses Handbuchs ist, erzielen Sie kürzere Wiederherstellungszeiten von:  
  
- Erstellen eines Wiederherstellungsplans ausführliche Gesamtstruktur, in regelmäßigen Abständen aktualisieren und eignen, die sie in einer simulierten Umgebung angemessene Größe mindestens einmal im Jahr  
- Verwenden von Klonen virtualisierter Domänencontroller (DC)  
   - Klonen von virtualisierten Domänencontroller beschleunigt den Prozess zum Abrufen der zusätzliche Domänencontroller ausführen, nachdem ein DC aus einer Sicherung in jeder Domäne wiederhergestellt wird. Die zusätzliche virtualisierte Domänencontroller können geklont werden, statt zu warten für möglicherweise langwierigen AD DS-Installation und den Abschluss der nicht kritische Replikation nach der Installation.  
   - Gesamtstrukturen, in denen virtuelle DCs potenziell in eine relativ kleine Anzahl von gut verbundenen Rechenzentren gehostet werden, profitieren am meisten von Klonen, während der Wiederherstellung. Allerdings muss jeder Umgebung, in denen mehrere virtualisierte Domänencontroller für dieselbe Domäne auf demselben hypervisorhost zusammengestellt werden, profitieren.  
- Bereitstellen von schreibgeschützten Domänencontrollern (RODCs)  
   - RODCs bieten Geschäftskontinuität während der Wiederherstellung, da sie nicht vom Netzwerk getrennt werden, wie beschreibbare DCs verfügen. RODCs führen keine ausgehende Replikation aus. Aus diesem Grund sind sie nicht das gleiche Risiko stellen, das beschreibbaren DCs zum Replizieren von schädlichen Daten wieder in die wiederhergestellte Umgebung darstellen.  
  
Die folgenden: anderen Faktoren, die die Dauer des Wiederherstellungsprozesses Gesamtstruktur auswirken  
  
- Wenn Sie Domänencontroller aus Sicherungen wiederherstellen, dauert die Zeit:  
   - Suchen Sie das physische Sicherungsmedium, z. B. Bänder an.  
   - Installieren Sie das Betriebssystem neu.  
   - Stellen Sie Daten von einem Sicherungsmedium wieder her.  
      - Sie können den Zeitaufwand für das Betriebssystem neu installieren und Wiederherstellen von Daten aus einer Sicherung durch Ausführen von vollständigen serverwiederherstellung anstelle der Wiederherstellung des Systemstatus reduzieren. Da binäre vollständige Wiederherstellung des Servers ist, wird es viel schneller als die Wiederherstellung des Systemstatus abgeschlossen.  
      - Aber wenn der Server Daten, die von Systemstatusdaten ausgeschlossen wird, die nicht enthält wiederhergestellt werden sollen, vollständigen serverwiederherstellung eine durchführbare Alternative zur Wiederherstellung des Systemstatus möglicherweise nicht. Berücksichtigen Sie die Vorteile der Ausführung einer vollständigen Wiederherstellungs statt eine Wiederherstellung des Systemstatus für Ihre Server insbesondere und entsprechend vorbereiten anhand von den entsprechenden Typ der Sicherung, die Sie später wiederherstellen möchten.  
- Wenn Sie den Domänencontroller neu erstellen, dauert die Zeit zum Replizieren von Daten für die Netzwerk-basierte heraufstufungen.  
   - Sie können die erforderliche Zeit für die Wiederherstellung von DCs durch den folgenden Schritten verringern:  
- Verkürzt die zum Abrufen von Sicherungsmedien durch:  
   - Verwenden das Tool Active Directory-Datenbank bereitstellen (Dsamain.exe) zum Identifizieren der besten Sicherung für Wiederherstellungsvorgänge. Weitere Informationen zur Verwendung des Active Directory-Datenbank bereitstellen kennen, finden Sie die [zum Active Directory-Datenbank bereitstellen Tool schrittweise](https://go.microsoft.com/fwlink/?LinkId=132577) (https://go.microsoft.com/fwlink/?LinkId=132577).  
   - Das Sicherungsmedium folglich eindeutig zu bezeichnen, und speichern die Medien in einer strukturierten Weise an eine praktische, noch sicherer, Speicherort, der schnelle abrufen kann.  
   - Verwenden den Volumeschattenkopie-Dienst mit einem Storage Area Network (SAN), um Sicherungen von verschiedenen Punkten in der Zeit zu verwalten. Weitere Informationen finden Sie unter [Windows Server 2003 schnelle Wiederherstellung der Active Directory mit Volumeschattenkopie-Dienst und der Dienst für virtuelle Datenträger](https://go.microsoft.com/fwlink/?LinkId=70781) (https://go.microsoft.com/fwlink/?LinkId=70781).  
- Erzwingen, dass das Entfernen von AD DS von den DCs anstelle einer Neuinstallation des Betriebssystems. Wenn die Ursache des Fehlers eine gesamtstrukturweite identifiziert wurde, um ausschließlich innerhalb des Bereichs von AD DS sein, müssen Sie nicht das Betriebssystem neu installieren, auf den DCs.  
   - Weitere Informationen zum Erzwingen von des Entfernens von AD DS von einem Domänencontroller, die WindowsServer 2008 oder höher ausgeführt wird, finden Sie unter [Erzwingen des Entfernens von einem Windows Server 2008-Domänencontroller](https://go.microsoft.com/fwlink/?LinkId=132627) (https://go.microsoft.com/fwlink/?LinkId=132627). Weitere Informationen zum Erzwingen von des Entfernens von AD DS von einem Domänencontroller, die Windows Server 2003 ausgeführt wird, finden Sie unter [Artikel 332199](https://go.microsoft.com/fwlink/?LinkId=70780) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=70780).  
- Verwenden Sie schnellere Bandmedien, oder Wiederherstellungsvorgängen für datenträgersicherungen Reduzierung die Zeit, die für erforderlich ist.  
  
Darüber hinaus können AD DS-Installationen zu beschleunigen, indem Sie mithilfe von Install from Media (IFM) Funktion DCs in jeder Domäne neu zu erstellen. IFM reduziert die Replikationswartezeit, die anfallen, wenn Sie DCs in jeder Domäne neu erstellen.  
  
Unternehmen, die eine aggressivere Vereinbarung zum Servicelevel (SLA) sollten in Betracht ziehen, ändern die Prozeduren zur schnelleren Wiederherstellung.  
  
**F: Kann ich die Gesamtstruktur Recovery automatisieren?**

Aufgrund der komplexen und kritischen des Wiederherstellungsprozesses Gesamtstruktur gibt es derzeit keine End-to-End-Automatisierung des Zertifikats. Der Wiederherstellungsprozess Gesamtstruktur ist mehr eine logistische und organisatorische Herausforderung der Wiederherstellung der Geschäftskontinuität als ein technisches Problem prozessautomatisierung. Aus diesem Grund sollte die Person, die die Umgebung verwaltet Erstellen eines Wiederherstellungsplans für Gesamtstrukturen, das für diese Umgebung spezifisch sind und dann automatisieren Abschnitte des Zertifikats, die erfolgreich automatisiert werden kann.  
  
Sie können die meisten Schritte zur Wiederherstellung der Gesamtstruktur mithilfe von Befehlszeilentools ausführen. Aus diesem Grund sind die meisten Schritte skriptfähig. Beispielsweise ist eines der am häufigsten verwendeten Tools in der Gesamtstruktur-Wiederherstellungsprozess, Ntdsutil.exe.  
  
Obwohl Skripts Wiederherstellung beschleunigt werden können, müssen Sie diese Skripts gründlich testen, bevor Sie sie in der Praxis anwenden. Darüber hinaus müssen Sie sie entsprechend den Änderungen in Active Directory-Umgebung, z. B. das Hinzufügen einer neuen Domäne oder der Domänencontroller oder eine neue Version des Active Directory aktualisieren.

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der Gesamtstruktur der Active Directory - Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - Ausarbeiten eines Wiederherstellungsplans für die benutzerdefinierte Gesamtstruktur](AD-Forest-Recovery-Devising-a-Plan.md)  
- [Wiederherstellung der Gesamtstruktur des Active Directory - Ermittlung des Problems](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD-Gesamtstruktur-Wiederherstellung: Bestimmen der Vorgehensweise beim Wiederherstellen](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - erste Wiederherstellung ausführen](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur – häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
- [AD-Gesamtstruktur-Wiederherstellung: Wiederherstellen einer einzelnen Domäne innerhalb einer Gesamtstruktur Multidomain](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [Wiederherstellung der Active Directory-Gesamtstruktur - Wiederherstellung der Gesamtstruktur mit Windows Server 2003-Domänencontrollern](AD-Forest-Recovery-Windows-Server-2003.md)  
