---
ms.assetid: 8be8c48d-790c-4199-b9d3-9f4a07d5ced2
title: Sammeln von Informationen zum Netzwerk
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d88cc2fafd9aa4fc221efc901c48fa41ef007a21
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867041"
---
# <a name="collecting-network-information"></a>Sammeln von Informationen zum Netzwerk

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der erste Schritt beim Entwerfen einer effektiven Standorttopologie in Active Directory Domain Services (AD DS) ist, finden Sie in Ihrer Organisation Netzwerkgruppe zum Sammeln von Informationen und regelmäßig über die physischen Netzwerktopologie mit ihnen kommunizieren.  
  
## <a name="creating-a-location-map"></a>Erstellen einer Standortkarte

Erstellen Sie eine standortzuordnung, die die physischen Netzwerkinfrastruktur Ihres Unternehmens darstellt. Identifizieren Sie auf der Karte Speicherort die geografischen Standorte, die Gruppen von Computern mit einer internen Konnektivität von 10 Megabit pro Sekunde (Mbit/s) oder höher (Geschwindigkeit des lokalen Netzwerks (LAN) oder besser) enthalten.  
  
## <a name="listing-communication-links-and-available-bandwidth"></a>Auflisten von kommunikationsverbindungen und die verfügbare Bandbreite

Dokumentieren Sie den Typ der kommunikationsverbindung, die verbindungsgeschwindigkeit und die verfügbare Bandbreite zwischen jedem Standort, nach der Erstellung einer standortzuordnung können. Abrufen einer wide Area Network (WAN)-Topologie aus Ihrer Gruppe Netzwerkbetrieb. Eine Liste der häufig verwendeten Typen von WAN-Verbindung und ihre Bandbreiten, finden Sie unter "Festlegen, die Kosten" im Abschnitt [Erstellen eines Entwurfs für Standortverknüpfungen](../../ad-ds/plan/Creating-a-Site-Link-Design.md). Sie benötigen diese Informationen weiter unten in den Entwurfsprozess der Standorttopologie standortverknüpfungen zu erstellen.  
  
Bandbreite bezieht sich auf die Menge der Daten, mit denen Sie über einen Kommunikationskanal in einem bestimmten Zeitraum übertragen können. Verfügbare Bandbreite bezieht sich auf die Menge an Bandbreite, die tatsächlich für die Verwendung von AD DS verfügbar sind. Verfügbare Bandbreiteninformationen erhalten Sie von Ihrer Gruppe Netzwerkbetrieb, oder Sie können Datenverkehr für jede Verbindung mit einem Netzwerkprotokoll-Analyseprogramm wie Network Monitor analysieren. Informationen zum Installieren von Network Monitor finden Sie im Artikel [Überwachung des Netzwerkdatenverkehrs](https://go.microsoft.com/fwlink/?LinkId=107058).  
  
Dokumentieren Sie jeden Standort und die anderen Standorte, die verknüpft sind. Notieren Sie außerdem die Art der kommunikationsverbindung und die verfügbare Bandbreite. Ein Arbeitsblatt, das Sie beim Auflisten von kommunikationsverbindungen und die verfügbare Bandbreite zu unterstützen, finden Sie unter [Auftrag Hilfsmittel für Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558), Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip, herunterladen und Öffnen Sie "Geografische Standorte und Kommunikationsverbindungen" (DSSTOPO_1.doc).  
  
## <a name="listing-ip-subnets-within-each-location"></a>Auflisten von IP-Subnetze an jedem Standort

Nachdem Sie die kommunikationsverbindungen und die verfügbare Bandbreite zwischen einzelnen Standorten zu dokumentieren, notieren Sie die IP-Subnetze an jedem Standort. Wenn Sie die Subnetzmaske und die IP-Adresse, an jedem Standort noch nicht kennen, finden Sie in Ihrer Gruppe Netzwerkbetrieb.  
  
AD DS ordnet eine Arbeitsstation mit einer Website durch Vergleichen der Arbeitsstation des IP-Adresse mit den Subnetzen, die von jedem Standort zugeordnet sind. Wenn Sie Domänencontroller einer Domäne hinzufügen, wird in AD DS auch überprüft ihre IP-Adressen und platziert sie in den am besten geeigneten Standort.  
  
Ein Arbeitsblatt, das Sie beim Auflisten der IP-Subnetze an jedem Standort unterstützen, finden Sie unter [Auftrag Hilfsmittel für Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558)Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip herunterladen und öffnen Sie " Standorte und Subnetze"(DSSTOPO_2.doc).  
  
> [!NOTE]  
> Zusätzlich zu den IP-Version 4 (IPv4)-Adressen, Windows Server unterstützt auch die IP-Version 6 (IPv6) Subnetzpräfixe. Ein Arbeitsblatt, das Sie beim Auflisten der IPv6-Subnetzpräfixe unterstützen, finden Sie unter [Anhang A: Speicherorte und Subnetzpräfixe](../../ad-ds/plan/Appendix-A--Locations-and-Subnet-Prefixes.md).  

## <a name="listing-domains-and-number-of-users-for-each-location"></a>Auflisten von Domänen und die Anzahl der Benutzer für jeden Standort

Die Anzahl der Benutzer für jede Regionaldomäne, die an einem Ort dargestellt wird ist einer der Faktoren, die bestimmen, die Platzierung der regionalen Domänencontroller und globalen Katalogservern, die im nächsten in den Entwurfsprozess der Standorttopologie Schritt. Planen Sie beispielsweise einen regionalen Domänencontroller an einem Speicherort zu platzieren, die mehr als 100 Regionaldomäne-Benutzer enthält, damit sie weiterhin mit der Domäne anmelden können, wenn die WAN-Verbindung ein Fehler auftritt.  
  
Notieren Sie die Standorte, Domänen, die dargestellt werden, in jedem Speicherort sowie die Anzahl der Benutzer für jede Domäne, die an jedem Standort dargestellt wird. Ein Arbeitsblatt, hilft Ihnen bei der Auflistung, die Domänen und die Anzahl der Benutzer, die an jedem Standort dargestellt werden, finden Sie unter [Auftrag Hilfsmittel für Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558), Job_Aids_Designing_and_Deploying_Directory_and_ herunterladen Security_Services.ZIP, und öffnen "Domänen und Benutzer in jeder Location" (DSSTOPO_3.doc).  
