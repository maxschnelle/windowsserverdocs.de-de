---
ms.assetid: eb600904-24b8-4488-a278-c1c971dc2f2d
title: "Planen der Platzierung der regionalen Domänencontroller"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c5254560e9b1a10030fa37ec0966868986212a4a
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="planning-regional-domain-controller-placement"></a>Planen der Platzierung der regionalen Domänencontroller

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Um sicherzustellen, dass Kosteneffizienz, möglichst wenige regionale Domänencontroller möglichst platzieren möchten. Sehen Sie sich zuerst in verwendet "Geografische Standorte und Kommunikationsverbindungen" (DSSTOPO_1.doc) Arbeitsblatt [Sammeln von Netzwerkinformationen](../../ad-ds/plan/Collecting-Network-Information.md) zu bestimmen, ob ein Standort ein Hub ist.  
  
Planen der regionalen Domänencontroller für jede Domäne platziert, der an jedem Hubstandort dargestellt wird. Nachdem Sie regionale Domänencontroller an allen Hubstandorten platzieren, bewerten Sie die Notwendigkeit für die Platzierung der regionalen Domänencontroller bei Satelliten-Speicherorte. Eliminieren unnötige regionale Domänencontroller von Satellitenstandorten verringert die Supportkosten erforderlich, um eine Remote-Server-Infrastruktur.  
  
Darüber hinaus stellen Sie die physische Sicherheit der Domänencontroller im Hub und Satelliten-Speicherorte, damit nicht autorisierte Mitarbeiter darauf zugreifen können nicht sicher. Platzieren Sie beschreibbaren Domänencontroller im Hub und Satelliten-Speicherorte, in denen Sie die physische Sicherheit des Domänencontrollers nicht garantiert werden können. Eine Person mit physischem Zugriff auf einen beschreibbaren Domänencontroller kann das System durch Angriffe:  
  
-   Zugriff auf physische Datenträger durch Starten von einem anderen Betriebssystem auf einem Domänencontroller.  
  
-   Physische Datenträger auf einem Domänencontroller entfernen (und möglicherweise ersetzen).  
  
-   Abrufen und bearbeiten eine Kopie einer systemstatussicherung des Domain-Controller.  
  
Fügen Sie nur für die Speicherorte, an denen Sie die physische Sicherheit garantieren können, beschreibbaren regionalen Domänencontroller hinzu.  
  
An Standorten mit ausreichender physische Sicherheit Bereitstellung von einem schreibgeschützten Domänencontroller (RODC) ist die empfohlene Lösung. Mit Ausnahme von Kontokennwörtern enthält ein RODC alle Active Directory-Objekte und Attribute, die ein beschreibbaren Domänencontroller enthält. Allerdings kann nicht in die Datenbank geändert werden, die auf dem RODC gespeichert ist. Änderungen müssen auf einem beschreibbaren Domänencontroller vorgenommen und dann wieder auf den RODC repliziert werden.  
  
Informationen zum Authentifizieren von Clients und den Zugriff auf lokale Dateiserver platzieren die meisten Organisationen regionale Domänencontroller für alle regionalen Domänen, die in einer bestimmten Position dargestellt werden. Allerdings müssen Sie viele Variablen berücksichtigen, beim Auswerten, ob Unternehmen erfordert, dass die Clients lokale Authentifizierung oder die Clients können über die Verbindung ein wide Area Network (WAN) Authentifizierung und Abfragen verlassen. Die folgende Abbildungzeigt, wie Sie bestimmen, ob Domänencontroller an Satellitenstandorten platziert wird.  
  
![Platzierung der regionalen Domänencontroller Plan](media/Planning-Regional-Domain-Controller-Placement/49892c8c-2c99-4aab-92ba-808dbc8048e2.gif)  
  
## <a name="onsite-technical-expertise-availability"></a>Vor-Ort-Expertenwissen Verfügbarkeit  
Domänencontroller aus verschiedenen Gründen fortlaufend verwaltet werden müssen. Platzieren Sie einen regionalen Domänencontroller nur an Standorten, die Mitarbeiter berücksichtigt, die den Domänencontroller verwalten können, oder stellen Sie sicher, dass der Domänencontroller remote verwaltet werden kann.  
  
