---
title: "Wiederherstellung der Active Directory-Gesamtstruktur - verbleibenden Domänencontroller bereitstellen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: 66b0bc65b3b8e5dfbf5f1a85350dab60ac3a11c8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---redeploy-remaining-dcs"></a>Wiederherstellung der Active Directory-Gesamtstruktur - verbleibenden Domänencontroller bereitstellen

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

 Die Schritte, bis zu diesem Punkt gelten für alle Gesamtstrukturen: finden Sie eine gültige Sicherung für jede Domäne, die Domänen isoliert wiederherstellen, sofort wieder, der globale Katalog zurückgesetzt und bereinigen. In diesem nächsten Schrittwerden Sie die Gesamtstruktur erneut bereitstellen. Die Möglichkeit hierzu ist beim Entwurf der Gesamtstruktur, die Vereinbarungen zum Servicelevel, Struktur, verfügbare Bandbreite und zahlreiche andere Faktoren erheblich abhängig. Sie müssen zum Entwerfen Ihrer eigenen für die erneute Bereitstellung planen, die basierend auf den Prinzipien und Vorschläge in diesem Abschnitt, in einer Weise, die für Ihre geschäftlichen Anforderungen am besten geeignet ist.  
  
 Der nächste Schrittist zum Installieren von AD DS auf alle Domänencontroller, die vorhanden ist, bevor die Wiederherstellung der Gesamtstruktur übernommen wurden. Wenn die DCs immer noch vorhanden, der AD DS-Dienst nach Ablauf der Anmeldezeit entfernt werden müssen oder die Domänencontroller erneut installiert werden können. Alle vorhandenen Sicherungen für diesen Domänencontroller können nicht wiederverwendet werden, da die entsprechende Metadaten während der Wiederherstellung der Gesamtstruktur entfernt wurde. In einer Umgebung unkompliziert kann diesen Prozess für die erneute Bereitstellung so einfach wie das Wiederherstellen der Verbindung den wiederhergestellten Domänencontroller zum Produktionsnetzwerk und neue Domänencontroller heraufstufen, je nach Bedarf.  
  
 In einem großen Unternehmen mit einer weltweiten Infrastruktur konfrontiert wird ein anspruchsvollerer Plan benötigt. Die erste Phase ist normalerweise die Anzeige als Dienst wiederherstellen. Dies bedeutet strategisch installieren platziert DCs, dass alle kritischen Geschäftsbereiche und Anwendungen erneut mit der Arbeit beginnen können. Es kann für Filialen vorübergehend die Leistung dadurch geringer sein. Als zweiter sind alle verbleibenden Phase und weniger wichtige Domänencontroller erneut bereitgestellt.  
  
 Es gibt zwei Methoden, um zusätzliche Domänencontroller zu installieren, die automatisiert werden können:  
  
