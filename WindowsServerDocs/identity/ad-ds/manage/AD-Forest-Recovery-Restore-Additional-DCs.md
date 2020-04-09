---
title: Wiederherstellung der Active Directory-Gesamtstruktur-erneute Bereitstellung
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: 17e5ceec74277c888232d17adca5c2bbb305af97
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823623"
---
# <a name="ad-forest-recovery---redeploy-remaining-dcs"></a>Wiederherstellung der Active Directory-Gesamtstruktur-erneute Bereitstellung

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Die bis zu diesem Punkt beschriebenen Schritte gelten für alle Gesamtstrukturen: Suchen Sie eine gültige Sicherung für jede Domäne, stellen Sie die Domänen isoliert wieder her, verbinden Sie Sie neu, setzen Sie den globalen Katalog zurück, und bereinigen Sie Sie. Im nächsten Schritt wird die Gesamtstruktur erneut bereitgestellt. Die Vorgehensweise hängt stark von Ihrem Gesamtstruktur Entwurf, ihren Vereinbarungen zum Service Level, der Standortstruktur, der verfügbaren Bandbreite und vielen anderen Faktoren ab. Sie müssen ihren eigenen Plan zur erneuten Bereitstellung basierend auf den Prinzipien und Vorschlägen in diesem Abschnitt entwerfen, was für Ihre geschäftlichen Anforderungen am besten geeignet ist.  
  
Der nächste Schritt besteht darin, AD DS auf allen DCS zu installieren, die vor der Wiederherstellung der Gesamtstruktur vorhanden waren. Wenn die DCS weiterhin vorhanden sind, muss der AD DS Dienst zwangsweise entfernt werden, oder die DCS können neu installiert werden. Alle vorhandenen Sicherungen für diese DCS können nicht wieder verwendet werden, da die entsprechenden Metadaten während der Wiederherstellung der Gesamtstruktur entfernt wurden. In einer unkomplizierten Umgebung kann dieser Prozess der erneuten Bereitstellung so einfach sein wie das erneute Verbinden der wiederhergestellten DCS mit dem Produktionsnetzwerk und das herauf Stufen neuer DCs nach Bedarf.  
  
In einem großen Unternehmen, das mit einer weltweiten Infrastruktur verbunden ist, ist ein anspruchsvolleren Plan erforderlich. Die erste Phase besteht in der Regel darin, den AD als Dienst wiederherzustellen. Dies bedeutet, dass strategisch platzierte DCS so installiert werden, dass alle wichtigen Geschäftsbereiche und Anwendungen wieder funktionieren können. Möglicherweise ist es für Zweigstellen akzeptabel, dass dadurch die Leistung vorübergehend beeinträchtigt wird. In der zweiten Phase werden alle verbleibenden und weniger kritischen DCS erneut bereitgestellt.  
  
 Es gibt zwei Methoden zum Installieren zusätzlicher DCS, die beide automatisiert werden können:  
  
