---
ms.assetid: 22c514b2-401e-49e1-a87e-0cbaa2c1dac1
title: Site-Funktionen
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f40122d84185c69fa19f5158c2b1c370ec1bfe82
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="site-functions"></a>Site-Funktionen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

 Windows Server2008 verwendet Standortinformationen für zahlreiche Zwecke verwenden, einschließlich Routing-Replikation, Clientaffinität, Systemvolume (SYSVOL)-Replikation, verteilt Datei System Namespaces (DFSN) und -Speicherort.  
  
## <a name="routing-replication"></a>Routing-Replikation  
Active Directory-Domänendienste (AD DS) verwendet eine multimaster, Store-and-Forward-Methode der Replikation. Ein Domänencontroller kommuniziert Directory Änderungen an einen zweiten Domänencontroller, der dann eine Verbindung mit einem dritten usw., bis alle Domänencontroller die Änderung erhalten hat. Um den besten Kompromiss zwischen Reduzierung der Replikationswartezeit und Reduzieren des Datenverkehrs zu erreichen, steuert die Standorttopologie Active Directory-Replikation durch die Unterscheidung zwischen Replikation innerhalb eines Standorts und Replikation zwischen Standorten.  
  
Innerhalb von Standorten Replikation ist für Speeddata Updates-Replikation optimiert, und die Daten werden gesendet, ohne den Aufwand, der durch die datenkomprimierung erforderlich. Im Gegensatz dazu wird Replikation zwischen Standorten komprimiert, um die Kosten für die Übertragung über wide Area Network (WAN) Links zu minimieren. Bei der Replikation zwischen Standorten erfasst ein einzelnen Domänencontroller pro Domäne an jedem Standort und speichert die verzeichnisänderungen und diese zu einem geplanten Zeitpunkt zu einem Domänencontroller an einem anderen Standort kommuniziert.  
  
## <a name="client-affinity"></a>Clientaffinität  
Domänencontroller verwenden Standortinformationen in Active Directory-Clients über Domänencontroller vorhanden ist, in dem nächstgelegenen übergeordneten Standort wie der Client informiert. Betrachten Sie beispielsweise einen Client am Standort Seattle, die die Standort-Zuordnung ist nicht bekannt und eine Verbindung mit einen Domänencontroller in der Atlanta-Website. Basierend auf die IP-Adresse des Clients bestimmt die Domänencontroller in Atlanta welchem Standort des Clients handelt es sich tatsächlich aus und sendet die Informationen an den Client zurück. Der Domänencontroller wird, ob die ausgewählten Domänencontroller die nächste aus, es ist auch der Client informiert. Der Client speichert die Informationen bereitgestellt, die vom Domänencontroller in Atlanta, Abfragen für den standortspezifischen Dienste (SRV)-Ressourceneintrag (ein Domain Name System (DNS) Ressourceneintrag zum Suchen nach Domänencontrollern für AD DS) und somit sucht nach einem Domänencontroller am selben Standort.  
  
Anhand der Suche nach einem Domänencontroller am selben Standort, muss der Client Kommunikation über WAN-Links. Wenn keine Domänencontroller am Clientstandort befinden, kündigt ein Domänencontroller, der die niedrigsten Kosten Verbindungen relativ zu anderen verbundenen Standorten hat selbst (einen Ressourceneintrag standortspezifische Dienste (SRV) in DNS registriert) auf der Website, die nicht über einen Domänencontroller verfügt. Die Domänencontroller, die in DNS veröffentlicht werden sind die von dem nächstgelegenen übergeordneten Standort gemäß der Standorttopologie. Dieser Prozess wird sichergestellt, dass jeder Standort einen bevorzugten Domänencontroller für die Authentifizierung hat.  
  
Weitere Informationen über den Prozess der Suchen eines Domänencontrollers finden Sie unter Active Directory-Sammlung ([https://go.microsoft.com/fwlink/?LinkID=88626](https://go.microsoft.com/fwlink/?LinkID=88626)).  
  
## <a name="sysvol-replication"></a>SYSVOL-Replikation  
SYSVOL ist eine Sammlung von Ordnern im Dateisystem, das auf jedem Domänencontroller in einer Domäne vorhanden ist. Die SYSVOL-Ordner bieten einen Standard-Active Directory-Speicherort für Dateien, die in der gesamten Domäne, einschließlich von Gruppenrichtlinienobjekten (GPOs), starten und Herunterfahren von Skripts und Anmelde- und Abmeldeskripts repliziert werden müssen.  Windows Server2008 (File Replication Service, FRS) oder verteilte Datei-Replikation (DFSR) können Änderungen an der SYSVOL-Ordner von einem Domänencontroller auf andere Domänencontroller repliziert werden. FRS und DFSR repliziert diese Änderungen gemäß dem Zeitplan, den während des Entwurfs der Standorttopologie erstellt.  
  
## <a name="dfsn"></a>DFSN  
DFSN verwendet Standortinformationen, um ein Client mit dem Server zu verweisen, die die angeforderten Daten innerhalb des Standorts gehostet wird. Wenn DFSN nicht über eine Kopie der Daten am selben Standort wie der Client findet, DFSN verwendet die Informationen in AD DS, um zu bestimmen, welche Dateiserver mit DFSN Daten freigegeben am nächsten ist an den Client.  
  
## <a name="service-location"></a>Speicherort  
Durch das Veröffentlichen von Diensten wie z.B. Datei und Druckdienste in AD DS, können Sie Active Directory-Clients auf den angeforderten Dienst innerhalb desselben oder nächstgelegenen Standort suchen. Druckdienste verwenden die Location-Attribut in AD DS gespeichert, um Benutzer für Drucker nach Standort zu durchsuchen, ohne zu wissen, ihre genaue Position zu ermöglichen. Weitere Informationen zum Entwerfen und Bereitstellen von Druckerservern finden Sie unter Entwerfen und Bereitstellen von Druckerserver ([https://go.microsoft.com/fwlink/?LinkId=107041](https://go.microsoft.com/fwlink/?LinkId=107041)).  
  