-   Das Klonen  
  
     Für virtualisierte Umgebungen, in denen Windows Server2012 ausgeführt wird, ist das Klonen die schnellste und einfachste Möglichkeit, eine große Anzahl von Domänencontrollern wiederherstellen aus. Sie können die Wiederherstellung der alle virtualisierten Domänencontroller in einer Domäne automatisieren, nachdem Sie einen virtualisierten Domänencontroller aus einer Sicherung wiederherstellen.  
  
     Weitere Informationen über das Klonen und die erforderlichen Komponenten finden Sie unter [Introduction to Active Directory-Domänendienste (AD DS) Virtualization (Level100)](https://technet.microsoft.com/library/hh831734.aspx).  
  
-   Installieren Sie AD DS mithilfe von Windows PowerShell auf Servern mit Windows Server2012 (oder Dcpromo.exe auf Servern, auf denen frühere Versionen von Windows Server ausgeführt) oder mithilfe der Benutzeroberfläche neu  
  
     Zum erneuten Installieren von AD DS zu beschleunigen, können Installieren von Medium (IFM)-Option Sie um während der Installation des Replikations-Datenverkehr reduzieren. Weitere Informationen zur Verwendung der **Ntdsutil Ifm** Befehl zum Erstellen eines Installationsmediums finden Sie unter [Installieren von AD DS von einem Medium](https://technet.microsoft.com/library/cc770654\(WS.10\).aspx).  
  
 Berücksichtigen Sie folgende zusätzliche Punkte für jedes Replikat-DC, die in der Gesamtstruktur durch Klonen von virtualisierten Domänencontroller oder nach der Installation von AD DS (im Gegensatz zu wiederherstellen aus einer Sicherung) wiederhergestellt werden:  
  
-   Die gesamte Software auf einem Domänencontroller, die als Quelle verwendet wird, für das Klonen geklont werden kann. Vor dem Klonen initiiert wird, sollten Anwendungen und Dienste, die nicht geklont werden können entfernt werden. Wenn dies nicht möglich ist, sollte eine alternative virtualisierten Domänencontrollers als Quelle ausgewählt werden.  
  
-   Wenn Sie zusätzliche virtualisierte Domänencontroller aus der ersten virtualisierte Domänencontroller wiederhergestellt werden klonen, müssen der Quelldomänencontroller heruntergefahren werden, während die VHDX-Datei kopiert wird. Sie müssen ausgeführt werden und verfügbar online sein, wenn das Klonen virtueller Domänencontroller sind bei der ersten. Wenn die Ausfallzeit erforderlich, die für das Herunterfahren nicht zulässig für die ersten wiederhergestellten Domänencontroller ist, Installieren von AD DS, die als Quelle für das Klonen fungieren bereitstellen Sie zusätzlichen virtualisierte Domänencontroller.  
  
-   Es besteht keine Einschränkung für den Hostnamen des geklonten virtualisierten Domänencontrollers oder dem Server, auf dem Sie AD DS installieren möchten. Sie können einen neuen Hostnamen oder den Hostnamen, der zuvor verwendet wurde. Weitere Informationen zur Syntax für DNS-Host finden Sie unter [Erstellen von DNS-Computernamen](https://technet.microsoft.com/library/cc785282.aspx) ([https://go.microsoft.com/fwlink/?LinkId=74564](https://go.microsoft.com/fwlink/?LinkId=74564)).  
  
-   Konfigurieren Sie jeden Server mit dem ersten DNS-Server in der Gesamtstruktur (des ersten Domänencontrollers, die in der Stammdomäne wiederhergestellt wurde), als bevorzugten DNS-Server in den TCP/IP-Eigenschaften des Netzwerkadapters. Weitere Informationen finden Sie unter [Konfigurieren von TCP/IP für DNS](https://technet.microsoft.com/library/cc779282.aspx).  
  
-   Erneut alle RODCs in der Domäne bereitstellen, indem virtualisierte Domänencontroller klonen, wenn mehrere RODCs an einem zentralen Ort bereitgestellt werden, oder indem der traditionellen Methode der Neuerstellung werden durch Entfernen und Neuinstallieren von AD DS, wenn sie einzeln in isolierten sich Speicherorten, z.B. Zweigstellen bereitgestellt werden.  
  
     Neuerstellen von RODCs wird sichergestellt, dass sie alle veralteten Objekte enthalten und, dass Replikationskonflikten später verhindern können. Beim Entfernen von AD DS von einem RODC *die Option zum Beibehalten der DC-Metadaten*. Mit dieser Option behält das Krbtgt-Konto für den RODC behält die Berechtigungen für das delegierte RODC-Administratorkonto und das Kennwort Replikation Richtlinie (PRP) und verhindert, dass Sie müssen Domänenadministrator-Anmeldeinformationen verwenden, entfernen und erneutes Installieren von AD DS auf einem RODC. Er behält auch der DNS-Server und den globalen Katalog Rollen, wenn sie ursprünglich auf dem RODC installiert sind.  
  
     Wenn Sie neu Domänencontrollern (RODCs oder beschreibbaren Domänencontroller) erstellen, besteht möglicherweise Replikationsdatenverkehr während ihrer Neuinstallation erhöht. Um die Auswirkungen zu reduzieren, können Sie den Zeitplan der RODC-Installationen staffeln und können Sie die Option (Installieren von Media, IFM) verwenden. Wenn Sie die IFM-Option verwenden, führen Sie die **Ntdsutil Ifm** -Befehl auf einem beschreibbaren Domänencontroller, denen Sie vertrauen, kostenlos sein beschädigt Daten. Dies verhindert, dass einer möglichen Beschädigung auf dem RODC angezeigt wird, nach die Neuinstallation von AD DS abgeschlossen ist. Weitere Informationen zu IFM, finden Sie unter [Installieren von AD DS von einem Medium](https://technet.microsoft.com/library/cc770654\(WS.10\).aspx).  
  
     Weitere Informationen zum Neuerstellen von RODCs, finden Sie unter [RODC entfernen und erneute Installation](https://technet.microsoft.com/library/cc835490\(WS.10\).aspx).  
  
-   Wenn ein Domänencontroller den DNS-Serverdienst vor der Gesamtstruktur Fehlfunktion ausgeführt wurde, installieren Sie und konfigurieren Sie den DNS-Server-Dienst während der Installations von AD DS. Konfigurieren Sie andernfalls den früheren DNS-Clients mit anderen DNS-Servern.  
  
-   Wenn Sie zusätzliche globale Kataloge freigeben Authentifizierung oder Laden der Abfrage für Benutzer oder Anwendungen benötigen, können Sie entweder der globale Katalog an die Quelle virtualisierte Domänencontroller vor dem Klonen oder Sie können einem Domänencontroller einen globaler Katalogserver während der Installations von AD DS hinzufügen.  
  
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