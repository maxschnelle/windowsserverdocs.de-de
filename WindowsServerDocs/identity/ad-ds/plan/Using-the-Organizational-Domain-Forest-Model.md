---
ms.assetid: 093ef1ae-ebc1-490f-9fb1-2c000ce89eb6
title: "Verwenden des organisatorischen Domänengesamtstruktur-Modell"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 22d871d9157622375619dd90336e597d4bfb3d68
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="using-the-organizational-domain-forest-model"></a>Verwenden des organisatorischen Domänengesamtstruktur-Modell

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Im Gesamtstrukturmodell Organisationsdomäne Besitzer jeder mehrere autonome Gruppen eine Domäne innerhalb einer Gesamtstruktur. Jede Gruppe steuert auf Domänenebene Verwaltung, ermöglicht es ihnen, bestimmte Aspekte der dienstverwaltung selbst verwalten, während der Gesamtstrukturbesitzer auf Gesamtstrukturebene Management steuert.  
  
Die folgende Abbildung zeigt ein Organisationsdomäne Gesamtstrukturmodell.  
  
![verwenden das Org Gesamtstruktur Domänenmodell](../../media/Using-the-Organizational-Domain-Forest-Model/c50a3c6a-b0e4-43ec-ad62-f05d05f0bbd2.gif)  
  
## <a name="domain-level-service-autonomy"></a>Auf Domänenebene Autonomie  
Das Organisationsdomäne Gesamtstruktur ermöglicht der Delegierung von Autorität für die Verwaltung auf Domänenebene. Die folgende Tabelle enthält die Arten von Servicemanagement, die auf der Domänenebene gesteuert werden können.  
  
|Typ der Servicemanagement|Zugehörige Aufgaben|  
|------------------------------|--------------------|  
|Verwaltung von den Betrieb von Domänencontrollern|-Erstellen und Entfernen von Domänencontrollern<br />-Überwachung die Funktionsweise von Domänencontrollern<br />-Verwalten von Diensten, die auf Domänencontrollern ausgeführt werden<br />– Sichern und Wiederherstellen von das Verzeichnis|  
|Konfiguration der Einstellungen für den gesamten Domäne|– Erstellen von Domänen- und Domänenbenutzer Kontorichtlinien, z. B. Kennwort, Kerberos und Kontosperrungsrichtlinien<br />-Erstellen und Anwenden von Gruppenrichtlinien für die gesamte Domäne|  
|Delegierung der Verwaltung der Daten-Stufe|– Erstellen von Organisationseinheiten (OUs) und Delegieren der Verwaltung<br />-Beim Reparieren von Problemen in der OE-Struktur, die OU-Besitzer nicht über ausreichenden Zugriffsrechte zum Beheben von verfügen|  
|Verwaltung von Vertrauensstellungen|-Einrichten von Vertrauensstellungen mit Domänen außerhalb der Gesamtstruktur|  
  
Andere Arten von Service, z. B. Schema oder die Verwaltung von Replikationstopologien, sind die Verantwortung für den Gesamtstrukturbesitzer.  
  
## <a name="domain-owner"></a>Domänenbesitzer  
In einer Gesamtstrukturmodell Organisationsdomäne sind Domänenbesitzer für Verwaltungsaufgaben auf Domänenebene verantwortlich. Domänen sind berechtigt, über die gesamte Domäne sowie den Zugriff auf alle anderen Domänen in der Gesamtstruktur. Aus diesem Grund müssen der Domänenbesitzer vertrauenswürdige Personen, die vom Gesamtstrukturbesitzer aktiviert sein.  
  
Weisen Sie auf Domänenebene dienstverwaltung auf einen Besitzer, wenn die folgenden Bedingungen erfüllt sind:  
  
-   Alle Gruppen, die durch die Teilnahme an der Gesamtstruktur vertrauen, der Besitzer der neuen Domäne und der Dienst Verwaltungsverfahren der neuen Domäne.  
  
-   Der Besitzer der neuen Domäne vertraut der Gesamtstrukturbesitzer und alle anderen Domänenbesitzer.  
  
-   Alle Domänenbesitzer in der Gesamtstruktur erklären sich damit einverstanden, dass der Besitzer der neuen Domäne verfügt, Administrator Servicemanagement und Richtlinien für die Dateiauswahl und Methoden, die strikter als eigene oder gleich sind.  
  
-   Alle Domänenbesitzer in der Gesamtstruktur stimmen zu, dass Domänencontroller, die von den Besitzer der neuen Domäne in der neuen Domäne verwaltet physisch geschützt sind.  
  
Beachten Sie, dass wenn ein Besitzer Delegaten auf Domänenebene Verwaltung der Gesamtstruktur auf einen Besitzer, andere Gruppen möglicherweise nicht für die Gesamtstruktur hinzugefügt werden, wenn sie nicht die Domänenbesitzer vertrauen.  
  
Alle Domänenbesitzer müssen bedenken, wenn eine dieser Bedingungen in der Zukunft ändern, es notwendig, verschieben Sie die Organisationseinheiten Domänen in einer Bereitstellung mit mehreren Gesamtstrukturen werden könnten.  
  
> [!NOTE]  
> Eine weitere Möglichkeit zur Minimierung von Sicherheitsrisiken zu einer Windows Server 2008 Active Directory-Domäne besteht im einsetzen von administratorrollentrennung, die die Bereitstellung von einem schreibgeschützten Domänencontroller (RODC) in Ihrer Active Directory-Infrastruktur erforderlich sind. Ein RODC ist eine neue Art von Domänencontroller in der Windows Server 2008-Betriebssystem, das nur-Lese-Partitionen der Active Directory-Datenbank hostet. Vor der Veröffentlichung von Windows Server 2008 mussten alle Server Wartungsarbeiten auf einem Domänencontroller von einem Domänenadministrator durchgeführt werden. In Windows Server 2008 können Sie lokale Administratorberechtigungen für einen RODC an alle Domänenbenutzer delegieren, ohne dem Benutzer Administratorrechte für die Domäne oder andere Domänencontroller. Dies ermöglicht die delegierten Benutzer melden Sie sich bei einem RODC und Wartungsarbeiten, z. B. das Aktualisieren eines Treibers auf dem Server ausführen. Allerdings nicht dieser delegierte Benutzer melden Sie sich auf alle anderen Domänencontroller oder andere administrative Aufgabe ausführen, in der Domäne. Auf diese Weise beliebige vertrauenswürdige Benutzer delegiert die Möglichkeit, den RODC effektiv zu verwalten, ohne die Sicherheit der Rest der Domäne zu gefährden. Weitere Informationen zu RODCs finden Sie unter AD DS: Read-Only Domänencontroller ([https://go.microsoft.com/fwlink/?LinkId=106616](https://go.microsoft.com/fwlink/?LinkId=106616)).  
  


