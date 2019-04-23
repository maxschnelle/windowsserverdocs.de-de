---
ms.assetid: eb600904-24b8-4488-a278-c1c971dc2f2d
title: Planen der Platzierung der regionalen Domänencontroller
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: bec8595ab6eae8eb6cedaf9307ab97ac9c8316b8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880441"
---
# <a name="planning-regional-domain-controller-placement"></a>Planen der Platzierung der regionalen Domänencontroller

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Um sicherzustellen, dass Kosteneffizienz, möglichst wenige regionalen Domänencontroller möglichst platzieren möchten. Prüfen Sie zunächst in verwendet "Geografische Standorte und Kommunikationsverbindungen" (DSSTOPO_1.doc) Arbeitsblatt [Sammeln von Netzwerkinformationen](../../ad-ds/plan/Collecting-Network-Information.md) zu bestimmen, ob ein Speicherort, einen Hub ist.  
  
Planen der regionalen Domänencontroller für jede Domäne platziert, die an jedem Hubstandort dargestellt wird. Nachdem Sie die regionalen Domänencontroller in allen Standorten platziert, die Notwendigkeit für die Platzierung der regionalen Domänencontroller an Satellitenstandorten-ausgewertet werden. Beseitigen unnötigen regionalen Domänencontroller von Satellitenstandorten reduziert die Supportkosten erforderlich, um eine remote-Server-Infrastruktur beizubehalten.  
  
Darüber hinaus stellen Sie die physische Sicherheit der Domänencontroller im Hub und Satelliten-Speicherorte, damit nicht autorisierte Personen darauf zugreifen können nicht sicher. Platzieren Sie nicht beschreibbaren Domänencontroller im Hub- and -Satelliten-Speicherorte, in denen Sie die physische Sicherheit des Domänencontrollers nicht garantieren können. Eine Person mit physischem Zugriff auf einen beschreibbaren Domänencontroller kann das System durch Angriffe:  
  
- Zugriff auf physische Datenträger durch Starten von einem anderen Betriebssystem auf einem Domänencontroller aus.  
- Physische Datenträger auf einem Domänencontroller entfernen (und möglicherweise ersetzt).  
- Abrufen und bearbeiten eine Kopie einer systemstatussicherung des Domain Controllers.  
  
Fügen Sie nur den Speicherorten, die in denen Sie ihre physische Sicherheit gewährleisten können beschreibbare regionalen Domänencontroller hinzu.  
  
An Standorten mit nicht ausreichend physischer Sicherheit Bereitstellung von einem schreibgeschützten Domänencontroller (RODC) ist die empfohlene Lösung. Mit Ausnahme von Kontokennwörtern sind ein RODC enthalten alle Active Directory-Objekte und Attribute, die ein beschreibbarer Domänencontroller verfügt. Änderungen können nicht jedoch in der Datenbank vorgenommen werden, die auf dem RODC gespeichert ist. Änderungen müssen auf einen beschreibbaren Domänencontroller vorgenommen und dann zurück auf den RODC repliziert werden.  
  
Um Clients und den Zugriff auf lokale Dateiserver zu authentifizieren, platzieren Sie die meisten Organisationen regionalen Domänencontroller für alle regionalen Domänen, die einem bestimmten Standort dargestellt werden. Allerdings müssen Sie viele Variablen berücksichtigen, bei der Auswertung, ob ein Business-Speicherort erfordert, dass die Clients lokale Authentifizierung oder die Clients können über ein wide Area Network (WAN)-Link zur Authentifizierung und die Abfrage basieren. Die folgende Abbildung zeigt, wie zu bestimmen, ob Domänencontroller an Satellitenstandorten platziert wird.  
  
![Plan regionalen dc-Platzierung](media/Planning-Regional-Domain-Controller-Placement/49892c8c-2c99-4aab-92ba-808dbc8048e2.gif)  
  
## <a name="onsite-technical-expertise-availability"></a>Vor-Ort-Fachkenntnisse Verfügbarkeit

