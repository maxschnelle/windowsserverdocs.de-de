---
ms.assetid: 22c514b2-401e-49e1-a87e-0cbaa2c1dac1
title: Standortfunktionen
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0a330a9dae8ab8d3b9de5d1fff0e52060908f520
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815811"
---
# <a name="site-functions"></a>Standortfunktionen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

 Windows Server 2008 werden Standortinformationen für viele Zwecke, einschließlich routing-Replikation, Clientaffinität, Systemvolume (SYSVOL)-Systemreplikation, Distributed Datei System-Namespaces (DFSN) und dienstidentifizierung verwendet.  
  
## <a name="routing-replication"></a>Routing-Replikation  
Active Directory-Domänendienste (AD DS) verwendet eine multimaster, speichern-und-Weiterleiten-Methode der Replikation. Domänencontroller kommuniziert verzeichnisänderungen, ein zweiter Domänencontroller, klicken Sie dann eine Verbindung mit einer dritten usw., bis alle Domänencontroller die Änderung erhalten hat. Um das optimale Gleichgewicht zwischen der Replikationswartezeit zu reduzieren und Senkung des Datenverkehrs zu erzielen, steuert die Standorttopologie Active Directory-Replikation durch die Unterscheidung zwischen Replikation innerhalb eines Standorts und Replikation zwischen Standorten.  
  
Innerhalb von Standorten wird die Replikation optimiert, für die Geschwindigkeit, die Updates Trigger Datenreplikation und die Daten ohne den Aufwand erforderlich, durch die datenkomprimierung gesendet wird. Im Gegensatz dazu wird die Replikation zwischen Standorten komprimiert, um die Kosten für die Übertragung über Verbindungen wide Area Network (WAN) zu minimieren. Bei der Replikation zwischen Standorten, ein einzelnen Domänencontroller pro Domäne an jedem Standort erfasst und speichert die Änderungen, und sie zu einem geplanten Zeitpunkt zu einem Domänencontroller an einem anderen Standort kommuniziert ab.  
  
## <a name="client-affinity"></a>Clientaffinität  
Domänencontroller verwenden Standortinformationen in Active Directory-Clients über Domänencontroller vorhanden ist, in dem nächstgelegenen Standort wie der Client informiert. Betrachten Sie beispielsweise einen Client am Standort Seattle, die weiß nicht, dass die Site-Zuordnung und kontaktiert einen Domänencontroller, von der Atlanta-Website. Basierend auf die IP-Adresse des Clients, bestimmt der Domänencontroller in Atlanta, welchem Standort der Client ist jedoch aus und sendet Standortinformationen zurück an den Client. Der Domänencontroller enthält außerdem dem Client, ob die ausgewählten Domänencontroller dasjenige, es ist. Der Client speichert die Informationen bereitgestellt, die vom Domänencontroller in Atlanta dabei, Abfragen für den standortspezifischen Dienste (SRV)-Ressourceneintrag (ein Domain Name System (DNS) Ressourceneintrag verwendet, um für AD DS-Domänencontroller zu finden), und dadurch sucht nach einer Domäne Controller innerhalb desselben Standorts.  
  
Durch das Suchen eines Domänencontrollers am selben Standort, vermeidet der Client Kommunikation über WAN-Verbindungen. Wenn keine Domänencontroller am Clientstandort befinden, kündigt ein Domänencontroller, die die niedrigsten Kosten Verbindungen relativ zu anderen verbundenen Standorte selbst (registriert einen standortspezifischen Dienste (SRV)-Ressourceneintrag in DNS) auf der Website, die keinem Domänencontroller. Die Domänencontroller, die im DNS veröffentlicht werden stammen von dem nächstgelegenen Standort gemäß der Standorttopologie. Dadurch wird sichergestellt, dass jeder Standort einen bevorzugten Domänencontroller für die Authentifizierung hat.  
  
Weitere Informationen zu den Prozess zum Auffinden von einem Domänencontroller, finden Sie unter Active Directory-Benutzersammlung ([https://go.microsoft.com/fwlink/?LinkID=88626](https://go.microsoft.com/fwlink/?LinkID=88626)).  
  
## <a name="sysvol-replication"></a>SYSVOL-Replikation  
SYSVOL ist eine Auflistung von Ordnern im Dateisystem, das auf jedem Domänencontroller in einer Domäne vorhanden ist. Der Ordner "SYSVOL" Geben Sie ein Active Directory-Standardverzeichnis für Dateien, die in der gesamten Domäne, einschließlich der Gruppenrichtlinienobjekte (GPOs), starten und Herunterfahren von Skripts und Anmelde-und Abmeldeskripts repliziert werden müssen.  Windows Server 2008 können die Windows-Verwaltungsinstrumentation (File Replication Service, FRS) oder Distributed Datei System Replikation (DFSR) verwenden, um Änderungen, die für die SYSVOL-Ordner von einem Domänencontroller mit anderen Domänencontrollern zu replizieren. FRS und DFSR repliziert diese Änderungen gemäß dem Zeitplan, den Sie bei der Gestaltung Ihrer Site-Topologie zu erstellen.  
  
## <a name="dfsn"></a>DFSN  
DFSN verwendet Standortinformationen, um einen Client an den Server zu leiten, die die angeforderten Daten innerhalb des Standorts gehostet wird. Wenn eine Kopie der Daten nicht am selben Standort wie der Client DFSN gefunden wird, DFSN verwendet die Standortinformationen in AD DS zu bestimmen, welche Dateiserver mit DFSN Daten freigegeben am nächsten ist an den Client.  
  
## <a name="service-location"></a>Dienstidentifizierung  
Veröffentlichen Sie in AD DS-Dienste wie z. B. Datei und Druckdienste, können Sie die Active Directory-Clients, um den angeforderten Dienst in derselben oder nächstgelegenen Standort suchen. Druckdienste verwenden die Location-Attribut in AD DS gespeichert, um Benutzer nach Druckern nach Standort zu suchen, ohne zu wissen, genaue Ort zu lassen. Weitere Informationen zum Entwerfen und Bereitstellen von Druckerservern finden Sie unter Entwerfen und Bereitstellen von Druckserver ([https://go.microsoft.com/fwlink/?LinkId=107041](https://go.microsoft.com/fwlink/?LinkId=107041)).  
  