- Klonen  
   - Für virtualisierte Umgebungen, in denen Windows Server 2012 ausgeführt wird, ist das Klonen die schnellste und einfachste Möglichkeit, eine große Anzahl von DCS wiederherzustellen. Nachdem Sie einen einzelnen virtualisierten Domänen Controller aus einer Sicherung wieder hergestellt haben, können Sie die Wiederherstellung aller virtualisierten DCS in einer Domäne automatisieren.  
   - Weitere Informationen zum Klonen und zu den Voraussetzungen finden [Sie unter Introduction to Active Directory Domain Services (AD DS) Virtualization (Stufe 100)](https://technet.microsoft.com/library/hh831734.aspx).  
- Erneutes Installieren von AD DS mithilfe von Windows PowerShell auf Servern mit Windows Server 2012 (oder Dcpromo. exe auf Servern, auf denen frühere Versionen von Windows Server ausgeführt werden) oder über die Benutzeroberfläche  
   - Zum beschleunigen der erneuten Installation von AD DS können Sie die Option Install From Media (IFM) verwenden, um den Replikations Datenverkehr während der Installation zu verringern. Weitere Informationen zum Erstellen von Installationsmedien mithilfe des Befehls **ntdsutil ifm** finden Sie unter [Installieren von AD DS von einem Medium](https://technet.microsoft.com/library/cc770654\(WS.10\).aspx).  

Beachten Sie die folgenden zusätzlichen Punkte für alle Replikat Domänen Controller, die in der Gesamtstruktur durch das Klonen virtualisierter Domänen Controller oder durch die Installation von AD DS wieder hergestellt werden (im Gegensatz zur Wiederherstellung von  
  
- Die gesamte Software auf einem Domänen Controller, die als Quelle für das Klonen verwendet wird, muss geklont werden können. Anwendungen und Dienste, die nicht geklont werden können, sollten entfernt werden, bevor das Klonen initiiert wird. Wenn dies nicht möglich ist, sollte ein alternativer virtualisierter DC als Quelle ausgewählt werden.  
- Wenn Sie zusätzliche virtualisierte DCS von dem ersten virtualisierten Domänen Controller Klonen, der wieder hergestellt werden soll, muss der Quell-DC heruntergefahren werden, während die zugehörige vhdx-Datei kopiert wird. Anschließend muss sie ausgeführt werden und online verfügbar sein, wenn die virtuellen Domänen Controller zum ersten Mal gestartet werden. Wenn die für das Herunterfahren erforderliche Ausfallzeit für den ersten wiederhergestellten DC unzulässig ist, stellen Sie einen zusätzlichen virtualisierten Domänen Controller bereit, indem Sie AD DS installieren, der als Quelle für das Klonen fungiert.  
- Der Hostname des geklonten virtualisierten Domänen Controllers oder der Server, auf dem Sie AD DS installieren möchten, ist nicht eingeschränkt. Sie können einen neuen Hostnamen oder den zuvor verwendeten Hostnamen verwenden. Weitere Informationen zur Syntax des DNS-Host namens finden Sie unter [Erstellen von DNS-Computer Namen](https://technet.microsoft.com/library/cc785282.aspx) ([https://go.microsoft.com/fwlink/?LinkId=74564](https://go.microsoft.com/fwlink/?LinkId=74564)).  
- Konfigurieren Sie jeden Server mit dem ersten DNS-Server in der Gesamtstruktur (dem ersten in der Stamm Domäne wiederhergestellten DC) als bevorzugten DNS-Server in den TCP/IP-Eigenschaften des Netzwerkadapters. Weitere Informationen finden Sie unter [Konfigurieren von TCP/IP für die Verwendung von DNS](https://technet.microsoft.com/library/cc779282.aspx).  
- Stellen Sie alle RODCs in der Domäne erneut bereit, entweder durch das Klonen von virtualisierten Domänen Controllern, wenn mehrere RODCs an einem zentralen Speicherort bereitgestellt werden, oder durch die herkömmliche Methode, Sie neu zu erstellen, indem Sie AD DS entfernen und neu installieren, wenn Sie an isolierten Orten wie Zweigstellen einzeln bereitgestellt werden.  
   - Das Neuerstellen von RODCs stellt sicher, dass Sie keine veralteten Objekte enthalten, und kann dazu beitragen, dass Replikations Konflikte später auftreten. Wenn Sie AD DS von einem RODC entfernen, *Wählen Sie die Option zum Beibehalten von DC-Metadaten*aus. Wenn Sie diese Option verwenden, wird das krbtgt-Konto für den RODC beibehalten und die Berechtigungen für das delegierte RODC-Administrator Konto und das Kennwortreplikationsrichtlinie (PRP) beibehalten, und es wird verhindert, dass Sie Domänen Administrator-Anmelde Informationen verwenden müssen, um AD DS auf einem RODC zu entfernen und neu zu installieren. Außerdem werden die DNS-Server-und globalen Katalog Rollen beibehalten, wenn Sie ursprünglich auf dem RODC installiert sind.  
   - Wenn Sie DCS (RODCs oder beschreibbare DCS) neu erstellen, kann während der erneuten Installation ein erhöhter Replikations Datenverkehr vorhanden sein. Um diese Auswirkungen zu reduzieren, können Sie den Zeitplan der RODC-Installationen Staffeln, und Sie können die Option Install From Media (IFM) verwenden. Wenn Sie die IFM-Option verwenden, führen Sie den Befehl " **ntdsutil ifm** " auf einem beschreibbaren Domänen Controller aus, dem Sie Vertrauen, dass Sie nicht über beschädigte Daten verfügen. Dadurch wird verhindert, dass auf dem RODC mögliche Beschädigungen angezeigt werden, nachdem die AD DS Neuinstallation beendet wurde. Weitere Informationen zu IFM finden Sie unter [Installieren von AD DS von einem Medium](https://technet.microsoft.com/library/cc770654\(WS.10\).aspx).  
   - Weitere Informationen zum Neuerstellen von RODCs finden Sie unter [RODC-Entfernung und-Neuinstallation](https://technet.microsoft.com/library/cc835490\(WS.10\).aspx).  
- Wenn ein Domänen Controller den DNS-Server Dienst vor der Gesamtstruktur Fehler ausgeführt hat, installieren und konfigurieren Sie den DNS-Server Dienst während der Installation von AD DS. Andernfalls konfigurieren Sie die früheren DNS-Clients mit anderen DNS-Servern.  
- Wenn Sie zusätzliche globale Kataloge benötigen, um die Authentifizierung oder die Abfrage Last für Benutzer oder Anwendungen freizugeben, können Sie den globalen Katalog vor dem Klonen dem virtualisierten Quell-Domänen Controller hinzufügen, oder Sie können während der Installation von AD DS einen Domänen Controller als globalen Katalogserver erstellen.  
  
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
