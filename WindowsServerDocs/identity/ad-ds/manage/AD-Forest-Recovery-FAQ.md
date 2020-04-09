---
title: Wiederherstellung der AD-Gesamtstruktur - häufig gestellte Fragen
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: ac9e5a3d-8b1e-41b7-8e02-f64b7acf1359
ms.technology: identity-adds
ms.openlocfilehash: f32111cf7cc81f8f49b7b1058cc1a0ccc780da7f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80824003"
---
# <a name="ad-forest-recovery---faq"></a>Wiederherstellung der AD-Gesamtstruktur - häufig gestellte Fragen

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2, Windows Server 2003

Dieses Dokument enthält häufig gestellte Fragen (FAQs) bezüglich der Wiederherstellung der Gesamtstruktur:  

## <a name="general-recovery"></a>Allgemeine Wiederherstellung

**F: Was kann ich tun, um die Wiederherstellung zu beschleunigen?**

Obwohl die Geschwindigkeit der Wiederherstellung nicht das Hauptziel dieses Handbuchs ist, können Sie kürzere Wiederherstellungszeiten erzielen, indem Sie folgende Schritte ausführen:  
  
- Erstellen eines detaillierten Wiederherstellungs Plans für die Gesamtstruktur, regelmäßiges Aktualisieren und testen in einer simulierten Testumgebung mit angemessener Größe mindestens einmal pro Jahr  
- Verwenden des Klonens von virtualisierten Domänen Controllern (DC)  
   - Virtualisierte Domänen Controller Klonen beschleunigt den Prozess, um zusätzliche DCS zu erhalten, die nach der Wiederherstellung eines Domänen Controllers aus einer Sicherung in jeder Domäne ausgeführt werden Die zusätzlichen virtualisierten DCS können geklont werden, anstatt darauf zu warten, dass möglicherweise lange AD DS Installationen abgeschlossen werden, und für den Abschluss der nicht kritischen Replikation nach der Installation.  
   - Gesamtstrukturen, in denen virtuelle DCS in einer relativ kleinen Anzahl von gut verbundenen Rechenzentren gehostet werden, profitieren möglicherweise von dem Klonen während der Wiederherstellung. Jede Umgebung, in der sich mehrere virtualisierte DCS für dieselbe Domäne auf demselben Hypervisor-Host befinden, sollte jedoch von Vorteil sein.  
- Bereitstellen von schreibgeschützten Domänen Controllern (RODCs)  
   - RODCs können während des Wiederherstellungsprozesses Geschäftskontinuität bereitstellen, da Sie nicht vom Netzwerk getrennt werden müssen, da beschreibbare DCS dies tun. RODCs führen keine ausgehende Replikation aus. Daher stellen Sie nicht dasselbe Risiko dar, dass beschreibbare DCS zum Replizieren schädlicher Daten in der wiederhergestellten Umgebung darstellen.  
  
Weitere Faktoren, die sich auf die Dauer des Wiederherstellungsprozesses der Gesamtstruktur auswirken, sind folgende:  
  
- Wenn Sie DCS aus Sicherungen wiederherstellen, dauert Folgendes:  
   - Suchen Sie das physische Sicherungsmedium, z. b. Bänder.  
   - Installieren Sie das Betriebssystem neu.  
   - Stellen Sie Daten von einem Sicherungsmedium wieder her.  
      - Sie können die erforderliche Zeit für die Neuinstallation des Betriebssystems und die Wiederherstellung von Daten aus einer Sicherung verringern, indem Sie anstelle der Systemstatus Wiederherstellung eine vollständige Server Wiederherstellung ausführen Da die vollständige Server Wiederherstellung Binär basiert ist, wird Sie wesentlich schneller abgeschlossen als die Systemstatus Wiederherstellung.  
      - Wenn der Server jedoch Daten enthält, die von Systemstatus Daten ausgeschlossen sind, die Sie nicht wiederherstellen möchten, ist die vollständige Server Wiederherstellung möglicherweise keine geeignete Alternative zur Wiederherstellung des Systemstatus. Berücksichtigen Sie die Vorteile der vollständigen Server Wiederherstellung anstelle einer Systemstatus Wiederherstellung für Ihre Server, und bereiten Sie sich entsprechend vor, indem Sie den entsprechenden Sicherungstyp ausführen, den Sie später wiederherstellen möchten.  
- Wenn Sie DCS neu erstellen, dauert es Zeit, Daten für netzwerkbasierte herauf stufungen zu replizieren.  
   - Sie können die erforderliche Zeit für die Wiederherstellung von DCS verringern, indem Sie die folgenden Schritte ausführen:  
