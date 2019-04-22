---
title: Wiederherstellung der AD-Gesamtstruktur - erneut bereitstellen, die verbleibenden DCs
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: af9ec02a480b35e573edebcdd5928451174b6c1d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812001"
---
# <a name="ad-forest-recovery---redeploy-remaining-dcs"></a>Wiederherstellung der AD-Gesamtstruktur - erneut bereitstellen, die verbleibenden DCs

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Die Schritte bis zu diesem Zeitpunkt gelten für alle Gesamtstrukturen: finden Sie eine gültige Sicherung für jede Domäne, die Domänen in Isolation wiederherstellen, schließen Sie sie wieder, der globale Katalog zurückgesetzt und bereinigen. Im nächsten Schritt werden Sie die Gesamtstruktur bereitstellen. Die Möglichkeit hierzu hängt beim Entwurf Ihrer Gesamtstruktur, Ihre Vereinbarungen zum Servicelevel, Websitestruktur, verfügbare Bandbreite und zahlreiche andere Faktoren erheblich ab. Sie benötigen, Entwerfen Ihre eigenen für die erneute Bereitstellung planen, die auf Basis der Prinzipien und Vorschläge in diesem Abschnitt, in einer Weise, die Ihre geschäftsanforderungen am besten geeignet ist.  
  
Der nächste Schritt ist zum Installieren von AD DS auf allen Domänencontrollern, die vorhanden waren, bevor die Wiederherstellung der Gesamtstruktur stattgefunden hat, waren. Wenn die DCs immer noch vorhanden ist, der AD DS-Dienst zwangsweise entfernt werden müssen, oder die DCs neu installiert werden können. Alle vorhandenen Sicherungen für diese Domänencontroller können nicht wiederverwendet werden, da die entsprechenden Metadaten während der Wiederherstellung der Gesamtstruktur entfernt wurde. In einer unkomplizierten Umgebung kann diesen Prozess für die erneute Bereitstellung so einfach wie das Wiederherstellen der Verbindung wiederhergestellten Domänencontroller zum Produktionsnetzwerk sowie das Heraufstufen von neuer DCs nach Bedarf sein.  
  
In einem großen Unternehmen, die mit einer weltweiten Infrastrukturfunktionen konfrontiert wird ist ein komplexer Plan erforderlich. Die erste Phase ist in der Regel um die Anzeige als Dienst wiederherzustellen; Dies bedeutet, installieren strategisch platziert DCs, dass alle kritischen Geschäftsbereiche und Anwendungen erneut mit der Arbeit beginnen können. Es kann für Filialen vorübergehend die Leistung dadurch geringer sein. Als einer Sekunde werden alle verbleibenden Phase und weniger wichtige Domänencontroller erneut bereitgestellt.  
  
 Es gibt zwei Methoden, um zusätzliche Domänencontroller, installieren Sie beide automatisiert werden können:  
  