In Zweigniederlassungen mit in der Regel eine schlechte physische Sicherheit und Mitarbeiter mit wenig Informationen Technologie Wissen ist das Bereitstellen eines RODC häufig die empfohlene Lösung. Lokale Administratorberechtigungen für einen RODC können alle Domänenbenutzer ohne Benutzerrechte dieses Benutzers für die Domäne oder andere Domänencontroller delegiert werden. Dies ermöglicht lokalen Zweigstelle Benutzer melden Sie sich bei einem RODC, und führen Wartungsarbeiten auf dem Server, z.B. das Aktualisieren eines Treibers. Jedoch nicht die Branch-Benutzer melden Sie sich auf alle anderen Domänencontroller oder andere administrative Aufgabe ausführen, in der Domäne. Auf diese Weise kann der Benutzer Branch delegiert die Möglichkeit, den RODC in der Zweigstelle effektiv zu verwalten, ohne die Sicherheit des restlichen der Domäne oder der Gesamtstruktur zu gefährden.  
  
## <a name="wan-link-availability"></a>Verfügbarkeit der WAN-Verbindung  
WAN-Verbindungen, die häufige Ausfälle auftreten können zum Verlust Produktivität für Benutzer, wenn der Speicherort nicht in einen Domänencontroller enthalten ist, der den Benutzer authentifizieren können. Wenn Ihre Verfügbarkeit WAN-Verbindung nicht 100Prozent ist und Remotestandorten ein dienstausfalls tolerieren können nicht, platzieren Sie einen regionalen Domänencontroller an, in denen die Benutzer die Möglichkeit zum Anmelden oder Zugriff auf exchange Server bei der WAN-Verbindung benötigen.  
  
## <a name="authentication-availability"></a>Authentifizierung-Verfügbarkeit  
Bestimmte Organisationen wie Banken, erfordern, dass Benutzer jederzeit authentifiziert werden. Platzieren Sie einen regionalen Domänencontroller an einem Speicherort, in denen die Verfügbarkeit der WAN-Verbindung ist nicht 100Prozent jedoch Benutzer die Authentifizierung immer erforderlich.  
  
## <a name="logon-performance-over-wan-links"></a>Leistung beim Anmelden über WAN-links  
Wenn Ihre Verfügbarkeit WAN-Verbindung sehr zuverlässig ist, hängt Platzierung eines Domänencontrollers am Standort auf die Leistung anmeldeanforderungen über die WAN-Verbindung. Faktoren für Anmeldung über das WAN enthalten, verbindungsgeschwindigkeit und die verfügbare Bandbreite, Anzahl von Benutzern und Nutzung und die Menge an Netzwerkdatenverkehr im Vergleich zu Replikationsdatenverkehr Anmeldung.  
  
### <a name="wan-link-speed-and-bandwidth-utilization"></a>Auslastung von WAN-Geschwindigkeit und Bandbreite  
Die Aktivitäten des einen einzelnen Benutzer können eine langsame WAN-Verbindung belasten. Platzieren Sie einen Domänencontroller an einem Standort, wenn Leistung beim Anmelden über die WAN-Verbindung nicht akzeptabel ist.  
  
Der durchschnittliche Prozentsatz der bandbreitennutzung zeigt an, wie überlastete eine Verknüpfung im Netzwerk ist. Wenn eine Verknüpfung im Netzwerk durchschnittliche bandbreitennutzung, die größer als ein gültiger Wert ist aufweist, legen Sie einen Domänencontroller an dieser Stelle.  
  
### <a name="number-of-users-and-usage-profiles"></a>Anzahl der Benutzer und Nutzung  
Die Anzahl der Benutzer und ihre Verwendungsprofile an einer bestimmten Position können Sie ermitteln, ob regionale Domänencontroller an dieser Stelle platziert werden muss. Um Produktivitätsverluste zu vermeiden, wenn eine WAN-Verbindung ein Fehler auftritt, platzieren Sie einen regionalen Domänencontroller an einen Speicherort mit mindestens 100 Benutzer.  
  
