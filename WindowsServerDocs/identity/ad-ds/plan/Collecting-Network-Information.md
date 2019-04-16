---
ms.assetid: 8be8c48d-790c-4199-b9d3-9f4a07d5ced2
title: Sammeln von Netzwerkinformationen
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 174f11ca85a659f9d0c52e220d5ce37b1804f39b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="collecting-network-information"></a>Sammeln von Netzwerkinformationen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Der erste Schrittbeim Entwerfen einer effektiven Standorttopologie in Active Directory-Domänendienste (AD DS) ist, finden Sie in Ihrer Organisation Netzwerke Gruppe, um die Informationen erfasst und regelmäßig über die physischen Netzwerktopologie mit ihnen kommunizieren.  
  
## <a name="creating-a-location-map"></a>Erstellen eine Karte  
Erstellen Sie eine Karte, die die physische Netzwerkinfrastruktur Ihrer Organisation darstellt. Ermitteln Sie auf der Karte die geografische Standorte, die Gruppen von Computern mit einer internen Konnektivität von 10 Megabit pro Sekunde (MBit/s) oder höher (Geschwindigkeit des lokalen Netzwerks (LAN) oder höher) enthalten.  
  
## <a name="listing-communication-links-and-available-bandwidth"></a>Auflisten von kommunikationsverbindungen und die verfügbare Bandbreite  
Nach dem Erstellen einer Karte, dokumentieren Sie den Typ der Verbindung, die Übertragungsrate und die verfügbare Bandbreite zwischen jedem Speicherort. Eine wide Area Network (WAN)-Topologie aus Ihrem Netzwerk Gruppe zu erhalten. Eine Liste der allgemeinen WAN-Verbindung Typen und ihre Bandbreiten, finden Sie im Abschnitt "Bestimmen der Kosten" [Erstellen eines Entwurfs für Standortverknüpfungen](../../ad-ds/plan/Creating-a-Site-Link-Design.md). Sie benötigen diese Informationen weiter unten in den Entwurfsprozess der Standorttopologie standortverknüpfungen zu erstellen.  
  
Bandbreite bezieht sich auf die Menge der Daten, die Sie über einen Kommunikationskanal in einem bestimmten Zeitraum übertragen können. Verfügbare Bandbreite bezieht sich auf die Menge an Bandbreite für die Verwendung von AD DS tatsächlich verfügbar. Verfügbare Bandbreite Informationen erhalten Sie über Ihr Netzwerk Gruppe oder können Sie Datenverkehr für jede Verbindung mit einem Netzwerkprotokoll-Analyseprogramms wie Network Monitor, einer Komponente, die mit den im Lieferumfang von Windows Server2008 analysieren. Informationen zum Installieren des Netzwerkmonitors, finden Sie unter Überwachen des Netzwerkverkehrs ([https://go.microsoft.com/fwlink/?LinkId=107058](https://go.microsoft.com/fwlink/?LinkId=107058)).  
  
Dokumentieren Sie jeden Standort und den anderen Speicherorten, die verknüpft sind. Darüber hinaus erfassen Sie, die Verbindung und die verfügbare Bandbreite. Ein Arbeitsblatt, die Sie beim Auflisten von kommunikationsverbindungen und die verfügbare Bandbreite zu unterstützen, finden Sie unter Auftrag Hilfsmittel für Windows Server2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)), herunterladen Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip, und Öffnen Sie "Geografische Standorte und Kommunikationsverbindungen" (DSSTOPO_1.doc).  
  
## <a name="listing-ip-subnets-within-each-location"></a>Auflisten von IP-Subnetzen dieser Standorte  
Nachdem Sie die Kommunikation zwischen Links und die verfügbare Bandbreite zwischen jedem Speicherort dokumentieren, notieren Sie die IP-Subnetze an jedem Standort. Wenn Sie die Subnetzmaske und IP-Adresse an jedem Standort noch nicht kennen, finden Sie in Ihrem Netzwerk Gruppe.  
  
AD DS ordnet eine Arbeitsstation mit einem Standort durch einen Vergleich der Arbeitsstation IP-Adresse mit der Subnetze, die jedem Standort zugeordnet sind. Wie Sie die Domänencontroller einer Domäne hinzufügen, wird in AD DS auch untersucht die IP-Adressen und speichert sie in der am besten geeignete Website.  
  
Ein Arbeitsblatt, die Sie beim Auflisten der IP-Subnetzen dieser Standorte unterstützen, finden Sie unter Auftrag Hilfsmittel für Windows Server2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)), Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip, und öffnen "Standorte und Subnetze" (DSSTOPO_2.doc).  
  
> [!NOTE]  
> Zusätzlich zur IP-Version 4 (IPv4)-Adressen, Windows Server 2008 unterstützt auch IP Version 6 (IPv6) Subnetzpräfixe. Ein Arbeitsblatt, die Sie beim Auflisten der IPv6-Subnetzpräfixe unterstützen, finden Sie unter [AnhangA: Speicherorte und Subnetzpräfixe](../../ad-ds/plan/Appendix-A--Locations-and-Subnet-Prefixes.md).  
  
## <a name="listing-domains-and-number-of-users-for-each-location"></a>Auflisten von Domänen und Anzahl der Benutzer für jeden Standort  
Die Anzahl der Benutzer für jede regionale Domäne, die an einem Standort vorhanden ist ist einer der Faktoren, die bestimmen, die Platzierung der regionalen Domänencontroller und globale Katalogserver, die im nächsten in den Entwurfsprozess der Standorttopologie Schritt. Planen Sie z.B. einen regionalen Domänencontroller an einem Speicherort zu platzieren, die mehr als 100 regionale Domänenbenutzer enthält, damit sie weiterhin mit der Domäne anmelden können, wenn die WAN-Verbindung ein Fehler auftritt.  
  
Notieren Sie die Speicherorte, die Domänen in jedem Standort und die Anzahl der Benutzer für jede Domäne, die an jedem Standort dargestellt wird. Ein Arbeitsblatt, hilft Ihnen bei der Liste der Domänen und die Anzahl der Benutzer, die an jedem Standort dargestellt werden, finden Sie unter Auftrag Hilfsmittel für Windows Server2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)), herunterladen < DICT__Job_Aids_Designing_and_Deploying_ Directory_and_Security_Services.ZIP>Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.ZIP</DICT__Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.ZIP >, und öffnen Sie "Domänen und Benutzer in jeder Standort" (DSSTOPO_3.doc).  
  