Domänencontroller müssen kontinuierlich aus unterschiedlichen Gründen verwaltet werden. Platzieren Sie einen regionalen Domänencontroller nur an Standorten, die Mitarbeiter enthalten, die Verwaltung des Domänencontrollers oder Achten Sie darauf, dass der Domänencontroller kann remote verwaltet werden können.  
  
In Umgebungen von Zweigstellen mit in der Regel eine schlechte physische Sicherheit und der Mitarbeiter mit wenig Informationen Technologie Wissen ist das Bereitstellen eines RODC oft die empfohlene Lösung. Ohne dass diesem Benutzer Benutzerrechte für die Domäne oder andere Domänencontroller gewährt wird, können an jeden Domänenbenutzer lokale Administratorrechte für einen RODC delegiert werden. Dies ermöglicht einen lokale Verzweigung Benutzer melden Sie sich bei einem RODC, und führen Wartungsarbeiten auf dem Server, z. B. Aktualisieren eines Treibers. Allerdings kann nicht der Branch-Benutzer melden Sie sich auf alle anderen Domänencontroller oder andere administrative Aufgaben in der Domäne ausführen. Auf diese Weise kann der Benutzer für die Verzweigung sein delegiert die Möglichkeit, den RODC in der Zweigstelle effektiv zu verwalten, ohne Beeinträchtigung der Sicherheits des restlichen der Domäne oder Gesamtstruktur.  
  
## <a name="wan-link-availability"></a>Verfügbarkeit der WAN-Verbindung

WAN-Verbindungen, die häufigen Ausfälle auftreten können zum Verlust kann die Produktivität erheblich an Benutzer, wenn der Speicherort keinen Domänencontroller enthalten ist, der die Benutzer authentifizieren können. Wenn Ihre Verfügbarkeit für die WAN-Verbindung nicht 100 Prozent und Remotestandorten können nicht zu einen Dienstausfall tolerieren, platzieren Sie einen regionalen Domänencontroller an Standorten, in denen die Benutzer die Berechtigung zum Anmelden oder exchange Server-Zugriff benötigen, wenn die WAN-Verbindung ausgefallen ist.  
  
## <a name="authentication-availability"></a>Authentifizierung-Verfügbarkeit

Bestimmten Organisationen wie Banken, erfordern, dass Benutzer jederzeit authentifiziert werden. Platzieren Sie einen regionalen Domänencontroller an einem Speicherort, in denen die Verfügbarkeit der WAN-Verbindung ist nicht 100 Prozent, aber Benutzer erfordert Authentifizierung immer, ein.  
  
## <a name="logon-performance-over-wan-links"></a>Leistung der Anmeldung über WAN-Verbindungen

Wenn Ihre Verfügbarkeit für die WAN-Verbindung äußerst zuverlässig ist, hängt von Platzierung eines Domänencontrollers am Standort der leistungsanforderungen für die Anmeldung über die WAN-Verbindung. Logon-Leistung über das WAN Faktoren beeinflussen verbindungsgeschwindigkeit und die verfügbare Bandbreite, Anzahl von Benutzern und von Nutzungsprofilen und die Menge des Netzwerkdatenverkehrs für Anmeldung und der Replikationsdatenverkehr.  
  
### <a name="wan-link-speed-and-bandwidth-utilization"></a>Auslastung von WAN-Geschwindigkeit und Bandbreite

Die Aktivitäten von einem einzelnen Benutzer können eine langsame WAN-Verbindung zu belasten. Setzen Sie einen Domänencontroller an einem Speicherort ein, wenn Leistung der Anmeldung über die WAN-Verbindung nicht akzeptabel ist.  
  
Die durchschnittliche prozentuale Nutzung der Netzwerkbandbreite gibt an, wie überlastet wird von eine Netzwerkverbindung verbinden. Wenn eine Netzwerkverbindung durchschnittliche bandbreitenauslastung, die größer als ein zulässiger Wert ist verfügt, platzieren Sie einen Domänencontroller an diesem Speicherort aus.  
  
### <a name="number-of-users-and-usage-profiles"></a>Anzahl von Benutzern und Nutzungsprofilen