Die Verwendungsprofile anzugeben, wie die Benutzer die Netzwerkressourcen verwenden. Sie müssen sich nicht um einen Domänencontroller an einem Speicherort zu platzieren, die nur wenige Benutzer enthält, die nicht häufig auf Netzwerkressourcen zugreifen.  
  
### <a name="logon-network-traffic-vs-replication-traffic"></a>Anmeldung des Netzwerkdatenverkehrs im Vergleich mit dem Replikations-Datenverkehr  
Wenn ein Domänencontroller nicht am gleichen Speicherort wie die Active Directory-Client verfügbar ist, erstellt der Client Anmeldung Datenverkehr im Netzwerk. Die Menge Anmeldung-Netzwerkdatenverkehr, der auf dem physischen Netzwerk erstellt wird, wird durch mehrere Faktoren, z.B. Gruppenmitgliedschaften beeinflusst; Anzahl und Größe der Gruppenrichtlinienobjekte (GPOs); Anmeldeskripts; und Funktionen, z.B. Offline-Ordner, ordnerumleitung und servergespeicherte Profile.  
  
Andererseits, generiert ein Domänencontroller, der an einer bestimmten Position platziert wird Replikations-Datenverkehr im Netzwerk. Die Häufigkeit und Umfang von Aktualisierungen auf die Partitionen, die auf den Domänencontrollern gehostet beeinflussen, die Menge des Replikations-Datenverkehr, der im Netzwerk erstellt wird. Die verschiedenen Typen von Updates, die auf die Partitionen, die auf den Domänencontrollern gehostet werden können, gehören hinzufügen oder Ändern von Benutzern und Benutzerattributen, Ändern von Kennwörtern und hinzufügen oder Ändern von globalen Gruppen, Drucker oder Volumes.  
  
Um festzustellen, ob der regionalen Domänencontroller an einem Standort platziert werden müssen, vergleichen Sie die Kosten für die Anmeldung Datenverkehr von einem Ort ohne einen Domänencontroller und die Kosten der Replikations-Datenverkehr durch das Platzieren eines Domänencontrollers an dem Speicherort erstellt erstellt.  
  
Angenommen, ein Netzwerk mit Zweigstellen, die über langsame Verbindungen mit der zentrale verbunden sind und in der Domäne Domänencontroller können leicht hinzugefügt werden. Der tägliche Anmeldung und Lookup-Datenverkehr, der einige Remotestandort Benutzer mehr Netzwerkverkehr als die Replikation alle Daten des Unternehmens in den Zweig bewirkt, erwägen Sie, die einen Domänencontroller in den Zweig.  
  
Senken der Kosten der Verwaltung von Domänencontrollern wichtiger als Netzwerkverkehr ist, entweder Zentralisieren Sie die Domänencontroller für diese Domäne zu und platzieren Sie der regionalen Domänencontroller an der Stelle oder nicht platzieren Sie RODCs an der Stelle.  
  
Ein Arbeitsblatt, hilft Ihnen bei der Dokumentieren der Platzierung der regionalen Domänencontroller und die Anzahl der Benutzer für jede Domäne, die an jedem Standort dargestellt wird, finden Sie unter Auftrag Hilfsmittel für Windows Server2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)), herunterladen < DICT__Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip>Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip</DICT__Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip>, and Öffnen Sie "Domänencontrollerkapazität" (DSSTOPO_4.doc).  
  
Sie benötigen, um die Informationen zu Standorten finden in der regionalen Domänencontroller platziert, beim Bereitstellen von Regionaldomänen werden müssen. Weitere Informationen zum Bereitstellen von Regionaldomänen finden Sie unter [Bereitstellen von Windows Server2008 Regionaldomänen](https://technet.microsoft.com/library/cc755118.aspx).  
  