- Klonen  
   - Beim Klonen für virtualisierte Umgebungen, auf denen Windows Server 2012 ausgeführt wird, ist die schnellste und einfachste Möglichkeit, eine große Anzahl von Domänencontrollern wiederhergestellt. Nachdem Sie einen einzelnen virtualisierte Domänencontroller aus einer Sicherung wiederhergestellt haben, können Sie die Wiederherstellung alle virtualisierten Domänencontroller in einer Domäne automatisieren.  
   - Weitere Informationen zu klonen und Voraussetzungen finden Sie unter [Einführung in die Active Directory Domain Services (AD DS) Virtualization (Level 100)](https://technet.microsoft.com/library/hh831734.aspx).  
- Erneutes Installieren von AD DS mithilfe von Windows PowerShell auf Servern mit Windows Server 2012 (oder Dcpromo.exe auf Servern mit früheren Versionen von Windows Server) oder über die Benutzeroberfläche  
   - Zum Beschleunigen der erneuten Installation von AD DS können Installieren von Medium (IFM)-Option Sie zum Reduzieren des Replikationsdatenverkehrs während der Installation. Weitere Informationen zur Verwendung der **Ntdsutil Ifm** Befehl zum Erstellen eines Installationsmediums finden Sie unter [Installieren von AD DS von einem Medium](https://technet.microsoft.com/library/cc770654\(WS.10\).aspx).  

Beachten Sie die folgenden weiteren Punkte für jedes Replikat-DC, der in der Gesamtstruktur durch Klonen von virtualisierten Domänencontroller oder nach der Installation von AD DS (im Gegensatz zur Wiederherstellung aus einer Sicherung) wiederhergestellt wird:  
  
- Die gesamte Software auf einem Domänencontroller, die als Quelle verwendet wird, für das Klonen geklont werden kann. Vor dem Klonen gestartet wird, sollten Anwendungen und Dienste, die geklont werden, können nicht entfernt werden. Wenn dies nicht möglich ist, sollte ein alternatives virtualisierten Domänencontrollers als Quelle ausgewählt werden.  
- Wenn Sie zusätzliche virtualisierte Domänencontroller von den ersten virtualisierten Domänencontroller wiederhergestellt werden klonen, müssen der Quell-DC Herunterfahren, während die VHDX-Datei kopiert wird. Es müssen ausgeführt werden und verfügbar online sein, wenn das Klonen virtueller Domänencontroller werden zuerst gestartet. Ist die Ausfallzeit erforderlich, die für das Herunterfahren nicht zulässig, für den ersten wiederhergestellten DC, Bereitstellen eines zusätzlichen virtualisierten Domänencontrollers Installation von AD DS, das als Quelle zum Klonen fungiert.  
- Es gibt keine Einschränkung für den Hostnamen des geklonten virtualisierten Domänencontrollers oder dem Server, auf dem zum Installieren von AD DS werden sollen. Sie können einen neuen Hostnamen oder den Hostnamen, der zuvor verwendet wurde. Weitere Informationen zu DNS-Host die Syntax, finden Sie unter [Erstellen von DNS-Computernamen](https://technet.microsoft.com/library/cc785282.aspx) ([https://go.microsoft.com/fwlink/?LinkId=74564](https://go.microsoft.com/fwlink/?LinkId=74564)).  
- Konfigurieren Sie jeden Server mit der ersten DNS-Server in der Gesamtstruktur (des ersten Domänencontrollers, die in der Stammdomäne wiederhergestellt wurde) als bevorzugten DNS-Server in den TCP/IP-Eigenschaften des Netzwerkadapters an. Weitere Informationen finden Sie unter [Konfigurieren von TCP/IP, DNS zu verwenden](https://technet.microsoft.com/library/cc779282.aspx).  
- Alle RODCs in der Domäne erneut bereitstellen, entweder durch virtualisierte Domänencontroller klonen, wenn mehrere RODCs an einem zentralen Ort bereitgestellt werden oder durch die herkömmliche Methode der Neuerstellung werden durch das Entfernen und Neuinstallieren von AD DS, wenn sie einzeln in isolierten sich Standorte bereitgestellt werden wie Zweigstellen reduzieren.  
   - Neuerstellen von RODCs wird sichergestellt, dass sie keine veralteten Objekte enthalten und können verhindern, dass Replikationskonflikten später noch mal. Wenn Sie von einem RODC, AD DS entfernen *wählen die Option zum Beibehalten der DC-Metadaten*. Mit dieser Option behält das Krbtgt-Konto für den RODC und behält die Berechtigungen für das delegierte RODC-Administratorkonto und das Kennwort Kennwortreplikationsrichtlinie (PRP) und verhindert, dass Sie mit der Verwendung von Domänenadministrator-Anmeldeinformationen zu entfernen und Neuinstallieren von AD DS auf ein RODC. Er behält auch die DNS-Server und den globalen Katalog-Rollen, wenn sie ursprünglich auf dem RODC installiert sind.  
   - Wenn Sie neu Domänencontrollern (RODCs oder beschreibbare DCs) erstellen, ist möglicherweise Replikationsdatenverkehr erhöht, während die Neuinstallation. Um diese Auswirkungen zu verringern, können Sie den Zeitplan der RODC-Installationen staffeln, und können Sie die Option (Installieren von Media, IFM). Wenn Sie die IFM-Option verwenden, führen Sie die **Ntdsutil Ifm** Befehl auf einem beschreibbaren DC, der Sie vertrauen, frei von sein beschädigter Daten. Dies verhindert mögliche Beschädigungen auf dem RODC angezeigt werden, nachdem Sie die AD DS-Neuinstallation abgeschlossen ist. Weitere Informationen zu IFM finden Sie unter [Installieren von AD DS von einem Medium](https://technet.microsoft.com/library/cc770654\(WS.10\).aspx).  
   - Weitere Informationen zur Neuerstellung von RODCs finden Sie unter [RODC entfernen und die Neuinstallation abzukürzen](https://technet.microsoft.com/library/cc835490\(WS.10\).aspx).  
- Wenn ein Domänencontroller den DNS-Serverdienst vor der Fehlfunktion Gesamtstruktur ausgeführt wurde, installieren Sie und konfigurieren Sie den DNS-Server-Dienst während der Installations von AD DS. Konfigurieren Sie andernfalls den früheren DNS-Clients mit anderen DNS-Servern.  
- Wenn Sie zusätzliche globale Kataloge-Authentifizierung oder durch Abfragen verursachte Last für Benutzer oder Anwendungen freigeben benötigen, können Sie entweder hinzufügen, der globale Katalog an der Quelle virtualisierte Domänencontroller vor dem Klonen, oder Sie können einem Domänencontroller einen globaler Katalogserver vornehmen, während der Installations von AD DS.  
  
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