- Verkürzen Sie die Zeit für das Abrufen von Sicherungsmedien durch:  
   - Verwenden Sie das Active Directory Daten Bank Bereitstellungs Tool (Dsamain. exe), um die beste Sicherung für Wiederherstellungs Vorgänge zu ermitteln. Weitere Informationen zur Verwendung des Active Directory-Daten Bank Bereitstellungs Tools finden Sie in der [schrittweisen Anleitung zum Active Directory-Daten Bank](https://go.microsoft.com/fwlink/?LinkId=132577) Bereitstellungs Tool (https://go.microsoft.com/fwlink/?LinkId=132577).  
   - Sie können die Sicherungsmedien eindeutig bezeichnen und die Medien an einem geeigneten, aber sicheren Speicherort speichern, der einen schnellen Abruf ermöglicht.  
   - Verwenden der Volumeschattenkopie-Dienst mit einer Storage Area Network (San), um Sicherungen von unterschiedlichen Zeitpunkten zu verwalten. Weitere Informationen finden Sie unter [Windows Server 2003 Active Directory Fast Recovery with Volumeschattenkopie-Dienst und Virtual Disk Service](https://go.microsoft.com/fwlink/?LinkId=70781) (https://go.microsoft.com/fwlink/?LinkId=70781).  
- Erzwingen Sie das Entfernen von AD DS aus den DCS, anstatt das Betriebssystem neu zu installieren. Wenn die Ursache für den Gesamtstruktur weiten Ausfall allein innerhalb des Bereichs von AD DS erkannt wurde, müssen Sie das Betriebssystem auf den DCS nicht neu installieren.  
   - Weitere Informationen zum Erzwingen der Entfernung von AD DS von einem Domänen Controller, auf dem Windows Server 2008 oder höher ausgeführt wird, finden Sie unter [Erzwingen des Entfernens eines Windows Server 2008-Domänen Controllers](https://go.microsoft.com/fwlink/?LinkId=132627) (https://go.microsoft.com/fwlink/?LinkId=132627). Weitere Informationen zum Erzwingen der Entfernung von AD DS von einem Domänen Controller, auf dem Windows Server 2003 ausgeführt wird, finden Sie im [Artikel 332199](https://go.microsoft.com/fwlink/?LinkId=70780) der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=70780).  
- Verwenden Sie schnellere Bandgeräte oder Datenträger Sicherungen, um die Zeit zu verkürzen, die für Wiederherstellungs Vorgänge erforderlich ist.  
  
Sie können AD DS Installationen auch beschleunigen, indem Sie die Funktion "Install From Media" (IFM) zum erneuten Erstellen von DCS in jeder Domäne verwenden. IFM reduziert die Replikations Wartezeit, die beim erneuten Erstellen von DCS in den einzelnen Domänen auftritt.  
  
Unternehmen mit einer aggressiveren Vereinbarung zum Service Level (SLA) können die Wiederherstellungsverfahren für die Gesamtstruktur ändern, um die Wiederherstellung zu beschleunigen.  
  
**F: kann ich den Wiederherstellungsprozess für die Gesamtstruktur automatisieren?**

Aufgrund der komplexen und kritischen Natur des Wiederherstellungsprozesses der Gesamtstruktur gibt es zurzeit keine End-to-End-Automatisierung. Der Wiederherstellungsprozess der Gesamtstruktur ist eher eine logistische und organisatorische Herausforderung bei der Wiederherstellung der Geschäftskontinuität als ein technisches Problem bei der Prozessautomatisierung. Aus diesem Grund sollte die Person, die die Umgebung verwaltet, einen Wiederherstellungs Plan für die Gesamtstruktur erstellen, der für diese Umgebung spezifisch ist, und dann Abschnitte davon automatisieren, die erfolgreich automatisiert werden können.  
  
Mithilfe der Befehlszeilen Tools können Sie den größten Teil der Wiederherstellungsschritte in der Gesamtstruktur ausführen. Daher sind die meisten Schritte skriptfähig. Beispielsweise ist "Ntdsutil. exe" eines der am häufigsten verwendeten Tools im Wiederherstellungsprozess der Gesamtstruktur.  
  
Obwohl Skripts die Wiederherstellung beschleunigen können, müssen Sie diese Skripts gründlich testen, bevor Sie Sie in einer realen Umgebung anwenden. Außerdem müssen Sie diese gemäß den Änderungen in der Active Directory Umgebung aktualisieren, z. b. durch Hinzufügen einer neuen Domäne oder eines Domänen Controllers oder durch eine neue Version von Active Directory.

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Voraussetzungen](AD-Forest-Recovery-Prerequisties.md)  
- [AD-Gesamtstruktur Wiederherstellung: Entwerfen eines benutzerdefinierten Wiederherstellungs Plans](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD-Gesamtstruktur Wiederherstellung: Identifizieren des Problems](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD-Gesamtstruktur Wiederherstellung: Bestimmen der Wiederherstellung](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD-Gesamtstruktur Wiederherstellung: Ausführen der ersten Wiederherstellung](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)  
- [AD-Gesamtstruktur Wiederherstellung: häufig gestellte Fragen](AD-Forest-Recovery-FAQ.md)  
- [Wiederherstellung der AD-Gesamtstruktur: Wiederherstellen einer einzelnen Domäne innerhalb einer Gesamtstruktur mit mehreren](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [Active Directory-Gesamtstruktur Wiederherstellung mit Windows Server 2003-Domänen Controllern](AD-Forest-Recovery-Windows-Server-2003.md)  