Die Anzahl von Benutzern und deren Nutzung Profile an einer bestimmten Position helfen zu bestimmen, ob der regionalen Domänencontroller an diesem Speicherort platziert werden müssen. Um Produktivitätsverluste zu vermeiden, wenn eine WAN-Verbindung ein Fehler auftritt, platzieren Sie einen regionalen Domänencontroller an einem Speicherort an, die mindestens 100 Benutzer.  
  
Die Usage-Profile geben an, wie sich die Benutzer auf die Netzwerkressourcen verwenden. Sie müssen sich nicht um einen Domänencontroller an einem Speicherort zu platzieren, die nur wenige Benutzer enthält, die nicht häufig auf Netzwerkressourcen zugreifen.  
  
### <a name="logon-network-traffic-vs-replication-traffic"></a>Anmeldung des Netzwerkdatenverkehrs im Vergleich zu den Replikations-Datenverkehr

Wenn ein Domänencontroller nicht am gleichen Speicherort wie der Client Active Directory verfügbar ist, erstellt der Client Anmeldung Datenverkehr im Netzwerk. Die Menge des Netzwerkdatenverkehrs von Anmeldung, die auf dem physischen Netzwerk erstellt wird, wird von mehreren Faktoren ab, einschließlich der Gruppenmitgliedschaften beeinflusst; Anzahl und Größe der Gruppenrichtlinienobjekte (GPOs); Anmeldeskripts; und Funktionen wie Offlineordner, ordnerumleitung und servergespeicherte Profile.  
  
Andererseits, generiert ein Domänencontroller, der an einer bestimmten Position befindet, Replikations-Datenverkehr im Netzwerk. Die Häufigkeit und Umfang des Updates, die auf die Partitionen, die auf den Domänencontrollern gehostet beeinflussen den Umfang des Replikationsdatenverkehrs, die im Netzwerk erstellt wird. Die verschiedenen Typen von Updates, die an die Partitionen, die auf den Domänencontrollern gehostet vorgenommen werden können, enthalten hinzufügen "oder" Benutzer und Benutzerattribute ändern "," Ändern von Kennwörtern, "und" hinzufügen "oder" ändern, globale Gruppen, Drucker oder Volumes.  
  
Um zu bestimmen, wenn Sie einen regionalen Domänencontroller an einem Ort platzieren möchten, vergleichen Sie die Kosten für die Anmeldung Datenverkehr erstellt, die nach einem Standort ohne einen Domänencontroller im Vergleich zu den Kosten von Replikationsdatenverkehr durch die Platzierung eines Domänencontrollers am Standort erstellt.  
  
Betrachten Sie beispielsweise ein Netzwerk mit Zweigstellen, die über langsame Verbindungen mit der zentrale verbunden sind und in der Domäne Domänencontroller können ganz einfach hinzugefügt werden. Wenn der täglichen Anmeldung und Lookup-Datenverkehr, der einige Benutzer von remote-standortsystemserver bewirkt, mehr Netzwerkdatenverkehr dass als die Replikation aller Daten des Unternehmens in die Verzweigung, erwägen Sie, die einen Domänencontroller-Branch.  
  
Bei Senkung der Kosten der Verwaltung von Domänencontrollern wichtiger als die des Netzwerkdatenverkehrs wird entweder Zentralisieren Sie die Domänencontroller für diese Domäne und keine platzieren Sie regionalen Domänencontroller, an dem Ort, oder sollten Sie RODCs an der Position platzieren.  
  
Ein Arbeitsblatt, hilft Ihnen bei der Dokumentieren der Platzierung der regionalen Domänencontroller und die Anzahl der Benutzer für jede Domäne, die an jedem Standort dargestellt wird, finden Sie unter [Auftrag Hilfsmittel für Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558), Job_ herunterladen Aids_Designing_and_Deploying_Directory_and_Security_Services.ZIP, und öffnen "Domänencontrollerkapazität" (DSSTOPO_4.doc).  
  
Sie müssen auf die Informationen zu Speicherorten finden in der regionalen Domänencontroller platziert werden, beim Bereitstellen von Regionaldomänen werden müssen. Weitere Informationen zum Bereitstellen von Regionaldomänen finden Sie unter [Bereitstellen von Windows Server 2008 Regionaldomänen](https://technet.microsoft.com/library/cc755118.aspx).  
